# Testing handoff

**Status: Phase 3 testing is not finished.** This file separates saved evidence from test files that are merely present. It does not claim a passing Phase 3 test run.

## Repository snapshot

- Source repo: `CapAhabb/tundra-otter-tundra-pine`
- Branch under handoff: `phase3/rooms-hud-flashlight-ages`
- Current head: `42c17f2fb8d3961705b6112cd34181a15691e9b3` (`Turn on Kara's voice narration by default`, 2026-09-25)

## Saved evidence located

1. `screenshots/app-builder-preview.json` records a browser preview snapshot committed on 2026-09-20 (`9cad754`). It reports HTTP 200 at desktop (1280x800) and mobile (390x844), no horizontal overflow, and no browser console or page errors. The report has no test command or interaction checklist, and it predates the current branch head. It does not verify Phase 3 gameplay or the latest voice changes.
2. `GAME_REVIEW.md` describes a read-only real-browser pass through a demo family. It is a qualitative review, not a reproducible test report: it does not record a test date, exact steps, test-runner output, or pass/fail results for Phase 3. Its latest recorded change is `dfab7a1` (2026-09-25), before the current head.

No attributable Phase 3 test-run log or complete Phase 3 acceptance results were found in this repository snapshot. Test source files are not proof that the tests were run.

## Existing automated test command

`package.json` defines `npm test` as:

```sh
node --test 'scripts/**/*.test.mjs' && node --experimental-strip-types --test \
  src/lib/app-data/app-data.test.ts \
  src/lib/app-data/readiness-schedule.test.ts \
  src/lib/auth/gate-identity.test.ts \
  src/lib/auth/sign-in-gate.test.ts
```

The checked-in test files cover workspace helpers, preview/deployment behavior, auth, and app-data. There are no checked-in game-specific test files under `src/lib/game` or `src/components/game`. No result log for `npm test`, `npm run build`, or `npm run typecheck` was located, so their status is **unknown** for this handoff.

## Remaining before Phase 3 can be called tested

- Run the existing `npm test` suite and preserve the command, date, exit code, and output.
- Define and run Phase 3 game acceptance checks against the current head, including gameplay interactions and narration behavior.
- Save the browser and deployment results with the exact commit SHA tested. A preview render alone is not a substitute for gameplay acceptance.

Do not mark Phase 3 complete until these results are recorded and reviewed.
