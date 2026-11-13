# 🛏️ Torts & Twirls

**Torts & Twirls** is a full-stack e-commerce web application for a premium bedsheet brand. Customers can browse collections, manage a cart and wishlist, check out securely with Razorpay, and track their orders, while admins manage products, orders, and users from a dedicated dashboard.

🌐 **Live Demo:** [torts-twirls-website-seven.vercel.app](https://torts-twirls-website-seven.vercel.app)

---

## 🚀 Features

- 👤 **User Authentication**
  - Register and log in with JWT-based authentication
  - Forgot / reset password via email link
  - Update profile and change password
  - Protected customer and admin routes

- 🛍️ **Product Catalogue**
  - Browse all products with filters by category
  - Featured products on the home page
  - Product detail page with image gallery, sizes, and reviews
  - Categories: cotton, silk, linen, microfiber, printed, plain, embroidered, luxury

- 🛒 **Cart & Wishlist**
  - Add, update, and remove items in the cart
  - Save favourite products to a wishlist

- 💳 **Checkout & Payments**
  - Multiple saved delivery addresses
  - Secure online payments with **Razorpay**
  - Order success page with order summary

- 📦 **Order Management**
  - View order history and order details
  - Track order status and shipping details
  - Request returns

- ⭐ **Reviews & Ratings**
  - Customers can rate and review products

- 🛠️ **Admin Dashboard**
  - Sales and order statistics
  - Add, edit, and delete products
  - Update order status and shipping information
  - Process returns
  - Manage users

- 🔐 **Security**
  - Password hashing with bcrypt
  - Rate limiting on login and registration
  - Helmet security headers, XSS and NoSQL-injection sanitisation
  - CORS restricted to the frontend URL

- 📱 **Responsive Design**
  - Mobile-friendly layouts for desktop, tablet, and mobile devices

---

## 🛠️ Tech Stack

### Frontend
- React.js (Create React App)
- React Router
- Tailwind CSS
- Context API
- Axios
- React Toastify

### Backend
- Node.js
- Express.js
- JWT Authentication
- Nodemailer
- Razorpay SDK

### Database
- MongoDB
- MongoDB Atlas
- Mongoose

### Deployment
- Vercel (frontend)
- Render (backend)
- MongoDB Atlas (database)

---

## 📂 Project Structure

```text
torts-twirls-website/
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── common/        # Navbar, Footer, route guards
│   │   │   └── product/       # ProductCard, skeleton loaders
│   │   ├── context/           # Auth, Cart, Wishlist
│   │   ├── hooks/
│   │   ├── pages/
│   │   │   └── admin/         # Admin dashboard pages
│   │   ├── utils/api.js
│   │   ├── config.js
│   │   └── App.js
│   ├── package.json
│   ├── tailwind.config.js
│   └── vercel.json
│
├── backend/
│   ├── controllers/
│   ├── middleware/
│   ├── models/                # User, Product, Cart, Order
│   ├── routes/
│   ├── scripts/seed.js
│   ├── utils/sendEmail.js
│   ├── server.js
│   └── package.json
│
└── README.md
```

---

## ⚙️ Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/nishant70000/torts-twirls-website.git
cd torts-twirls-website
```

---

### 2. Setup Backend

Navigate to the backend directory:

```bash
cd backend
```

Install dependencies:

```bash
npm install
```

Create a `.env` file inside the `backend` folder (see [Environment Variables](#-environment-variables)).

(Optional) Load sample products and demo accounts:

```bash
npm run seed
```

> ⚠️ The seed script **deletes all existing users and products** before inserting sample data. Only run it on a fresh database.

Start the backend server:

```bash
npm run dev
```

The backend will run on:

```text
http://localhost:5000
```

Health check:

```text
http://localhost:5000/api/health
```

---

### 3. Setup Frontend

Open another terminal and navigate to the frontend:

```bash
cd frontend
```

Install dependencies:

```bash
npm install
```

Create a `.env` file inside the `frontend` folder:

```env
REACT_APP_API_URL=http://localhost:5000/api
```

Start the development server:

```bash
npm start
```

The frontend will run on:

```text
http://localhost:3000
```

---

## 🔑 Environment Variables

### Backend (`backend/.env`)

```env
PORT=5000
NODE_ENV=development

MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
JWT_EXPIRES_IN=7d

FRONTEND_URL=http://localhost:3000

RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret

# Optional – for password reset emails
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password
SMTP_FROM=Torts & Twirls <your_email@gmail.com>
```

### Frontend (`frontend/.env`)

```env
REACT_APP_API_URL=http://localhost:5000/api
```

> ⚠️ **Important:** Never commit your `.env` files or API keys to GitHub. They are already listed in `.gitignore`.

---

## 🔄 Application Flow

```text
Customer / Admin
  │
  ▼
React Frontend (Vercel)
  │
  │ Axios / HTTP Requests + JWT
  ▼
Express REST API (Render)
  │
  ▼
Auth Middleware (protect / admin)
  │
  ▼
Controllers ──────► Razorpay (payments)
  │          └────► SMTP (emails)
  ▼
MongoDB Atlas
```

---

## 📡 API Structure

All endpoints are prefixed with `/api`.

### Auth & Profile

| Method | Endpoint | Description |
|---|---|---|
| POST | `/auth/register` | Register a new user |
| POST | `/auth/login` | Login user |
| GET | `/auth/me` | Get logged-in user |
| PUT | `/auth/profile` | Update profile |
| PUT | `/auth/password` | Change password |
| POST | `/auth/forgot-password` | Send password reset email |
| POST | `/auth/reset-password/:token` | Reset password |
| GET / POST | `/auth/addresses` | List / add addresses |
| PUT / DELETE | `/auth/addresses/:addressId` | Update / delete an address |

### Products & Reviews

| Method | Endpoint | Description |
|---|---|---|
| GET | `/products` | List products (with filters) |
| GET | `/products/featured` | Featured products |
| GET | `/products/categories` | Product categories |
| GET | `/products/:id` | Product details |
| POST | `/products/:id/reviews` | Add a review |
| GET | `/reviews/product/:productId` | Reviews for a product |

### Cart, Wishlist & Orders

| Method | Endpoint | Description |
|---|---|---|
| GET / POST / DELETE | `/cart` | View / add to / clear cart |
| PUT / DELETE | `/cart/:itemId` | Update / remove a cart item |
| GET | `/wishlist` | View wishlist |
| POST | `/wishlist/:productId` | Toggle wishlist item |
| POST | `/orders` | Place an order |
| GET | `/orders/my` | My orders |
| GET | `/orders/:id` | Order details |
| PUT | `/orders/:id/pay` | Mark order as paid |
| POST | `/orders/:id/return` | Request a return |

### Payments

| Method | Endpoint | Description |
|---|---|---|
| POST | `/payment/razorpay/create` | Create Razorpay order |
| POST | `/payment/razorpay/verify` | Verify Razorpay payment |

### Admin

| Method | Endpoint | Description |
|---|---|---|
| GET | `/admin/stats` | Dashboard statistics |
| DELETE | `/admin/products/:id` | Delete a product |
| GET | `/admin/orders` | All orders |
| GET | `/admin/orders/:id` | Order details |
| PUT | `/admin/orders/:id/status` | Update order status |
| PUT | `/admin/orders/:id/shipping` | Update shipping details |
| PATCH | `/admin/orders/:id/return` | Process a return |

---

## 🗄️ Database

Torts & Twirls uses **MongoDB Atlas** for storing application data.

```text
Users
  │
  ├── Profile & Authentication
  ├── Saved Addresses
  ├── Wishlist
  └── Role (user / admin)

Products
  │
  ├── Name, Description, Price
  ├── Category & Sizes
  ├── Images
  └── Reviews & Ratings

Carts
  └── Items (product, size, quantity)

Orders
  │
  ├── Items & Pricing
  ├── Shipping Address
  ├── Payment Details (Razorpay)
  ├── Status & Tracking
  └── Return Requests
```

---

## 🌐 Deployment

| Part | Platform | Settings |
|---|---|---|
| Frontend | **Vercel** | Root directory `frontend`, env `REACT_APP_API_URL` |
| Backend | **Render** | Root directory `backend`, build `npm install`, start `npm start` |
| Database | **MongoDB Atlas** | Allow network access from `0.0.0.0/0` |

After deploying the frontend, set `FRONTEND_URL` on the backend to the Vercel URL so CORS allows it.

> ℹ️ Render's free tier sleeps after ~15 minutes of inactivity, so the first request may take 30–50 seconds.

---

## 🔮 Future Improvements

- 🔎 Full-text product search
- 🎟️ Coupon and discount codes
- 📧 Order confirmation and shipping emails
- 🖼️ Cloud image uploads for products
- 📊 Advanced sales analytics for admins
- 🌍 Multi-currency support
- 📱 Progressive Web App (PWA) support

---

## ⭐ Contributing

Contributions are welcome!

1. Fork the repository
2. Create a new branch

```bash
git checkout -b feature/your-feature
```

3. Make your changes
4. Commit your changes

```bash
git commit -m "Add new feature"
```

5. Push the branch

```bash
git push origin feature/your-feature
```

6. Open a Pull Request

---

## 📄 License

This project is developed for educational and portfolio purposes.
