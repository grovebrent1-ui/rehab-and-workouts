# Rehab and workouts dashboard

Single-file phone dashboard for Brent's rehab and surf fitness training.

- Live page: https://grovebrent1-ui.github.io/rehab-and-workouts/rehab-dashboard.html
- Source: `rehab-dashboard.html` (vanilla HTML, CSS and JS, no external dependencies, no build step)
- Hosting: GitHub Pages, branch `main`, root folder. Added to the phone home screen.

## How to pick this up in a future chat
1. Attach this repo and pull the latest `main`.
2. Edit only `rehab-dashboard.html`.
3. Check JS syntax (`node --check` on the script block), test in headless Chromium at 390x844 (ticks, reload persistence, Week tab, no console errors), and make sure the file contains no em or en dashes.
4. Commit and push to `main`. Pages updates in a minute or two.
5. Add a line to the change log below.

## Structure of the file
- `GOALS` and `GKEYS`: five goals (arm, back, knee, mob, surf).
- `EX`: exercise library. Fields: `n` name, `rx` prescription, `m` minutes, `g` goal tags, `t` timer seconds, `v` video link, `i` instructions, `w` warning.
- `BLOCKS`: named groups of exercises (`id` or `id:minutes`). Block type: arm, str, mob, am, back.
- `PLAN`: Monday to Sunday. Each day has `am` (gym, surf or rest) and `ev` (evening blocks). `backPM` is added to the start of every `ev` by code after `PLAN`.
- `bamBlocks(i)` returns `["backAM"]`, shown every day under the morning slot.
- Tabs: Today, Week, Goals, Check-in, Safety.

## Clinical rules baked in
- Back rehab is Daniel Harvey's (spinal physiotherapist) five exercises, twice a day, every day: quads stretch using chair, kneeling hip flexor stretch, table top alternate LL (lower limb) lowering, table top bilateral LL extension (to about 45 degrees), bird dog. Blocks `backAM` and `backPM`.
- Only those exercises carry the `back` tag. Glute and hip strength is tagged knee only.
- Open book (`sobk`) and scorpion (`scor`) carry "Check with Daniel Harvey before doing this (spinal rotation)". Thread the needle and lizard lunge also rotate the spine and are not yet flagged.
- Removed from the back program: McGill curl-up, side plank, Pallof press, old bird dog.
- Gym sessions and the abs routine are Brent's own program and are only ticked, not edited.
- Tendon loading: pain up to 4 to 5 out of 10 acceptable if it settles within hours; increase load by no more than 10 percent a week.

## Saved progress (do not break)
Progress is stored in the browser's localStorage under the key `rehab_v2_state`, per device and browser. Shape: `{done:{date:{"blockId|exId":1}}, feel, surfed, checkins, start, dan, open}`. Do not rename the key or change this shape, or existing history is lost. The Check-in tab has Copy data and Paste data buttons for backup. Because exercise keys are `blockId|exId`, renaming a block or exercise id orphans its past ticks.

## Change log
- 2026-11-05: Merged Daniel Harvey's back prescription (morning and evening sets, every day) into the v2 tracking dashboard. Removed old back items. Retagged glute and hip work as knee only. Added the spinal rotation flags. Removed the older simple `index.html`.
