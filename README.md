# Inventory-system
A full-stack Inventory Management System built using React, PHP, MySQL, and JWT for efficient stock and user management.

# 📦 InvenTrack Pro — Inventory Management System
### Capstone Project | Full-Stack Web Application

---

## Tech Stack

| Layer     | Technology                          |
|-----------|-------------------------------------|
| Frontend  | React 18 (CDN), Chart.js, HTML/CSS  |
| Backend   | PHP 8.x REST API                    |
| Database  | MySQL 8 (managed via phpMyAdmin)    |
| Auth      | JWT (HS256 via hash_hmac)           |

---

## Project Structure

```
inventory-system/
├── database/
│   └── inventory_db.sql        ← Import into phpMyAdmin
├── backend/
│   ├── config.php              ← DB config + JWT helpers
│   └── api/
│       ├── auth.php            ← POST  /api/auth.php
│       ├── products.php        ← CRUD  /api/products.php
│       ├── categories.php      ← CRUD  /api/categories.php
│       ├── suppliers.php       ← CRUD  /api/suppliers.php
│       ├── transactions.php    ← Stock in/out
│       └── dashboard.php       ← Aggregated stats
└── frontend/
    └── index.html              ← Single-page React app
```

---

## Setup Instructions

### Step 1 — Import the Database

1. Open **phpMyAdmin** in your browser (`http://localhost/phpmyadmin`)
2. Click **Import** tab
3. Choose `database/inventory_db.sql`
4. Click **Go**

This creates the `inventory_db` database with all tables and sample data.

---

### Step 2 — Configure the Backend

Open `backend/config.php` and update:

```php
define('DB_HOST', 'localhost');
define('DB_USER', 'root');       // your MySQL username
define('DB_PASS', '');           // your MySQL password
define('DB_NAME', 'inventory_db');
```

---

### Step 3 — Place Files on Web Server

**Option A — XAMPP / WAMP / LAMP:**
Copy the entire `inventory-system/` folder to:
- XAMPP: `C:\xampp\htdocs\inventory-system\`
- WAMP:  `C:\wamp64\www\inventory-system\`
- Linux: `/var/www/html/inventory-system/`

**Option B — PHP built-in server (dev):**
```bash
cd inventory-system/backend
php -S localhost:8000
```
Then update `BASE_URL` in `frontend/index.html`:
```js
const BASE_URL = 'http://localhost:8000';
```

---

### Step 4 — Open the Frontend

Open `frontend/index.html` in your browser:
- Via XAMPP: `http://localhost/inventory-system/frontend/index.html`
- Direct file open also works (update CORS in config.php if needed)

---

## Login Credentials

| Username | Password  | Role  |
|----------|-----------|-------|
| admin    | password  | Admin |

> To change the password, generate a new bcrypt hash:
> ```php
> echo password_hash('YourNewPassword', PASSWORD_BCRYPT);
> ```
> Then update the `users` table via phpMyAdmin.

---

## Features

### Dashboard
- KPI cards: Total Products, Inventory Value, Low Stock, Out of Stock
- Bar chart: Stock In vs Stock Out (last 7 days)
- Category breakdown with progress bars
- Recent transactions feed
- Live low-stock alerts

### Products Module
- Full CRUD (Create, Read, Update, Delete)
- Search by name or SKU
- Filter by category and status
- Stock level visualization bar
- Quick stock update modal (stock in / stock out / adjustment)
- Profit margin calculation on detail view

### Transactions
- Complete audit log of all stock movements
- Stock In / Stock Out / Adjustment types
- Auto-updates product quantity on transaction

### Suppliers & Categories
- Manage supplier contacts and details
- Organize products into categories
- Relationship maintained via foreign keys

### Reports
- Inventory summary statistics
- Category breakdown
- Quick insights panel

---

## Database Schema

```
categories  →  products  ←  suppliers
                   ↓
             transactions
                   
users  (authentication)
```

**Foreign Keys:**
- `products.category_id` → `categories.id`
- `products.supplier_id` → `suppliers.id`
- `transactions.product_id` → `products.id`

---

## API Endpoints

| Method | Endpoint              | Description           |
|--------|-----------------------|-----------------------|
| POST   | /api/auth.php         | Login, returns JWT    |
| GET    | /api/products.php     | List all products     |
| POST   | /api/products.php     | Create product        |
| PUT    | /api/products.php?id= | Update product        |
| DELETE | /api/products.php?id= | Delete product        |
| GET    | /api/categories.php   | List categories       |
| POST   | /api/categories.php   | Create category       |
| GET    | /api/suppliers.php    | List suppliers        |
| POST   | /api/suppliers.php    | Create supplier       |
| PUT    | /api/suppliers.php?id=| Update supplier       |
| GET    | /api/transactions.php | List transactions     |
| POST   | /api/transactions.php | Record stock movement |
| GET    | /api/dashboard.php    | Aggregated stats      |

All endpoints (except auth) require `Authorization: Bearer <token>` header.

---

## Presentation Notes

This capstone project demonstrates:
- **Full-stack architecture**: Decoupled frontend + REST backend
- **Database design**: Normalized schema with foreign key constraints
- **Authentication**: Stateless JWT-based auth
- **CRUD operations**: Complete data lifecycle management
- **Real-time insights**: Dashboard with live aggregated data
- **Responsive UI**: Professional dark theme with Chart.js visualizations
- **Data integrity**: Transaction-based stock updates, constraint validation

---
