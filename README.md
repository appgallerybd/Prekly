# Prekly — Premium Islamic Bookstore
বাংলাদেশের জন্য বাংলা ভাষাভিত্তিক ইসলামী বইয়ের অনলাইন বুকশপ।

## Stack
- Storefront: React + Vite
- API: Node.js + Express
- Initial data source: Google Sheets API
- Checkout: Cash on Delivery
- Hosting: Vercel frontend + Render/Railway API

## Local setup
1. Install Node.js 20+.
2. Run API: `cd server && npm install && cp .env.example .env && npm run dev`
3. Run storefront: `cd client && npm install && cp .env.example .env && npm run dev`
4. Configure server secrets and Google Sheets before accepting real orders.

## Google Sheets
Create a spreadsheet with tabs and headers:
- Books: id,title,author,category,price,oldPrice,stock,cover,tag,active
- Orders: orderId,customerName,phone,address,paymentMethod,items,subtotal,deliveryCharge,total,status,createdAt
Share the spreadsheet with the service-account email as Editor. Put the service-account JSON in server environment variable GOOGLE_SERVICE_ACCOUNT_JSON. Never put secrets in client code or commit them.

## Deploy
Deploy `client` as Vite app (build: npm run build, output: dist); set VITE_API_URL to deployed API URL. Deploy `server` as Node service and set FRONTEND_ORIGIN, ADMIN_PASSWORD, GOOGLE_SHEET_ID, GOOGLE_SERVICE_ACCOUNT_JSON.

## Important
Starter/MVP implementation. Before public commerce launch, add persistent session storage, rate limiting, CSRF protection, order idempotency, status-update routes, stock decrement/locking, privacy/return policy, backup and end-to-end tests. Google Sheets is not a transactional database; migrate to PostgreSQL when orders/traffic grow.
