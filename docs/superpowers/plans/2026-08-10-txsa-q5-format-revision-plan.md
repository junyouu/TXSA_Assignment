# TXSA Part A Q5 Format Revision Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Refine Chew Aik Yang's Q5 notebook into the same concise seven-cell markdown/code pattern used by Yeow Jun You while preserving correct CountVectorizer and NLTK output.

**Architecture:** Rebuild the executed notebook as four short markdown cells alternating with three code cells. An external validator will check structure, headings, execution, token counts and repository scope without placing visible testing material in the coursework notebook.

**Tech Stack:** Jupyter Notebook JSON, Python 3, scikit-learn, NLTK, nbformat and nbclient.

## Global Constraints

- Preserve the target filename exactly as `PartA_Q5(ChewAikYang.ipynb`.
- Follow `PartA_Q5(YeowJunYou).ipynb` for markdown order, heading style and explanation length.
- Keep detailed evaluation for the written report rather than the code notebook.
- Retain the exact group `Data_1` corpus.
- Save successful execution output in the notebook.
- Do not modify any other assignment notebook.

---

### Task 1: Establish the failing format test

**Files:**
- Verify: `PartA_Q5(ChewAikYang.ipynb`

**Interfaces:**
- Consumes: the current 17-cell notebook.
- Produces: a failing external validation result proving that the current notebook does not match the required seven-cell format.

- [ ] **Step 1: Write the external validator**

Create a temporary Python validator that asserts:

```python
assert len(notebook.cells) == 7
assert [cell.cell_type for cell in notebook.cells] == [
    'markdown', 'markdown', 'code', 'markdown', 'code', 'markdown', 'code'
]
assert len([cell for cell in notebook.cells if cell.cell_type == 'markdown']) == 4
```

It must also check the four approved headings and reject error outputs.

- [ ] **Step 2: Run it to verify RED**

Run the validator against the current notebook.

Expected: failure because the current notebook contains 17 cells and long report-style markdown.

### Task 2: Build the concise reference-matched notebook

**Files:**
- Modify: `PartA_Q5(ChewAikYang.ipynb`

**Interfaces:**
- Consumes: the exact corpus from `PartA_Q1Q2.ipynb` and the approved revision design.
- Produces: `countvectorizer_tokens: list[str]` and `nltk_tokens: list[str]` with concise comparison output.

- [ ] **Step 1: Create four concise markdown cells**

Use these headings in order:

```markdown
**Group Assignment - Part A: Practical Text Pre-Processing (Q5)**
**Environment Setup**
**Q5: Alternative Approach Implementation**
**Step 5.2: Compare and Contrast the Alternative Approach with Q1's Best Approach**
```

The third markdown cell must also contain `**Step 5.1: Alternative Tokenization using CountVectorizer**`. Each explanation is limited to one short paragraph.

- [ ] **Step 2: Create the setup code cell**

Import NLTK, `word_tokenize` and `CountVectorizer`; ensure `punkt` and `punkt_tab` are available; print one short setup confirmation.

- [ ] **Step 3: Create the CountVectorizer code cell**

Embed the exact corpus, create the default analyser, and print the 80 ordered tokens and their count.

- [ ] **Step 4: Create the comparison code cell**

Tokenise the same corpus with NLTK, print the NLTK and CountVectorizer counts, then show focused comparisons for capitalisation, punctuation and `open-class`.

- [ ] **Step 5: Execute to verify GREEN**

Execute all three code cells with nbclient and save the result back to the requested notebook.

Expected: execution counts `[1, 2, 3]`, no error output, CountVectorizer count 80 and NLTK count 94.

### Task 3: Validate and commit the revision

**Files:**
- Verify: `PartA_Q5(ChewAikYang.ipynb`
- Create: `docs/superpowers/plans/2026-08-10-txsa-q5-format-revision-plan.md`

**Interfaces:**
- Consumes: the executed seven-cell notebook.
- Produces: verified repository state and a local commit.

- [ ] **Step 1: Run the external validator**

Confirm exact cell order, four concise markdown cells, three executed code cells, zero errors, matching corpus and expected token-count output.

- [ ] **Step 2: Review repository scope**

Run `git status --short` and `git diff --stat`. Confirm no other assignment notebook changed.

- [ ] **Step 3: Commit the revision**

```bash
git add 'PartA_Q5(ChewAikYang.ipynb' docs/superpowers/plans/2026-08-10-txsa-q5-format-revision-plan.md
git commit -m "refactor: simplify individual TXSA Q5 notebook"
```
