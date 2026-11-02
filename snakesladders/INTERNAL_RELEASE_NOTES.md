# Corporate Snakes and Ladders: internal release notes

INTERNAL REFERENCE ONLY. Not for customers and not for any website or front end. Written on 2 Nov 2026 for the owner and future maintainers. All times are IST (India Standard Time, UTC plus 5:30). Facts were read from git, from the Cloudflare Pages deployment list (read-only) and from the live address on 2 Nov 2026 between 01:45 and 02:05 IST (the live state was still changing during that time, so a release made after 02:05 is not described here); anything that could not be checked is marked "unverified".

## What this is
Corporate Snakes and Ladders is the board game for company teams: players move on a board with snakes and ladders in a fixed turn window; the Organizer or Host runs the game and prizes go to the top places.

| Item | Value |
|---|---|
| Live address | https://snakes.corporatetambola.com |
| Cloudflare Pages project | `corporate-snakes-and-ladders` |
| GitHub repository | `FChecklist/corporate-snakes-and-ladders` (public) |
| Branch holding the latest release work | `feat/snakes-wording-2026-11-01` (tip at the time of writing: `63f6fc1`) |
| What is live now | Commit `63f6fc1`, deployment `17eab148-1192-4d78-abdd-ebaf1ec40b30` (2 Nov 2026 01:45 IST; the release before it, `7004e9e`, went live at 22:28 IST on 1 Nov and was re-deployed at 00:00 IST). Confirmed by the Cloudflare list and by version.json (commit 63f6fc178a7b, dirty false). Release-list version 1.3.0. |

## Release table (newest first, since 31 Oct 2026)
| Date and time (IST) | Version | Commit | Cloudflare deployment id | Rollback id (the live one before it) | Tests and exceptions |
|---|---|---|---|---|---|
| 02 Nov 2026 01:45 | 1.3.0* | `63f6fc1` | `17eab148-1192-4d78-abdd-ebaf1ec40b30` | `5f76a78b-58e4-40ba-8c80-b133d41d4de9` | Released 2 Nov 2026 01:45 IST, after the 01:30 snapshot; the handover release log has no line for it yet. A full partner run on the earlier board head ecb9284 (run r85) gave 1,745 pass / 0 fail. This exact head 63f6fc1 was sent to the partner laptop as run r90 at about 01:36 IST; its result was NOT found (unverified). Live: version.json 63f6fc178a7b, built about 01:44 IST. No migration, wrangler or sql file differs between 7004e9e and 63f6fc1 (git diff on 2 Nov). |
| 02 Nov 2026 00:00 | 1.3.0* | `7004e9e` | `5f76a78b-58e4-40ba-8c80-b133d41d4de9` | `8d13f2f2-509d-46cd-848d-4938355c118d` | Same build as the deployment before it, redeployed only to add the GOOGLE_CLIENT_ID setting (Google sign-in stays dormant on game pages: the owner switched it off in code on 23 Oct 2026; it is live on the console). version.json unchanged. No new tests. |
| 01 Nov 2026 22:28 | 1.3.0* | `7004e9e` | `8d13f2f2-509d-46cd-848d-4938355c118d` | `69ed3c62-8cc6-4d14-8380-84064084f63f` | Full partner run on the exact commit: 1,740 pass / 2 fail. Both fails were load timeouts (two jobs ran on the partner laptop at once): 'board rules R7-R10 over 3,000 boards' and 'invoice rendering ... 6.2 s'. Both test files re-run alone on the exact commit: 37 pass / 0 fail. An earlier head (cc5ab3d) had failed 28 tests (old tests after the 2,000 cap) and was fixed first. DISCLOSED EXCEPTION: not a clean full-green run. Live checks: version.json 7004e9e24ce5, hide files present, built robots Disallow /, no sitemap file, noindex tag on every page, X-Robots-Tag, all pages 200. /sitemap.xml 200 is the old edge-cached copy. |
| 01 Nov 2026 09:32 | 1.3.0* | `798b90d` | `69ed3c62-8cc6-4d14-8380-84064084f63f` | `fc94024a-d067-48ac-9460-b4b10d57294c` | Hide-from-search release (noindex tag, X-Robots-Tag header, robots.txt Disallow all, no sitemap). A private-site test pins it. Full-run count not recorded in the handover (unverified). |
| 01 Nov 2026 03:58 | 1.3.0* | `95afbd2` | `fc94024a-d067-48ac-9460-b4b10d57294c` | `f4fdf67e-caaa-400d-8e40-41931763bf99` | Counts not recorded in the 1 Nov handover (unverified). |
| 31 Oct 2026 23:28 | 1.3.0* | `4c8cd53` | `f4fdf67e-caaa-400d-8e40-41931763bf99` | `70fee577-f096-4cdd-93d9-c3e9c3e6199f` | Counts not recorded in the 1 Nov handover (unverified). |
| 31 Oct 2026 23:25 | 1.3.0* | `72d4ea5` | `70fee577-f096-4cdd-93d9-c3e9c3e6199f` | `09d5f813-9cd6-4fb5-9fc8-752bc8d66bd6` | Counts not recorded in the 1 Nov handover (unverified). |
| 31 Oct 2026 23:15 | 1.3.0* | `8295c76` | `09d5f813-9cd6-4fb5-9fc8-752bc8d66bd6` | `b585a642-c1f2-4e45-a5f1-5943c4b6ee98` | Counts not recorded in the 1 Nov handover (unverified). |
| 31 Oct 2026 22:33 | 1.3.0* | `e12733a` | `b585a642-c1f2-4e45-a5f1-5943c4b6ee98` | `b26b9100-3233-4df0-8be6-47b129260776` | Counts not recorded in the 1 Nov handover (unverified). |

