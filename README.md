# أهوة حارتنا — Haretna Café

> A full-stack digital menu and order management system built for Haretna Café, Amman, Jordan. Customers scan a QR code at their table, browse the menu, and place orders — all without a waiter. Staff manage everything in real time from the same interface.

---

## Features

### Customer Side
- **QR-based table detection** — customers scan a table QR code and are taken straight to their table's menu session
- **Bilingual UI** — full Arabic and English throughout (RTL/LTR aware)
- **Item detail popup** — tap any item to see its image, description, price, and add a custom note (e.g. "no onions")
- **Smart cart bar** — a sticky gold bar slides up from the bottom as soon as an item is added, showing live item count and total
- **Categories navigator** — a docked tab at the bottom lets customers jump between menu categories instantly
- **Table calls** — one-tap buttons to request a waiter, water, napkins, or the bill, with a 30-second cooldown to prevent spam
- **Order confirmation** — a 5-second countdown before submitting gives customers a chance to cancel
- **Cart resets after order** — all quantities return to zero after a successful order is placed

### Admin Side
- **Live order dashboard** — new orders appear instantly via Socket.io with an audio alert
- **Order stacking by table** — if a table places a second order, items are merged into the existing card with a "NEW" badge and gold highlight (auto-clears after 8 seconds)
- **Order status flow** — New → Preparing → Ready → Done → Cashed Out
- **Table call notifications** — waiter/water/napkins/bill requests appear as separate cards on the dashboard
- **Receipt generation** — one click prints a formatted receipt with subtotal, 16% tax, and grand total
- **Trending items** — admin pins up to 5 trending items that appear in the cart for upselling; persists via localStorage
- **Offers / combos** — admin creates combo deals with custom pricing; customers can add them from the menu; persists via localStorage
- **Item editing** — admin can edit any item's name (EN/AR), description, and price directly from the item popup
- **Stock management** — toggle items in/out of stock; syncs across all connected devices in real time
- **Image uploads** — upload custom photos per item; stored via the backend API
- **Sales history** — view cashed-out orders by date with revenue totals

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript (single-file SPA) |
| Real-time | Socket.io (client v4.7.5) |
| Font | Rubik (self-hosted, Arabic-compatible) |
| Backend | Node.js REST API (hosted on Railway) |
| Database | PostgreSQL (via Railway) |
| Deployment | Railway (backend + DB), static file hosting (frontend) |

---

## Project Structure

```
/
├── index.html          # Entire frontend — menu, cart, admin dashboard
└── README.md
```

The frontend is intentionally a single self-contained HTML file with no build step, no bundler, and no framework dependencies. This makes it trivial to deploy anywhere — just serve the file.

The backend lives in a separate repository and exposes a REST API consumed by this frontend.

---

## Configuration

Open `index.html` and find line ~1264:

```js
const API_URL = 'https://haretna-backend-production.up.railway.app';
```

Change this to point to your backend if you fork or self-host.

---

## API Endpoints Used

| Method | Path | Description |
|---|---|---|
| `POST` | `/api/auth/login` | Admin login |
| `GET` | `/api/auth/me` | Verify session token |
| `GET` | `/api/menu` | Fetch full menu with categories and items |
| `GET` | `/api/menu/trending` | Fetch trending item IDs |
| `PATCH` | `/api/menu/items/:id/stock` | Toggle item stock status |
| `GET` | `/api/offers` | Fetch active offers/combos |
| `POST` | `/api/orders` | Place a new order |
| `GET` | `/api/orders` | Fetch active orders (admin) |
| `PATCH` | `/api/orders/:id/status` | Update order status |
| `DELETE` | `/api/orders/:id/items/:itemId` | Remove item from order |
| `GET` | `/api/orders/history` | Fetch cashed-out order history |
| `POST` | `/api/upload/menu-item/:id` | Upload item image |

---

## Socket.io Events

| Event | Direction | Description |
|---|---|---|
| `admin:join` | Client → Server | Admin joins the real-time room |
| `order:new` | Server → Client | New order placed by a customer |
| `order:updated` | Server → Client | Order status changed |
| `order:cashed` | Server → Client | Order cashed out |
| `menu:updated` | Server → Client | Item stock or image updated |
| `table:call` | Client ↔ Server | Customer requests waiter/water/napkins/bill |

---

## Running Locally

Since the frontend is a single HTML file, you just need to serve it:

```bash
# Using Python
python3 -m http.server 3000

# Using Node.js (npx)
npx serve .

# Using VS Code
# Install the Live Server extension and click "Go Live"
```

Then open `http://localhost:3000` in your browser.

> **Note:** You'll need the backend running and `API_URL` pointing to it for any data to load.

---

## QR Code Setup

Each table gets its own QR code that encodes a URL with the table number as a query parameter:

```
https://your-domain.com/?table=5
```

The frontend reads `?table=` from the URL on load and uses it for all orders and calls placed during that session. Generate QR codes using any free QR generator (e.g. qr-code-generator.com) and print them for each table.

---

## Admin Access

Navigate to the menu and tap the admin login button (key icon in the header). Enter your staff credentials. Admin features — item editing, stock toggling, image uploads, the order dashboard, and offers management — are all gated behind this login.

Credentials are managed on the backend. Contact your backend administrator or check your Railway environment variables to reset them.

---

## Browser Support

Tested on:
- iOS Safari 16+
- Android Chrome 110+
- Desktop Chrome / Firefox / Edge (latest)

Not supported: Internet Explorer.

---

## License

Private — all rights reserved. Built for Haretna Café, Amman, Jordan.
