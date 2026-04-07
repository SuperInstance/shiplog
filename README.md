# ShipLog

A package tracking agent you run yourself. It polls carriers, logs updates to your git repository, and can notify you—all without sending your data to a third-party service.

Live Example: https://the-fleet.casey-digennaro.workers.dev/shiplog

---

## What This Is For
You manage packages for projects, teams, or clients. Most trackers are built as data-harvesting SaaS. This is different: you fork the code, deploy it to your own Cloudflare account, and provide your own carrier API keys. Your tracking history and configuration live in your repository, not on a company server.

It is built on the open-source Cocapn agent runtime, designed for fork-first development.

---

## How It Works
- **Self-Deployed Agent:** You deploy this code as a Cloudflare Worker. It executes on your infrastructure.
- **Repository as Memory:** The agent reads its task list (tracking numbers) from your repository and writes all status updates back as commits.
- **Scheduled Execution:** It runs on a cron schedule you control, fetching updates from carrier APIs using your stored credentials.
- **Optional Coordination:** It can send webhook alerts and is compatible with the Cocapn Fleet protocol for inter-agent communication.

---

## What It Does
*   Runs as a scheduled Cloudflare Worker (no servers to manage).
*   Fetches status from UPS and USPS APIs (extensible to other carriers).
*   Commits all package status changes directly to your git repository, creating a permanent, auditable log.
*   Stores all API keys and configuration as secrets in your Worker, never exposed in code.
*   Can be modified to send notifications via webhook, email, or other agents.

---

## Limitations
Status accuracy and update frequency depend on the external carrier APIs. This agent polls them but cannot control their data or latency.

---

## Quick Start
1.  **Fork this repository.**
2.  Deploy to Cloudflare Workers using Wrangler:
    ```bash
    npm install
    wrangler deploy
    ```
3.  Add your carrier API keys as Worker secrets:
    ```bash
    wrangler secret put UPS_API_KEY
    wrangler secret put USPS_API_KEY
    ```
4.  Add tracking numbers to the `packages.json` file in your repo and commit. The agent will process them on its next scheduled run.

---

## Contributing
The best way to build on ShipLog is to fork it and adapt it to your needs. For bug fixes or minor improvements to the core agent, pull requests are welcome.

---

## License
MIT

Superinstance & Lucineer (DiGennaro et al.)

---

<div align="center">
  <a href="https://the-fleet.casey-digennaro.workers.dev">The Fleet</a> •
  <a href="https://cocapn.ai">Cocapn</a>
</div>