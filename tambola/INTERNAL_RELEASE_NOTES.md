# Corporate Tambola (housie): internal release notes

INTERNAL REFERENCE ONLY. Not for customers and not for any website or front end. Written on 2 Nov 2026 for the owner and future maintainers. All times are IST (India Standard Time, UTC plus 5:30). Facts were read from git, from the Cloudflare Pages deployment list (read-only) and from the live address on 2 Nov 2026 between 01:45 and 02:05 IST (the live state was still changing during that time, so a release made after 02:05 is not described here); anything that could not be checked is marked "unverified".

## What this is
Corporate Tambola is the online tambola (housie) game for company teams: an Organizer sets up a closed-group game, people join by ID on their phones, numbers are called on a timer, winners claim prizes. It is the first and most complete of the six Corporate Games; the other games copy its rules and screens.

| Item | Value |
|---|---|
| Live address | https://housie.corporatetambola.com |
| Cloudflare Pages project | `corporate-tambola` |
| GitHub repository | `FChecklist/corporate-tambola` (public) |
| Branch holding the latest release work | `feat/tambola-gentle-wording` (tip at the time of writing: `88fa696`) |
| What is live now | Release 1.9.0, commit `88fa696` (deployment `5a0429d6-667d-4e4e-b550-8f75696e24ae`, 1 Nov 2026 23:04 IST; re-deployed 23:57 IST as `785c5a93-bf91-43a0-975f-63dbba23159e`). Checked by the Cloudflare list and by version.json (commit 88fa696d5b42, version 1.9.0, dirty true). |

## Release table (newest first, since 31 Oct 2026)
| Date and time (IST) | Version | Commit | Cloudflare deployment id | Rollback id (the live one before it) | Tests and exceptions |
|---|---|---|---|---|---|
| 01 Nov 2026 23:57 | 1.9.0* | `88fa696` | `785c5a93-bf91-43a0-975f-63dbba23159e` | `5a0429d6-667d-4e4e-b550-8f75696e24ae` | Same build as the deployment before it, redeployed only to add the GOOGLE_CLIENT_ID setting (Google sign-in stays dormant on game pages: the owner switched it off in code on 23 Oct 2026; it is live on the console). version.json unchanged. No new tests. |
| 01 Nov 2026 23:04 | 1.9.0* | `88fa696` | `5a0429d6-667d-4e4e-b550-8f75696e24ae` | `21dc251c-2182-40c9-927a-844c5c0f9f39` | Partner full run on this exact commit: 3,866 pass / 11 fail (5 different failures): (a) the 'no flags' game test hangs (old; it also failed on 47e4fda, before the hide and claim work); (b) CRD-10 and CRD-11 crowd simulations (old; they fail on the live site too); (c) 'published and paid game in new screens' and 'Orders API client stand-in' pass when run alone (43 pass / 0 fail), so they are timing flakes on the 2-core partner laptop. DISCLOSED EXCEPTION: not a clean full-green run. Dirty build: the two deploy-time constants PRIZES_FROM_MS and EMP_CLEAN_FROM_MS were set to the deploy instant 1793554453235 and are not committed (version.json says dirty true). Live checks: version.json 88fa696d5b42; noindex header and tag on every page; robots Disallow; all pages 200; /api/mode LIVE. |
| 01 Nov 2026 09:07 | 1.9.0* | `e3d93e3` | `21dc251c-2182-40c9-927a-844c5c0f9f39` | `255e1087-95dc-40f2-8ac7-6d64b9b86423` | Hide-from-search release (noindex tag, X-Robots-Tag header, robots.txt Disallow all, no sitemap). A private-site test pins it. Full-run count not recorded in the handover (unverified). Private-site test and cache test: 5 pass. |
| 01 Nov 2026 09:05 | 1.9.0* | `7882fc1` | `255e1087-95dc-40f2-8ac7-6d64b9b86423` | `dbe07b54-8fe9-4bf1-881e-8e8859dbf0ed` | First hide deployment; its header default still lacked noindex, so the next deployment (21dc251c) fixed it.  |
| 01 Nov 2026 09:01 | 1.9.0* | `58d6d34` | `dbe07b54-8fe9-4bf1-881e-8e8859dbf0ed` | `b49698d2-fbc0-47fa-a0d5-143045093ab5` | Live before the hide release. Count for this exact commit not recorded; an earlier head of the same line (65a2e83) had 3,604 pass / 18 fail on the partner laptop (handover of 31 Oct). |
| 01 Nov 2026 05:44 | 1.9.0* | `1331b09` | `b49698d2-fbc0-47fa-a0d5-143045093ab5` | `bcc866a8-59c4-46bd-a4fe-d32fb20917f1` | Counts not recorded in the 1 Nov handover (unverified). |
| 31 Oct 2026 23:55 | 1.9.0* | `bbbcdb2` | `bcc866a8-59c4-46bd-a4fe-d32fb20917f1` | `cbb60284-07a7-41db-8083-fd8901a77257` | Counts not recorded in the 1 Nov handover (unverified). |
| 31 Oct 2026 13:18 | 1.9.0* | `646010d` | `cbb60284-07a7-41db-8083-fd8901a77257` | `71a6d8b7-7bfd-4981-9d28-f7b04e0192dc` | First deployment of version 1.9.0 (release-list entry in commit 646010d). Count not recorded in the 1 Nov handover (unverified). |
| 31 Oct 2026 12:48 | 1.8.5* | `168bff4` | `71a6d8b7-7bfd-4981-9d28-f7b04e0192dc` | `90d0e0d5-da6c-4407-88a9-ffceaad91d58` | Release-candidate build: the release list already said 1.8.5 (dated 30 Oct 07:38 IST) but this is the first deployment that carries that entry. Count not recorded (unverified). |
| 31 Oct 2026 09:33 | 1.8.5* | `e7302ef` | `90d0e0d5-da6c-4407-88a9-ffceaad91d58` | `0891ca59-727e-4626-a80d-08db5a26171a` | Release-candidate build, browser pass 5. Count not recorded (unverified). |

