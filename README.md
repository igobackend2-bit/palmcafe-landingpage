# Palm Cafe – Landing Page

Single-page website for Palm Cafe ("The Healthy Food Joint"), a smoothie/juice/healthy-food outlet in Uthandi, Chennai. No backend — browsing, cart, and checkout all happen client-side, with orders handed off to WhatsApp.

## Tech Stack

- Plain HTML5 + CSS3 (all inline in one file, no framework)
- Vanilla JavaScript (no build step, no bundler)
- `live-server` (dev-only, via npx) for local preview
- Data persistence: browser `localStorage` only (key `pc_v9`) — no database, no server

## Features

- Menu across 5 categories: Smoothies, Juices, Hydrants, Healthy Bowls, Food & Snacks (51 products total, hardcoded in JS)
- Cart drawer with add/remove/qty controls and running total
- Checkout form (name, phone, address, pickup/delivery) that builds a formatted message and opens WhatsApp (`wa.me`) to send the order — no order is stored server-side
- Customer "profile" (name/phone/address + local order history) saved to `localStorage`, not a real account system
- Admin overlay (gear icon, password-gated) to edit WhatsApp numbers, address, hours, Swiggy/Zomato links, and add products — all changes save to the *visitor's own browser*, not a shared config
- Image lightbox / gallery, mobile nav, scroll-reveal animations, preloader
- Links out to WhatsApp, Swiggy, Zomato, Facebook, Instagram

## Project Structure

```
Igo-Palm Cafe/
├── index.html              # entire site: markup + <style> + <script> in one file
├── package.json             # only dependency is a dev-time live-server script
├── package-lock.json
├── HOSTINGER-DEPLOY.md       # step-by-step upload guide for Hostinger hosting
└── images/
    ├── products/             # smoothie images (s1–s12)
    ├── Juice/                 # juice images
    ├── Drinks/                # "hydrants" category images
    ├── Healthy Bowls/
    ├── Food & Snacks/
    ├── palm cafe image/       # appears to duplicate images/products — see Next Steps
    ├── logo.svg, favicon.svg, hero_background.png, gallery_1–5.png, why_us.png, divider_bg.jpg
```

There is no `src/`, no `components/`, no server code, and no test folder — the whole site is `index.html`.

## Getting Started

### Prerequisites
- Node.js (only needed to run the local dev server via `npx`)
- Any modern browser

### Run locally
```bash
npm run dev
```
This runs `npx live-server .`, which opens `index.html` in your browser with auto-reload. There is no install step beyond having Node/npx available — no `npm install` is required for the site itself.

### Deploy
No build step. Deployment is literally uploading `index.html` (and `images/`) to a host's `public_html`. See `HOSTINGER-DEPLOY.md` for the exact Hostinger walkthrough already written for this project.

## Available Scripts

| Command | Purpose |
|---|---|
| `npm run dev` | Serve the site locally with live-reload (`live-server`) |
| `npm test` | Placeholder only — exits with an error, no tests exist |

## Admin Panel Reference

| Setting | Default value (hardcoded in `index.html`, `DEF` object) |
|---|---|
| Admin password | `palmcafe2024` |
| WhatsApp (primary) | 91 89259 62259 |
| WhatsApp (secondary) | 91 89258 93320 |
| Address | No 17, Kovalan Street, 2nd Main Road, Uthandi Kanathur, Chennai – 600 119 |

Changes made through the admin overlay are saved to `localStorage` in the visitor's own browser (`pc_v9` key) — they do **not** update the site for other visitors or persist across devices. Permanent changes must be edited directly in the `DEF` object in `index.html`.

## Project Status & Known Limitations

This is a static, no-backend marketing/ordering page — not a production e-commerce system. Known limitations as of this audit:

- **No real backend or database.** All products, prices, and settings live in a single hardcoded `DEF` object inside `index.html`.
- **Orders aren't actually tracked.** `sendOrder()` writes an order to the customer's local order history with `status: 'Pending'`, and the code comment itself notes this status is "faked since there's no backend." The only real record of an order is the WhatsApp message sent to the cafe's phone.
- **Admin password is stored in plaintext in client-side JS** (`pass:'palmcafe2024'`) and is trivially visible to anyone who views page source — this is not real authentication, just a UI gate.
- **Admin/settings changes are per-browser, not global.** Because everything persists to `localStorage`, an admin who updates settings on one device won't see that reflected on another device, and visitors never see admin changes unless made directly in the source.
- **No automated tests.** `npm test` is a stub.
- **No sitemap.xml or robots.txt** in the repo.
- **One external hotlinked image** (`images.unsplash.com`, used for the Open Graph preview image) — this will break if Unsplash changes/removes that asset.
- **Duplicate image assets:** `images/palm cafe image/` appears to contain the same smoothie photos as `images/products/` under different filenames — likely leftover from an earlier pass and safe to consolidate.
- **Exposed credential in git remote:** the local git config's `origin` remote URL currently embeds a GitHub personal access token in plaintext (visible via `git remote -v`). This should be rotated/revoked and the remote re-added using SSH or a credential helper instead of an inline token.

## Suggested Next Steps for Whoever Picks This Up

1. **Rotate the exposed GitHub token immediately** and reconfigure the `origin` remote without embedding credentials in the URL (use SSH keys or a Git credential manager).
2. **Move the admin password out of client-side JS.** Even a simple serverless function or a build-time environment variable would be an improvement over a password anyone can read in view-source.
3. **Decide on a real order-management path.** If order tracking/history matters, a lightweight backend (even a serverless function + spreadsheet/DB) would replace the "faked" pending status and per-browser history.
4. **Clean up duplicate image folders** — reconcile `images/palm cafe image/` with `images/products/` and remove whichever set is unused.
5. **Add `sitemap.xml` and `robots.txt`** for basic SEO hygiene, and consider self-hosting the Open Graph image instead of hotlinking Unsplash.
6. **Add a minimal test/lint step** (even just HTML validation) so `npm test` does something useful.
7. **Consider splitting `index.html`** (currently ~2,300 lines of markup + CSS + JS in one file) into separate `.css`/`.js` files as the site grows, to make future changes easier to review and diff.
8. **Document the WhatsApp order flow** for non-technical staff (what a customer's order message looks like, where it lands, how to update the WhatsApp numbers) since that's the only real "order system" in place today.
