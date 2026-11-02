# Home (corporatetambola.com): internal release notes

INTERNAL REFERENCE ONLY. Not for customers and not for any website or front end. Written on 2 Nov 2026 for the owner and future maintainers. All times are IST (India Standard Time, UTC plus 5:30). Facts were read from git, from the Cloudflare Pages deployment list (read-only) and from the live address on 2 Nov 2026 between 01:45 and 02:05 IST (the live state was still changing during that time, so a release made after 02:05 is not described here); anything that could not be checked is marked "unverified".

## What this is
The home site is the one public website of the family: what the games are, who they are for (HR teams), pricing, contact, the one legal document at /terms, privacy, and the games menu. All create and sign-in buttons go to the console. It is a plain static site with one small Cloudflare function for redirects.

| Item | Value |
|---|---|
| Live address | https://home.corporatetambola.com (also corporatetambola.com and www.corporatetambola.com, which redirect here) |
| Cloudflare Pages project | `corporatetambola-home` |
| GitHub repository | `FChecklist/corporate-home` (public) |
| Branch holding the latest release work | `release/home-2026-11-01 (worktree `C:\ct\test-sites\wt-home-rel`)` (tip at the time of writing: `e3d367d`) |
| What is live now | Commit `b8b9fc2`, deployment `11f72250-...` (2 Nov 2026 10:17 IST), read from the Cloudflare list. The apex and www answer 301 to home.corporatetambola.com. No version number; the commit is the identifier. |

## Rules that hold for the whole family (as decided by the owner)
- One public site: home.corporatetambola.com. The game sites are not listed in search (noindex in the page, in the headers and in robots.txt) but open by link. One master console, one engine. No feature deleted.
- One single legal document for every product, at home.corporatetambola.com/terms (with anchors). Legal text version 2026-11-01 (document revision v4, owner approved 2 Nov 2026). No tick-boxes: one small line below the buttons with three links. No street, city or state anywhere, only "India". No age, 18+ or gambling lines. Third person only (no first-person plural words). Soft, user-favouring words. The old word for wiping a record is not used: timers say "auto-deleted", a person's own action says "deleted".
- Joining is by ID only ("Employee, Associate, Vendor or Member ID"): no mobile number and no e-mail from participants. The Organizer, Host or Co-host confirms people who are not on the list.
- Everything about the participants is deleted within 24 hours after the game (the code runs it at 20 hours). Kept: winners' results, game logs, Organizer and Host details, tax invoices.
- Payments only through IT SERVICES BY RAJAT AGARWAL and Razorpay (one central payment ledger). No other payee, no other gateway.
- Sign-in: e-mail code and Google sign-in are live on the console (checked 2 Nov 2026 between 01:45 and 02:05 IST (the live state was still changing during that time, so a release made after 02:05 is not described here) IST: the console says google true, microsoft false). Microsoft sign-in was dropped by the owner on 2 Nov 2026 ("lets not do microsoft", "just hide microsoft"; the owner also said no legal changes and no code changes at that point). The console, console.corporatetambola.com, is the one address to sign in and to create a game.
- People limits (owner, 31 Oct and 1 Nov 2026): Tambola, Bingo and Lucky Draw up to 100,000; Tic Tac Toe, Snakes and Ladders and Luck by Chance up to 2,000 (100,000 needs a load test before it is promised). Family pass limit: the person plus 4 (changed from 10 on 1 Nov 2026 about 19:45 IST).
- Demo game: same flow, Rs 0, up to 10 people, 3 per day per Organizer. Pause and Resume exist in all six games (Organizer or Host only).

