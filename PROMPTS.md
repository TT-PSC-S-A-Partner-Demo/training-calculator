# Exercise kit — browser calculator (no-IDE track)

For participants with **no IDE and no compiler** — leaders, PMs, anyone who is
not set up to write code. The whole exercise is one self-contained `index.html`.
The agent edits the file; they refresh the browser to see it. No build, no
toolchain, no Gradle, no Go. Lowest possible barrier — and it still teaches the
real method: lock what works, then let the agent change code you did not write.

Tool: **Codex CLI in the folder + a browser tab.** That is all.

> **On purpose:** the folder carries extra files that the calculator does not need -
> `CHANGELOG.md`, `NOTES.md`, `docs/roadmap.md`, `data/sample-history.json`. They are
> context bait. "Read the whole project and improve it" pulls all of them in and costs
> more; scoping to `index.html` skips them. A cheap live demo of the cost lesson.

---

## Setup (T-5 min)

```bash
cd demo-kit-calc            # the folder with index.html
codex                       # start Codex CLI here
```
Open `index.html` in a browser (double-click it, or drag it into a tab). You get
a working calculator. Keep the terminal and the browser side by side. After every
change: **save is automatic (the agent writes the file); you press Ctrl+R / Cmd+R
in the browser to see it.**

> Say this once: "The agent edits the file. You refresh the page. That loop —
> ask, refresh, check — is the whole job today. You will not type any code."

---

## The tripwire (do this BEFORE any change)

Non-developers do not write unit tests, but they still need a safety net. Ours is
a five-line checklist. Write it on screen and re-run it after **every** change:

```
TRIPWIRE — must still be true after each change:
  1. 2 + 2 =            -> 4
  2. 7 x 8 =            -> 56
  3. 9 - 4 - 1 =        -> 4
  4. C                  -> clears to 0
  5. 5 . 5 + 1 =        -> 6.5
```
> Say: "This is the same idea the developers are using next door, just by hand.
> Before you let the agent touch anything, you write down what already works.
> Then any change that breaks the list is caught in ten seconds."

---

## Beats — paste into Codex CLI, refresh after each

Give people **one** at a time. After each: run the tripwire, then move on.

**Beat 1 — Understand it first (read-only).**
```
Read index.html and explain in plain language how this calculator works:
where the numbers are stored, how an operation like plus is handled, and what
happens when I press equals. Do not change anything yet.
```
> The point: the agent explains code they did not write, in words they understand.

**Beat 2 — Fix a real bug (divide by zero).**
```
Right now, dividing by zero shows "Infinity". Change it so that dividing by zero
shows the message "Cannot divide by 0" on the display instead, and the next
number I press starts fresh. Keep everything else working exactly as it is.
```
Refresh → try `6 ÷ 0 =`. Then run the tripwire.

**Beat 3 — Add keyboard support.**
```
Let me use the keyboard as well as the buttons: number keys and "." type digits,
+ - * / choose the operation, Enter or = computes, Escape or "c" clears. Do not
remove the on-screen buttons.
```
Refresh → type `12+30` then Enter. Tripwire.

**Beat 4 — Add a backspace.**
```
Add a backspace/delete button in the top row and make the Backspace key remove
the last digit I typed. If everything is removed, show 0.
```
Tripwire.

**Beat 5 — Add a percent key.**
```
Add a "%" key. When I press it, turn the current number into its percentage
(divide it by 100). For example 50 then % shows 0.5.
```
Tripwire.

**Beat 6 — Show a running history.**
```
Below the calculator, show a short history: each completed calculation as a line
like "2 + 2 = 4", newest at the top, keep the last five. Clearing with C does not
wipe the history.
```
Tripwire.

**Beat 7 (optional, if time) — A dark mode toggle.**
```
Add a small button that toggles a dark colour theme for the calculator, and
remember my choice so it stays dark when I refresh the page.
```

**Beat 8 — Optimize a bloated prompt.**
Here is a deliberately wasteful prompt. **Your task: get the same result for far fewer
tokens.** Run it as-is first (`/status` = BEFORE), then rewrite it and run yours
(`/new`, `/status` = AFTER).
```
WASTEFUL (run this first, note the tokens):
Hi! Please take a very thorough look at this entire calculator project - read every
single file in the folder, the changelog, the notes, the sample data, all of it, plus
index.html - then give me a complete detailed explanation of how everything works, its
full history and every design decision and all known issues, and while you're at it add
a nice dark mode theme with a toggle, and explain in detail everything you changed.
```
Rewrite it so it does only what you actually want (the dark-mode toggle), scoped to
`index.html`, skipping the noise files. Run your tripwire. Compare the two token counts.
> Say: "Same outcome, a fraction of the cost. It read the changelog and sample data for
> nothing. Scoping and saying what to skip is the whole skill - the cheaper one that
> still passes the tripwire wins."

**Wrap — count the cost.**
```
/status
```
> Say: "You just changed software six times without writing a line of code —
> and you had a checklist that caught mistakes instantly. That is the whole
> method the developers use, minus the compiler."

---

## When it breaks

| Symptom | Do this |
|---|---|
| Change did not appear | You forgot to refresh. Ctrl+R / Cmd+R. Hard refresh: Ctrl+Shift+R. |
| Calculator is now blank / broken | Ask the agent: "undo your last change, the page is blank." Or the tripwire caught it — say "that broke rule 3, please fix it." |
| Agent rewrote the whole file | Fine if the tripwire still passes. If not: "restore the buttons and the basic + - x / that worked before." |
| Someone is far ahead | Give them beat 7, or "add an M+ / MR / MC memory, storing one number." |
| Someone is stuck on setup | They can still follow on the shared screen — this track is meant to be watchable too. |

---

## Facilitator note

The starter `index.html` is deliberately simple and readable (plain state:
`current`, `previous`, `operator`) so the agent's edits stay legible when you put
them on screen. The divide-by-zero gap in beat 2 is intentional — it is the one
real bug seeded so the first change fixes something that visibly matters.
