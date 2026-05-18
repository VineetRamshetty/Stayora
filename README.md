# Stayora

Stayora is a full stack property discovery web application built with Node.js, Express, MongoDB and EJS. It provides user authentication, listing creation and management, image uploads (Cloudinary), location search (Mapbox), and a review system.

**Status:** Prototype / demo-ready

**Demo:** https://stayora-s5ul.onrender.com/

**Quick highlights**
- Secure username/password authentication with `passport` and `passport-local-mongoose`.
- Persistent sessions using `express-session` + `connect-mongo`.
- Image uploads stored in Cloudinary via `multer-storage-cloudinary`.
- Location geocoding and interactive maps using Mapbox (`@mapbox/mapbox-sdk`).
- Server-side validation using `joi`.

**Tech stack**
- Node.js (engine declared: 24.x)
- Express 5
- MongoDB + Mongoose
- EJS templates (`ejs` + `ejs-mate`)
- Mapbox, Cloudinary, Passport, Multer

**Getting started (local)**

Prerequisites
- Node.js (v24 recommended)
- MongoDB (local or Atlas)

Install
```bash
npm install
```

Environment variables
Create a `.env` file in the project root and set the following values:

```
ATLASDB_URL=<your MongoDB connection string>       # e.g. mongodb+srv://... or leave unset to use local DB in seeds
SECRET=<session secret string>
MAPBOX_TOKEN=<mapbox token>
CLOUDINARY_NAME=<cloudinary cloud name>
CLOUDINARY_API_KEY=<cloudinary api key>
CLOUDINARY_API_SECRET=<cloudinary api secret>
NODE_ENV=development
```

Run the app
```bash
# development (run directly)
node app.js

# or with nodemon if installed
nodemon app.js
```

Server listens on port 3000 by default (see `app.js`).

Seeding local sample data
- The project includes a lightweight seed script in `init/`. To seed the local MongoDB used by the seed script, run:
```bash
node init/index.js
```

Project layout (important files)
- `app.js` — server entry, middleware, passport/session setup, route mounting
- `routes/` — route modules for listings, reviews and users
- `controllers/` — controller logic for routes
- `models/` — Mongoose schemas (`listing.js`, `review.js`, `user.js`)
- `views/` — EJS templates and layouts
- `public/` — static assets (CSS, client JS including `map.js`)
- `cloudinaryConfig.js` — Cloudinary and Multer storage configuration
- `schema.js` — Joi validation schemas for listings & reviews
- `init/` — sample data and seeding script

Architecture (MVC)
- This project follows the Model View Controller (MVC) pattern:
	- Models: Mongoose schemas in the `models/` folder (data layer).
	- Views: EJS templates in the `views/` folder (presentation layer).
	- Controllers: Business logic in the `controllers/` folder (application layer), invoked by route handlers in `routes/`.
	This separation keeps concerns modular and simplifies testing, maintenance and future API additions.

Environment notes & deployment tips
- Ensure `CLOUDINARY_*` and `MAPBOX_TOKEN` are set in production environment variables.
- Add a `start` script to `package.json` for production (e.g. `"start": "node app.js"`).
- Consider using `process.env.PORT` in `app.js` for host-assigned ports when deploying (e.g. Heroku, Render, Fly).

Security
- Do not commit `.env` or secret keys. Use host secrets or GitHub Actions secrets for CI.
- The app uses `httpOnly` cookies for session storage; review session cookie settings for production (secure flag).

Contributing
- Fork, branch, and open pull requests. Add tests and update docs where appropriate.

License
- See the `LICENSE` file for the project license.

Questions / Contact
- Open an issue or reach out via your GitHub profile.