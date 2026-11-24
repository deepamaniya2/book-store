# 📚 BookStop - Full-Stack Mobile & Web Bookstore Application

[![Frontend Build](https://img.shields.io/badge/Frontend-Vite%20%2B%20React-blue.svg)](https://vitejs.dev/)
[![Backend](https://img.shields.io/badge/Backend-Node.js%20%2B%20Express-green.svg)](https://expressjs.com/)
[![Styling](https://img.shields.io/badge/Styling-Tailwind%20CSS-38B2AC.svg)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**BookStop** is a modern, responsive full-stack bookstore application designed with an aesthetic literary theme, smooth micro-interactions, and a complete e-commerce user experience. It provides a mobile-first responsive layout, dynamic book browsing, interactive cart and wishlist management, promo code validation, and checkout flows powered by a RESTful Express backend.

---

## 🌟 Key Features

### 📖 User Experience & Frontend
- **Aesthetic Literary Design**: Warm editorial color palette, clean typography (Google Manrope font), and smooth mobile-first responsive layouts.
- **Dynamic Book Catalog & Search**: Real-time search across titles, authors, and genres, with dedicated views for Trending and Recommended books.
- **Detailed Book Pages**: Rich synopsis display, ratings, user reviews count, genre tags, and contextual "Similar Books" recommendations.
- **Interactive Shopping Cart**: Live quantity increments/decrements, item removal, dynamic subtotal calculations, and free/express delivery options.
- **Promo Code Engine**: Discount validation supporting codes such as `SUMMER40` (40% off) and `BOOKSTOP10` (10% off) with instant UI feedback.
- **Checkout & Order Flow**: Multi-step checkout with address selection, payment method choices, order reference generation, and automated cart clearing.
- **Wishlist & User Profile**: Interactive wishlist toggling, user statistics (reviews, read books, reading streak), and past order history viewing.
- **Resilient Dual-Layer Architecture**: Communicates with the live backend API, with automatic graceful fallback to local data if the backend is offline.

### ⚙️ REST API & Backend
- **Express.js Architecture**: Clean ES-module based REST API with modular routing.
- **Persistent JSON Database**: Lightweight and portable file-based JSON storage (`db.json`) for books, categories, cart state, orders, and user profile.
- **CORS & Logging Middleware**: Full cross-origin resource sharing support and morgan request logging.
- **Dynamic Port Assignment**: Supports production deployment environments via `process.env.PORT` with local fallback to port `5000`.

---

## 🛠️ Technologies Used

### Frontend
- **React 18**: Component-based UI library.
- **Vite 5**: High-performance next-generation frontend bundler and dev server.
- **React Router v6**: Client-side routing with SPA fallback.
- **Tailwind CSS 3**: Utility-first responsive CSS styling with custom theme variables.
- **Lucide React & Google Material Symbols**: Clean modern iconography.

### Backend
- **Node.js**: Modern JavaScript runtime (ES Modules enabled).
- **Express.js 4**: Fast, unopinionated web framework.
- **CORS**: Cross-origin resource sharing middleware.
- **Morgan**: HTTP request logger middleware.
- **Dotenv**: Environment variable configuration.
- **File System (fs/promises)**: Asynchronous JSON database persistence.

---

## 📁 Folder Structure

```text
stitch_bookshop_mobile_bookstore_app/
├── Frontend/                          # React + Vite Frontend Application
│   ├── public/                        # Static public assets
│   ├── src/
│   │   ├── components/                # Reusable UI components
│   │   │   ├── BookCard.jsx           # Individual book card display
│   │   │   ├── BottomNav.jsx          # Mobile bottom navigation bar
│   │   │   ├── Header.jsx             # Top desktop/mobile header
│   │   │   └── Toast.jsx              # Global notification toast
│   │   ├── context/
│   │   │   └── CartContext.jsx        # Global state for cart, wishlist & promos
│   │   ├── data/
│   │   │   └── books.js               # Initial catalog and fallback mock data
│   │   ├── pages/                     # Application views / routes
│   │   │   ├── BookDetails.jsx        # Single book details view
│   │   │   ├── Categories.jsx         # Category browser view
│   │   │   ├── Checkout.jsx           # Checkout and payment view
│   │   │   ├── HomeFeed.jsx           # Main home page with search and trending
│   │   │   ├── Onboarding.jsx         # App onboarding walkthrough
│   │   │   ├── Profile.jsx            # User profile, orders, and wishlist
│   │   │   ├── ShoppingCart.jsx       # Cart view with promo discounts
│   │   │   └── SplashScreen.jsx       # Initial welcome splash
│   │   ├── services/
│   │   │   └── api.js                 # Unified API client with backend integration
│   │   ├── App.jsx                    # Root component with routing
│   │   ├── index.css                  # Global Tailwind CSS definitions
│   │   └── main.jsx                   # React DOM entry point
│   ├── index.html                     # HTML template
│   ├── package.json                   # Frontend dependencies and scripts
│   ├── tailwind.config.js             # Tailwind CSS theme configuration
│   ├── vercel.json                    # Vercel deployment configuration
│   └── vite.config.js                 # Vite bundler & local /api proxy config
│
├── backend/                           # Node.js + Express Backend Application
│   ├── src/
│   │   ├── data/
│   │   │   ├── db.js                  # Database query and mutation methods
│   │   │   └── db.json                # JSON data store (books, cart, orders, user)
│   │   ├── routes/                    # Modular API route controllers
│   │   │   ├── books.routes.js        # /api/books endpoints
│   │   │   ├── cart.routes.js         # /api/cart endpoints
│   │   │   ├── categories.routes.js   # /api/categories endpoints
│   │   │   ├── orders.routes.js       # /api/orders endpoints
│   │   │   ├── promos.routes.js       # /api/promos endpoints
│   │   │   └── user.routes.js         # /api/user endpoints
│   │   └── server.js                  # Main server entry file
│   └── package.json                   # Backend dependencies and scripts
│
├── .gitignore                         # Git ignore rules for node_modules and builds
└── README.md                          # Project documentation
```

---

## 📡 Backend API Endpoints

The backend listens on `http://localhost:5000` (or `process.env.PORT`) with the following endpoints:

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` or `/api` | API directory and service health overview |
| `GET` | `/api/health` | Health check endpoint |
| `GET` | `/api/books` | Get books list (supports `?genre=`, `?search=`, `?trending=true`) |
| `GET` | `/api/books/:id` | Get single book details by ID |
| `GET` | `/api/books/:id/similar` | Get similar books for a specific book |
| `GET` | `/api/categories` | Get category list with live book counts |
| `GET` | `/api/cart` | Get current cart items, total quantity, and subtotal |
| `POST` | `/api/cart` | Add a book to the cart (`{ bookId, quantity }`) |
| `PATCH` | `/api/cart/:bookId` | Increment/decrement item quantity (`{ delta }`) |
| `DELETE` | `/api/cart/:bookId` | Remove a specific item from cart |
| `DELETE` | `/api/cart` | Clear all items from cart |
| `POST` | `/api/promos/validate` | Validate discount code (`{ code: "SUMMER40" }`) |
| `GET` | `/api/orders` | Get list of all past orders |
| `POST` | `/api/orders` | Place a new order (`{ items, shippingAddress, ... }`) |
| `GET` | `/api/user/profile` | Get user profile information and reading stats |
| `PUT` | `/api/user/profile` | Update user profile information |
| `GET` | `/api/user/wishlist` | Get wishlisted books as full objects |
| `POST` | `/api/user/wishlist/:bookId` | Toggle a book in/out of the user wishlist |

---

## 🚀 Installation & Local Development

### Prerequisites
- **Node.js** (v18.0.0 or higher recommended)
- **npm** (v9.0.0 or higher)
- **Git**

---

### Step 1: Clone the Repository

```bash
git clone https://github.com/deepamaniya2/stitch-bookshop-mobile-bookstore-app.git
cd stitch-bookshop-mobile-bookstore-app
```

---

### Step 2: Install and Run the Backend

1. Navigate into the `backend` folder:
   ```bash
   cd backend
   ```

2. Install backend dependencies:
   ```bash
   npm install
   ```

3. Start the backend server:
   ```bash
   npm start
   ```

   The backend will start on **`http://localhost:5000`**. You should see:
   ```text
   =============================================
   🚀 BookStop Backend API is running!
   📡 URL: http://localhost:5000
   🩺 Health: http://localhost:5000/api/health
   📚 Books: http://localhost:5000/api/books
   =============================================
   ```

---

### Step 3: Install and Run the Frontend

1. Open a **new terminal window** and navigate into the `Frontend` folder:
   ```bash
   cd Frontend
   ```

2. Install frontend dependencies:
   ```bash
   npm install
   ```

3. Start the Vite development server:
   ```bash
   npm run dev
   ```

4. Open your browser and navigate to:
   ```text
   http://localhost:3000
   ```

> **Note on Local Proxy:** The frontend Vite dev server includes an integrated proxy configured in `Frontend/vite.config.js` that automatically forwards requests from `/api/*` to `http://127.0.0.1:5000`. This allows seamless communication without manual CORS configuration.

---

### Step 4: Build for Production

To test or verify the production bundle:

```bash
cd Frontend
npm run build
```

The compiled output will be generated in `Frontend/dist/`.

---

## ☁️ Deployment Instructions

### Deploying the Frontend to Vercel

1. Import your GitHub repository into [Vercel](https://vercel.com).
2. In the **Configure Project** screen, set:
   - **Framework Preset**: `Vite`
   - **Root Directory**: `Frontend`
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
   - **Install Command**: Leave default (`npm install`) — **do not override with `npm run build`**
3. (Optional) In **Environment Variables**, add:
   - `VITE_API_BASE_URL`: `https://your-backend-domain.com/api` (if connecting to a remote backend).
4. Click **Deploy**.

> `Frontend/vercel.json` includes SPA routing rewrites (`"source": "/(.*)", "destination": "/index.html"`) so all routes reload cleanly on Vercel without 404 errors.

---

## 🧪 Testing Verification

All core flows and endpoints have been thoroughly tested:
- **Backend API Suite**: 16/16 endpoints verified with status `200` and `201`.
- **Frontend Integration**: 10/10 service calls verified for catalog, cart mutations, promo validation, and checkout.
- **Frontend Build**: Zero-error Vite production build tested and verified (`dist/index.html`, CSS, and JS bundles).

---

## 📄 License
This project is submitted for academic assessment purposes under the MIT License.
