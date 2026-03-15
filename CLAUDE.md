# Playlab Sales Hub

Vanilla JS app serving as the Playlab Sales Hub — includes a package builder, pricing reference, key resources, and a welcome landing page. No build step, no framework. Deployed via GitHub Pages from `main` branch.

## File Structure
- `index.html` — HTML structure only (~385 lines)
- `style.css` — All styles (~345 lines)
- `app.js` — All logic (~2,100 lines)

## Tabs
- **Welcome** (default) — Landing page linking to other tabs (`#welcomeView`)
- **Builder** — Package builder for service quotes (`.builder`)
- **Pricing Sheet** — Reference pricing tables (`#pricingView`)
- **Key Resources** — Embedded Google Docs/Sheets/Slides (`#resourcesView`)

## Auth
Passphrase gate using SHA-256 hash stored in `app.js`. Persists for the browser session via `sessionStorage`.

## Rules & Pricing Source of Truth

All pricing, business rules, and requirements are maintained in this Google Doc:

**[Playlab Package Builder — Rules & Pricing](https://docs.google.com/document/d/1oNTf-jdb5tAlrg2kVbXAa5AJ0jrCKz3Hj3YQrNLjk-8/edit)**

> Doc ID: `1oNTf-jdb5tAlrg2kVbXAa5AJ0jrCKz3Hj3YQrNLjk-8`

Read this doc at the start of every conversation before making changes to the app. Use the gdrive MCP to fetch the latest version.

## Key Architecture Notes
- All prices derive from 3 base rates (LP $250, Dev $200, Travel $125) via `getBlockPrice()`
- Package components are static (defined in `PACKAGES`); support items (Launch Meeting, Office Hours, Check-ins, Reflection) are auto-included by `confirmAddPackage()`
- Quote state is serialized to URL hash (base64 JSON) for shareable links
- Multi-tab quotes persist in `localStorage`
- State hydration is centralized in `hydrateState()` — used by both URL loading and tab switching