Version marked with a star comes from the repo's release list (`apps/edge/src/releases.json`); the live version.json carries only the commit.

## What changed in each release

### 2 Nov 2026 01:45 IST, commit 63f6fc1 (the new board)
Previous live: `5f76a78b` (the 00:00 re-deploy of 7004e9e). Released after the 01:30 IST snapshot; at 01:30 this commit was described as not released, and this section was written when the Cloudflare list and version.json showed it live. Five commits since 7004e9e:
- Users: a new board with 10 snakes, 10 ladders, 5 penalty squares and 5 reward squares (67f9eb0; the rule check asserts these numbers). The Organizer guide now says "10 snakes and 10 ladders" (it said 30 snakes and 15 ladders in 7004e9e).
- Users: the live board is redrawn as one picture: printed-tile squares, illustrated snakes, wooden ladders, a frame, a trophy and START (ecb9284). Then redone with slim snakes and ladders kept inside the grid and no flat snake or ladder, phone-first numbers and badges (2eb70bb); then short, separate snakes and ladders of 2 to 5 rows that do not cross and are spread over the board, with bigger snake heads (2fa1be2).
- Technical: the board generator is fast (median 16 ms, it was 65 to 700) and remembered per game id (63f6fc1); tests use fewer ids and explicit timeouts.
- Owner approval of this board: not recorded in the files read (at 01:00 IST on 2 Nov the owner had not yet said "approve" for Snakes) (unverified).

### 1 Nov 2026 22:28 IST, commit 7004e9e (owner rules, wording, 2,000 cap release)
Previous live: `798b90d` (the hide release of 09:32 IST). Release-list version 1.3.0.
- Users: a fixed 10-second turn window; a game is 7 or 8 minutes long (default 26 turns); the Organizer guide has a rules section.
- Users and Organizers: wording in the soft third person on legal, privacy, DPA, trust, report/PDF, mail and console texts (parts 1 to 3), remaining first-person plural text removed; no street, city, state or pin code.
- Organizers: a cap of 2,000 people per game with a refusal that says "number of people"; the family limit is self plus 4 (decision by the owner 1 Nov about 19:45 IST); the guide lists owner rule numbers (30 snakes, 15 ladders, 10 penalty, 10 reward squares, 2 extra throws, a 10-second window and gap, a lost throw).
- Organizers: a free Demo game exists behind the switch DEMO_GAME (off).
- Two hide-release code comments reworded so that no internal-note words are in the output.

### 1 Nov 2026 09:32 IST, commit 798b90d (hide-from-search release)
Noindex tag and header, robots Disallow all, no sitemap. Rollback target of the 22:28 release: `69ed3c62-8cc6-4d14-8380-84064084f63f`.

### 31 Oct to 1 Nov 2026 early morning
Cache safety (?v=commit) at 23:25 and 23:28; landing-page script fix at 23:15; a verify-test fix at 22:33; secrets list name FUNNEL_EVENTS at 03:58.

### 27 Oct 2026, release-list 1.3.0
Tambola hardening: joining by mobile number or employee ID, device proof on every vote, a Co-host must accept before paying, guided errors, data deleted 20 hours after the game, a red bar on the big screen when the connection is lost.

## Earlier numbered releases (before 31 Oct 2026)
| Version | First live (IST) | Commit | Cloudflare deployment id | Title in the release list |
|---|---|---|---|---|
| 1.3.0 | 27 Oct 2026 16:15 | `778e6dc` | `a3f44bfa-0548-44dc-89c1-c753bc203547` | Snakes and Ladders gets the Tambola hardening |

