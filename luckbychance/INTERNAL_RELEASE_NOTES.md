# Corporate Luck by Chance: internal release notes

INTERNAL REFERENCE ONLY. Not for customers and not for any website or front end. Written on 2 Nov 2026 for the owner and future maintainers. All times are IST (India Standard Time, UTC plus 5:30). Facts were read from git, from the Cloudflare Pages deployment list (read-only) and from the live address on 2 Nov 2026 between 01:45 and 02:05 IST (the live state was still changing during that time, so a release made after 02:05 is not described here); anything that could not be checked is marked "unverified".

## What this is
Corporate Luck by Chance is the dice game for company teams: every player rolls a realistic dice in a timed window, the target is a score, and the top five win prizes.

| Item | Value |
|---|---|
| Live address | https://luck.corporatetambola.com |
| Cloudflare Pages project | `corporate-luck-by-chance` |
| GitHub repository | `FChecklist/corporate-luck-by-chance` (public) |
| Branch holding the latest release work | `feat/luck-wording-2026-11-01` (tip at the time of writing: `bf86f4d`) |
| What is live now | Commit `eab061f`, deployment `b4985a78-...` (2 Nov 2026 10:56 IST), read from the Cloudflare list. Release-list version 1.3.0. |

## Release table (newest first, since 31 Oct 2026)
| Date and time (IST) | Version | Commit | Cloudflare deployment id | Rollback id (the live one before it) | Tests and exceptions |
|---|---|---|---|---|---|
| 02 Nov 2026 10:56 | 1.3.0* | `eab061f` | `b4985a78-4b0a-412c-bf5a-46cd06c892ed` | `634b627b-4d58-401c-ab99-039511e7ad78` | Same build, no code change: only the shared owner password was set (Tambola's ORGANIZER_SECRET) so one password opens /paytest and /api/owner/* on all six games. Checked after deploy: shared password 200, wrong or no password 404, version.json equals the commit, mode LIVE, noindex present, /paytest 200. |
| 02 Nov 2026 09:04 | 1.3.0* | `eab061f` | `634b627b-4d58-401c-ab99-039511e7ad78` | `c1d46912-c056-49d3-87d1-24af9ba576b7` | Design pass: two columns on laptops, header gradient contrast, 44 px logo. Full partner run r93: 1680 pass, 0 fail. |
| 02 Nov 2026 00:02 | 1.3.0* | `bf86f4d` | `c1d46912-c056-49d3-87d1-24af9ba576b7` | `ff5b36f6-ab42-4d79-a56c-ea1c9cd65510` | Same build as the deployment before it, redeployed only to add the GOOGLE_CLIENT_ID setting (Google sign-in stays dormant on game pages: the owner switched it off in code on 23 Oct 2026; it is live on the console). version.json unchanged. No new tests. |
| 01 Nov 2026 21:49 | 1.3.0* | `bf86f4d` | `ff5b36f6-ab42-4d79-a56c-ea1c9cd65510` | `e4c3e95c-5f64-45fc-a1c0-d998a62d8f53` | Partner full run on this exact commit: 1,680 pass / 0 fail. Live checks: version.json bf86f4da10e1, hide files present, built robots Disallow /, no sitemap file, noindex tag on every page, X-Robots-Tag, all pages 200. Odd: /sitemap.xml still answered 200 from the edge cache (an old copy; with a query string it is 404). |
| 01 Nov 2026 09:38 | 1.3.0* | `9d4d17c` | `e4c3e95c-5f64-45fc-a1c0-d998a62d8f53` | `56d26c90-c9ab-4403-bf13-56b812105ff2` | Hide-from-search release (noindex tag, X-Robots-Tag header, robots.txt Disallow all, no sitemap). A private-site test pins it. Full-run count not recorded in the handover (unverified). |
| 01 Nov 2026 08:04 | 1.3.0* | `c86e050` | `56d26c90-c9ab-4403-bf13-56b812105ff2` | `3dfacc7d-c9d4-45fe-b15d-ebd37f103c1e` | Partner laptop 1,661 pass / 0 fail on this head (31 Oct note). |
| 01 Nov 2026 02:31 | 1.3.0* | `732e640` | `3dfacc7d-c9d4-45fe-b15d-ebd37f103c1e` | `b0017000-6809-49f3-b7ff-1b52a6ba0116` | Full suite 1,629 pass / 0 fail on the partner laptop (31 Oct note). Fixes a console error where the console loads /pack/employee-id.js as a module. |
| 01 Nov 2026 02:08 | 1.3.0* | `f4d3a34` | `b0017000-6809-49f3-b7ff-1b52a6ba0116` | `1ba080ca-611d-4961-a6da-96474a7b70ed` | Tested head 2447911: 1,589 pass / 0 fail, plus one build-only commit (cache safety); cache test 3 pass, and 1 fail with the step off. This deployment had a console error, fixed by the next one. |

Version marked with a star comes from the repo's release list (`apps/edge/src/releases.json`); the live version.json carries only the commit. The deployment list shows no Luck deployment between 23 Oct 03:31 IST and 1 Nov 02:08 IST, so release-list versions 1.2.0 (24 Oct) and 1.3.0 (29 Oct) first went live on 1 Nov 2026.

## What changed in each release

### 1 Nov 2026 21:49 IST, commit bf86f4d (wording, no address, 2,000 cap, demo release)
Previous live: `9d4d17c` (the hide release of 09:38 IST). Release-list version 1.3.0.
- Users: every customer-visible sentence got a warm third-person wording (383 sentences in 610 places): refunds as credit, no blunt first-person refusal lines, no first-person plural words.
- Users: no city, state, street or pin code anywhere, only India.
- Organizers: every new game takes at most 2,000 people (at creation and when settings change), with a polite refusal and pricing text. Five default prize lines (the top five win). The guide states the 10-second window, the 220 maximum, 10 points for an exact hit.
- Organizers: a free Demo game exists behind the switch DEMO_GAME (off): Demo label, 3 a day per account and per address, no paid pack or payment row.
- Family pass limit (self plus 4): Luck has no code for a family limit, so nothing was changed (boss note of 1 Nov).
- Two hide-release code comments reworded so that no internal-note words are in what is deployed.

### 1 Nov 2026 09:38 IST, commit 9d4d17c (hide-from-search release)
Noindex tag and header, robots Disallow all, no sitemap. Rollback target of the 21:49 release: `e4c3e95c-5f64-45fc-a1c0-d998a62d8f53`.

### 1 Nov 2026 02:08 to 08:04 IST (first live of release-list 1.2.0 and 1.3.0)
- 02:08 cache safety (f4d3a34); 02:31 the console loads /pack/employee-id.js as a module (732e640); 08:04 cache-test timing fix (c86e050).
- From release-list 1.3.0: safer joining (an employee ID or a mobile number is checked against the Organizer's list; a stranger waits for the Organizer's yes; one phone cannot play as another); a game for up to 10 people is Rs 0; players' data deleted 20 hours after the game (promise stays 24); a permanent record of each game's settings with no personal data; one payment is finished exactly once; the daily write guard raised to 2,000,000.
- From release-list 1.2.0: the Organizer chooses per game what a person gives to get in; the people list takes an Employee ID column (type, paste, CSV, PDF read on the Organizer's own device).

## Earlier numbered releases (before 31 Oct 2026)


Before numbered releases there were 22 earlier production deployments listed by Cloudflare (from 13 Oct 2026 16:32 to 23 Oct 2026 03:31 IST). They are not listed one by one here; open Cloudflare, Pages, the project, Deployments to see them.

## How to roll back
1. Sign in to the Cloudflare dashboard (the account that holds the Corporate Games sites).
2. Left menu: Workers and Pages. Open the project `corporate-luck-by-chance`.
3. Open the Deployments tab. Find the rollback id from the table above (the list shows the first 8 characters).
4. On that line press the three dots, then "Rollback to this deployment", and confirm.
5. Open https://luck.corporatetambola.com/version.json and check that the commit is the old one. Check that the home page of the site opens.

Things to know before pressing the button:
- Do it only when no real game is being played or about to start (the release rule is: no real game within 3 hours; test games are named LT-...).
- A rollback puts back the old files and old code only. It does NOT undo database changes. Settings such as secrets are fixed into each deployment when it is made, so an old deployment may lack a setting that was added later (this is why same-build redeploys were needed to add the Google setting on 1 to 2 Nov 2026).
- After a rollback, check that the site is still hidden from search: robots.txt must say Disallow /, and every page must carry a noindex tag.


Database: Luck has its own database; the diff against live had no migration, wrangler or sql file for the 1 Nov release, so no database step is needed.

## Known gaps and open decisions
- Real Rs 1 payment test for each game: the owner makes it himself on the main website. Open.
- Independent, water-tight review of the text of the one legal document (checklist row 45): not yet done.
- The new free Demo game sits behind a setting called DEMO_GAME. That name was not found in the Cloudflare settings of this project (read 2 Nov 2026), so it appears to be off. When to switch it on needs an audit and the owner's go. If the setting is held somewhere else this is unverified.
- /sitemap.xml: the new build has no sitemap, but an old copy can still be answered from Cloudflare's edge cache (a request with a query string such as ?x=1 shows 404). It leaves the cache by itself; a cache purge of the zone would clear it at once (not done).
- Test games used for live checks are named LT-... and are deleted afterwards.
- A 100,000-person game is not promised for Luck (owner cap is 2,000 until a load test).
- /sitemap.xml: the old edge-cached copy answered 200 after the release (see above).
- Whether ID-only joining is in this game's live code is not confirmed in the records (unverified). Luck still has the release-list 1.3.0 wording "an employee ID or a mobile number".
- Stale base never to use: the main checkout of this repo sits on `local/base-2026-10-24` (b3479c0).

## Where the details are
- Handover file: `C:\ct\test-sites\handover\2026-11-01\RELEASE-HANDOVER-2026-11-01.md` (the release log is its section 10, open owner items are section 11). Older release notes of 31 Oct 2026 are in the folder `C:\ct\test-sites\handover\2026-10-31\`.
- Memory notes of the boss session, folder `C:\Users\Dell\.claude\projects\C--ct-ct\memory\`: `boss-state-2026-11-01.md` (state at each hour of 1 to 2 Nov 2026), `central-payment-ledger-rules-2026-11-01.md`, `wording-tone-rule-flowery-2026-11-01.md`, `game-rules-owner-decisions-2026-10-31.md`, `partner-laptop-2026-10-30.md` (how the test laptop is used).
- The list of decisions by the owner with status: `decisions-72h-checklist.md` and `decisions-72h-tambola-verified.md` in the handover folder; who did what: `sessions-done-register.md`.
- Release steps and rollback command: `release-runbook-2026-11-01.md` in the folder `handover\2026-10-31`.
- Technical readers can also open `docs/DEPLOYS.md` in a game repo (list of deployments by commit), where it exists.
