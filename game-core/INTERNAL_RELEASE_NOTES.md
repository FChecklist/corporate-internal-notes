# game-core (shared rules, wording, legal text, UI kit): internal release notes

INTERNAL REFERENCE ONLY. Not for customers and not for any website or front end. Written on 2 Nov 2026 for the owner and future maintainers. All times are IST (India Standard Time, UTC plus 5:30). Facts were read from git, from the Cloudflare Pages deployment list (read-only) and from the live address on 2 Nov 2026 between 01:45 and 02:05 IST (the live state was still changing during that time, so a release made after 02:05 is not described here); anything that could not be checked is marked "unverified".

## What this is
game-core is the shared engine for the six Corporate Games: roles (Organizer, Host, Co-host, participant, family pass), joining and ID rules, start modes and the pause clock, the organizer flow, retention (24-hour deletion), the plain-words messages, the one common legal text, and the Tambola look and 44 px rules. It is a library: it has NO website and NO Cloudflare project of its own. A game picks up a version only when the game is released with a copy of it ("vendored" into `vendor/game-core/`).

| Item | Value |
|---|---|
| Live address | none (library, nothing is deployed from this repo) |
| Cloudflare Pages project | `none` |
| GitHub repository | `FChecklist/corporate-game-core` (public) |
| Branch holding the latest release work | `feat/legal-v4-2026-11-02` (tip at the time of writing: `444ad31`) |
| What is live now | Nothing is "live" from here. Version `0.10.0` (file `VERSION`). Which version each live game carries (read from `vendor/game-core/CORE_VERSION` in the live commit): Bingo 0.10.0 (0224581), Tic Tac Toe 0.10.0 (0224581), Luck by Chance 0.9.11 (04dc49c), Lucky Draw 0.9.11 (04dc49c), Snakes and Ladders 0.9.11 (04dc49c). Tambola holds no vendored copy (the core was extracted from Tambola 1.9.0) and carries its own legal text. Home generates /terms from this repo with `tools/make-terms.mjs`. |

## Rules that hold for the whole family (as decided by the owner)
- One public site: home.corporatetambola.com. The game sites are not listed in search (noindex in the page, in the headers and in robots.txt) but open by link. One master console, one engine. No feature deleted.
- One single legal document for every product, at home.corporatetambola.com/terms (with anchors). Legal text version 2026-11-01 (document revision v4, owner approved 2 Nov 2026). No tick-boxes: one small line below the buttons with three links. No street, city or state anywhere, only "India". No age, 18+ or gambling lines. Third person only (no first-person plural words). Soft, user-favouring words. The old word for wiping a record is not used: timers say "auto-deleted", a person's own action says "deleted".
- Joining is by ID only ("Employee, Associate, Vendor or Member ID"): no mobile number and no e-mail from participants. The Organizer, Host or Co-host confirms people who are not on the list.
- Everything about the participants is deleted within 24 hours after the game (the code runs it at 20 hours). Kept: winners' results, game logs, Organizer and Host details, tax invoices.
- Payments only through IT SERVICES BY RAJAT AGARWAL and Razorpay (one central payment ledger). No other payee, no other gateway.
- Sign-in: e-mail code and Google sign-in are live on the console (checked 2 Nov 2026 between 01:45 and 02:05 IST (the live state was still changing during that time, so a release made after 02:05 is not described here) IST: the console says google true, microsoft false). Microsoft sign-in was dropped by the owner on 2 Nov 2026 ("lets not do microsoft", "just hide microsoft"; the owner also said no legal changes and no code changes at that point). The console, console.corporatetambola.com, is the one address to sign in and to create a game.
- People limits (owner, 31 Oct and 1 Nov 2026): Tambola, Bingo and Lucky Draw up to 100,000; Tic Tac Toe, Snakes and Ladders and Luck by Chance up to 2,000 (100,000 needs a load test before it is promised). Family pass limit: the person plus 4 (changed from 10 on 1 Nov 2026 about 19:45 IST).
- Demo game: same flow, Rs 0, up to 10 people, 3 per day per Organizer. Pause and Resume exist in all six games (Organizer or Host only).

## Release table (newest first)
There is no Cloudflare deployment, so there are no deployment ids and no rollback ids. A "release" of game-core is a commit that a game then copies in. The package version in `package.json` stayed at 0.10.0 for all the legal-text commits listed on 1 and 2 Nov.

