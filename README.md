<div align="center">
  <img src="https://cdn-icons-png.flaticon.com/512/3514/3514491.png" alt="ShopNest Logo" width="80" />
  <h1>ShopNest - Full-Stack MERN E-Commerce App</h1>
  <p>A professionally engineered, full-stack E-commerce platform built strictly using modern standard React (CRA) on the frontend and Express/MongoDB on the backend.</p>
</div>

---

## 🛠 Tech Stack Details

- **Frontend:** Pure React.js (`react-scripts`), Redux Toolkit (for Cart state management), AuthContext API (for JWT user sessions).
- **Backend:** Node.js, Express.js architecture mapped with middleware-based routing.
- **Database:** MongoDB (via Mongoose schemas).
- **Features:** Unified Admin Dashboard, Direct Cloudinary Content Maps, Personal User Profiles matching mapped Order Histories.
- **Payments:** Razorpay fully implemented (utilize your test metrics or placeholder).
- **Cloud Storage:** Cloudinary integration for Product image uploading securely via Multer.

---

## Local Development

Use Node.js 22 and npm. MongoDB must be available locally or through MongoDB Atlas.

1. Create `backend/.env` using `backend/.env.example` as a template. Set at least:

   ```env
   PORT=5000
   NODE_ENV=development
   MONGO_URI=mongodb://127.0.0.1:27017/shopnest
   JWT_SECRET=replace_with_a_long_random_secret
   FRONTEND_URL=http://localhost:3000
   ```

2. From the repository root, install the three packages of dependencies:

   ```bash
   npm run install:all
   ```

3. Start the API and React development server together:

   ```bash
   npm run dev
   ```

   The frontend is at `http://localhost:3000` and the API is at `http://localhost:5000`.

4. To optionally load sample data into the database, run:

   ```bash
   npm run seed
   ```

   Seeding deletes existing users and products before inserting sample records. The seeded admin is `admin@shopnest.com` / `password123`; change that password immediately if using the account beyond local testing.

## Deploy To Render

Deploy this repository as one Render **Web Service** so Express can serve both the API and the production React build.

1. Push the repository to GitHub. Keep `.env` files and credentials out of Git.
2. In Render, create a Web Service connected to the repository. Leave **Root Directory** blank.
3. Set **Build Command** to `npm run render-build` and **Start Command** to `npm start`.
4. Add these required environment variables in Render:

   - `NODE_ENV` = `production`
   - `MONGO_URI` = your MongoDB Atlas connection string
   - `JWT_SECRET` = a long, randomly generated secret

   Render supplies `PORT`; do not hard-code it. In MongoDB Atlas, allow network access from Render (commonly `0.0.0.0/0` for hosted services) and use a database user with a strong password.

5. Add feature credentials when needed: `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, and `CLOUDINARY_API_SECRET` for image uploads; `RAZORPAY_KEY_ID` and `RAZORPAY_KEY_SECRET` for payments; `GMAIL_USER` and `GMAIL_PASS` for email. Use test payment keys until production approval is complete.
6. Deploy. The API and frontend share the Render URL; check that URL’s `/` route and API endpoints after deployment.

The Render build installs backend and frontend dependencies, then creates `frontend/build`. The backend serves that directory when `NODE_ENV=production`.

**Production payment warning:** the current checkout includes a test bypass, and the order API does not independently verify a successful payment before saving an order. Treat the deployed app as a demo until payment verification and trusted server-side price validation are implemented; never use live payment credentials with this flow.

---

## 📄 Postman Documentations
This repository includes a fully-scaffolded API testing toolkit: **`ShopNest_Postman_Collection.json`**. 
Simply Import this file directly into the local Postman IDE. It features variables like `{{token}}` properly mapped to effortlessly check protected admin/user/order payloads. Happy coding!
