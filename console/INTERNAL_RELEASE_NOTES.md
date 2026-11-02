# Master Organizer Console: internal release notes

INTERNAL REFERENCE ONLY. Not for customers and not for any website or front end. Written on 2 Nov 2026 for the owner and future maintainers. All times are IST (India Standard Time, UTC plus 5:30). Facts were read from git, from the Cloudflare Pages deployment list (read-only) and from the live address on 2 Nov 2026 between 01:45 and 02:05 IST (the live state was still changing during that time, so a release made after 02:05 is not described here); anything that could not be checked is marked "unverified".

## What this is
The master console is the one place where an Organizer signs in and creates a game for any of the six Corporate Games (Tambola, Bingo, Tic Tac Toe, Snakes and Ladders, Luck by Chance, Lucky Draw). It also holds the owner pages (visitor statistics, owner numbers). It is a single-page app with its own database (Cloudflare D1 `corporate-games-master-console`).

| Item | Value |
|---|---|
| Live address | https://console.corporatetambola.com |
| Cloudflare Pages project | `corporate-console` |
| GitHub repository | `FChecklist/corporate-console` (public) |
| Branch holding the latest release work | `release/console-google-signin-2026-11-01` (tip at the time of writing: `584cc77`) |
| What is live now | Commit `584cc77`, deployment `9210e824-bbcf-4678-9c64-01a4b04008a1` (1 Nov 2026 23:52 IST). The built version.json still says commit 6ef68cdf032d (see the exception in the table), version label 0.1.0, released 1 Nov 2026 22:39 IST. Confirmed by the Cloudflare list and by a live fetch of version.json and /auth/providers. |

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
| 01 Nov 2026 23:52 | 0.1.0* | `584cc77` | `9210e824-bbcf-4678-9c64-01a4b04008a1` | `cbabefdc-fb5a-4b30-b4a4-f14b357d7310` | Config-only change on top of 6ef68cd (wrangler.toml: own address and the public Google client id); no new test run recorded (unverified). DISCLOSED EXCEPTION: wrangler.toml changed in commit 584cc77 without the dist version.json update, so version.json still says 6ef68cd while the deployed config is 584cc77 (the built files are identical). Live checks (2 Nov about 01:45 IST): /auth/providers says google true, microsoft false. |
| 01 Nov 2026 23:49 | 0.1.0* | `584cc77` | `cbabefdc-fb5a-4b30-b4a4-f14b357d7310` | `ee61bd80-f719-4725-8f86-996216af9276` | First deployment of 584cc77; replaced 3 minutes later by 9210e824 (same commit). Rollback target of 9210e824. |
| 01 Nov 2026 23:47 | 0.1.0* | `6ef68cd` | `ee61bd80-f719-4725-8f86-996216af9276` | `b2a22033-4f98-42ff-b801-0a054683722f` | Same build as b2a22033 (6ef68cd), redeployed while the Google settings were being added. |
| 01 Nov 2026 22:40 | 0.1.0* | `6ef68cd` | `b2a22033-4f98-42ff-b801-0a054683722f` | `ee97d23e-ccd8-4925-b22c-6b47d92bc498` | Migration 0004_visit_event applied first to the D1 database corporate-games-master-console (additive, repeat-safe: 12 statements, 0 failed). Partner full run: 349 pass / 9 fail, all 9 'Cannot find package happy-dom' (the partner install was stuck and restarted); the 8 happy-dom files re-run on the boss laptop: 86 pass / 0 fail. DISCLOSED EXCEPTION: split run on two machines, not one clean full run. Live checks: version.json commit 6ef68cd, noindex header and tag, robots Disallow, pages 200, /auth/me signedIn false, #/create loads with the version footer. /sitemap.xml answers 200 with the app page (noindex), not a real sitemap. |
| 01 Nov 2026 09:09 | 0.1.0* | `2b151ce` | `ee97d23e-ccd8-4925-b22c-6b47d92bc498` | `2bd56635-4f12-43e2-8b74-5ff296982976` | Hide-from-search release (noindex tag, X-Robots-Tag header, robots.txt Disallow all, no sitemap). A private-site test pins it. Full-run count not recorded in the handover (unverified). The gamesbar test has 1 failure that is also on the live commit before it (unrelated). |
| 01 Nov 2026 04:32 | 0.1.0* | `128e17b` | `2bd56635-4f12-43e2-8b74-5ff296982976` | `80506d5d-6eec-4666-b070-e314175bdcaa` | Partner laptop 431 pass / 0 fail on head 4d6e247 plus one stamp commit (31 Oct note). |
| 31 Oct 2026 20:18 | 0.1.0* | `2644125` | `80506d5d-6eec-4666-b070-e314175bdcaa` | `ddf54f7a-e8e7-442d-b121-0d81bd0696f9` | Linux run 423 pass / 8 fail, all environment causes (a hard-coded Windows git path and one timeout); Windows run 424 pass / 7 fail (31 Oct note). |

