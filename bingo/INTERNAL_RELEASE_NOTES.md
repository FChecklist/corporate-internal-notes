# Corporate Bingo: internal release notes

INTERNAL REFERENCE ONLY. Not for customers and not for any website or front end. Written on 2 Nov 2026 for the owner and future maintainers. All times are IST (India Standard Time, UTC plus 5:30). Facts were read from git, from the Cloudflare Pages deployment list (read-only) and from the live address on 2 Nov 2026 between 01:45 and 02:05 IST (the live state was still changing during that time, so a release made after 02:05 is not described here); anything that could not be checked is marked "unverified".

## What this is
Corporate Bingo is the online bingo game for company teams (closed group, participants join by ID, Organizer or Host calls the numbers). It shares the beacon, claim and pause ideas with Tambola and uses the shared rules in game-core.

| Item | Value |
|---|---|
| Live address | https://bingo.corporatetambola.com |
| Cloudflare Pages project | `corporate-bingo` |
| GitHub repository | `FChecklist/corporate-bingo` (public) |
| Branch holding the latest release work | `feat/bingo-design-2026-11-02` (tip at the time of writing: `fc5f01f`) |
| What is live now | Commit `fc5f01f`, deployment `abeaae52-...` (2 Nov 2026 10:57 IST), read from the Cloudflare list. Release-list version 1.4.0. |

