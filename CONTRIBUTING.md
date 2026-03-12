# Contributing to ML Mastery

Thank you for wanting to improve this repo. Here is everything you need to know.

---

## What contributions are welcome

- Fixing errors in math explanations or code
- Adding clearer diagrams or visualizations
- Improving existing notebook explanations
- Adding new exercises with solutions
- Fixing typos or broken code cells
- Translating notebook comments (keep code in English)

---

## What to follow before submitting

### Notebook standards

Every notebook must follow this structure in order:

1. **Header cell** — Title, one-line description, Open in Colab badge
2. **Concept overview** — Plain English, no jargon, 3-5 sentences max
3. **Math intuition** — Full derivation with LaTeX. Include cost function, key equations, and step-by-step derivation
4. **Visual intuition** — At least one matplotlib plot built from scratch
5. **Code from scratch** — NumPy only implementation
6. **Sklearn implementation** — Production code with all key parameters explained
7. **Common mistakes** — At least 3 real gotchas with code examples
8. **Exercises** — At least 3 tasks, solutions in a collapsed cell

### Code style

- All code must run top to bottom without errors
- Every code cell must have a markdown cell above it explaining what it does
- Print outputs must be visible — do not clear outputs before committing
- Variable names must be descriptive (`X_train`, not `a` or `data1`)
- No magic numbers — define constants at the top of the cell

### Math style

- Use LaTeX in markdown cells for all equations: `$equation$` for inline, `$$equation$$` for block
- Always explain what each variable in an equation represents
- Derive from first principles — do not just state the final formula

---

## How to submit

1. Fork this repo
2. Create a branch: `git checkout -b fix/numpy-broadcasting-example`
3. Make your changes
4. Run all cells top to bottom and verify no errors
5. Open a pull request with a clear description of what you changed and why

---

## Branch naming

| Type | Format | Example |
|---|---|---|
| Bug fix | `fix/description` | `fix/logistic-regression-cost-formula` |
| New content | `add/description` | `add/svm-kernel-examples` |
| Improvement | `improve/description` | `improve/pandas-groupby-section` |

---

## Questions

Open an issue with the label `question` and someone will respond.
