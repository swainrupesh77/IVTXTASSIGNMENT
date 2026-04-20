# 🍔 Burger Builder

A full-stack Burger Builder application built with **ReactJS**, **NodeJS (Express)**, and **MongoDB Atlas**.

---

## Project Structure

```
burger-builder/
├── server/
│   ├── index.js              # Express server entry point
│   ├── models/
│   │   └── Order.js          # Mongoose order schema
│   └── routes/
│       └── orders.js         # Order API routes
├── client/
│   └── src/
│       ├── constants.js      # Slice types & prices
│       ├── context/
│       │   └── BurgerContext.js   # Global state (useReducer)
│       ├── utils/
│       │   └── pricing.js         # Price calculation logic
│       ├── components/
│       │   ├── BurgerVisualization.js
│       │   ├── SliceSelector.js
│       │   ├── PriceSummary.js
│       │   └── CheckoutForm.js
│       ├── pages/
│       │   └── Builder.js
│       ├── App.js
│       ├── index.js
│       └── index.css
├── .env                      # MongoDB URI (do not commit)
├── .gitignore
└── package.json
```

---

## Setup & Run

### 1. Clone and install dependencies

```bash
git clone <your-repo-url>
cd burger-builder
npm run install-all
```

### 2. Configure MongoDB Atlas

1. Go to [https://cloud.mongodb.com](https://cloud.mongodb.com)
2. Create a free cluster
3. Create a database user with read/write access
4. Get your connection string
5. Edit `.env` and replace with your actual URI:

```env
MONGO_URI=mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/burgerbuilder?retryWrites=true&w=majority
PORT=5000
```

### 3. Run the full app (single command)

```bash
npm run dev
```

This starts:
- **Backend** on `http://localhost:5000`
- **Frontend** on `http://localhost:3000` (auto-proxied to backend)

### 4. Production build

```bash
npm run build
npm start
```

The React build is served by Express at `http://localhost:5000`.

---

## Features

| Feature | Details |
|---|---|
| Burger Visualization | Real-time stacked layer view with distinct colors |
| Add/Remove Slices | Aloo Tikki, Paneer, Cheese, Tomato, Onion, Lettuce |
| Reorder Slices | ↑ ↓ controls on each filling layer |
| Structural Rules | Bread fixed at top & bottom, max 10 slices |
| Quantity Control | +/− buttons, updates total price live |
| Conditional Pricing | Cheese+Paneer discount, Aloo Tikki pair charge |
| Chef Warning | Shows message if burger has 6+ fillings |
| Checkout | Name, Mobile, Address, Payment with validation |
| Order Storage | Saved to MongoDB Atlas |

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/orders` | Place a new order |
| GET | `/api/orders` | Get all orders |

---

## Price Formula

```
Total = (Sum of slice prices - discounts + extras) × Quantity + ₹10 Platform Fee
```

**Conditional Rules:**
- Cheese + Paneer together → **-₹3 discount**
- Two consecutive Aloo Tikki → **+₹2 extra**
- More than 6 fillings → show chef warning message
npm run dev
