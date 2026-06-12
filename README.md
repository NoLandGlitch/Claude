# Gateway Realty — Lead Generation Website Template

A fully client-side, zero-dependency real estate lead generation template. No server, no framework, no build step — open `index.html` in a browser and it works.

---

## File Structure

```
/
├── index.html      — Public landing page (hero, listings carousel, lead forms)
├── listing.html    — Individual property detail page (dynamic, reads ?id= param)
├── about.html      — About the agency / agent page
├── members.html    — Password-protected agent dashboard (add/edit/delete listings)
└── README.md       — This file
```

---

## Features

| Feature | Where |
|---|---|
| Lead capture forms (hero + contact section) | `index.html` |
| Auto-rotating listings carousel | `index.html` |
| Property search bar (UI only) | `index.html` |
| Share listing link (copy + native share) | `index.html`, `listing.html`, `members.html` |
| Individual listing detail pages | `listing.html?id=LISTING_ID` |
| Similar properties section | `listing.html` |
| Agent inquiry form | `listing.html` |
| About page (story, team, timeline, awards) | `about.html` |
| Password-protected agent portal | `members.html` |
| Add / edit / delete listings | `members.html` |
| Listing status management | `members.html` |
| Feature tags per listing | `members.html` |
| Image URL preview | `members.html` |
| Agent profile editor | `members.html` |
| Stats dashboard (total, active, value, sold) | `members.html` |
| Data persistence via localStorage | All pages |
| Fully responsive (mobile / tablet / desktop) | All pages |
| Scroll-reveal animations | `index.html`, `about.html` |

---

## How Data Works

All listing data is stored in the browser's `localStorage` under the key `gw_listings`. This means:

- Data **persists between sessions** in the same browser
- Data is **per-browser** — it does not sync across devices
- Data is **seeded automatically** on first load with 6 example listings

To connect to a real backend, replace the `localStorage.getItem / setItem` calls with `fetch()` calls to your API.

### Listing Data Model

```json
{
  "id":          "uuid-string",
  "address":     "123 Main St",
  "city":        "Clearview",
  "state":       "CA",
  "zip":         "90210",
  "price":       549000,
  "type":        "Single Family",
  "beds":        4,
  "baths":       3,
  "sqft":        2340,
  "year":        2008,
  "status":      "Active",
  "description": "Full property description...",
  "image":       "https://example.com/photo.jpg",
  "tags":        ["Pool", "Garage", "Renovated Kitchen"],
  "date":        1718150400000
}
```

**Status values:** `Active` | `Pending` | `Sold` | `Draft`

**Property types:** `Single Family` | `Condo / Townhome` | `Multi-Family` | `Luxury Estate` | `Land` | `Commercial`

---

## Customization Guide

### 1 — Company Name & Branding

Search and replace `Gateway Realty` across all four HTML files with your company name.

Change the logo icon (currently 🏡) in each file's nav section:
```html
<div class="nav-logo-icon">🏡</div>  <!-- change emoji or replace with <img> -->
<span class="nav-logo-text">Gateway Realty</span>  <!-- your name here -->
```

### 2 — Color Scheme

All four pages share the same CSS custom properties in the `:root` block. To retheme the entire site, edit these variables in **each** HTML file's `<style>` tag:

```css
:root {
  /* Page background */
  --bg:        #f8fafc;

  /* Card / panel background */
  --surface:   #ffffff;

  /* Dark primary — nav, headings, dark sections */
  --primary:   #0f172a;
  --primary2:  #1e293b;

  /* Accent blue — links, active states, chips */
  --accent:    #2563eb;
  --accent2:   #3b82f6;
  --accent-bg: #eff6ff;

  /* CTA orange — primary buttons, highlights */
  --cta:       #f97316;
  --cta2:      #fb923c;

  /* Body text */
  --text:      #1e293b;
  --muted:     #64748b;

  /* Borders */
  --border:    #e2e8f0;
}
```

**Example alternative palettes:**

Classic Navy & Gold:
```css
--primary: #0d1f3c; --primary2: #162d52;
--cta: #c9973a; --cta2: #e8b84b;
--accent: #1e40af;
```

