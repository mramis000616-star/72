# Mod-72 Maximally Even Circle

An interactive, self-contained visualization (single `index.html`, no build/deps —
just open it in a browser) of maximally even (ME) patterns on a circle of 72 points.

## Layout
- **72 points**, index `0..71`, point `0` at the top, clockwise = increasing index.
- **Bold notes** are the **multiples of 6** → `{0,6,12,…,66}` (12 notes). These are
  the selectable "keys" / centers of symmetry.

## Patterns
Buttons `5 7 17 19 29 31` each activate a maximally even pattern whose onset count
equals the button label. Each onset is marked with a **ring**; the center of
symmetry (on the selected key) gets a gold ring.

A pattern is a symmetric chain of a generating interval `g` (mod 72) about the center:

```
pos(i) = ( center + dir · i · g )  mod 72 ,   i = -m..m,  m = (k-1)/2
```

| pattern k | generator g | direction (first generator) |
|----------:|------------:|------------------------------|
| 5  | 29 | counter-clockwise (`dir = -1`) |
| 7  | 31 | clockwise (`dir = +1`) |
| 17 | 17 | counter-clockwise (`dir = -1`) |
| 19 | 19 | clockwise (`dir = +1`) |
| 29 | 5  | counter-clockwise (`dir = -1`) |
| 31 | 7  | clockwise (`dir = +1`) |

The dot set is symmetric either way; `dir` fixes which physical onset is the
"+1 generator" onset, which is what makes interval matching direction-aware.

## Modes (mutually exclusive; each deactivates **Change Key**)
- **Change Key** — click a bold note to move the center of symmetry (one at a time).
- **Interval Mode** — click any two onsets to draw a dotted line. The status panel
  shows the generator count `n` and position `d = (dir·n·g) mod 72`. Any other
  pattern that can form the **same interval with the same generator count**
  (`|n| ≤ T-1` and `(dir_T·n·g_T) mod 72 == d`) is **highlighted**; clicking it
  switches to that pattern.
- **Scale Mode** — pick a bold note (root) and a pattern button; the app selects
  the interval (root → onset) within the active pattern that would lead to that
  target pattern in Interval Mode, if one exists.

## Interpretation decisions
Two points in the brief were ambiguous; these were resolved with the requester:
1. **Bold notes = multiples of 6 (12 notes)** — reconciles "multiple of 12" with
   the later "select one of the 12 bolded notes" (72-EDO = 12 semitones × 6).
2. **Interval match = same generator count `n` AND same position `d` (mod 72)**,
   with each pattern's ccw/cw generation direction baked into the comparison.

Scale Mode is implemented as the inverse of Interval Mode (find the interval that
leads to the chosen pattern); the exact desired behavior here is the most
open-ended part of the spec and is easy to adjust in `tryScaleSelect()`.