Version 1.9.0 is the number in the repo's release list (`apps/edge/src/releases.json`) and in the live `version.json`; the live file also names the commit. The release worktree used for the 1 Nov deploy was `C:\ct\test-sites\wt-tamb-r80`. Release steps (gate, build, deploy script, checks) are in `release-runbook-2026-11-01.md`.

## What changed in each release

### Release 1.9.0 build 88fa696, 1 Nov 2026 23:04 IST (the "gentle wording and join by ID" release)
Previous live: `e3d93e3` (the hide release of 09:07 IST). Decided by the owner on 1 Nov 2026 (rules written into the 72-hour decisions checklist).
- Users: every sentence the participants and Organizers read was rewritten in a soft, third-person voice (no blunt first-person refusal lines). Refunds are explained as credit for the next game, valid 365 days. Timers say "auto-deleted", a person's own action says "deleted", and the old word for wiping a record is not used anywhere in customer text.
- Users: no street, city or state is shown anywhere, only "India".
- Users: joining is by ID only. Each game has its own unique link; step 1 asks the ID; name and location are asked only for an ID that is not on the list. Mobile numbers and e-mails are not taken. Pasted ID lists may have 1, 2 or 3 columns and a header row; serial, name, e-mail and mobile columns are ignored. Letters and digits must be English ones.
- Organizers: a new "People asking to join" screen (ID, name, location, Confirm or No) for the Organizer, Host or Co-host; a small "Who is playing" panel with a collapsible Questions part.
- Organizers: the free demo game is limited to 3 per Organizer in 24 hours, with a polite refusal and a guide entry. The family pass limit is the host plus 4; a fifth person is refused politely (decision by the owner of 1 Nov about 19:45 IST, it was 10).
- Built but switched OFF: "claim hold" (while a claim is being checked the game waits for everyone, then restarts for everyone; the claimant's golden button reads "Claim now in N s"). The switch is CLAIM_HOLD; no such setting exists on Cloudflare, so it is off. It has not had the live 3-phone test (accept, reject, 60-second timeout, simultaneous claims) that must happen before it is switched on.
- Not changed: payments (IT SERVICES BY RAJAT AGARWAL and Razorpay only), prize sheet behaviour, all the 1.9.0 prize features below.

### 1 Nov 2026 09:01 to 09:07 IST, hide-from-search release (commits 58d6d34, 7882fc1, e3d93e3)
- The site stopped being listed in search: a noindex tag on every page, an X-Robots-Tag header on every rule, robots.txt Disallow all, and no sitemap in the built output. Owner rule: game sites are private but open by link.
- 58d6d34 (TT-34) was deployed first: an announcement saved before the console was ever opened now tells the Organizer it will not reach the phones yet.
- 7882fc1 missed one header rule, so e3d93e3 was deployed 2 minutes later. The wording branch did not contain these commits at first; deploying it as it was would have switched noindex off again (the "hide trap" found on 1 Nov at 19:55 IST), so the live hide commits were merged into it (119e4a5) before the 23:04 release.

### 31 Oct 2026 13:18 IST, version 1.9.0 first live (commit 646010d; builds at 09:33 and 12:48 were release candidates)
- Prizes step in the new organizer screens: Auto shows each prize with its share of the budget; Manual lets the Organizer set each amount and a gift name.
- After a game, the prize sheet lists each prize with the winner's ticket, ID, name and mobile number, for the Organizer only. A winner sees the prize name on the phone.
- A practice game is marked "Rehearsal, practice only" on both the organizer and participant pages. Buttons and tick boxes are at least 44 px; the prize table fits a phone.
- 31 Oct 23:55 IST (bbbcdb2): cache safety, every local script and style address carries ?v=commit so phones never keep an old file.

### Earlier in the series
Versions 1.2.1 to 1.8.5 (27 to 30 Oct 2026) are in the "Earlier numbered releases" table below with their titles.

## Earlier numbered releases (before 31 Oct 2026)
| Version | First live (IST) | Commit | Cloudflare deployment id | Title in the release list |
|---|---|---|---|---|
| 1.8.3 | 30 Oct 2026 06:49 | `751df6c` | `0891ca59-727e-4626-a80d-08db5a26171a` | Optional email ID for open games |
| 1.8.2 | 30 Oct 2026 05:37 | `a2f4b99` | `df7909ba-d9d2-4cfb-9f27-0769186fb0fd` | The new organizer screens open first |
| 1.8.0 | 30 Oct 2026 05:08 | `c28b42c` | `880c1c45-bbf7-4592-bcf6-2a3848a17ec2` | Family Passes, waiting limits and the player screens that go with them |
| 1.7.1 | 30 Oct 2026 02:42 | `8eddbde` | `0c96282f-635a-4dea-b935-9c1ee04236cd` | The player screens in two looks |
| 1.7.0 | 30 Oct 2026 01:10 | `e3c2365` | `ace8bb82-8708-420d-92fe-7cb41af73992` | One clean top menu, the new logo and fixes from user feedback |
| 1.6.7 | 29 Oct 2026 10:03 | `e6759a0` | `b043b02d-2434-4bd9-bd72-57440c083806` | Game names, plain wording |
| 1.6.6 | 29 Oct 2026 04:34 | `15b8003` | `a1ff42de-035e-4fce-a404-4a30630fcc74` | A fresher, friendlier front page |
| 1.6.5 | 28 Oct 2026 20:41 | `447487a` | `146d1ddd-305f-4f19-b3a2-9115a06978c7` | Front page headline in plain English |
| 1.6.4 | 28 Oct 2026 20:06 | `a3b9825` | `fa4a8140-ebde-4789-8396-36bac1e97aa8` | The game has its own address: housie.corporatetambola.com |
| 1.6.3 | 28 Oct 2026 17:40 | `963d6fd` | `910fa81d-62a6-4f0a-9d90-a5e882f7cb26` | Rehearsal guests, listening count, the logo in the PDF, shorter claims |
| 1.6.2 | 28 Oct 2026 16:58 | `65f962f` | `51cfe076-7d49-4f86-bda8-a5a85efab629` | Language dropdown (English for now) |
| 1.6.0 | 28 Oct 2026 15:21 | `7172997` | `9751a73a-f5dd-4fe1-931e-f9e14912189e` | Three free rehearsals for every paid game |
| 1.5.1 | 28 Oct 2026 14:19 | `998759d` | `eefb6df6-3fd4-4fd5-83d4-040ef965c1be` | A crowd joining at once is cheaper for the database |
| 1.5.0 | 28 Oct 2026 13:29 | `31f48ff` | `fd3dd1ae-38a8-4e6a-8286-fed4bbcbb677` | Claim buttons, claim timer, fast claim notice |
| 1.4.4 | 27 Oct 2026 22:05 | `5c6385e` | `8970bd21-d816-4bbb-af50-74eb294c7e93` | Manual play has no fixed gap |
| 1.4.3 | 27 Oct 2026 18:39 | `6e0f643` | `5b777c77-224f-4c4f-acc0-deb61329df2e` | One plain story for everybody |
| 1.4.1 | 27 Oct 2026 14:55 | `1229f11` | `1e8d7d6a-5a1c-4533-8c60-d3074edb8d8c` | Game-day clarity |
| 1.4.0 | 27 Oct 2026 12:47 | `45edbb2` | `3a095dc3-c42d-494f-9d86-00930a02f163` | Four game modes |
| 1.3.8 | 27 Oct 2026 11:05 | `c1f8c88` | `417c82e3-3322-47d4-86c8-4230d2157089` | The owner can make one game free |
| 1.3.7 | 27 Oct 2026 10:14 | `fd7f742` | `8358676d-46a6-4d3e-b9d1-31738f865b6c` | A free pack is used when you press Publish again |
| 1.3.6 | 27 Oct 2026 09:59 | `8e88ed1` | `7f324d62-8400-4213-8947-e6f57eeb031b` | One-time Rs 0 prospect links made from the owner console |
| 1.3.5 | 27 Oct 2026 09:45 | `19db44f` | `b09b8477-dd37-49dc-8cf7-e3e9f9212087` | A demo link now works when you are taken straight back into your game |
| 1.3.3 | 27 Oct 2026 07:07 | `a87dad5` | `4a01874b-c766-4932-b217-b2cea3fef3b4` | A join that gets no answer is asked again by itself |
| 1.3.2 | 27 Oct 2026 02:57 | `9e58a15` | `0583c6f2-53c3-42c8-9265-78018340dfff` | A Host's AI work link and an unaccepted Co-host can do less |
| 1.3.1 | 27 Oct 2026 02:31 | `cf3ca7b` | `4423b1b0-96e5-4a01-86cb-9e677367dc12` | Unknown country codes are refused with a plain sentence |
| 1.3.0 | 27 Oct 2026 01:59 | `4b8dcae` | `03e2150e-c435-49d5-87ae-14f1842bd39a` | Simpler organizer console, the organizer has the final say on prizes, and safety fixes |
| 1.2.1 | 27 Oct 2026 00:33 | `09d6696` | `fbf22266-5982-4df9-967d-6a95f42225da` | Join and organizer fixes found by the 10,000-case scenario tests |



## How to roll back
1. Sign in to the Cloudflare dashboard (the account that holds the Corporate Games sites).
2. Left menu: Workers and Pages. Open the project `corporate-tambola`.
3. Open the Deployments tab. Find the rollback id from the table above (the list shows the first 8 characters).
4. On that line press the three dots, then "Rollback to this deployment", and confirm.
5. Open https://housie.corporatetambola.com/version.json and check that the commit is the old one. Check that the home page of the site opens.

Things to know before pressing the button:
- Do it only when no real game is being played or about to start (the release rule is: no real game within 3 hours; test games are named LT-...).
- A rollback puts back the old files and old code only. It does NOT undo database changes. Settings such as secrets are fixed into each deployment when it is made, so an old deployment may lack a setting that was added later (this is why same-build redeploys were needed to add the Google setting on 1 to 2 Nov 2026).
- After a rollback, check that the site is still hidden from search: robots.txt must say Disallow /, and every page must carry a noindex tag.


Database: Tambola has its own database; no migration was part of the 1 Nov releases (none since e3d93e3), so a rollback needs no database step.

## Known gaps and open decisions
- Real Rs 1 payment test for each game: the owner makes it himself on the main website. Open.
- Independent, water-tight review of the text of the one legal document (checklist row 45): not yet done.
- The new free Demo game sits behind a setting called DEMO_GAME. That name was not found in the Cloudflare settings of this project (read 2 Nov 2026), so it appears to be off. When to switch it on needs an audit and the owner's go. If the setting is held somewhere else this is unverified.
- /sitemap.xml: the new build has no sitemap, but an old copy can still be answered from Cloudflare's edge cache (a request with a query string such as ?x=1 shows 404). It leaves the cache by itself; a cache purge of the zone would clear it at once (not done).
- Test games used for live checks are named LT-... and are deleted afterwards.
- Claim hold (CLAIM_HOLD) is built but off. The live game does NOT pause for everyone at a claim: the live game follows the public beacon (CLAIM_WINDOW_CALLS = 1); the 2.4-second pause exists only in `packages/engine`, which the live edge code does not use. Honest limits of the built version: the restart is "within about 3 seconds", not exactly 2.4; the hold starts about 30 seconds after the claim. Switch on only after a live 3-phone test.
- The win screen still shows "Share with friends / WhatsApp" (the Organizer switch TA32 is not applied).
- Sneha's points S01 to S22: passed live S02, S03, S04, S05, S09, S10, S12, S21; partly S07, S08, S15, S17; not tested live S01, S06, S11, S13, S14, S18, S19, S22; S16 is an open question for Sneha (see `tambola-claim-timer-and-sneha-tables.md`).
- Tests known to fail and not to chase again: CRD-10 and CRD-11 crowd simulations; the 'no flags' hang.
- Stale branches never to use as a base: `wip/join-redesign` (the main checkout of this repo sits on it, at 751df6c, 1.8.3).
- Unverified: whether the live Google client id setting is used by any game page (the button is off in code).

## Where the details are
- Handover file: `C:\ct\test-sites\handover\2026-11-01\RELEASE-HANDOVER-2026-11-01.md` (the release log is its section 10, open owner items are section 11). Older release notes of 31 Oct 2026 are in the folder `C:\ct\test-sites\handover\2026-10-31\`.
- Memory notes of the boss session, folder `C:\Users\Dell\.claude\projects\C--ct-ct\memory\`: `boss-state-2026-11-01.md` (state at each hour of 1 to 2 Nov 2026), `central-payment-ledger-rules-2026-11-01.md`, `wording-tone-rule-flowery-2026-11-01.md`, `game-rules-owner-decisions-2026-10-31.md`, `partner-laptop-2026-10-30.md` (how the test laptop is used).
- The list of decisions by the owner with status: `decisions-72h-checklist.md` and `decisions-72h-tambola-verified.md` in the handover folder; who did what: `sessions-done-register.md`.
- Release steps and rollback command: `release-runbook-2026-11-01.md` in the folder `handover\2026-10-31`.
- Technical readers can also open `docs/DEPLOYS.md` in a game repo (list of deployments by commit), where it exists.
