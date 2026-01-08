# BattleBeacon: Project Blueprint & Battle Plan

**Date:** January 7, 2026  
**Status:** Initialization Phase  
**Mission:** To create the ultimate autonomous "Command Center" for the modern digital warrior.

---

## 1. The Vision: "Records of War"

**BattleBeacon** is not just a leaderboard; it is the permanent record of a digital soldier's career. It acts as the bridge between ephemeral gameplay sessions and lasting glory.

*   **The Artifact:** Every player is issued a **Beacon**—a cryptographically salted digital dog tag.
*   **The Community:** Warriors form **Squads**. Squads form **Alliances**.
*   **The Conflict:** Users organize **Campaigns**—custom, time-bound wars with specific scoring rules.

**Design Aesthetic:** Dark mode, high-contrast neon (Green/Red/Gold), "Heads Up Display" (HUD) style. Serious, tactical, gamified.

---

## 2. Core Features (The Gameplay Loop)

### Identity & The Beacon
*   **Frictionless Enlistment:** Login via OpenID (Google, etc.). No new passwords to remember.
*   **The Beacon:** On registration, a unique `beacon_id` is minted. This is the player's universal key across all campaigns.

### The Campaign Engine
*   **Create:** Commanders (users) define the Rules of Engagement (Start/End time, Scoring Metric).
*   **Deploy:** Players "mint" their Beacon into a specific campaign.
*   **Judge:** The system autonomously tracks, scores, and declares winners based on hard data from the combat logs.

### Squad Management
*   **Unit Cohesion:** Group play tracking. "How does my Squad compare to yours?"
*   **Aggregate Scoring:** Warfare is rarely solo. Track collective performance.

---

## 3. Technical Architecture (The Engine)

**Philosophy:** *Automation First. Zero-Touch Operations.*

### The Data Core: Apache Iceberg
We choose **Apache Iceberg** to handle the massive influx of combat logs.
*   **Why?** Transactional consistency, massive scale, and "Time Travel" capabilities (querying the state of the war at any point in the past).
*   **Structure:**
    *   `CombatLog` table: Partitioned by Day and Campaign.
    *   `Beacon` table: The source of truth for identity.

### The "Automater" (Infrastructure Supervisor)
A dedicated service solely responsible for system health.
*   **Self-Healing:** Monitors game server heartbeats. If a pulse is missed, it kills and restarts the instance.
*   **Alerting:** Pings human command *only* when automation fails.
*   **Frugal:** Auto-scales down when the battlefield is quiet.

### The Interface
*   **Frontend:** Single Page Application (SPA). Fast, reactive, branded "Loading" experience.
*   **API:** ReSTful interaction for Campaign management (`/mint`, `/deploy`, `/score`).

---

## 4. Business & Operations Strategy

**Goal:** Sustainable, profitable side-business.

### Monetization Tiers
1.  **Mercenary (Free):** Join campaigns, view basic stats.
2.  **Commander ($5/mo):** Create Private Campaigns, Squad Management, Advanced "Time Travel" Analytics.
3.  **Warlord (Enterprise):** White-label dashboards for esports orgs.

### Operational Discipline
*   **Infrastructure as Code (IaC):** Terraform for everything. No manual server setups.
*   **FinOps:** Rigid tagging of resources to track "Cost per Campaign".
*   **Compliance:** Built-in GDPR "Right to be Forgotten" (Beacon Burn).

---

## 5. Execution Roadmap

### Phase 1: Foundation (The "Automater")
- [ ] Initialize Git & Terraform repo.
- [ ] Build the "Automater" watchdog service (Go/Python).
- [ ] Prove the "Self-Healing" concept (Crash a dummy service, watch it revive).

### Phase 2: Intelligence (The Data)
- [ ] Spin up Apache Iceberg & Catalog.
- [ ] Define `Beacon` and `CombatLog` schemas.
- [ ] Write the first telemetry ingestion API.

### Phase 3: Recruitment (The Frontend)
- [ ] Build the OpenID Login flow.
- [ ] Design the "Mint Your Beacon" landing page.
- [ ] Connect the "Commander" dashboard to Iceberg data.

---

*In code we trust. Through data we conquer.*
