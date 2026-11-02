# Corporate Tic Tac Toe: internal release notes

INTERNAL REFERENCE ONLY. Not for customers and not for any website or front end. Written on 2 Nov 2026 for the owner and future maintainers. All times are IST (India Standard Time, UTC plus 5:30). Facts were read from git, from the Cloudflare Pages deployment list (read-only) and from the live address on 2 Nov 2026 between 01:45 and 02:05 IST (the live state was still changing during that time, so a release made after 02:05 is not described here); anything that could not be checked is marked "unverified".

## What this is
Corporate Tic Tac Toe is the team tournament game: players are placed on a board and play tic tac toe in stages; the Organizer or Host runs the tournament and prizes go to the top places.

| Item | Value |
|---|---|
| Live address | https://tictactoe.corporatetambola.com |
| Cloudflare Pages project | `corporate-tic-tac-toe` |
| GitHub repository | `FChecklist/corporate-tic-tac-toe` (public) |
| Branch holding the latest release work | `feat/tictactoe-wording-pass2-2026-11-01` (tip at the time of writing: `7e4f912`) |
| What is live now | Commit `4b37bf3`, deployment `05f7a0e0-...` (2 Nov 2026 10:51 IST), read from the Cloudflare list. Release-list version 1.3.1. |

## Release table (newest first, since 31 Oct 2026)
| Date and time (IST) | Version | Commit | Cloudflare deployment id | Rollback id (the live one before it) | Tests and exceptions |
|---|---|---|---|---|---|
| 02 Nov 2026 10:51 | 1.3.1* | `4b37bf3` | `05f7a0e0-30fe-4ea1-a609-80943bc652fb` | `f4c1a710-840d-4e7a-8f0a-77c5428627fb` | Same build, no code change: only the shared owner password was set (Tambola's ORGANIZER_SECRET) so one password opens /paytest and /api/owner/* on all six games. Checked after deploy: shared password 200, wrong or no password 404, version.json equals the commit, mode LIVE, noindex present, /paytest 200. |
| 02 Nov 2026 09:11 | 1.3.1* | `4b37bf3` | `f4c1a710-840d-4e7a-8f0a-77c5428627fb` | `cf036f06-8500-4e3b-9a09-a6c08e892bf5` | Design pass: two columns on laptops, 44 px taps, darker Refer and earn text, cache v11. Full partner run r95: 2357 pass, 0 fail. |
| 01 Nov 2026 23:59 | 1.3.1* | `7e4f912` | `cf036f06-8500-4e3b-9a09-a6c08e892bf5` | `99bb1e46-204b-4405-9b76-8b6bc6f976b9` | Same build as the deployment before it, redeployed only to add the GOOGLE_CLIENT_ID setting (Google sign-in stays dormant on game pages: the owner switched it off in code on 23 Oct 2026; it is live on the console). version.json unchanged. No new tests. |
| 01 Nov 2026 21:42 | 1.3.1* | `7e4f912` | `99bb1e46-204b-4405-9b76-8b6bc6f976b9` | `63999bb6-2a4e-4696-9252-ec16759443a6` | Partner full run on this exact commit: 2,357 pass / 0 fail. Live checks: version.json 7e4f91208373, hide files present, built robots Disallow /, no sitemap, noindex on every page, no 'internal note' words in the output, all pages 200. GitHub push of 7e4f912 was done later the same night. |
| 01 Nov 2026 09:27 | 1.3.1* | `fc177f6` | `63999bb6-2a4e-4696-9252-ec16759443a6` | `8cb1146f-96f1-47d4-a4a4-8cc394f5cbaf` | Hide-from-search release (noindex tag, X-Robots-Tag header, robots.txt Disallow all, no sitemap). A private-site test pins it. Full-run count not recorded in the handover (unverified). |
| 01 Nov 2026 04:29 | 1.3.1* | `a4e9f78` | `8cb1146f-96f1-47d4-a4a4-8cc394f5cbaf` | `e2eb4d2b-f4c8-4427-9b45-f7679b765fd6` | Home-page funnel scripts load deferred. Count not recorded (unverified). |
| 31 Oct 2026 23:49 | 1.3.1* | `4a458ae` | `e2eb4d2b-f4c8-4427-9b45-f7679b765fd6` | `9fa0e7d1-d977-457a-8ab0-3efb4995300c` | Cache safety release. Count not recorded (unverified). |
| 31 Oct 2026 23:04 | 1.3.1* | `74b2f10` | `9fa0e7d1-d977-457a-8ab0-3efb4995300c` | `16445db4-98d9-42c8-9e81-747fd376e807` | Strict DOM test release. Count not recorded (unverified). |

Version marked with a star comes from the repo's release list (`apps/edge/src/releases.json`); the live version.json carries only the commit.

## What changed in each release

### 1 Nov 2026 21:42 IST, commit 7e4f912 (wording, no address, 2,000 cap release)
Previous live: `fc177f6` (the hide release). Release-list version 1.3.1.
- Users and Organizers: the refund sentences everywhere (console, guides, legal pages, mails, billing text) now say what the Organizer gets (credit for the next game); privacy, legal, refund policy, partner and sub-processor pages, report PDFs, mails and console texts moved to the third person.
- Users: no street, city, state or pin code anywhere; courts in India.
- Organizers: people limit 2,000 shown in the console box, the pay page and the guide; five prize places by default; rule numbers on the How it works page. The 100,000 limit is not promised (needs a load test).
- Organizers: a free Demo game exists behind the switch DEMO_GAME (off).
- The game-core pack was updated to 0224581 (participants give an employee ID only, one 24-hour deletion line). The hide test now expects noindex on every page.

### 1 Nov 2026 09:27 IST, commit fc177f6 (hide-from-search release)
Noindex tag and header, robots Disallow all, no sitemap. Rollback target of the 21:42 release: `63999bb6-2a4e-4696-9252-ec16759443a6`.

### 31 Oct and 1 Nov early morning (commits 74b2f10, 4a458ae, a4e9f78)
Strict DOM test (every id a rebuilt page's scripts look for exists), cache safety (?v=commit), and funnel scripts loaded deferred on the home page.

### 27 Oct 2026, versions 1.3.0 and 1.3.1
Tambola hardening: joining checked against the Organizer's list, one phone cannot play as another, a Co-host must accept before paying, simpler console, players' data deleted 20 hours after the end (promise stays 24 hours); daily write guard raised to 2,000,000.

## Earlier numbered releases (before 31 Oct 2026)
| Version | First live (IST) | Commit | Cloudflare deployment id | Title in the release list |
|---|---|---|---|---|
| 1.3.1 | 27 Oct 2026 12:59 | `045d629` | `16445db4-98d9-42c8-9e81-747fd376e807` | Bigger daily write guard |
| 1.3.0 | 27 Oct 2026 12:27 | `c00e029` | `2cb6aff3-5f64-499d-b86d-8f7377e832f1` | Same hardening as Corporate Tambola 1.3.3: joining, permissions, messages, simpler console |

Before numbered releases there were 19 earlier production deployments listed by Cloudflare (from 13 Oct 2026 16:13 to 23 Oct 2026 03:28 IST). They are not listed one by one here; open Cloudflare, Pages, the project, Deployments to see them.

## How to roll back
1. Sign in to the Cloudflare dashboard (the account that holds the Corporate Games sites).
2. Left menu: Workers and Pages. Open the project `corporate-tic-tac-toe`.
3. Open the Deployments tab. Find the rollback id from the table above (the list shows the first 8 characters).
4. On that line press the three dots, then "Rollback to this deployment", and confirm.
5. Open https://tictactoe.corporatetambola.com/version.json and check that the commit is the old one. Check that the home page of the site opens.

Things to know before pressing the button:
- Do it only when no real game is being played or about to start (the release rule is: no real game within 3 hours; test games are named LT-...).
- A rollback puts back the old files and old code only. It does NOT undo database changes. Settings such as secrets are fixed into each deployment when it is made, so an old deployment may lack a setting that was added later (this is why same-build redeploys were needed to add the Google setting on 1 to 2 Nov 2026).
- After a rollback, check that the site is still hidden from search: robots.txt must say Disallow /, and every page must carry a noindex tag.


Database: no migration was part of the 1 Nov releases (the diff against live had none), so no database step is needed.

## Known gaps and open decisions
- Real Rs 1 payment test for each game: the owner makes it himself on the main website. Open.
- Independent, water-tight review of the text of the one legal document (checklist row 45): not yet done.
- The new free Demo game sits behind a setting called DEMO_GAME. That name was not found in the Cloudflare settings of this project (read 2 Nov 2026), so it appears to be off. When to switch it on needs an audit and the owner's go. If the setting is held somewhere else this is unverified.
- /sitemap.xml: the new build has no sitemap, but an old copy can still be answered from Cloudflare's edge cache (a request with a query string such as ?x=1 shows 404). It leaves the cache by itself; a cache purge of the zone would clear it at once (not done).
- Test games used for live checks are named LT-... and are deleted afterwards.
- A 100,000-person game is not promised for Tic Tac Toe (owner cap is 2,000 until a load test).
- Stale base never to use: the main checkout of this repo is on `rel/after-tambola-ui-untested` at bb111a3, "Tic Tac Toe 1.4.0 (UNTESTED)". Do not release from it.
- Whether the ID-only join is fully in this game's live code is not confirmed in the records (the core pack 0224581 carries the ID-only legal text) (unverified).

## Where the details are
- Handover file: `C:\ct\test-sites\handover\2026-11-01\RELEASE-HANDOVER-2026-11-01.md` (the release log is its section 10, open owner items are section 11). Older release notes of 31 Oct 2026 are in the folder `C:\ct\test-sites\handover\2026-10-31\`.
- Memory notes of the boss session, folder `C:\Users\Dell\.claude\projects\C--ct-ct\memory\`: `boss-state-2026-11-01.md` (state at each hour of 1 to 2 Nov 2026), `central-payment-ledger-rules-2026-11-01.md`, `wording-tone-rule-flowery-2026-11-01.md`, `game-rules-owner-decisions-2026-10-31.md`, `partner-laptop-2026-10-30.md` (how the test laptop is used).
- The list of decisions by the owner with status: `decisions-72h-checklist.md` and `decisions-72h-tambola-verified.md` in the handover folder; who did what: `sessions-done-register.md`.
- Release steps and rollback command: `release-runbook-2026-11-01.md` in the folder `handover\2026-10-31`.
- Technical readers can also open `docs/DEPLOYS.md` in a game repo (list of deployments by commit), where it exists.
