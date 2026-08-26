# Design notes (scratch)

Rambling background, kept on purpose as extra context for the cost lab. None of it
is needed to change the calculator. If your prompt pulls this in, that is the point.

## Why a plain HTML file
No build step, no toolchain, no framework. A leader with no dev setup can open it in
a browser and evolve it with an agent. Everything lives in one `index.html` - markup,
styles, and logic - so there is exactly one file to reason about.

## The seeded bug
Divide by zero returns JavaScript's `Infinity`. It is left in on purpose: the first
real change in the exercise is to make it show a friendly message instead. Two earlier
attempts "fixed" it by special-casing `/0` but broke chained operations, which is a nice
lesson in changing behaviour without a test.

## Layout decisions nobody needs to re-litigate
- Grid is 4 columns. Operators down the right, like a phone.
- Equals spans a single cell now; an earlier version spanned two and looked odd.
- Colours come from a small set of CSS variables at the top of the style block.

## Things deliberately out of scope
- No keyboard input yet (that is one of the evolution beats).
- No history (also an evolution beat).
- No percentage or expression parsing with precedence - later, if at all.

## Random observations
- Users expect `C` to clear everything and `CE` to clear the entry; we only have `C`.
- Floating point means `0.1 + 0.2` shows `0.30000000000000004`. Not fixed here.
- The display truncates very long numbers rather than scrolling. Good enough.
