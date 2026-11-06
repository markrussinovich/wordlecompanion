# Pre-Publication Checklist

Use this checklist before submitting **WordlePop — Play & Stats 1.1.3** to the Chrome Web Store. Update the status column as you complete each step.

| Step                                                                | Status | Owner | Notes                                                                 |
| ------------------------------------------------------------------- | ------ | ----- | --------------------------------------------------------------------- |
| Verify manifest version matches marketing copy                      | ☑      |       | WordlePop 1.1.3; package and lockfile agree                           |
| Run unit tests (`npm test`)                                         | ☑      |       | 106 tests passed                                                      |
| Run quick build script (`npm run build:quick`)                      | ☑      |       | Typechecked build passed; new WordlePop ZIP generated                 |
| Manually smoke-test extension from `dist/`                          | ☐      |       | 32 isolated Chrome/Edge checks passed; personal-profile smoke not run |
| Capture/update screenshots in `listing/assets/`                     | ☑      |       | Five current 1280×800 RGB screenshots reviewed                        |
| Export promo tile (440×280)                                         | ☑      |       | WordlePop promo and 1400×560 marquee reviewed                         |
| Update store listing copy in `store-listing.md` if features changed | ☑      |       | New branding and automatic NYT connection; 118-character summary      |
| Confirm privacy statement matches data usage                        | ☑      |       | Automatic background NYT connection disclosed                         |
| Provide support URL and contact method                              | ☑      |       | Existing GitHub issues URL retained                                   |
| Double-check policies (spam, metadata, impersonation)               | ☐      |       | See Chrome Web Store Program Policies                                 |
| Upload zip to developer dashboard, save draft                       | ☐      |       | New package: `wordlepop-1.1.3.zip`; not uploaded                      |
| Submit for review                                                   | ☐      |       | WordlePop 1.1.3 has not been submitted                                |

The earlier Wordle Companion 1.1.1 package was uploaded and submitted November 1, 2026. Its ZIP is preserved unchanged; this checklist tracks the new release, not that prior submission.

## Verification notes

- Adversarial correctness review found no significant issues in the release changes. Packaging verification caught an obsolete generated popup page with the old brand; the build now removes it before packaging.
- Two opt-in live NYT browser checks were skipped. Automated runs did not submit real current-day guesses or use a personal account.
- All screenshot and promo PNGs have the required dimensions and RGB encoding; the refreshed store icon preserves transparency.
- No exact **WordlePop** result was returned by the Chrome Web Store search, but an existing **Wordle Popup** extension has a similar name. This is not trademark clearance.
- Store upload/submission and GitHub push are not performed by the build.
- Dependency verification compared all 74 open GitHub advisory ranges against every installed lockfile version: 73 are addressed. The npm audit service was unavailable (registry proxy returned HTTP 400; direct registry access failed TLS), so this is not a successful npm audit report.

## Release notes guidance

- Highlight fixes or new charts in 1–2 bullet points.
- Mention any onboarding tweaks (e.g., improved NYT login detection).
- Link back to docs or GitHub for detailed changelog if desired.

### 1.1.3

- Updated React Router and runtime dependencies, plus Vite, esbuild, Sharp, ts-jest, and transitive build/test packages to patched versions.
- The refreshed lockfile no longer matches any of the current critical, high, or moderate GitHub dependency alerts. One low-severity `deepmerge` advisory remains in Jest's development-only configuration dependency; no patched upstream release is available. It is not bundled into the extension.
- Use Node.js 20.9 or later and `npm ci` for a reproducible installation.
- Previous release ZIPs are preserved. No update has been uploaded or submitted to the store.

### 1.1.2

- Renamed to **WordlePop — Play & Stats**, with updated UX, documentation, extension icons, screenshots, and promotional graphics. Existing storage keys, games, and play sessions remain compatible.
- Today's eligible board connects automatically to the real NYT game; removed manual Connect/Sync and Open NYT buttons. NYT login and site prompts may still require opening its tab.
- Pop out is the emphasized, left-aligned action below the keyboard in every gameplay view. Pop-outs fit their content as dates change, while preserving manual window resizing.
- Historical replays remain local and do not update NYT account history. NYT continues to handle official current-day guesses and account persistence.

### 1.1.1 (previously submitted as Wordle Companion)

- Renamed to Wordle Companion — Play & Stats, with consistent popup, dashboard, play-view, and store branding. Existing saved games and sessions remain compatible.
- Play unplayed dates directly in the popup, dashboard tiles, or a persistent pop-out. Shared drafts and guesses, tile-entry pops, staggered feedback flips, and invalid-guess shakes.
- Browse blank and missing dates with Show unplayed, popup arrows/Left-Right keys, or the dedicated puzzle picker. Existing user games remain read-only.
- Historical replays are local; today's guesses use the real NYT game tab and official feedback. Replays do not update NYT history.
- Local WordleBot-style solver: see its normal-mode heuristic turn count and guess path in the dashboard and popup; not a globally optimal solver.
- Compare every game and your trend with NYT reader averages, including "vs Solver" and "vs NYT Readers" stats for any date range.
- Reliable backfill of missed games, a refreshed NYT Wordle look, and popup navigation that jumps back to the latest game.

## Support & Contact

- Primary support: <https://github.com/markrussinovich/wordlecompanion/issues>

Keep the checklist with the repository so future releases stay consistent and auditable.