| Date and time (IST) | Core version | Commit(s) | What it brought |
|---|---|---|---|
| 2 Nov 2026 00:33 | 0.10.0 (legal revision v4) | `444ad31` | Legal document v4, owner approved 2 Nov: free demo game line, Google or Microsoft sign-in, participant caps, family of up to 4. |
| 1 Nov 2026 18:16 | 0.10.0 | `0224581` | Legal text: participants give an employee ID only; no e-mail join; one 24-hour statement; kept records tied to the table. THIS is the commit Bingo and Tic Tac Toe pin. |
| 1 Nov 2026 17:49 | 0.10.0 | `dfd9bb2` | Legal document: what is kept (no mobile number or e-mail taken or kept; participant information deleted within 24 hours; only winners' results, logs, Organizer details and invoices kept). |
| 1 Nov 2026 10:49 to 10:53 | 0.10.0 | `d1912ec, 34a081c` | No city, state or street address (only India) with a conformance check; no age, adults-only, gambling-status or consent-taking lines. |
| 1 Nov 2026 10:19 to 10:30 | 0.10.0 | `21493ed, 24c9d02, 42e5edc, 5e151f4` | One legal document, no checkboxes: notice below the button; nine-section single document; retention table; legacy redirects. |
| 1 Nov 2026 00:24 | 0.9.11 | `04dc49c` | Journey runbook (docs only). THIS is the commit Luck, Lucky Draw and Snakes pin. |
| 31 Oct 2026 23:08 to 23:10 | 0.9.9, 0.9.10 | `6eb0382, 052a584` | Journey smoke model and run tools (test tooling only). |
| 31 Oct 2026 20:27 to 20:45 | 0.9.5 to 0.9.8 | `3e8f81b, 6fff169, 6ea428a, f27e267` | No old wiping-word wording; calm third-person data wording; funnel-event helper; one common legal text (privacy, terms, cookies, grievance). |
| 31 Oct 2026 19:08 to 19:49 | 0.9.1 to 0.9.4 | `74f0476, 9368f3c, d35bc78, eb6a5e8` | Tic Tac Toe pairing and sit-out rules; stage settle fix; merge of the Snakes fixes. |
| 31 Oct 2026 17:06 to 18:45 | 0.2.0 to 0.9.0 | `01b7d3d ... 1934ebc` | People step with Host and Co-host rows, 52 text-only reactions pack (redrawn as original work), reaction scheduler (2.2 s, one at a time, 15 s gap), five prize places for Tic Tac Toe, Snakes and Luck, slot rules for Tic Tac Toe. |

Before 31 Oct 2026 17:06 IST the core was at 0.1.0 (extracted by copy from Tambola 1.9.0, commit ead5520) and was vendored into games from 31 Oct 15:03 IST ("Engine step 1" in Bingo).

## What changed (plain words)
- One legal document for every product, no tick-boxes, one small notice line below the buttons (decided by the owner on 1 Nov 2026). Legal text version 2026-11-01; revision v4 approved by the owner on 2 Nov 2026.
- The legal text says: participants give an ID only (no mobile number, no e-mail); the Organizer, Host or Co-host confirms people who are not on the list; all participant information is deleted within 24 hours after the game; winners' results, game logs, Organizer and Host details and tax invoices are kept; payments only through IT SERVICES BY RAJAT AGARWAL and Razorpay.
- Wording rules: third person, soft and user-favouring, no street, city or state (only India), no age or gambling lines, "auto-deleted" for timers and "deleted" for a person's action, never the old wiping word. A wording guard and a conformance check fail the build if these are broken.
- The reaction pack (about 50 comic text reactions, 52 in the code; original shapes and colours, 2 to 3 seconds each, at most 15 per 10 minutes) and the Tic Tac Toe, Snakes and Luck owner rules (slots, stages, 7 to 8 minute Snakes games, five prize places) were added on 31 Oct 2026.

## How to roll back
game-core has no deployment. To go back, a game re-copies the earlier version into itself (`bun tools/vendor.ts ../my-game --expect <version>`, see `README.md`) and is released again through its own Cloudflare project (see that game's notes for its rollback ids). Changing this repo alone changes nothing on any live site.

## Known gaps and open decisions
- The test "luck-owner" (R8) fails in this repo, and it also fails on old heads; known, not to be chased again.
- The legal text still says "Google or Microsoft" sign-in. The owner dropped Microsoft sign-in on 2 Nov 2026 but said not to change the legal text. Open decision.
- Claim-hold wording must not be published until CLAIM_HOLD is on in the games (boss note of 1 Nov). Whether the revision-v4 text contains it was not checked (unverified).
- The branch `feat/legal-v4-2026-11-02` (444ad31) had NOT been pushed to GitHub before these notes were added (the remote only knew `feat/common-legal-2026-11-01`). The notes branch pushed with these notes carries it.
- Games are not all on the same core version (see the top table). Tambola, Luck, Lucky Draw and Snakes do not yet carry the 0.10.0 legal text from game-core; whether their own legal pages match the home document is unverified.
- game-core test results for the commits above (the independent conformance suite; the partner run named r66) were not found in the records (unverified).
- Coders do not test here; independent test authors own the conformance suite.

## Where the details are
- Handover file: `C:\ct\test-sites\handover\2026-11-01\RELEASE-HANDOVER-2026-11-01.md` (the release log is its section 10, open owner items are section 11). Older release notes of 31 Oct 2026 are in the folder `C:\ct\test-sites\handover\2026-10-31\`.
- Memory notes of the boss session, folder `C:\Users\Dell\.claude\projects\C--ct-ct\memory\`: `boss-state-2026-11-01.md` (state at each hour of 1 to 2 Nov 2026), `central-payment-ledger-rules-2026-11-01.md`, `wording-tone-rule-flowery-2026-11-01.md`, `game-rules-owner-decisions-2026-10-31.md`, `partner-laptop-2026-10-30.md` (how the test laptop is used).
- The list of decisions by the owner with status: `decisions-72h-checklist.md` and `decisions-72h-tambola-verified.md` in the handover folder; who did what: `sessions-done-register.md`.
- Release steps and rollback command: `release-runbook-2026-11-01.md` in the folder `handover\2026-10-31`.
- Technical readers can also open `docs/DEPLOYS.md` in a game repo (list of deployments by commit), where it exists.
