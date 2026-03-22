# ☕ Coffee Concierge · Tulsa

> Find the best independent coffee shops in Tulsa, OK — sorted by what you need, near you, no chains.

**Live demo:** [michaeldambold.com/coffee-concierge](https://michaeldambold.com/coffee-concierge)

![Coffee Concierge screenshot](public/og-preview.png)

---

## What it does

Coffee Concierge helps visitors and locals find the right independent Tulsa coffee shop for their situation — not just a generic list, but ranked by:

- **Your occasion** — Work remotely, Coffee date, Just relaxing, Quick stop, or Exploring Tulsa
- **Your location** — Share location to sort by distance + get real drive/walk times
- **An AI guide** — Type anything ("nervous first date, not too loud") and get a specific recommendation powered by Claude

Every shop is independently owned. No Starbucks, no Dutch Bros.

---

## Features

- 📍 **Geolocation sorting** — Haversine distance calculation, composite fit + proximity score
- ✨ **AI Concierge** — Claude-powered chat that knows each shop's personality, distance from you, and occasion fit
- 🌙 **Occasion picker** — Work / Date / Relax / Explore / Quick stop
- 🏷️ **Personality badges** — Human-language labels like "First Date Gem" and "Laptop Haven"
- ☕ **Why not a chain** — Each shop card explains what makes it worth choosing over Starbucks
- 📱 **Mobile-first** — Designed for someone standing on a street corner in Tulsa

---

## Tech stack

| Layer | Choice |
|---|---|
| Framework | React 18 + Vite |
| Styling | Inline CSS with CSS-in-JS patterns (no build-time deps) |
| AI | Anthropic Claude API (`claude-sonnet-4-20250514`) |
| Geolocation | Browser `navigator.geolocation` (no third-party SDK) |
| Distance | Haversine formula (pure JS, no maps SDK needed) |
| Fonts | Google Fonts — Playfair Display + DM Sans |

---

## Getting started

### Prerequisites

- Node.js 18+
- An [Anthropic API key](https://console.anthropic.com/)

### Install & run

```bash
git clone https://github.com/yourusername/coffee-concierge.git
cd coffee-concierge
npm install
npm run dev
```

### API key setup

The AI Concierge calls the Anthropic API directly from the browser. For local development this works out of the box in the Claude.ai artifact environment. For a standalone deploy you have two options:

**Option A — Vite env variable (simple, dev only):**
```bash
# .env.local
VITE_ANTHROPIC_KEY=sk-ant-...
```
Then in `src/App.jsx`, add the header:
```js
"x-api-key": import.meta.env.VITE_ANTHROPIC_KEY,
```

**Option B — Proxy server (recommended for production):**
Create a small serverless function (Cloudflare Worker, Vercel Edge Function, etc.) that holds the key server-side and proxies requests. Never expose API keys in client-side bundles in production.

### Build for production

```bash
npm run build
# Output lands in /dist — deploy that folder anywhere
```

---

## Adding more shops

All shop data lives in the `SHOPS` array at the top of `src/App.jsx`. Each entry follows this shape:

```js
{
  id: "unique_id",
  name: "Shop Name",
  subtitle: "Neighborhood descriptor",
  neighborhood: "Neighborhood Name",
  lat: 36.0000,
  lng: -95.0000,
  price: 2,              // 1-3 ($ to $$$)
  seating: 24,           // rough seat count
  outlets: 4.0,          // 0-5 score
  wifi: 4.5,             // 0-5 score
  noise: 2.0,            // 0-5 (lower = quieter)
  parking: 3.0,          // 0-5 score
  drive_thru: false,
  mobile_order: true,
  gf_food: true,
  df_milks: 2,           // number of dairy-free milk options
  aesthetic: 4.2,        // 0-5 score
  dessert: 3.8,          // 0-5 score
  cleanliness: 4.5,      // 0-5 score
  restroom: true,
  hours: "Mon–Fri 7am–7pm · Sat–Sun 8am–5pm",
  address: "123 Main St, Tulsa, OK",
  phone: "(918) 555-0100",
  website: "https://example.com",
  accent: "#C9763D",     // brand color for the card
  badges: ["Badge One", "Badge Two", "Badge Three"],
  whyNotChain: "One sentence on what makes this shop worth choosing over a chain.",
  personality: "One sentence describing the vibe and who it's for.",
  occasionFit: {
    date: 4,     // 1-5
    work: 5,     // 1-5
    relax: 4,    // 1-5
    explore: 3,  // 1-5
    quick: 2,    // 1-5
  },
}
```

---

## Deploying to GitHub Pages

```bash
npm install -D gh-pages

# Add to package.json scripts:
# "deploy": "npm run build && gh-pages -d dist"

npm run deploy
```

Set your repo's Pages source to the `gh-pages` branch.

---

## Roadmap

- [ ] More Tulsa shops (Roosevelt Coffee, Dwelling Spaces, Shades of Brown, etc.)
- [ ] React Native / Expo port for App Store
- [ ] Admin Google Sheet → JSON pipeline for community data updates
- [ ] Neighborhood filter
- [ ] "Open now" filter using real hours data
- [ ] City expansion (Tulsa → other Oklahoma cities)

---

## License

MIT — use it, fork it, build your own city's version.

---

## Credits

Built by [Michael Dambold](https://michaeldambold.com) · Tulsa, OK  
AI powered by [Anthropic Claude](https://anthropic.com)