## Release table (newest first, since 31 Oct 2026)
| Date and time (IST) | Version | Commit | Cloudflare deployment id | Rollback id (the live one before it) | Tests and exceptions |
|---|---|---|---|---|---|
| 02 Nov 2026 10:17 | none | `b8b9fc2` | `11f72250-3e43-479a-922a-89aa6924e5c2` | `fd7310d2-2c4f-4bb6-8c23-f0d83a096dbe` | Top-bar tagline under Corporate Games on all 12 pages (owner wording: Closed-group games for teams anywhere and their families: bonding, fun, your message and your brand.). Test limits changed with dated comments: words T09 1710 to 1725 (real 1724), top-bar height 80 to 90 px. Brand link has no aria-label (an aria-label fails axe label-content-name-mismatch). First full run had 2 failing cases, both fixed; released after the clean re-run (exact check count not recorded). |
| 02 Nov 2026 09:10 | none | `c005f50` | `fd7310d2-2c4f-4bb6-8c23-f0d83a096dbe` | `95ff2563-6249-4694-85b8-4084780dc43c` | Owner-approved wording: ID answer in the HR, IT and Legal questions; compliance bullets (no personal data asked, no advertising trackers). Word limit 1700 to 1710. Full browser run on this tree: 15 cases, 1871 checks, 0 failed. |
| 02 Nov 2026 01:41 | none | `e3d367d` | `95ff2563-6249-4694-85b8-4084780dc43c` | `ccc38f8d-7d4d-4b28-9368-5772479adb2a` | Full browser test: 15 cases, 1,871 checks, 0 failed (boss note; commit b5b1a03 says 1,870 checks at source ec8b0fc: a difference of one check, unverified which is exact). Earlier light checks: no-address 40, wording-links 80, cache 9, gamesbar checksum. Released 2 Nov 01:41 IST, after the 01:30 snapshot. Live checks (fetch about 01:45 IST): version.json commit e3d367d9b39d; corporatetambola.com and www.corporatetambola.com answer 301 to home.corporatetambola.com; /terms answers 200. |
| 01 Nov 2026 09:49 | none | `709f1d7` | `ccc38f8d-7d4d-4b28-9368-5772479adb2a` | `6f31d7a5-f6c8-4336-8d1f-7c68db220130` | Cache-versioning test 9 checks, 0 failed. Preview only before: production was 709f1d7. |
| 01 Nov 2026 00:04 | none | `9bfcf3e` | `6f31d7a5-f6c8-4336-8d1f-7c68db220130` | `8e9681cd-b091-49f8-bccc-ea3fdffcbf92` | Cache safety release; cache-versioning test 9 checks, 0 failed. |
| 31 Oct 2026 21:38 | none | `7d59872` | `8e9681cd-b091-49f8-bccc-ea3fdffcbf92` | `3afe6b11-4758-4489-a8db-677d47049270` | Privacy and Data page rewritten in the third person (owner wording of 31 Oct). Count not recorded here (unverified). |
| 31 Oct 2026 20:09 | none | `c2f9d88` | `3afe6b11-4758-4489-a8db-677d47049270` | `dabe1eee-da8f-4018-8db9-8f2c65d17ba7` | Per the commit message: last full test run 1,628 checks, 0 failed. |

## What changed in each release

### 2 Nov 2026 01:41 IST, commit e3d367d (the approved legal document and the redirects)
Previous live: `709f1d7`. Released after the 01:30 IST snapshot; this section was added when the Cloudflare list and a live fetch showed it live. Owner approvals typed at 23:00 IST on 1 Nov 2026: the home page is approved; the legal text v4 was approved on 2 Nov.
- Users: the one legal document (revision v4, text version 2026-11-01) is published at /terms with anchors; the old legal addresses stay as redirects. One document for every product, no tick-boxes, three small links below the buttons.
- Users: corporatetambola.com and www.corporatetambola.com now send visitors to home.corporatetambola.com with a permanent redirect (a small Cloudflare function, `functions/_middleware.js`).
- Users: the hero has one button, "Create your closed-group game", with a small line "(Try a free game with 10 people)" and a small Sign in link; all game cards and logos link to the console create page; the games menu lists every game, Lucky Draw included, with no direct game-site address.
- Users: new "Who can play" section and collapsed "Questions from HR, IT and Legal"; a band "Closed group and private by design"; "What you can count on" is the owner's list of eight claims; the Contact link is a small link in the sticky bar on every page.
- Users: third person only (no first-person plural words); no street, city or state, only India; no age, gambling, consent or who-plays lines.
- Quality: the phone Contact link is 44 px tall; the "Closed group and private by design" heading reaches contrast 4.5 to 1; the tests that were stale (T01, T02, T09) were brought in line with the owner's rules of 1 Nov.

### 1 Nov 2026 09:49 IST, commit 709f1d7
Home text change: "Virtual team building games" (no "in India"). Rollback target of the 2 Nov release: `ccc38f8d-7d4d-4b28-9368-5772479adb2a`.

### 31 Oct to 1 Nov 00:04 IST
Privacy and Data page fully rewritten in the third person (31 Oct 21:38); last full test 1,628 checks (31 Oct 20:09); cache safety, every local script and style address carries ?v=commit (1 Nov 00:04).

