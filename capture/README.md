# Domain Valuation Tracker — Laptop Capture Tool

Captures screenshots of Domain.com.au property profile pages to document automated valuation estimates before and after properties are listed for sale.

## Quick Start

```bash
git clone https://github.com/Will954633/propertybullshit.git
cd propertybullshit/capture
npm install          # Downloads Puppeteer + bundled Chrome (~300MB)
npm start            # Start capturing (resumes automatically if interrupted)
```

## How It Works

1. **`addresses.json`** — 15,000 residential addresses across Brisbane, Sydney and Melbourne (sampled from Australian Government G-NAF data)
2. **`capture.js`** — Opens each property's Domain profile page, extracts the valuation estimate, and takes a screenshot
3. **`progress.json`** — Tracks every capture. If you stop and restart, it picks up where it left off
4. **`export.js`** — Generates comparison data for the website after rechecking

## Commands

| Command | What it does |
|---------|-------------|
| `npm start` | Start/resume baseline capture |
| `npm run status` | Show progress summary |
| `npm run export` | Generate website comparison data |
| `node capture.js --city brisbane` | Capture only one city |
| `node capture.js --recheck` | Re-capture properties to detect valuation changes |

## Timing

- ~15,000 properties at ~4.5 seconds each = **~19 hours**
- Can be stopped and restarted unlimited times (Ctrl+C)
- Progress is saved after every single capture

## Workflow

### Phase 1: Baseline (run once)
```bash
npm start    # Captures "before" valuation for all 15,000 properties
```

### Phase 2: Recheck (run weekly)
```bash
node capture.js --recheck    # Re-visits all properties, flags any that are now listed
npm run export               # Generates comparison data for the website
```

Properties that have been listed since the baseline will have both "before" and "after" screenshots, showing whether Domain changed their valuation estimate.

## Output

Screenshots are saved to `screenshots/{city}/{address-slug}/`:
- `before-full.png` — Full page screenshot
- `before-valuation.png` — Valuation section screenshot
- `before-data.json` — Extracted valuation data + metadata
