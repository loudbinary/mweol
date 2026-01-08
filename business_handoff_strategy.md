# Operational Handoff & Business Strategy

This document outlines the strategy for transitioning "BattleBeacon" from a development project into a manageable, scalable, and profitable side business.

## 1. The Handoff: From Code to Product

The goal is to create a system that runs itself ("Zero-Touch Ops").

### Phase 1: Hardened Automation (The "Automater")
*   **Self-Healing Infrastructure:** Ensure Kubernetes readiness/liveness probes are perfectly tuned. If a game collector service crashes, it must restart without you waking filled with dread.
*   **Alerting, Not Watching:** Do not build a dashboard you have to stare at. Build alerts (PagerDuty/Slack hooks) that only ping you when the *automation fails to fix a problem*, not just when a problem occurs.
*   **FinOps Tags:** Tag every cloud resource (Terraform tags). You need to know exactly how much a single "Campaign" costs to host so you can price it correctly.

### Phase 2: User Onboarding "Sidecar"
*   **Documentation Site:** Deploy a Docusaurus or MkDocs site. Users will have questions. If you are answering emails, it's not a side business, it's a job. The documentation must cover "How to Mint a Beacon" and "Integrating with our API" extensively.
*   **Status Page:** Publicly accessible uptime monitoring. Ideally automated via the "Server Automater" health checks.

## 2. Business Model: Monetization

How to pay for the Iceberg storage and generate profit without high overhead.

### Tier 1: The "Mercenary" (Free)
*   Join existing campaigns.
*   Basic stats viewing.
*   Single Beacon.
*   *Cost to you:* Negligible (cold storage).

### Tier 2: The "Commander" (Subscription - $5/mo)
*   **Create Campaigns:** Ability to host private leaderboards for friends.
*   **Advanced Analytics:** Access to "Time Travel" queries (e.g., "Show my kill/death ratio progression over the last 6 months").
*   **Squad Management:** Create and brand a Squad Unit.

### Tier 3: The "Warlord" (API Access - Enterprise/B2B)
*   For game server hosts or large esports organizations.
*   Direct API access to push high-volume telemetry.
*   White-labeled dashboards.

## 3. Maintenance Loop (The "Side Hustle" Routine)

To keep this manageable, adhere to a strict maintenance schedule.

1.  **Weekly:** Review "FinOps" report. Are cloud costs scaling linearly with users? If storage costs spike, adjust Iceberg compaction settings.
2.  **Monthly:** Library & Security updates. Run the automated test suite.
3.  **Quarterly:** Feature drop. e.g., "New Visualization Type" or "New Game Integration".

## 4. Legal & Compliance (Crucial for Data Projects)

*   **GDPR/CCPA:** Since we are tracking "playees" (people) and their behaviors:
    *   Implement a "Right to be Forgotten" button that purges a Beacon ID and its history from Iceberg.
    *   Clear Terms of Service defining "Virtual Assets" (Beacons) ownership.
*   **Anti-Cheat Policy:** Define strict rules for Beacon revocation if telemetry data is spoofed.

## 5. Next Immediate Steps (The "Roadmap")

1.  **Scaffold Repo:** Initialize Git, Terraform, and Docker structures.
2.  **Prototype "The Automater":** simple Go or Python service that listens for a heartbeat and logs to a dummy Iceberg table.
3.  **Lobby UI:** Build the "Landing/Login" flow to verify OpenID hookups.
