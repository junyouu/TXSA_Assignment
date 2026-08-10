# TXSA Part A Q5 CountVectorizer Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Produce an executed, self-contained Part A Q5 notebook for Chew Aik Yang using scikit-learn CountVectorizer as the alternative tokenisation method.

**Architecture:** The notebook embeds the exact group `Data_1` corpus, obtains ordered alternative tokens through `CountVectorizer.build_analyzer()`, reproduces the three Q1 baselines, and presents evidence tables and a balanced interpretation. One final assertion cell acts as the executable acceptance test for the observable tokenisation behaviour.

**Tech Stack:** Jupyter Notebook JSON, Python 3, scikit-learn, NLTK, pandas, nbformat, nbclient.

## Global Constraints

- Preserve the unusual target filename exactly as `PartA_Q5(ChewAikYang.ipynb`.
- Do not modify another member's notebook or any Part B file.
- Use the exact embedded `Data_1` corpus from `PartA_Q1Q2.ipynb`.
- Use British English and student-level academic explanation.
- Save executed outputs in the final notebook.
- Do not depend on machine-specific absolute paths or a pretrained model download.

---

### Task 1: Establish the failing notebook acceptance test

**Files:**
- Modify: `PartA_Q5(ChewAikYang.ipynb`

**Interfaces:**
- Consumes: the required observable behaviour from the approved design.
- Produces: a valid but intentionally failing notebook whose assertion cell references the not-yet-implemented `countvectorizer_tokens` value.

- [ ] **Step 1: Generate the RED notebook**

Create a minimal notebook containing the embedded corpus and this code cell after imports:

```python
assert len(countvectorizer_tokens) == 80
assert all(token == token.lower() for token in countvectorizer_tokens)
assert 'open' in countvectorizer_tokens and 'class' in countvectorizer_tokens
assert 'open-class' not in countvectorizer_tokens
```

- [ ] **Step 2: Execute it to verify RED**

Run the notebook with `jupyter nbconvert --execute --to notebook`.

Expected: execution fails with `NameError: name 'countvectorizer_tokens' is not defined`, proving that the acceptance test detects the missing alternative-tokenisation implementation.

### Task 2: Implement the complete rubric-aligned notebook

**Files:**
- Modify: `PartA_Q5(ChewAikYang.ipynb`

**Interfaces:**
- Consumes: the exact embedded corpus and Task 1 acceptance behaviour.
- Produces: `countvectorizer_tokens: list[str]`, `feature_names: list[str]`, `document_term_matrix`, and comparison DataFrames used by the discussion.

- [ ] **Step 1: Add environment and corpus cells**

Import `re`, `pandas`, `CountVectorizer`, and NLTK's `word_tokenize`; locate/download `punkt` and `punkt_tab` only if missing. Embed the exact group corpus and print it.

- [ ] **Step 2: Add CountVectorizer tokenisation**

```python
vectorizer = CountVectorizer()
analyzer = vectorizer.build_analyzer()
countvectorizer_tokens = analyzer(corpus_text)
document_term_matrix = vectorizer.fit_transform([corpus_text])
feature_names = vectorizer.get_feature_names_out().tolist()
```

Print the complete ordered tokens, token count, unique feature count, matrix shape, and a feature-frequency table sorted by decreasing frequency and then alphabetically.

- [ ] **Step 3: Add the Q1 comparison**

Reproduce `split()`, `re.findall(r'\b\w+\b', corpus_text)`, and `word_tokenize(corpus_text)`. Build a table with method, token count, lowercase normalisation, punctuation treatment, hyphen handling, and intended use. Add focused output for the first token, `input.`, `labels;`, and `open-class`.

- [ ] **Step 4: Add evidence-grounded evaluation**

Explain that CountVectorizer is better for a compact machine-learning feature pipeline, worse when punctuation/case/order or linguistic detail matters, and different because it combines tokenisation, normalisation, vocabulary construction, and numerical feature extraction. Tie every claim to displayed outputs.

- [ ] **Step 5: Make the acceptance test pass**

Retain Task 1's assertions and add checks that the document-term matrix has one row, its column count equals `len(feature_names)`, and its summed counts equal `len(countvectorizer_tokens)`.

- [ ] **Step 6: Execute to verify GREEN**

Run the notebook from top to bottom.

Expected: exit code 0, all assertions pass, and every code cell has an execution count and output where appropriate.

### Task 3: Validate the notebook artifact and repository scope

**Files:**
- Verify: `PartA_Q5(ChewAikYang.ipynb`

**Interfaces:**
- Consumes: the executed notebook from Task 2.
- Produces: verification evidence for JSON validity, execution completeness, rubric coverage, and limited repository changes.

- [ ] **Step 1: Validate structure and outputs**

Use a Python/nbformat validation script to assert:

```python
assert notebook.nbformat == 4
assert not any(output.output_type == 'error' for cell in notebook.cells if cell.cell_type == 'code' for output in cell.get('outputs', []))
assert all(cell.execution_count is not None for cell in notebook.cells if cell.cell_type == 'code')
```

- [ ] **Step 2: Check rubric coverage**

Confirm the notebook contains explicit sections for implementation (3 marks), comparison (2 marks), and better/worse/different evaluation (5 marks), plus visible code outputs.

- [ ] **Step 3: Review the git diff**

Run `git status --short` and `git diff --stat`. Confirm no assignment notebook other than the requested Q5 file changed.

- [ ] **Step 4: Commit the implementation**

Stage the notebook and plan document, then commit with:

```bash
git commit -m "feat: complete individual TXSA Part A Q5"
```
