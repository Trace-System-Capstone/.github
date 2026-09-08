# 🛡️ TRACE System Development Hub

Welcome to the TRACE (Telemetry, Remediation, and Anomaly Control Engine) central repository hub. This organization houses the microservices required for our multi-module endpoint management and analytics system. 

## 🏗️ Architecture Overview
* **`trace-endpoint-agent`**: C# Native AOT Windows Service (Deep Freeze & Telemetry).
* **`trace-cloud-services`**: Azure IoT Routing, PostgreSQL DB, Python ML (Isolation Forest), and Azure OpenAI RAG Diagnostics.
* **`trace-admin-dashboard`**: Next.js observability frontend.

---

## 📜 Global Data Conventions (Master Contract)
To ensure compatibility across C#, Python, and Next.js, all developers must strictly adhere to these data rules:
* **Case Convention:** All JSON keys, database columns, and payload variables must use `snake_case` (e.g., `system_uptime`).
* **Unit Suffixes:** Include units in metric names (`_c` for temp, `_pct` for percentages, `_rpm`, `_w`).
* **Timestamps:** ISO 8601 UTC standard only (e.g., `2026-09-07T21:05:23Z`). Local timezones are forbidden in the backend.
* **Null Handling:** Missing sensor data must be explicitly passed as `null` (not `0` or `""`) to prevent ML baseline corruption.

---

## 🌿 Branching Strategy
We follow a strict integration workflow to protect the multi-module architecture.

* **`main`**: Production-ready code only. Deployments trigger from this branch.
* **`develop`**: The primary integration branch. All feature branches merge here first for end-to-end testing.
* **`feature/<module-name>-<feature>`**: For new development (e.g., `feature/endpoint-mqtt-sync`).
* **`fix/<issue-description>`**: For bug fixes (e.g., `fix/ui-heatmap-lag`).

---

## 💬 Commit Conventions
All commit messages must follow the [Conventional Commits](https://www.conventionalcommits.org/) standard to automate changelogs and maintain a clean history:
* `feat:` A new feature (e.g., `feat: implement SQLite offline buffer`)
* `fix:` A bug fix (e.g., `fix: correct UTC timestamp parsing`)
* `chore:` Maintenance or tooling updates (e.g., `chore: update Azure ML dependencies`)
* `docs:` Documentation changes

---

## 🛑 Pull Request (PR) Rules
1. **Never push directly to `main` or `develop`.**
2. All PRs must point to `develop` for integration.
3. PR titles must match the commit convention (e.g., `feat: add spatial heatmap view`).
4. Code cannot be merged without at least **1 peer review approval** to ensure it adheres to the Master Data Contract.
