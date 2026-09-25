# Northstar Guidance

A children's 2D interactive family planning and practice game for calm, low-stakes household preparedness practice.

> **Handoff status:** Phase 3 testing is unfinished. Read [TESTING_HANDOFF.md](TESTING_HANDOFF.md) before treating this checkout as release-ready.

## Source snapshot

This handoff repo was copied from `CapAhabb/tundra-otter-tundra-pine`, branch `phase3/rooms-hud-flashlight-ages`. The copied game source is preserved on both `main` and `phase3/rooms-hud-flashlight-ages`. The current phase 3 branch head is `42c17f2` (`Turn on Kara's voice narration by default`, 2026-09-25).

## Prerequisites

- Node.js 22.x
- npm (included with Node.js)
- A current desktop or mobile browser

## Local install and run

From the repository root:

```sh
npm ci
npm run dev
```

Open <http://localhost:8080>. The development server uses the checked-in `.grok/app-env.json` settings. The core game can run locally without an API key or a database URL; local database behavior uses the repository's PGlite fallback. If you do not install the optional local Piper voice, dialogue falls back to the browser's speech synthesis.

To stop the server, press `Ctrl+C` in the terminal where it is running.

## Tests and build

Run the repository's existing automated suite with:

```sh
npm test
```

This suite covers workspace helpers, auth, app-data, and deployment utilities. It does not currently provide Phase 3 gameplay acceptance coverage. The existing test evidence and its limits are recorded in [TESTING_HANDOFF.md](TESTING_HANDOFF.md).

Build with:

```sh
npm run build
```

The build also runs the database migration step. That step skips remote migrations when `DATABASE_URL` is unset; if it is set, migrations may modify the configured database. `npm run typecheck` is available as a separate check.

## Deployment

The app's Vite/Nitro configuration targets Vercel. For a Vercel deployment:

1. Install the Vercel CLI and sign in: `npm install --global vercel`, then `vercel login`.
2. From this repository, run `vercel link` and select or create the Vercel project intended for this handoff. Keep the GitHub source repo private.
3. Configure the project's environment in Vercel. This export was built for the Grok App Builder deployment path, which provisions auth and database settings. A standalone Vercel project must have its required integrations provisioned before sign-in or persistence can work.
4. Create a preview deployment with `vercel deploy`, then review it. Phase 3 acceptance is still pending.
5. After the required testing and review are complete, deploy with `vercel deploy --prod`.

See Vercel's [CLI deployment guide](https://vercel.com/docs/projects/deploy-from-cli) and [environment variable guide](https://vercel.com/docs/environment-variables) for current command details.

## API keys and other secrets

No recognizable API key or credential pattern was found in the current checkout or its reachable Git history, and no `.env` file is tracked. `.env*` and `.vercel` are ignored by Git. Keep credentials in the hosting provider's server-side environment settings; never commit them or expose private values through a `VITE_` variable. The game does not need a third-party API key for its local core loop.

The app's auth/database integration expects host-provided settings such as `DATABASE_URL`, `BETTER_AUTH_SECRET`, `BETTER_AUTH_URL`, `GROK_PROJECT_ID`, and the `GROK_AUTH_*` values when those services are enabled. Do not copy production values into this repository. Local `.grok/app-env.json` currently has auth and deploy database disabled.

Optional local Piper TTS uses `PIPER_BIN` and `PIPER_MODEL` to point to a local binary and model. These are local paths, not API credentials; without them the game uses browser speech synthesis. Piper is dev-only and is not used in the Vercel deployment.
