# LOOK STATUS — BBoyz responsive redesign

**LOOK ONLY.** No app code changed, nothing merged, no prod deploy, `train-wip` untouched.
`/home/box/bboyz-workout-app` is clean and on `main` at `7f03abb`. `styles.css` was copied out of
it read-only. No account was signed into and none of Paul's data was read or written.

## Three-way delivery

1. **Sheet + enlargeable PNGs** — `/workspace/bboyz-redesign-look/sheet.html` (+ `index.html` copy)
   with `befores/`, `shots/`, `frames/`, `refs/`
2. **Zip** — `/workspace/BBoyz-redesign-LOOK.zip`
3. **Hosted** — see *Hosting* below

## The gap, measured on the shipped build

Befores are prod `7f03abb` (includes the workout builder merged earlier today), served locally and
rendered by headless Chrome at 390 / 768 / 1280 at 2×, so the real CSS breakpoints apply. Numbers
are read out of the live layout, not estimated.

| At 1280 | Before | After |
|---|---|---|
| Visible content card | **764px** | 1064px |
| Empty space each side | **150px** | 0px |
| Post-rail width unused | **28%** | 0% |
| `.view` box (CSS `max-width`) | **820px**, 122px gutters | 1240px cap, fills |
| Content columns | **1** (eight full-width bands) | 2 |
| Day's primary CTA | **82% down the page** (y=1509 of 1839) | 23% down (y=231) |
| **At 768** | 64px icon rail + **704px single column** | two columns |
| **At 390** | 5 fixed bottom tabs — correct | unchanged, kept |

1. **REQUIRED — desktop is a phone column.** 820px of content in 1064px of space; eight top-level
   bands, none ever side by side.
2. **Tablet underuses width** — icon rail, then the same stretched single column.
3. **Today has no next-action band** — calories, macros, log, weight, sleep, tasks and the coach
   card all stack at equal weight, and *Start workout* ends up last.
4. **Train chrome competes** — *Program & options*, *My workouts*, *Library*, *Switch day* and
   *Program details* are five bands stacked above the session itself.
5. **Nav strategy stops at the rail** — the worded rail exists at 1024+, but nothing behind it
   changes.

## After direction

- **Phone (390):** bottom tab bar kept exactly as-is. The only change is order — the session card
  leads (CTA at 15% of the page), then the week strip, log, then the numbers.
- **Tablet (768):** two columns; the single stretched column becomes real bands.
- **Desktop (1280):** Mercury bones — the existing worded rail kept, and beside it a two-track
  grid. Today = session + week + log left, calories/macros/body right. Train = session left
  (timer, lifts two-up, set chips), context right (this week, the program switch, My workouts /
  Library / Program details).

Held: blue + gold Precision, both themes, one filled gold control per screen, 44px targets
(verified), light mode checked. **15 distinct computed colours on the After page, every one
resolved from an existing `styles.css` token — no new colour was introduced.** No Suite Warp dark,
no phone sidebar. All After numbers are **EXAMPLE** and labelled on the page.

## Refero locks used (not re-picked)

`refs/mercury-dashboard.jpg` · `refs/alo-wellness-home.jpg` · `refs/sunsama-dayboard.jpg` ·
`refs/trainfitness-session.jpg` — all four seeded, all four used and credited on the sheet.

## The one genuinely signed-in Before — and a number that did not check out

`befores/before-myworkouts-desktop.png` is a **real signed-in capture** of Paul's account (his own
saved plans). The headline measurement is taken from it by scanning the PNG: the rail ends at
x=216, the content card runs x=366&ndash;1130 &mdash; **764px of content in 1064px of space, 150px dead on
each side.** It is used on the sheet as the primary desktop evidence.

**A note left in `befores/` said the desktop content was "~610px centered". I could not reproduce
that.** Two independent measurements agree with each other and not with 610: reading the live
layout gives `.view` = 820px (its CSS `max-width`), and scanning the screenshot gives a 764px
visible card &mdash; which is exactly 820 minus 28px padding each side. Flagging it rather than quietly
picking a number. **The gap is real on any of these figures**; at 610px it would only be worse.

## Files in `befores/` were being written by two processes at once

Genuine signed-in captures were landing in `befores/` while this run was capturing into the same
folder, and **this run's captures overwrote several of them** — only the My workouts one survived.
No conclusion here depends on that: the headline measurement is confirmed independently by the
surviving capture and by the live layout. If more real signed-in Befores exist elsewhere, they can
be dropped in and swapped into the sheet without changing anything. Saying so plainly because the
overwrite was mine.

## Caveat stated plainly

**The Befores were rendered with EXAMPLE meal/weight values seeded into the app's own render
path**, because signing in needs Paul's password and Claude cannot type it. The chrome, the CSS,
the breakpoints and every measurement above are the shipped build's own; only the numbers inside
the cards are examples. Nothing was captured from, or written to, Paul's account. If a genuinely
signed-in Before is wanted for the record, that needs a human at the keyboard — say the word and
it can be swapped in without changing any conclusion here.

## One found while measuring

The first tablet pass put four macro tiles across a ~510px column and `104/175` rendered as
`104/17` — a different number, no ellipsis to warn you. Fixed to two across. Same silent-truncation
class as the four-character food name in the compact entry row; worth remembering for any future
tile grid.

## Paths

- Sheet: `/workspace/bboyz-redesign-look/sheet.html`
- Befores (10 PNGs + `before-measurements.txt`): `/workspace/bboyz-redesign-look/befores/`
  &mdash; `before-myworkouts-desktop.png` is the genuine signed-in one
- Afters (7 PNGs + `after-measurements.txt`): `/workspace/bboyz-redesign-look/shots/`
- After frames (one markup per surface): `/workspace/bboyz-redesign-look/frames/`
- New CSS under consideration: `/workspace/bboyz-redesign-look/redesign.css`
- Zip: `/workspace/BBoyz-redesign-LOOK.zip`

## Hosting

**Live.** No Allow card appeared; `gh repo create` and the Pages API call both went through on the
existing `covertggtv-a11y` token.

- Repo: https://github.com/covertggtv-a11y/bboyz-redesign-look (public, `main`)
- Hosted: **https://covertggtv-a11y.github.io/bboyz-redesign-look/**

Verified 200: sheet, both measurement text files, every Before and After PNG, the After frames
(live and resizable in a browser), `redesign.css`, `styles.css` and all four refs.

## Next

**STOP for look-yes** via Prometheus. No build, no PR, no code. On a yes the work is layout only —
a wider content column at 1024+, a two-track grid inside it, and reordering Today so the session
leads. It touches no data path, no storage and no program logic.
