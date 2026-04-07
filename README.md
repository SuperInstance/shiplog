# ShipLog — Track packages from your own repository

You can track packages without sharing your data with third-party services.

**Live demo:** https://the-fleet.casey-digennaro.workers.dev/shiplog

## Why ShipLog
Most package tracking services collect and monetize your delivery data. ShipLog runs as your own agent, keeping your tracking numbers and delivery history in your control. Built on the Cocapn open-source agent runtime.

## How it works
ShipLog is a scheduled Cloudflare Worker that:
1. Reads tracking numbers from your repository's `packages.json` file
2. Checks status directly with carrier APIs using your credentials
3. Commits status changes back to your repository
4. Optionally sends you notifications

Your data stays with you—we never see your tracking numbers, API keys, or delivery information.

## Quick start
1. **Fork this repository** to your GitHub account
2. Deploy to Cloudflare Workers:
   ```bash
   npm install
   wrangler deploy
   ```
3. Add carrier API keys as secrets and tracking numbers to `packages.json`

## What's included
- Self-hosted agent running on your Cloudflare account
- Full audit trail through git commits
- UPS and USPS carrier support (others require modification)
- API keys stored as Worker secrets, never committed
- Configurable schedule via wrangler.toml
- Zero runtime dependencies
- Fleet protocol compatible

## Limitations
Only UPS and USPS are implemented out of the box. Adding other carriers requires modifying the code in your fork.

## Configuration
Add your carrier API keys after deployment:
```bash
wrangler secret put UPS_API_KEY
wrangler secret put USPS_API_KEY
```

Then add tracking numbers to `packages.json` in your repository.

## Development
ShipLog follows the Cocapn Fleet fork-first philosophy. The intended way to modify it is to fork the repository and adapt it to your needs. Bug fixes and carrier additions are welcome as pull requests.

## License
MIT

Superinstance & Lucineer (DiGennaro et al.)

---

<div>
  <strong>Fleet:</strong> <a href="https://the-fleet.casey-digennaro.workers.dev">the-fleet</a> ·
  <strong>Cocapn:</strong> <a href="https://cocapn.ai">cocapn.ai</a>
</div>