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

The dot set is symmetric either way; `dir` fixes which physical onset is
generated first, which is what makes interval matching direction-aware.

Generation alternates outward from the center: chain index `+1` is the
first-generated onset, `-1` the second, `+2` the third, … so producing chain
index `i` takes `stepNum(i) = i>0 ? 2i-1 : -2i` steps. An interval is *created*
once both endpoints exist: `steps(A,B) = max(stepNum(i_A), stepNum(i_B))`.

## Modes (mutually exclusive; each deactivates **Change Key**)
- **Change Key** — click a bold note to move the center of symmetry (one at a time).
- **Interval Mode** — click any two onsets to draw a dotted line. The status
  panel shows the number of generation steps needed to create the interval.
  Another pattern **matches** when, centered on some bold note `C'`, it contains
  both endpoints at the **same absolute positions** and creates the interval in
  the **same number of steps**. Matched pattern buttons are highlighted and are
  the *only* pressable pattern buttons in this mode; pressing one keeps the
  interval selected and switches both the pattern and the key to the match.
  (Each matching pattern has exactly one matching center, and a pattern can
  never match itself at another key — same generator + same steps force the
  same center.)
- **Scale Mode** — pick a bold note as the **target center** (it need not belong
  to the active pattern) and a pattern button; the app selects the two points
  of the active pattern forming the interval that would lead to that pattern at
  that center in Interval Mode (fewest steps preferred), if one exists.

## Interpretation decisions
Two points in the brief were ambiguous; these were resolved with the requester:
1. **Bold notes = multiples of 6 (12 notes)** — reconciles "multiple of 12" with
   the later "select one of the 12 bolded notes" (72-EDO = 12 semitones × 6).
2. **Interval match = same generation step count AND same absolute endpoint
   positions**, with each pattern's ccw/cw generation direction baked in.
