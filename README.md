# Cursor model benchmark: tip calculator

MLH Global Hack Week: Builders Week, Challenge 2: Benchmark Cursor's Models.

One prompt, three models. Each run was a separate Cursor cloud agent in Cursor Origin, started from scratch and told not to look at the other folders.

**Live comparison:** https://eugenedraitsev.github.io/mlh-ghw-cursor-model-benchmark/

## Prompt

> Build a simple tip calculator as a single self-contained HTML page (inline CSS + JS, no dependencies). Inputs: bill amount, tip percent with quick buttons 10/15/20/25%, number of people. Show tip amount, total and per-person total, updating live. Clean, modern, mobile-friendly, with a dark mode toggle. Save it as `<model>/index.html` and commit it to main.

## Results

Test input: bill 100, tip 20%, 4 people. Expected $20.00 tip, $120.00 total, $30.00 per person. All three got it right.

| Model | Folder | Size | Time | Self-testing |
|---|---|---|---|---|
| Composer 2.5 Fast | [`composer-2.5/`](composer-2.5/index.html) | 438 lines | under a minute | none reported |
| Grok 4.7 High Fast | [`grok-4.7/`](grok-4.7/index.html) | 613 lines | a few minutes | checked in Chrome at desktop, 375px and 320px widths |
| Grok 4.6 High Fast | [`grok-4.6/`](grok-4.6/index.html) | 482 lines | about 2 minutes | 23/23 automated browser checks |

## Pros and cons

**Composer 2.5 Fast**
- Pros: by far the fastest turnaround; compact code; helpful hint text under the inputs; dark mode remembers your choice and follows the system setting.
- Cons: no testing of its own before committing; fewest extras (plain number field for people, no +/− buttons).

**Grok 4.7 High Fast**
- Pros: the most careful run; it tested live updates, the quick buttons, split math and dark mode, and checked the layout on phone widths; the clearest labels and helper copy, plus +/− buttons for the number of people.
- Cons: the largest file; the slowest of the three.

**Grok 4.6 High Fast**
- Pros: wrote and ran 23 browser checks (live updates, all four tip buttons, custom percent, people steppers, invalid input, dark mode, 390px layout); caught and fixed its own bug (the people +/− buttons did not match their CSS selector) and rebased cleanly when `main` moved.
- Cons: needed a fix-up pass before it passed its own checks.

**Takeaway:** Composer 2.5 is the pick for quick scaffolding. Grok 4.7 and 4.6 take longer but verify their own work, which matters more as the app grows.
