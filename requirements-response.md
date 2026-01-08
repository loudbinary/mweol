# Technical Review & Specification: BattleBeacon

Based on the initial `requirements.md`, this document outlines the technical vision, architecture, and automation strategy for the platform.

## 1. Executive Overview & "Gamified" Vision

**Project Name:** *BattleBeacon (Proposed)*

**Concept:** The ultimate "Command Center" for the modern digital warrior. It is not just a leaderboard; it is a live tactical feed of your gaming career.

*   **The Beacon:** Your digital dog tag. A salted, cryptographic token that uniquely identifies you across the battlefield.
*   **The Squad:** Groups of friends aren't just a list; they are a Unit. Your Unit's aggregate score competes against rival Units globally.
*   **The Campaign:** A specific war effort or seasonal challenge. You create it, share it, and the system judges the victors based on hard data.

**User Experience:**
*   **Login:** Frictionless entry via OpenID (Google, etc.).
*   **Dashboard:** sleek, dark-mode "Heads Up Display" (HUD) showing real-time server health, active campaigns, and your Squad's ranking.
*   **Visuals:** High-contrast neon metrics against dark backgrounds. "Green is clean (healthy server)", "Red is dead (server down)", "Gold is Glory (Campaign winner)."

### Analytics Strategy (Baseline Providers)

To measure engagement beyond raw game stats, we will integrate the following providers:

1.  **Google Analytics 4 (GA4):**
    *   *Role:* Baseline web traffic and user acquisition.
    *   *Usage:* Tracking "Where did these recruits come from?" (SEO, Social, Direct) and general page performance.

2.  **PostHog:**
    *   *Role:* Product Analysis & Session Recording.
    *   *Why:* Open-source friendly (can be self-hosted alongside the stack). Excellent for feature flags (testing new Campaign rules) and session replays to debug UI issues.

3.  **Mixpanel:**
    *   *Role:* Event-based User Journey Tracking.
    *   *Why:* Specialized in funnel analysis. Essential for tracking the "Mint to Combat" conversion rate—measuring how many users not only create a Beacon but actually deploy it in a game session.

---

## 2. Backend Specification & Data Architecture

**Core Technology:** Apache Iceberg
*   *Why:* You need to store massive amounts of combat logs ("Big Data") with transactional consistency. Iceberg allows "Time Travel" (querying data from a specific point in the past) and schema evolution without breaking the game.

### Data Relations (ERD Concept)

1.  **`PlayerIdentity`**: Links OpenID (Google) to internal ID.
2.  **`Beacon`**:
    *   `beacon_id` (PK)
    *   `salt_token` (Secret)
    *   `owner_id` (FK to Player)
    *   `status` (Active/MIA)
3.  **`Squad`**: Collection of `PlayerIdentity`. Aggregates scores.
4.  **`Campaign`**:
    *   `campaign_id`
    *   `owner_token`
    *   `rules_config` (JSON)
    *   `start_time` / `end_time`
5.  **`CombatLog` (Iceberg Table)**:
    *   *Partitioned by Day and Campaign*
    *   `timestamp`
    *   `beacon_id`
    *   `session_id`
    *   `event_type` (Kill, Death, Objective)
    *   `metric_value` (Score)

### API Endpoints (RESTful / GraphQL)

**Authentication & Beacon**
*   `POST /api/v1/auth/openid` (Exchange provider token for session)
*   `POST /api/v1/beacon/mint` (Generate new salted beacon)
*   `GET /api/v1/beacon/status` (Check if beacon is active)

**Campaign Ops**
*   `POST /api/v1/campaign/deploy` (Create new campaign)
*   `POST /api/v1/campaign/{id}/join` (Register beacon to campaign)
*   `GET /api/v1/campaign/{id}/intel` (Get scores/stats - queries Iceberg)

**Server Automater (The "Manager")**
*   `POST /api/v1/infra/report-health` (Heartbeat from game servers)
*   `POST /api/v1/infra/session/start`
*   `POST /api/v1/infra/session/terminate`

---

## 3. Automation & Infrastructure as Code (IaC)

To meet the requirement of "Automation from the start," manual server setup is forbidden. Everything must be defined in code.

**Infrastructure Tooling Strategy:**

1.  **Provisioning (Terraform):**
    *   Define the "Cloud Hardware" (Virtual Private Cloud, Kubernetes Cluster, S3 Buckets for Iceberg storage).
    *   Define the Database (Catalog for Iceberg).

2.  **Configuration (Ansible/Helm):**
    *   The "Server Automater" you requested needs to be a **Kubernetes Operator** or a **Sidecar container pattern**.
    *   *Self-Healing:* If a game session node stops sending `HealthReports`, the orchestrator (K8s) automatically kills the pod and spins up a new one.

3.  **The "Automater" Logic:**
    *   We build a lightweight "Watchdog" service.
    *   **Input:** Receives `Ping` and `HealthReports`.
    *   **Logic:** If `Ping` > 200ms or `LastSeen` > 30s -> Trigger `Restart` webhook.
    *   **Scaling:** If `ActiveCampaigns` increases -> Auto-scale compute nodes for Spark/Iceberg processing.
