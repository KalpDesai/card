# CardFlowExtract — Run instructions

This repository contains a Node + Express server and a Vite + React client in the `client/` folder. The server serves both the API and the client. Below are steps to run in development (recommended) and production.

Prerequisites

- Node.js (v18+ recommended)
- npm or yarn
- If you plan to use the database features, set up a PostgreSQL database and provide `DATABASE_URL`.

Development (Windows PowerShell)

1. Open PowerShell and change to the project folder:

```powershell
cd C:\Users\kalpd\Downloads\CardFlowExtract\CardFlowExtract
```

2. Install dependencies:

```powershell
npm install
```

3. Set any environment variables you need. For local dev you usually only need `PORT` (optional). Example (PowerShell):

```powershell
$env:PORT = "5000"
$env:DATABASE_URL = "postgres://user:pass@localhost:5432/dbname"  # only if you use DB features
```

4. Start the dev server (this runs `tsx server/index.ts` which sets up Vite in development):

```powershell
npm run dev
```

Open your browser at http://localhost:5000 (or the value of `PORT`). The dev server will serve client assets via Vite and proxied API routes.

Build and production

1. Build the client and bundle the server:

```powershell
npm run build
```

2. Set `NODE_ENV=production` and set `PORT` and any required env vars, then start:

```powershell
$env:NODE_ENV = "production"
$env:PORT = "5000"
$env:DATABASE_URL = "postgres://user:pass@..."  # if required
npm start
```

Notes and environment variables

- `PORT` — the port the app listens on (defaults to 5000).
- `DATABASE_URL` — required by `drizzle.config.ts` (used for migrations). If you are not running migrations or DB-backed features, you can omit it, but some commands like `npm run db:push` will fail without it.
- `NODE_ENV` — development vs production. `npm run dev` sets up Vite with hot reload.

Troubleshooting

- If `npm run dev` fails because of environment variable assignment (Windows PowerShell), the `package.json` dev script uses `NODE_ENV=development tsx server/index.ts`. On Windows, that syntax may not work in PowerShell. Use the following alternative to run the server with `NODE_ENV` set:

```powershell
$env:NODE_ENV = "development"; npx tsx server/index.ts
```

- If you see errors about missing `DATABASE_URL` when running drizzle commands, export `DATABASE_URL` as shown above.

Further steps

- To run migrations (drizzle-kit), set `DATABASE_URL` and run `npm run db:push`.
- To type-check: `npm run check`.

If you'd like, I can also:
- Try running the dev server here to verify (I will install dependencies and start it), or
- Add a small .env.example showing the common env vars.

