# BattleBeacon ⚔️

**The Autonomous Command Center for the Modern Digital Warrior.**

[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)]()
[![License](https://img.shields.io/badge/license-MIT-blue)]()
[![Status](https://img.shields.io/badge/status-active_combat-red)]()

---

## 🛑 Halt, Soldier. Identification Required.

**BattleBeacon** is the definitive platform for managing, promoting, and collecting combat metrics as your player saunters through the battlefield. 

We don't just track scores; we record **Legacies**.

### The Mission
In the chaos of modern digital warfare, stats are lost to the void. Friends are scattered. Victories are forgotten.
**BattleBeacon** changes that. We provide:
1.  **The Beacon:** A cryptographically salted identity token that tracks *you*, regardless of the game.
2.  **The Squad:** Collective ranking for you and your friends. 
3.  **The Campaign:** User-generated wars with custom scoring rules and time-bound challenges.

---

## 📡 The Tech Stack (Our Weaponry)

This system is built for **Scale** and **Zero-Touch Operations**.

*   **Core Data:** [Apache Iceberg](https://iceberg.apache.org/) - For massive scale combat logs and "Time Travel" analytics.
*   **Authentication:** OpenID Connect (Google/Top 5) - No friction, just action.
*   **Infrastructure:** Fully Automated Self-Healing Architecture. The "Automater" watches the servers so you don't have to.
*   **Frontend:** High-performance Single Page App (SPA).

---

## ⚡ Quick Start (Deploy Your Beacon)

### Prerequisites
*   Docker & Kubernetes
*   Python 3.11+ / Go (for the Automater)

### Installation

1.  **Clone the Command Center:**
    ```bash
    git clone https://github.com/yourusername/BattleBeacon.git
    cd BattleBeacon
    ```

2.  **Initialize Infrastructure:**
    ```bash
    # Spin up local Iceberg & Spark catalog
    make infra-up
    ```

3.  **Mint Your Dev Beacon:**
    ```bash
    ./scripts/mint_beacon.sh --user "Commandant"
    ```

---

## 🗺️ Roadmap

*   **Phase 1:** The Automater (Self-healing infra) & Iceberg Core.
*   **Phase 2:** Beacon Minting & OpenID Integration.
*   **Phase 3:** Squads, Leaderboards, and Campaign Deployment.

---

## 🤝 Join the Ranks

We are looking for specialists to help build the future of combat analytics.

*   **Backend Engineers:** Help us optimize Iceberg compaction.
*   **Frontend Specialists:** We need a UI that looks like a futuristic HUD.
*   **Tacticians:** Help us design new Campaign scoring algorithms.

> *Build the platform. Own your stats. Win the war.*

---
*© 2026 BattleBeacon Command.*
