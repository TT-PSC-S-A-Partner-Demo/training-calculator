# Roadmap (aspirational, not needed to code today)

Extra context for the cost lab. Skip it by scoping your prompt to `index.html`.

## Near term
- Keyboard input (digits, operators, Enter = equals, Esc = clear).
- Friendly divide-by-zero message instead of `Infinity`.
- Percentage key.

## Maybe later
- A history drawer showing the last N calculations.
- Expression mode: type `2+3*4` and evaluate with correct precedence.
- Memory keys (M+, M-, MR, MC).
- Theme toggle (light / dark) beyond the current system default.

## Probably never
- Scientific functions (sin, cos, log). Out of scope for a teaching kit.
- Unit conversions.
- Sync across devices. This is a single HTML file, on purpose.

## Open questions
- Should chained operations follow left-to-right, or full precedence? Today it is
  left-to-right, which surprises people who type `2+3*4` expecting 14.
- Do we need `CE` (clear entry) separate from `C` (clear all)? Users ask for it.