## Release table (newest first, since 31 Oct 2026)
| Date and time (IST) | Version | Commit | Cloudflare deployment id | Rollback id (the live one before it) | Tests and exceptions |
|---|---|---|---|---|---|
| 02 Nov 2026 10:57 | 1.4.0* | `fc5f01f` | `abeaae52-b1ce-434b-8c73-2540e6ebda69` | `ae24f6a9-a668-46c6-af19-f92e49ad1f86` | Same build, no code change: only the shared owner password was set (Tambola's ORGANIZER_SECRET) so one password opens /paytest and /api/owner/* on all six games. Checked after deploy: shared password 200, wrong or no password 404, version.json equals the commit, mode LIVE, noindex present, /paytest 200. |
| 02 Nov 2026 01:57 | 1.4.0* | `fc5f01f` | `ae24f6a9-a668-46c6-af19-f92e49ad1f86` | `27fc8e5a-96fa-4e23-bd05-37559862ae66` | Look-only change: two files differ from fabd9a9 (apps/web/public/z.css and zsw.js, the service-worker cache version). Test result for this exact commit not recorded (unverified). Live: version.json fc5f01f365e0, built about 01:57 IST. Released after the 01:30 snapshot; no handover log line yet. |
| 02 Nov 2026 01:40 | 1.4.0* | `fabd9a9` | `27fc8e5a-96fa-4e23-bd05-37559862ae66` | `c33752f8-f344-4b61-b57b-b61c73ca3d3e` | Released 2 Nov 2026 01:40 IST, i.e. after the 01:30 snapshot; the handover release log has no line for it yet. The full-run result for this exact commit was NOT found (it was bundled for the partner laptop as run r89 at about 01:26 IST; result unverified). The earlier head 542baa4 had 2,084 pass / 1 fail (a funnel.js message test). Live: version.json fabd9a906ef7, built about 01:35 IST. |
| 01 Nov 2026 22:10 | 1.4.0* | `d5156bf` | `c33752f8-f344-4b61-b57b-b61c73ca3d3e` | `06514d4f-a6cc-4ef2-b3b0-ad55567fcd16` | Head 340d525: full partner run 2,071 pass / 0 fail. d5156bf is 340d525 plus one file (vendor/game-core/packages/core/src/package.json) so the Functions bundle builds; the first attempt at 22:04 IST with 340d525 failed at the bundle step and deployed nothing. Run r82 on d5156bf: 1,798 pass but 19 files did not run (partner install timed out); after installing happy-dom the 18 edge files gave 456 pass / 1 fail (a chance match in a 'plus 91 and spaces' test, the file alone 85 pass / 0 fail) and gamesbar 3 pass / 0 fail. 0 real failures. DISCLOSED EXCEPTION: split run, not one clean full run. Live checks: version.json d5156bfd5ca8, noindex on every page, X-Robots-Tag, all pages 200. |
| 01 Nov 2026 09:21 | 1.4.0* | `4e0e210` | `06514d4f-a6cc-4ef2-b3b0-ad55567fcd16` | `8dbde163-e106-4ca8-8180-dfeef02be3c1` | Hide-from-search release (noindex tag, X-Robots-Tag header, robots.txt Disallow all, no sitemap). A private-site test pins it. Full-run count not recorded in the handover (unverified). |
| 01 Nov 2026 03:32 | 1.4.0* | `50247a8` | `8dbde163-e106-4ca8-8180-dfeef02be3c1` | `64c26339-3408-4ec0-a38b-a5191386e917` | Partner laptop 2,055 pass / 0 fail on this head (handover of 31 Oct). |
| 31 Oct 2026 23:52 | 1.4.0* | `7e0d1f7` | `64c26339-3408-4ec0-a38b-a5191386e917` | `401d9904-c88b-4d82-8273-e4d3696c4a7b` | Cache safety. cache-versioning test 3 pass (and 1 fail with the build step off). Full-suite count not recorded here. |
| 31 Oct 2026 21:19 | 1.4.0* | `39c662a` | `401d9904-c88b-4d82-8273-e4d3696c4a7b` | `d13ae6ee-c8db-4a9f-9808-e2d9cb4218d0` | First deployment of the 1.4.0 and 1.4.1 work. Count not recorded here (unverified); the 31 Oct note says 135 pass / 0 fail in the five files touched by the last fixes. |

Version marked with a star comes from the repo's release list (`apps/edge/src/releases.json`); the live version.json of this game carries only the commit, so the commit is the real identifier.

## What changed in each release

### 2 Nov 2026 01:57 IST, commit fc5f01f (laptop design pass, look only)
Previous live: `fabd9a9`. Released after the 01:30 IST snapshot; this section was added when the Cloudflare list and version.json showed it live.
- Users: on a laptop (screen 861 px wide or more) the play page has two columns: the card on the left (up to 520 px, larger numbers) and the called number and prizes on the right (container 90 percent of the width, up to 1228 px).
- Users: the called-numbers board digits are 13 px / bold, and the FREE square is a darker teal so its text reaches contrast 4.5 to 1.
- Technical: the service-worker cache version moved to v33, so phones and laptops pick up the new look. Only two files changed (z.css and zsw.js); no logic, no database.

### 2 Nov 2026 01:40 IST, commit fabd9a9 (the "Bingo gets the Tambola features" release)
Previous live: `d5156bf`. Released after the 01:30 IST snapshot; this section was added when the Cloudflare list and version.json showed it live. Decision by the owner on 1 Nov 23:00 IST: Bingo must get all the Tambola features, including claim hold, pause and restart, and it should be released before the home page so that "no mobile number" is true.
- Users: one legal document. The old separate legal pages now answer a permanent redirect to their section of the home document (both spellings); terms version 2026-11-01 everywhere.
- Users: no tick-boxes anywhere; one small line with three links below the buttons.
- Users: joining by ID only (name, location and an Employee, Associate, Vendor or Member ID; no mobile number or e-mail). It sits behind the switch ID_ONLY. Cloudflare holds a setting with that name, but its value cannot be read, so whether it is switched on is unverified (the plan on the boss notes was ID_ONLY on, claim hold off).
- Users: a plain page /fair.html on how the game is kept fair (six facts and the honest limit), linked from the join page. In the last 5 seconds of a pause that ends by itself the phone shows "Restarts in N seconds".
- Organizers: "Publish anyway" for a blank prize (the first tap asks, the second publishes); the rupee sign is used instead of "Rs". The people list keeps insertion order, so family rows do not shuffle.
- Built but OFF: claim hold (switch CLAIM_HOLD; no such setting on Cloudflare). Bingo's live claim and pause behaviour is as before.

### 1 Nov 2026 22:10 IST, commit d5156bf (the wording, no-address and family-4 release)
Previous live: `4e0e210` (the hide release). The first attempt at 22:04 IST failed at the Functions bundle and deployed nothing.
- Users and Organizers: warm, third-person wording for refund, prize, privacy and e-mail lines; no street, city, state or pin code, only India; the Terms read "IT Services".
- Organizers: a guest may bring up to 4 family members; a fifth is refused politely ("You and up to 4 family members"). Decision by the owner 1 Nov about 19:45 IST.
- Organizers: the free Demo game and an owner-only Rs 1 payment test exist behind the switch DEMO_GAME (off). The game-core pack was updated to 0.10.0 (commit 0224581, common legal text).

### 1 Nov 2026 09:21 IST, commit 4e0e210 (hide-from-search release)
Same hide rule as the other sites (noindex tag, header, robots Disallow, no sitemap).

### 31 Oct 2026 21:19 IST, first live of release-list version 1.4.0 and 1.4.1 (commit 39c662a; further builds 23:52 and 1 Nov 03:32)
- The Corporate Games look: new website, one logo, six-item menu (How it works, Free demo game, Guide, Brochure, Refer and earn, Log in), one Corporate Games bar on every public page. Wording: "close group" everywhere.
- Engine steps 1 to 19 (vendored game-core 0.1.0 up to 0.9.11): shared engine and pause/host key, Email ID or employee ID per game, approvals and rehearsals ported from Tambola, first-party sales funnel (13 events, off).

## Earlier numbered releases (before 31 Oct 2026)
| Version | First live (IST) | Commit | Cloudflare deployment id | Title in the release list |
|---|---|---|---|---|
| 1.3.2 | 27 Oct 2026 11:56 | `bd66d3c` | `d13ae6ee-c8db-4a9f-9808-e2d9cb4218d0` | A game waiting for payment never blocks a new game |
| 1.3.1 | 27 Oct 2026 11:39 | `47115ce` | `bb928492-1a53-47e9-9589-4f431e3102ba` | Bigger daily write guard |
| 1.3.0 | 27 Oct 2026 11:30 | `04515b0` | `80263baf-3826-41f4-b353-0b0b046b7a37` | Same hardening as Corporate Tambola 1.3.3: joining, permissions, messages, simpler console |

Before numbered releases there were 21 earlier production deployments listed by Cloudflare (from 12 Oct 2026 17:46 to 23 Oct 2026 03:29 IST). They are not listed one by one here; open Cloudflare, Pages, the project, Deployments to see them.

## How to roll back
1. Sign in to the Cloudflare dashboard (the account that holds the Corporate Games sites).
2. Left menu: Workers and Pages. Open the project `corporate-bingo`.
3. Open the Deployments tab. Find the rollback id from the table above (the list shows the first 8 characters).
4. On that line press the three dots, then "Rollback to this deployment", and confirm.
5. Open https://bingo.corporatetambola.com/version.json and check that the commit is the old one. Check that the home page of the site opens.

Things to know before pressing the button:
- Do it only when no real game is being played or about to start (the release rule is: no real game within 3 hours; test games are named LT-...).
- A rollback puts back the old files and old code only. It does NOT undo database changes. Settings such as secrets are fixed into each deployment when it is made, so an old deployment may lack a setting that was added later (this is why same-build redeploys were needed to add the Google setting on 1 to 2 Nov 2026).
- After a rollback, check that the site is still hidden from search: robots.txt must say Disallow /, and every page must carry a noindex tag.


Database: Bingo has its own database; no migration was part of the 1 Nov or 2 Nov releases (the handover log says so for d5156bf, and a git diff on 2 Nov showed no migration, wrangler or sql file between d5156bf and fc5f01f), so no database step is needed.

## Known gaps and open decisions
- Real Rs 1 payment test for each game: the owner makes it himself on the main website. Open.
- Independent, water-tight review of the text of the one legal document (checklist row 45): not yet done.
- The new free Demo game sits behind a setting called DEMO_GAME. That name was not found in the Cloudflare settings of this project (read 2 Nov 2026), so it appears to be off. When to switch it on needs an audit and the owner's go. If the setting is held somewhere else this is unverified.
- /sitemap.xml: the new build has no sitemap, but an old copy can still be answered from Cloudflare's edge cache (a request with a query string such as ?x=1 shows 404). It leaves the cache by itself; a cache purge of the zone would clear it at once (not done).
- Test games used for live checks are named LT-... and are deleted afterwards.
- ID_ONLY: the setting exists on Cloudflare but its value is not readable here, so whether Bingo joining is ID-only today is unverified. The home legal text says "no mobile number", which is only true for Bingo once ID_ONLY is on.
- Claim hold (pause for everyone while claims are checked, restart 2.4 seconds after) is in the code but off. No live 3-phone test has been done for Bingo.
- Full test of the exact commits fabd9a9 and fc5f01f is owed (unverified).
- Stale base never to use: the main checkout of this repo sits on `master` at bd66d3c (1.3.2).

## Where the details are
- Handover file: `C:\ct\test-sites\handover\2026-11-01\RELEASE-HANDOVER-2026-11-01.md` (the release log is its section 10, open owner items are section 11). Older release notes of 31 Oct 2026 are in the folder `C:\ct\test-sites\handover\2026-10-31\`.
- Memory notes of the boss session, folder `C:\Users\Dell\.claude\projects\C--ct-ct\memory\`: `boss-state-2026-11-01.md` (state at each hour of 1 to 2 Nov 2026), `central-payment-ledger-rules-2026-11-01.md`, `wording-tone-rule-flowery-2026-11-01.md`, `game-rules-owner-decisions-2026-10-31.md`, `partner-laptop-2026-10-30.md` (how the test laptop is used).
- The list of decisions by the owner with status: `decisions-72h-checklist.md` and `decisions-72h-tambola-verified.md` in the handover folder; who did what: `sessions-done-register.md`.
- Release steps and rollback command: `release-runbook-2026-11-01.md` in the folder `handover\2026-10-31`.
- Technical readers can also open `docs/DEPLOYS.md` in a game repo (list of deployments by commit), where it exists.