The version label 0.1.0 is a fixed label in `releases.json`; it does not change from release to release, so the commit and the "released at" time in version.json are the real identifiers.

## What changed in each release

### 1 Nov 2026 23:47 to 23:52 IST, commit 584cc77 (Google sign-in and the console's own address)
Previous live: `6ef68cd`. Decided by the owner on 1 Nov 2026 (Google sign-in) and set up by the boss session between 23:35 and 00:10 IST.
- Users and Organizers: a "Continue with Google" button is live on the console (verified e-mail only; no extra code step). E-mail code sign-in stays.
- Technical: the console's own address `console.corporatetambola.com` is now the origin (CONSOLE_ORIGIN; it had been the pages.dev name, which also broke the same-origin safety check on the custom address). The public Google client id is in `wrangler.toml`.
- Google sign-in was set up on 1 to 2 Nov 2026 (23:35 to 00:10 IST): one Google Cloud project named `corporate-tambola` and one OAuth client named "Corporate Games website", published to production. The public client id and the callback address are held in the Cloudflare settings of the console; the client secret exists only as a Cloudflare secret and is not written in any file.
- IMPORTANT for the next maintainer: this Pages project is managed by `wrangler.toml` (pages_build_output_dir), so plain variables set in the Cloudflare dashboard are ignored. Only secrets apply from the dashboard. Public values must be put into `wrangler.toml` under [vars].
- Secret handling: the client secret was copied by clipboard straight into Cloudflare and never displayed or written to a file. An earlier secret was shown once by accident in a tool result; it and an older one were disabled and deleted at Google the same night, and only the newest one exists.
- On 2 Nov 2026 the owner dropped Microsoft sign-in ("lets not do microsoft", "just hide microsoft"). The console says microsoft false. The server-side Microsoft code exists in the console but needs an app registration and a secret, which were not created.

### 1 Nov 2026 22:40 IST, commit 6ef68cd (wording, demo-first create, sign-in code release)
Previous live: `ee97d23e` (2b151ce, the hide release). The stamp commit 6ef68cd followed 1ded8cd.
- Organizers: gentler console screens, e-mails and report text (26 sentences). `/create?game=<id>` opens that game directly; the free Demo (up to 10 people) is listed first with a Demo label and reuses each game's own free path.
- Organizers: no tick box on sign-in; one small line below the buttons links the one legal document.
- Users: "Continue with Google and Microsoft" was added in the code (OAuth code with PKCE, verified e-mail only, switched on only when the secret names exist).
- Owner: visitor statistics: a collector (/stats/v, switch-gated, respects Global Privacy Control and Do Not Track, no personal details), owner numbers and a CSV, an owner page. Test-run traffic is not counted. Database migration 0004_visit_event was applied.
- Tests added: no city, state or address words in shipped files; no age, 18+ or gambling line in shipped files.

### 1 Nov 2026 09:09 IST, commit 2b151ce (hide-from-search release)
Noindex tag and header, robots Disallow all. Rollback target of the 22:40 release: `ee97d23e-ccd8-4925-b22c-6b47d92bc498`.

### 30 Oct to 1 Nov early morning
The console went live on 30 Oct 2026 08:08 IST with its own D1 database; stamp releases followed on 30 Oct (08:18, 08:53), 31 Oct 20:18 and 1 Nov 04:32 IST.