Forest Green & Amber:
```css
--primary: #14532d; --primary2: #166534;
--cta: #d97706; --cta2: #f59e0b;
--accent: #047857;
```

Slate & Purple:
```css
--primary: #1e1b4b; --primary2: #312e81;
--cta: #7c3aed; --cta2: #8b5cf6;
--accent: #4f46e5;
```

### 3 — Contact Information

Update in all four footers:
```html
<a href="tel:+15550001234">📞 (555) 000-1234</a>
<a href="mailto:hello@gatewayrealty.com">✉️ hello@gatewayrealty.com</a>
<a href="#">📍 200 Gateway Plaza, CA 90210</a>
```

Also update the DRE license number: `DRE #01234567`

### 4 — Member Login Credentials

In `members.html`, find the `USERS` array and update with real credentials (or replace with a proper auth system):

```javascript
const USERS = [
  { email: 'agent@yoursite.com', password: 'YourPassword', name: 'Agent Name', initials: 'AN' },
  { email: 'admin@yoursite.com', password: 'AdminPassword', name: 'Admin',      initials: 'AD' },
];
```

> ⚠️ **Security note:** Credentials in client-side JavaScript are not secure. For production, use a proper backend authentication system (e.g., Firebase Auth, Supabase, Auth0).

### 5 — Default / Seed Listings

The seed data appears in `index.html` (constant `SEED`) and `members.html`. Update or remove entries to match real listings. Each entry must have a unique `id` string.

To clear all data and reset to seed: open DevTools → Application → Local Storage → delete `gw_listings`.

### 6 — Agent Profiles (About Page)

Edit the agent cards in `about.html` and `index.html` (`#agents` section):

```html
<div class="agent-photo">👩‍💼</div>  <!-- emoji or <img src="..."> -->
<div class="agent-name">Your Agent Name</div>
<div class="agent-role">Your Agent Title</div>
<div class="agent-deals">X closings · X.X★</div>
```

### 7 — Hero Stats & Copy

In `index.html`, update the hero statistics:
```html
<div class="hero-stat"><strong>2,400+</strong><span>Homes Sold</span></div>
```

In `about.html`, update the story section and timeline with real company history.

### 8 — Carousel Speed

In `index.html`, find `resetCarouselTimer` and change `5500` (milliseconds) to your preferred interval:
```javascript
carouselTimer = setInterval(carouselNext, 5500);  // 5.5 seconds
```

Set to `0` and remove the `setInterval` call to disable auto-rotation.

---

## Deployment

This is a **static site** — any static host works.

| Host | Steps |
|---|---|
| **GitHub Pages** | Push to a repo, enable Pages in Settings → Pages |
| **Netlify** | Drag and drop the folder at netlify.com/drop |
| **Vercel** | `npx vercel` in the project folder |
| **Any web server** | Upload all 4 HTML files to your public directory |
| **Local** | Double-click `index.html` or run `npx serve .` |

> **Important:** Share links (`listing.html?id=...`) use `localStorage`, which is browser-scoped. When deployed to a real server, listing data won't persist for other visitors unless you replace localStorage with a backend API.

---

## Connecting a Real Backend

The template is designed to make this migration straightforward. Every data operation goes through two functions in `members.html`:

```javascript
// Replace these two with fetch() calls:
listings = JSON.parse(localStorage.getItem('gw_listings') || '[]');
localStorage.setItem('gw_listings', JSON.stringify(listings));
```

**Example with a REST API:**
```javascript
// Load listings
const listings = await fetch('/api/listings').then(r => r.json());

// Save listing
await fetch('/api/listings', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify(newListing)
});
```

---

## Browser Support

Works in all modern browsers. Requires:
- CSS Custom Properties (CSS variables)
- `localStorage`
- `URLSearchParams`
- `navigator.clipboard` (for share/copy — gracefully falls back to `prompt()`)
- `navigator.share` (optional — falls back to clipboard copy)

---

## License

This template is free to use and modify for personal and commercial projects. Attribution appreciated but not required.

---

*Built with plain HTML, CSS, and JavaScript — no frameworks, no build tools, no dependencies.*
