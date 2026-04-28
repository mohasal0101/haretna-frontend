# أهوة حارتنا — Haretna Café
### Digital Ordering System · Frontend

> A full-featured café ordering web app built as a single HTML file. Customers scan a QR code at their table, browse the menu, and place orders — which appear instantly on the admin dashboard in real time.

---

## ✨ Features

### Customer Side
- 📱 **QR Code ordering** — each table has a unique QR that auto-assigns the customer to their table
- 🍽️ **Full bilingual menu** — Arabic & English, 23 categories, 100+ items
- 🏷️ **Live offers banner** — combo deals and promotions set by admin
- 🔥 **Trending items** — highlighted popular items set by admin
- 🛒 **Smart cart** — item notes, quantity controls, suggested pairings
- ⏱️ **5-second cancel window** — animated countdown before order is sent
- 🔔 **Table bell** — customers can call waiter, request bill, water, napkins
- 📸 **Image zoom** — tap any menu item photo to expand it

### Admin Dashboard
- 🔐 **Secure login** — JWT-authenticated staff access
- 📋 **Live order tracking** — New → Preparing → Ready → Done → Cashed Out
- ✏️ **Edit orders** — remove items from an active order, totals recalculate automatically
- 📦 **Stock manager** — mark items out of stock by category, reflects on customer menu instantly
- 🏷️ **Offers editor** — create/edit/delete combo offers with item picker
- 🔥 **Trending editor** — choose which items appear in the trending section
- 📷 **Image uploads** — upload photos per menu item (stored on Cloudinary)
- 📊 **Sales summary** — revenue, order count, top items, orders by hour
- 📋 **Order history** — browse all cashed-out orders filtered by date
- 🖨️ **Receipt printing** — printable receipt with 16% tax breakdown
- 🔕 **Sound toggle** — audio alert for new orders
- 🖨️ **QR code generator** — print all 12 table QR codes at once

### Real-time
- ⚡ **Socket.io** — new orders appear on admin dashboard instantly, no refresh needed
- 🔄 **Live menu sync** — stock changes and image uploads reflect for all customers immediately

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript (single file) |
| Fonts | Rubik (Latin), Amiri (Arabic) — embedded |
| Real-time | Socket.io client |
| Backend API | Node.js + Express (separate repo) |
| Database | PostgreSQL via Neon |
| Image Storage | Cloudinary |
| Auth | JWT tokens |

---

## 🚀 Getting Started

### Prerequisites
- The **backend server** must be running — see [haretna-backend](../haretna-backend)
- A modern browser (Chrome, Safari, Firefox, Edge)

### Local Development

1. Make sure the backend is running on port 4000:
   ```bash
   cd haretna-backend
   npm run dev
   ```

2. Open `index.html` directly in your browser — no build step needed.

3. Select a table and start ordering!

### Configuration

At the top of the `<script>` section, find and update:

```javascript
const API_URL = 'http://localhost:4000';  // ← change to your production URL
```

For production, set this to your deployed backend URL:
```javascript
const API_URL = 'https://your-backend.up.railway.app';
```

---

## 🌐 Deployment (GitHub Pages)

Since this is a single HTML file, GitHub Pages works perfectly.

1. Rename the file to `index.html`
2. Push to a GitHub repository
3. Go to **Settings → Pages → Deploy from branch → main**
4. Your site will be live at `https://yourusername.github.io/haretna-frontend`

> ⚠️ **Important:** Update `API_URL` to your production backend URL before deploying, otherwise customers won't be able to place orders.

---

## 📱 QR Code Setup

Each table gets a unique QR code that encodes the table number directly in the URL:

```
https://yoursite.com/index.html?cafe=haretna&table=1
```

When a customer scans it, they are automatically assigned to Table 1 with no selection needed.

To print QR codes:
1. Log in to the admin dashboard
2. Click **🖨 Print QR Codes**
3. Print and laminate — place one on each table

---

## 🔐 Admin Access

| Username | Password |
|---|---|
| `haretna_admin` | `Haretna@2025!` |
| `manager` | `CafeManager#1` |

> Change these in the backend `.env` file and re-seed for production.

To access the admin dashboard:
- On the landing page, click **Staff Login · دخول الموظفين**
- Or go directly to the login screen

---

## 📂 Project Structure

```
index.html          ← The entire frontend (HTML + CSS + JS)
README.md           ← This file
```

The entire app lives in one file — no build tools, no dependencies, no `npm install`.

---

## 🔗 Related

- **Backend repo** — Node.js + Express + Prisma + Socket.io → `haretna-backend`
- **Database** — PostgreSQL hosted on [neon.tech](https://neon.tech)
- **Image CDN** — [Cloudinary](https://cloudinary.com)

---

## 📸 Menu Categories

The menu covers all of Haretna Café's offerings:

`Breakfast` · `Breakfast Sandwiches` · `Manakish` · `Appetizers` · `Salads` · `Pizza` · `Pasta` · `Sandwiches & Burgers` · `Fukharat` · `Soups` · `Main Dishes` · `Desserts` · `Snacks` · `Hot Coffee` · `Ice Coffee` · `Cold Drinks` · `Fresh Juice` · `Mojito` · `Milkshake` · `Fresh Mix` · `Tea` · `Soft Drinks` · `Hookah`

---

## 📄 License

Private — Haretna Café · Amman, Jordan 🇯🇴

---

*Built with ❤️ for أهوة حارتنا*