## Earlier numbered releases
| Version | First live (IST) | Commit | Cloudflare deployment id | Title in the release list |
|---|---|---|---|---|
| 0.1.0 | 30 Oct 2026 08:08 | `54c30e2` | `970c6af9-7631-46cb-a965-5b747b1b8e73` |  |



## How to roll back
1. Sign in to the Cloudflare dashboard (the account that holds the Corporate Games sites).
2. Left menu: Workers and Pages. Open the project `corporate-console`.
3. Open the Deployments tab. Find the rollback id from the table above (the list shows the first 8 characters).
4. On that line press the three dots, then "Rollback to this deployment", and confirm.
5. Open https://console.corporatetambola.com/version.json and check that the commit is the old one. Check that the home page of the site opens.

Things to know before pressing the button:
- Do it only when no real game is being played or about to start (the release rule is: no real game within 3 hours; test games are named LT-...).
- A rollback puts back the old files and old code only. It does NOT undo database changes. Settings such as secrets are fixed into each deployment when it is made, so an old deployment may lack a setting that was added later (this is why same-build redeploys were needed to add the Google setting on 1 to 2 Nov 2026).
- After a rollback, check that the site is still hidden from search: robots.txt must say Disallow /, and every page must carry a noindex tag.


Database: migration 0004_visit_event (visitor statistics) was applied to the console's D1 database. A rollback does NOT undo it; it is additive, so old code keeps working.

## Known gaps and open decisions
- Real Rs 1 payment test for each game: the owner makes it himself on the main website. Open.
- Independent, water-tight review of the text of the one legal document (checklist row 45): not yet done.
- The new free Demo game sits behind a setting called DEMO_GAME. That name was not found in the Cloudflare settings of this project (read 2 Nov 2026), so it appears to be off. When to switch it on needs an audit and the owner's go. If the setting is held somewhere else this is unverified.
- /sitemap.xml: the new build has no sitemap, but an old copy can still be answered from Cloudflare's edge cache (a request with a query string such as ?x=1 shows 404). It leaves the cache by itself; a cache purge of the zone would clear it at once (not done).
- Test games used for live checks are named LT-... and are deleted afterwards.
- Microsoft sign-in is dropped (owner, 2 Nov 2026). The legal text still says "Google or Microsoft" because the owner said not to change the legal text. Open decision: when to correct that sentence.
- The owner should test sign-in himself with his Google account and the e-mail code; no password is ever typed by the boss session.
- version.json still says 6ef68cd although 584cc77 is deployed. A later release should re-stamp (`tools/deploy/stamp-release.mjs`).
- The partner test laptop can miss the `happy-dom` package (install timeouts); a run showing 'Cannot find package happy-dom' is an install problem, not a code failure.
- The visitor-statistics collector is behind a switch and its first-party funnel reports are owner-only.
- The main checkout of this repo is on `main` at a56602c (27 Oct). Do not release from it.

## Where the details are
- Handover file: `C:\ct\test-sites\handover\2026-11-01\RELEASE-HANDOVER-2026-11-01.md` (the release log is its section 10, open owner items are section 11). Older release notes of 31 Oct 2026 are in the folder `C:\ct\test-sites\handover\2026-10-31\`.
- Memory notes of the boss session, folder `C:\Users\Dell\.claude\projects\C--ct-ct\memory\`: `boss-state-2026-11-01.md` (state at each hour of 1 to 2 Nov 2026), `central-payment-ledger-rules-2026-11-01.md`, `wording-tone-rule-flowery-2026-11-01.md`, `game-rules-owner-decisions-2026-10-31.md`, `partner-laptop-2026-10-30.md` (how the test laptop is used).
- The list of decisions by the owner with status: `decisions-72h-checklist.md` and `decisions-72h-tambola-verified.md` in the handover folder; who did what: `sessions-done-register.md`.
- Release steps and rollback command: `release-runbook-2026-11-01.md` in the folder `handover\2026-10-31`.
- Technical readers can also open `docs/DEPLOYS.md` in a game repo (list of deployments by commit), where it exists.
