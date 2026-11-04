# WordlePop Manual Testing

## Load the current build

1. Run `npm run build:extension`.
2. Open `edge://extensions` or `chrome://extensions`, enable Developer mode, and choose **Load unpacked**.
3. Select `C:\Source\Wordle\dist`. Confirm **WordlePop — Play & Stats** and the version from `src\extension\manifest.json`.
4. After rebuilding, reload the extension and close/reopen any existing popup or pop-out.

Use a separate test profile or exported backup when testing imports and data controls. Do not add synthetic records to your personal profile.

## Gameplay and layout

1. Enable **Show unplayed**, choose a past unplayed date, and type using both physical and on-screen keys.
2. Confirm five-letter entry, colored feedback, rejected-word shakes, and exactly six board rows.
3. Navigate between played and unplayed dates. Board and navigation positions should remain stable; imported games should be read-only.
4. Confirm **Pop out** is emphasized on the left below the keyboard. There should be no Connect, Sync, or Open NYT buttons.
5. Open a pop-out, continue the same draft, and confirm popup/dashboard progress stays synchronized. Check footer spacing and keyboard visibility.
6. Resize the pop-out manually and change dates; the extension should preserve your chosen window size.
7. Finish a historical replay. Confirm completed comparisons and dashboard statistics update, including after reopening. This must not change NYT history.

## Today's official game

Opening an eligible current-day board automatically finds or opens an NYT game tab in the background. No separate connect or completion-sync step is required.

- In a disposable test profile, verify the connection does not replace the active tab and displays official NYT feedback.
- NYT login, cookie, subscription, or game dialogs may require opening its tab yourself. Check that failures remain visible and reopening the extension view retries.
- Submit official guesses only if you intend to play that account's current game. Today's game cannot be reset by the extension.
- NYT controls signed-in persistence. Historical extension replays remain local and never synchronize to the NYT account.

## Analytics, imports, and preferences

1. Open **Dashboard** from the popup. Confirm the WordlePop heading, totals, timeline, and comparison controls.
2. Toggle solver, NYT reader, skill, and luck series; change averaging and the date range. Confirm tiles and head-to-head figures update.
3. Review user/solver guess paths, completed comparisons, and N/A handling for unavailable values.
4. With appropriate NYT access, verify incremental import and gap-fill; interrupted imports should retain results already read.
5. Check light/dark/system themes, export/import round-trips, and deletion only in a disposable test profile.

## Automated checks and release assets

```powershell
npm test -- --runInBand
npm run lint
npm run build:extension
npx playwright test --config config\playwright.config.ts test-play.spec.ts test-solve-analytics.spec.ts --workers 1 --reporter line
npx tsx --tsconfig config\tsconfig.json scripts\capture-listing-screenshots.ts
```

The screenshot generator uses synthetic records and simulated current-day connection responses, not personal history or a real NYT game. See `listing\asset-plan.md` and `listing\checklist.md` before store submission.
