# AgriSense — Smart Agriculture Monitoring

A simple agriculture IoT dashboard using the same backend pattern as the Campus Resource Booking project: React + Vite frontend, Express API, Mongoose models, MongoDB, seed script, CRUD endpoints, validation, and demo-admin checks for farm management.

## Features
- Shows soil moisture, temperature, humidity and soil pH.
- Saves and lists sensor readings in MongoDB.
- Adds and updates farm records through the API.
- Updates or deletes sensor readings.
- Gives a simple moisture recommendation in the frontend.
- Displays sample dashboard data if the backend is not running.

## Project structure
- `client/` — React + Vite dashboard
- `server/index.js` — Express routes and MongoDB connection
- `server/models/Farm.js` — farm model (similar to original `Resource` model)
- `server/models/Reading.js` — sensor reading model (agriculture equivalent of a booking record)
- `server/seed.js` — sample farms and readings

## Run on Windows / VS Code
1. Install Node.js 18+ and MongoDB Community Server, or use MongoDB Atlas.
2. Extract the ZIP and open the `smart-agriculture-monitoring` folder in VS Code.
3. Copy `server/.env.example` to `server/.env` and configure `MONGO_URI`.
4. In the root terminal run:
   ```bash
   npm install
   npm run install-all
   npm run seed
   npm run dev
   ```
5. Open `http://localhost:5173`.

## API endpoints
- `GET /api/health` — API health check
- `GET /api/farms` — list farms
- `POST /api/farms` — add a farm (requires `x-demo-role: admin` header)
- `PATCH /api/farms/:id` — update a farm (requires `x-demo-role: admin` header)
- `GET /api/readings` — list recent readings; optional `farmName` and `crop` query filters
- `POST /api/readings` — save a sensor reading with validation
- `PATCH /api/readings/:id` — update a reading
- `DELETE /api/readings/:id` — delete a reading

The `x-demo-role` header is only a demo pattern, not secure authentication. Add real authentication before deploying publicly.

## Simple logic
`Sensors → ESP32 (future hardware step) → Express API → MongoDB → Dashboard → Farmer action`

For now, values can be entered manually in the dashboard. The moisture thresholds are demonstration rules, not crop-specific agronomic advice. Later, an ESP32 can send sensor values to `POST /api/readings`.