Before numbered releases there were 22 earlier production deployments listed by Cloudflare (from 13 Oct 2026 16:13 to 23 Oct 2026 03:32 IST). They are not listed one by one here; open Cloudflare, Pages, the project, Deployments to see them.

## How to roll back
1. Sign in to the Cloudflare dashboard (the account that holds the Corporate Games sites).
2. Left menu: Workers and Pages. Open the project `corporate-snakes-and-ladders`.
3. Open the Deployments tab. Find the rollback id from the table above (the list shows the first 8 characters).
4. On that line press the three dots, then "Rollback to this deployment", and confirm.
5. Open https://snakes.corporatetambola.com/version.json and check that the commit is the old one. Check that the home page of the site opens.

Things to know before pressing the button:
- Do it only when no real game is being played or about to start (the release rule is: no real game within 3 hours; test games are named LT-...).
- A rollback puts back the old files and old code only. It does NOT undo database changes. Settings such as secrets are fixed into each deployment when it is made, so an old deployment may lack a setting that was added later (this is why same-build redeploys were needed to add the Google setting on 1 to 2 Nov 2026).
- After a rollback, check that the site is still hidden from search: robots.txt must say Disallow /, and every page must carry a noindex tag.


Database: no migration was part of the 1 Nov release (the diff against live had none), so no database step is needed.

## Known gaps and open decisions
- Real Rs 1 payment test for each game: the owner makes it himself on the main website. Open.
- Independent, water-tight review of the text of the one legal document (checklist row 45): not yet done.
- The new free Demo game sits behind a setting called DEMO_GAME. That name was not found in the Cloudflare settings of this project (read 2 Nov 2026), so it appears to be off. When to switch it on needs an audit and the owner's go. If the setting is held somewhere else this is unverified.
- /sitemap.xml: the new build has no sitemap, but an old copy can still be answered from Cloudflare's edge cache (a request with a query string such as ?x=1 shows 404). It leaves the cache by itself; a cache purge of the zone would clear it at once (not done).
- Test games used for live checks are named LT-... and are deleted afterwards.
- Board numbers: the earlier guide (7004e9e) said 30 snakes and 15 ladders; the board and guide live now (63f6fc1) say 10 snakes, 10 ladders, 5 penalty and 5 reward squares. The owner's approval of these numbers is not recorded in the files read (unverified). Rollback target `5f76a78b` brings back the old board and the old guide text.
- A local preview of the board was served at http://localhost:4180/ on the boss laptop (only while that session runs).
- A 100,000-person game is not promised for Snakes (owner cap is 2,000 until a load test).
- The "pause for everyone while claims are checked, restart 2.4 seconds later" idea was not built for Snakes (handover of 1 Nov); Pause and Resume themselves exist.
- Whether ID-only joining is in this game's live code is not confirmed in the records (unverified).
- The Microsoft sign-in code written for the games (commit 5ffee85, branch feat/microsoft-signin-2026-11-01) is not needed now, because the owner dropped Microsoft sign-in on 2 Nov 2026. It should not be merged unless the owner asks for Microsoft again.
- The main checkout of this repo is on `master` at d2a3ebd (1.3.0 release notes); the release worktree `wt-snk-rel` is on a hide branch. Do not release from them.

## Where the details are
- Handover file: `C:\ct\test-sites\handover\2026-11-01\RELEASE-HANDOVER-2026-11-01.md` (the release log is its section 10, open owner items are section 11). Older release notes of 31 Oct 2026 are in the folder `C:\ct\test-sites\handover\2026-10-31\`.
- Memory notes of the boss session, folder `C:\Users\Dell\.claude\projects\C--ct-ct\memory\`: `boss-state-2026-11-01.md` (state at each hour of 1 to 2 Nov 2026), `central-payment-ledger-rules-2026-11-01.md`, `wording-tone-rule-flowery-2026-11-01.md`, `game-rules-owner-decisions-2026-10-31.md`, `partner-laptop-2026-10-30.md` (how the test laptop is used).
- The list of decisions by the owner with status: `decisions-72h-checklist.md` and `decisions-72h-tambola-verified.md` in the handover folder; who did what: `sessions-done-register.md`.
- Release steps and rollback command: `release-runbook-2026-11-01.md` in the folder `handover\2026-10-31`.
- Technical readers can also open `docs/DEPLOYS.md` in a game repo (list of deployments by commit), where it exists.
