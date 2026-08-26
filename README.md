# demo-kit-calc — browser calculator (no-IDE track)

A hands-on exercise kit for teaching AI-assisted development to people **without
an IDE, compiler, or toolchain** — leaders, PMs, analysts. Everything is one
self-contained `index.html`. The agent edits the file; the participant refreshes
a browser tab to see the result.

No build. No dependencies. No install.

## What's in here

| File | Purpose |
|---|---|
| `index.html` | The starter calculator — HTML, CSS and ~60 lines of plain JS, all in one file. |
| `PROMPTS.md` | The facilitator script: setup, the tripwire checklist, 7 prompt "beats", troubleshooting table. |
| `README.md` | This file. |

## Quick start

```bash
cd demo-kit-calc
codex          # or: claude — any agent CLI, in this folder
```

Then open `index.html` in a browser (double-click it, or drag it into a tab).
Keep terminal and browser side by side. The loop is:

**ask the agent → refresh the page (Ctrl+R / Cmd+R) → run the tripwire.**

## The tripwire

The safety net for people who don't write unit tests. Re-run after **every**
change:

```
1. 2 + 2 =        -> 4
2. 7 x 8 =        -> 56
3. 9 - 4 - 1 =    -> 4
4. C              -> clears to 0
5. 5 . 5 + 1 =    -> 6.5
```

Same idea as a regression test suite — done by hand, in ten seconds.

## The exercise

Seven beats, given one at a time, each a single prompt pasted into the agent.
Full text in [PROMPTS.md](PROMPTS.md):

1. **Understand it first** — read-only explanation of the code.
2. **Fix a real bug** — divide by zero shows `Infinity`; make it say "Cannot divide by 0".
3. **Keyboard support** — digits, operators, Enter, Escape.
4. **Backspace** — button plus the Backspace key.
5. **Percent key** — `50` then `%` shows `0.5`.
6. **Running history** — last five completed calculations.
7. **Dark mode toggle** (optional) — persisted across refresh.

## How the starter works

State is three plain variables, deliberately readable so the agent's edits stay
legible on a shared screen:

- `current` — the string on the display
- `previous` — the stored left-hand operand
- `operator` — `"+"`, `"-"`, `"*"`, `"/"`
- `justEvaluated` — flag so the next digit starts a fresh number

`inputNumber()` appends digits, `chooseOperator()` stores the operand,
`compute()` does the arithmetic, `clearAll()` resets. One click listener on
`.keys` dispatches by `data-num` / `data-op` / `data-action`.

The divide-by-zero gap in `compute()` is **intentional** — it's the one real bug
seeded so beat 2 fixes something that visibly matters.

## Facilitator notes

- Participants type no code. That's the point.
- If a change doesn't appear: they forgot to refresh. Hard refresh is Ctrl+Shift+R.
- If the page goes blank: "undo your last change, the page is blank."
- If the agent rewrote the whole file: fine, as long as the tripwire passes.
- Full troubleshooting table at the end of [PROMPTS.md](PROMPTS.md).

## Resetting between sessions

```bash
git checkout index.html
```
