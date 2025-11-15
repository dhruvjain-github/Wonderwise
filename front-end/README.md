## Wanderwise — Front-end

This folder contains the front-end application for Wanderwise: a Vite + React single-page app built with Tailwind CSS. It provides UI for browsing trips, viewing trip details, and interacting with Google/Firebase-backed services.

This README describes how to set up, run, and contribute to the front-end.

## Quick overview

- Framework: React (18)
- Bundler / dev server: Vite
- Styling: Tailwind CSS
- State & routing: React + react-router-dom
- Services: Firebase (Firestore), Google APIs (Places, OAuth, Generative AI)

## Prerequisites

- Node.js 18+ (LTS recommended)
- npm (or yarn/pnpm) installed

## Setup (local development)

1. Install dependencies:

   ```bash
   npm install
   ```

2. Environment variables

   Create a `.env.local` file at the project root (this folder) and add the required Vite env variables. Example variables used in this project:

   - `VITE_GOOGLE_GEMINI_AI_API_KEY` — Generative AI / Gemini key
   - `VITE_GOOGLE_CLIENT_ID` — Google OAuth client ID
   - `VITE_GOOGLE_PLACE_API_KEY` — Google Places API key
   - `VITE_FIREBASE_API_KEY`, `VITE_FIREBASE_AUTH_DOMAIN`, `VITE_FIREBASE_PROJECT_ID`, `VITE_FIREBASE_STORAGE_BUCKET`, `VITE_FIREBASE_MESSAGING_SENDER_ID`, `VITE_FIREBASE_APP_ID`, `VITE_FIREBASE_MEASUREMENT_ID` — Firebase config (optional if using the firebaseConfig.js with hard-coded values)

   Do not commit `.env.local` to source control. Example `.env.local` (values redacted):

   ```bash
   VITE_GOOGLE_GEMINI_AI_API_KEY=your_api_key_here
   VITE_GOOGLE_CLIENT_ID=your_client_id_here
   VITE_GOOGLE_PLACE_API_KEY=your_place_api_key_here
   # Optional Firebase keys
   VITE_FIREBASE_API_KEY=your_firebase_api_key
   VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
   ...
   ```

3. Start the dev server:

   ```bash
   npm run dev
   ```

4. Open the app

   Visit http://localhost:5173 (or the address printed by Vite) to view the app with hot module reloading.

## Available scripts

- `npm run dev` — start Vite dev server (hot reload)
- `npm run build` — build production assets
- `npm run preview` — locally preview the production build
- `npm run lint` — run ESLint across the project

## Project structure (important files)

- `index.html` — main HTML template
- `src/main.jsx` — app bootstrap and routers
- `src/App.jsx` — top-level app component
- `src/pages/` — route pages (e.g., `HomePage.jsx`, `Travel.jsx`)
- `src/components/` — reusable UI components
- `src/service/` — external integrations (AI, Firebase, API clients)
  - `firebaseConfig.jsx` — Firebase initialization (consider moving secrets into `.env.local`)
  - `GlobalApi.jsx` — wrapper(s) for REST/API calls
- `src/my-trips/`, `src/view-trip/` — feature areas for trips and trip details
- `public/` — static assets

Refer to the codebase for more granular directories (components, ui, pages, view-trip subfolders).

## Environment & secrets guidance

- Vite exposes env variables prefixed with `VITE_` to the client. Only expose what is safe for the browser. Treat API keys and sensitive values carefully. For server-side secrets or proxies, keep them off the client.
- The project currently contains example Firebase config values in `src/service/firebaseConfig.jsx`. For production, move these to `.env.local` and update `firebaseConfig.jsx` to read from `import.meta.env.VITE_FIREBASE_API_KEY` etc.

## Deployment

- This project is configured to build static assets via `npm run build`. The generated `dist/` folder can be deployed to static hosts (Vercel, Netlify, S3+CloudFront).
- The repository contains a `vercel.json` configuration; Vercel is a straightforward hosting option for this app.

## Contributing

- Follow the existing code style (ESLint + Prettier-like rules via ESLint config).
- Run linting before pushing: `npm run lint`.
- Make small, focused pull requests with descriptive titles and changelogs.

## Notes & security

- Do not commit `.env.local` or any real API keys. The project currently includes example env variables for local development — rotate or remove any published credentials before sharing.
- Review third-party dependency licenses before production usage.

## Contact / Support

If you need help running the front-end, open an issue or contact the maintainers listed in the repository.

---

Generated and curated for the Wanderwise front-end. Keep this README up to date when you add new services or change environment requirements.
# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh
