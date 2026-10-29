# Test Report — Crystal Rebellion

## Executed checks

- `node --check src/main.js` — passed after the latest rune-puzzle and tap-input changes.
- Chromium smoke run — passed for main menu rendering, New Game, prologue/chapter dialogue, movement, repeated attacks, defeating an enemy, character switching, pause/resume, save serialization, returning to menu and Continue restore.
- Combat smoke run — one nearby enemy was defeated by player attacks; defeated-enemy state and XP were written to the save object.
- Boss transition — a seeded, one-hit-point boss was defeated through the normal attack loop; the victory dialogue appeared, the `bossDefeated` save flag was set, and the XP reward was stored. Boss phase patterns were not exhaustively tested.
- Menus/settings — opened Settings and Credits, changed quality, touch-button size and screen-shake settings, verified saved settings, and confirmed Reset Save Data cleared the Continue state.
- Resonance puzzle — seeded the player at the first rune, interacted as Steven, and verified that chapter 0 rune progress advanced to 1 and granted 8 XP. The remaining runes/rewards were not all automated in this run.
- Save recovery — malformed-but-parseable data (invalid collections, chapter, position and health values) was sanitized without a fatal overlay.
- Finale route — a seeded final-chapter save with the boss already defeated reached the final result panel after interaction at the exit. This is a route/ending check, not a complete five-chapter playthrough.
- Responsive layout smoke run at 390 × 844 — portrait hint and touchscreen control layer were visible; all seven touch buttons stayed inside the viewport bounds.
- Runtime diagnostics — no uncaught page errors or console errors in the tracked Chromium smoke sessions.

## Important scope notes

The browser smoke test used an in-memory `localStorage` adapter because this execution environment blocked browser navigation to a localhost test server. It validates the game's save serialization/restore flow, but does **not** verify long-term persistence in a real browser profile. The delivered code uses normal `localStorage` when served from an HTTP(S) origin.

No physical Android device test was run. A complete five-chapter playthrough, every boss phase, full three-rune puzzle completion in each chapter, audio quality across browsers, long-session performance, and all possible save-corruption cases remain manual QA items. They are not claimed as passed here.
