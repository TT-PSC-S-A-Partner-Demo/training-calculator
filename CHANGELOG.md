# Changelog

All notable changes to the calculator are recorded here. This file is **not**
needed to work on the calculator - it exists so the folder has some extra context.
Scoping a prompt to `index.html` should skip all of this.

## [0.9.0] - 2026-05-02
- Reworked the button grid to CSS grid.
- Added a subtle press animation on the operator keys.
- Fixed alignment of the equals button on narrow screens.

## [0.8.3] - 2026-04-18
- Tweaked the display font to a monospace stack for even digit widths.
- Reduced the corner radius on the outer shell from 18px to 14px.

## [0.8.2] - 2026-04-01
- Hotfix: clear button was not resetting the pending operator.
- Minor: darkened the background gradient for contrast.

## [0.8.1] - 2026-03-20
- Accessibility pass: added aria-labels to every key.
- Increased tap targets to 44px minimum.

## [0.8.0] - 2026-03-05
- First public build of the browser calculator.
- Add, subtract, multiply, divide. Chained operations.
- Known issue: divide by zero shows `Infinity` (left as the seeded bug).

## [0.7.x] - internal prototypes
- Several throwaway prototypes, not shipped. Notes lost.
- Experimented with a scientific mode, dropped as out of scope.
- Tried a history drawer, reverted for being half-baked.