## Earlier deployments
Before numbered releases there were 14 earlier production deployments listed by Cloudflare (from 28 Oct 2026 19:40 to 29 Oct 2026 04:24 IST). They are not listed one by one here; open Cloudflare, Pages, the project, Deployments to see them.



## How to roll back
1. Sign in to the Cloudflare dashboard (the account that holds the Corporate Games sites).
2. Left menu: Workers and Pages. Open the project `corporatetambola-home`.
3. Open the Deployments tab. Find the rollback id from the table above (the list shows the first 8 characters).
4. On that line press the three dots, then "Rollback to this deployment", and confirm.
5. Open https://home.corporatetambola.com/version.json and check that the commit is the old one. Check that the home page of the site opens.

Things to know before pressing the button:
- Do it only when no real game is being played or about to start (the release rule is: no real game within 3 hours; test games are named LT-...).
- A rollback puts back the old files and old code only. It does NOT undo database changes. Settings such as secrets are fixed into each deployment when it is made, so an old deployment may lack a setting that was added later (this is why same-build redeploys were needed to add the Google setting on 1 to 2 Nov 2026).
- After a rollback, check that the site is still hidden from search: robots.txt must say Disallow /, and every page must carry a noindex tag.


The redirect function `functions/_middleware.js` is part of the 2 Nov release. Rolling back to `ccc38f8d` removes the apex and www redirects and the /terms page (that older build had no /terms), so do it only if the live home page itself is broken.

## Known gaps and open decisions
- Real Rs 1 payment test for each game: the owner makes it himself on the main website. Open.
- Independent, water-tight review of the text of the one legal document (checklist row 45): not yet done.
- The new free Demo game sits behind a setting called DEMO_GAME. That name was not found in the Cloudflare settings of this project (read 2 Nov 2026), so it appears to be off. When to switch it on needs an audit and the owner's go. If the setting is held somewhere else this is unverified.
- /sitemap.xml: the new build has no sitemap, but an old copy can still be answered from Cloudflare's edge cache (a request with a query string such as ?x=1 shows 404). It leaves the cache by itself; a cache purge of the zone would clear it at once (not done).
- Test games used for live checks are named LT-... and are deleted afterwards.
- The legal text still says "Google or Microsoft" although the console now shows Google only (owner, 2 Nov: no legal changes). Open decision.
- The typo domain `corproatetambola.com` was not found (it does not exist in DNS as of 1 Nov); buying it is a paid step that needs the owner's yes. Not done.
- The home text says "no mobile number" and ID-only joining. That is true for Tambola (code is live); for Bingo it depends on the ID_ONLY setting, and for Tic Tac Toe, Snakes, Luck and Lucky Draw it is not confirmed in the records (unverified).
- Claim-hold wording must not be published in the legal text until CLAIM_HOLD is switched on in the games. Whether the live /terms mentions it was not checked (unverified).
- Google sign-in screen branding links point to home.corporatetambola.com/terms (now live).
- Browser test: 15 cases; the earlier 1 Nov runs failed 296 of 1,857 checks (stale rules, one real tap-size problem, one real contrast problem); all fixed before the 2 Nov release, final run 0 failed.

## Where the details are
- Handover file: `C:\ct\test-sites\handover\2026-11-01\RELEASE-HANDOVER-2026-11-01.md` (the release log is its section 10, open owner items are section 11). Older release notes of 31 Oct 2026 are in the folder `C:\ct\test-sites\handover\2026-10-31\`.
- Memory notes of the boss session, folder `C:\Users\Dell\.claude\projects\C--ct-ct\memory\`: `boss-state-2026-11-01.md` (state at each hour of 1 to 2 Nov 2026), `central-payment-ledger-rules-2026-11-01.md`, `wording-tone-rule-flowery-2026-11-01.md`, `game-rules-owner-decisions-2026-10-31.md`, `partner-laptop-2026-10-30.md` (how the test laptop is used).
- The list of decisions by the owner with status: `decisions-72h-checklist.md` and `decisions-72h-tambola-verified.md` in the handover folder; who did what: `sessions-done-register.md`.
- Release steps and rollback command: `release-runbook-2026-11-01.md` in the folder `handover\2026-10-31`.
- Technical readers can also open `docs/DEPLOYS.md` in a game repo (list of deployments by commit), where it exists.
