# JEE AI Helper V3 — Functional Rebuild Pass

This pass keeps the existing dark JEE workspace UI but fixes the biggest prototype problems identified from the deployed screenshots/audit.

## What changed

- Lazy-loaded application pages to reduce the initial JavaScript payload.
- Expanded the curriculum catalog with 41 additional chapter records.
- Expanded the formula bank with 106 additional curated reference entries (114+ total including the original set).
- Reworked the 30,000-item generated practice architecture so it produces formula-based and parameterized practice instead of the original generic placeholder wording.
- Kept generated practice explicitly separate from official PYQs.
- Fixed mock-test timer updates and automatic submit when time reaches zero.
- Added real test-attempt/error-log recording for incorrect answers.
- Added browser Fullscreen support to Focus Mode plus navigation protection; browsers still retain OS/browser exit controls.
- Added functional resource tracking with local progress, add and remove actions.
- Added shared input/label/focus styles that were missing from several generated pages.
- Added Vercel immutable asset caching for hashed `/assets/*` files.
- Updated SEO/canonical metadata for the Vercel deployment.
- Updated the server-side Gemini default to a current Gemini Flash model and removed the deprecated temperature parameter from the API request.

## AI setup

Set `GEMINI_API_KEY` in the Vercel server environment. Optional: `GEMINI_MODEL=gemini-3.6-flash`.
Never use a `VITE_` prefix for the secret.

The frontend deliberately shows a clear unavailable state when the backend key is missing; it does not invent an AI response.

## Authentication/security status

The included browser PBKDF2 login is still a development fallback. It is NOT production-grade authentication because browser local storage is not a secure server-side identity boundary.

For production:

1. Use a managed authentication provider such as Supabase Auth.
2. Put user records and activity data in Postgres.
3. Enable row-level security for every user-owned table.
4. Protect server APIs with authenticated sessions.
5. Add password reset/email verification, rate limits and audit logging.
6. Do not expose provider service-role keys or the Gemini key to the browser.

A starter Supabase schema is included under `supabase/schema.sql`.

## PYQs

The practice bank intentionally does not fabricate official PYQs. Use authorized/licensed or user-provided datasets via the CSV importer. Official exam information should remain linked to official sources.

## Build verification

Source files were transpiled successfully with the installed TypeScript compiler (20 TS/TSX source files checked; no syntax/transpile failures). A full Vite build was not run because this environment does not have the project's npm dependencies installed and the package registry was unavailable.
