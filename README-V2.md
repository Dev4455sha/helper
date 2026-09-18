# JEE AI Helper V2

This build converts the Figma-generated UI into a functional React/Vite application scaffold with persistent local activity, authentication scaffolding, a 30,000+ generated practice bank, working practice/test flows, revision/error tracking, protected Focus Mode navigation, real activity analytics, source-linked JEE information, and a secure server-side AI proxy.

## Run
npm install
npm run dev

## AI setup
Set `GEMINI_API_KEY` on the server/deployment environment and optionally `GEMINI_MODEL`. Never put the secret in a `VITE_` variable or frontend code.

The AI endpoint uses Google's REST `generateContent` path and sends the key server-side using the `x-goog-api-key` header. See Google's current Gemini API documentation for model/access requirements.

## Authentication/security
The included browser PBKDF2 login is a development fallback, not production authentication. For a production multi-user app, replace it with server-side authentication plus database authorization/RLS (a Supabase schema is included under `supabase/schema.sql`). Add rate limits, account verification, session expiry, password recovery and audit logging at the server layer.

## 30,000+ questions
The practice bank is generated on demand from the structured syllabus, so the app can expose 30,000+ distinct IDs without shipping a huge static JSON file. These are generated practice items, not official PYQs, and should be independently reviewed before educational release.

## PYQs
Use the CSV importer for authorized/licensed/user-provided PYQ datasets. The app deliberately avoids fabricating official PYQs. A template is provided in `PYQ-IMPORT-TEMPLATE.csv`.

## Verification status
Source code syntax was checked with TypeScript transpilation and relative imports were checked. A full `npm run build` could not be executed in this environment because dependency installation timed out; install dependencies and run `npm run build` locally/CI before deployment.
