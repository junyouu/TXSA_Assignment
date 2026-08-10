# TXSA Personal Report Sections Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Produce three verified, approximately 500-word, screenshot-led report sections for Part A Q4, Part A Q5, and Part B Q2.

**Architecture:** Correct and execute the source notebooks before drafting result-specific prose. Treat notebook cells and saved outputs as the evidence layer, then create one report-draft file that maps each paragraph to an exact screenshot boundary and caption.

**Tech Stack:** Jupyter Notebook, Python, NLTK, scikit-learn, pandas, matplotlib, seaborn, Markdown, DOCX source review.

## Global Constraints

- Use natural British undergraduate English.
- Keep each assigned question between 450 and 550 words, with a combined target near 1,500 words.
- Follow the sequence code screenshot, code explanation, output screenshot, and output explanation.
- CountVectorizer is the Part A Q5 alternative method; NLTK is only the Q1 comparison baseline.
- Do not report Part B metrics until genuine notebook outputs have been generated.
- Do not duplicate detailed Part B Q4 evaluation inside the Part B Q2 implementation section.

---

### Task 1: Correct and verify Part A Q4

**Files:**
- Modify: `PartA_Q4.ipynb`

**Interfaces:**
- Consumes: `Data_3.txt`, containing three training sentences followed by a target sentence.
- Produces: a notebook with exactly three training sentences and verified MLE and Laplace outputs.

- [ ] **Step 1: Record the current failure condition**

Run a notebook-structure check that extracts the saved training-corpus output and confirms that four sentences are currently present. The fourth sentence, `<s> I read a book by Danielle </s>`, is the target and must not be training data.

- [ ] **Step 2: Correct corpus extraction and NLTK padding**

Replace the Q4 corpus-preparation logic with the following behaviour:

```python
training_block = raw_text.split('Calculate sentence probability', 1)[0]
corpus = [
    line.strip()
    for line in training_block.splitlines()
    if line.strip().startswith('<s>')
]

# The file already shows boundary markers for readability. Remove them before
# padded_everygram_pipeline adds one boundary pair during model preparation.
tokenized_text = [sentence.split()[1:-1] for sentence in corpus]
```

Update the neighbouring Markdown so it explains that the displayed markers are removed before NLTK adds its own padding.

- [ ] **Step 3: Execute Q4 from a clean kernel**

Run all cells in order from the repository directory so `Data_3.txt` resolves correctly. Save the successful cell outputs in `PartA_Q4.ipynb`.

- [ ] **Step 4: Verify Q4 invariants**

Confirm all of the following:

```text
Training sentence count: 3
Target bigram count: 7
MLE probability: 0.07407407407407407
Laplace probability: 5.784626775880419e-06
No error outputs
```

- [ ] **Step 5: Commit the Q4 correction**

```bash
git add PartA_Q4.ipynb
git commit -m "fix: exclude Q4 target from language model training"
```

---

### Task 2: Generate verified Part B Q2 baseline outputs

**Files:**
- Modify: `PartB_WELFake_Classification_and_Tuning.ipynb`
- Read/execute: `PartB_WELFake_EDA_and_Preparation.ipynb`
- Read: `/Users/jeffrey1108/Downloads/WELFake_Dataset.csv`
- Generate temporarily: `WELFake_processed.csv`

**Interfaces:**
- Consumes: raw WELFake CSV and the EDA notebook's cleaning, partial undersampling, and `final_text` construction.
- Produces: train/test and TF-IDF outputs plus four trained baseline classifiers and a combined baseline comparison.

- [ ] **Step 1: Generate the processed dataset using the existing EDA logic**

Execute the EDA notebook in a temporary working directory containing the raw dataset. Verify that the generated file has these columns:

```text
final_text
label
```

Confirm the processed class counts match the EDA output and retain the existing approximately 52:48 partial-undersampling design.

- [ ] **Step 2: Correct inaccurate class-balance wording**

Change claims such as `exact 50/50 class balance` in the classification notebook to `approximately 52:48 class balance after partial undersampling`. Do not alter the sampling algorithm.

- [ ] **Step 3: Execute only the Part B Q2 baseline scope**

Run cells through the baseline comparison, including:

```text
train/test split
TfidfVectorizer(max_features=5000, ngram_range=(1, 2), sublinear_tf=True)
MultinomialNB
LogisticRegression
LinearSVC
DecisionTreeClassifier
baseline results table and chart
```

Save the executed outputs for cells 5, 6, 8, 12, 14, 16, 18, and 20 in `PartB_WELFake_Classification_and_Tuning.ipynb`. Leave hyperparameter-tuning cells outside this task unchanged.

- [ ] **Step 4: Verify Part B outputs**

Check that the notebook contains no error outputs, all four result keys are present, the train/test split is stratified, the TF-IDF vocabulary contains at most 5,000 features, and each metric lies between 0 and 1.

- [ ] **Step 5: Commit the Part B evidence update**

```bash
git add PartB_WELFake_Classification_and_Tuning.ipynb
git commit -m "fix: save verified Part B baseline outputs"
```

---

### Task 3: Draft the three report sections and screenshot map

**Files:**
- Create: `docs/report-drafts/txsa-chew-aik-yang-report-sections.md`

**Interfaces:**
- Consumes: verified notebook code, saved outputs, assignment marking requirements, and current Word-report structure.
- Produces: three ready-to-paste report sections with cell-specific screenshot instructions and captions.

- [ ] **Step 1: Draft Part A Q4**

Write 450-550 words covering the corrected three-sentence training corpus, bigram MLE, add-one Laplace smoothing, the probability multiplication loop, and the verified final results. Mark the screenshot boundaries for the model/calculation code and the per-bigram/final outputs.

- [ ] **Step 2: Draft Part A Q5**

Write 450-550 words covering CountVectorizer Cell 5 and comparison Cell 7. Explain lowercasing, punctuation removal, the 80-token CountVectorizer output, the 94-token NLTK output, and why CountVectorizer is convenient for later machine-learning vectorisation while NLTK retains more linguistic detail.

- [ ] **Step 3: Draft Part B Q2**

Write 450-550 words covering stratified splitting, TF-IDF, and all four baseline classifiers. Use the genuine baseline table or chart for implementation-level interpretation and reserve detailed model-selection judgement for Part B Q4.

- [ ] **Step 4: Add screenshot instructions and captions**

For every screenshot, provide:

```text
Notebook filename
Exact cell number or visible start/end line
Whether to capture code or output
Suggested figure caption
Cropping guidance
```

- [ ] **Step 5: Verify word counts and evidence alignment**

Run a word-count check for each prose section. Confirm every numerical statement appears in a saved notebook output and every requested assignment component is addressed.

- [ ] **Step 6: Commit the report draft**

```bash
git add docs/report-drafts/txsa-chew-aik-yang-report-sections.md
git commit -m "docs: draft TXSA personal report sections"
```

---

### Task 4: Final quality check and user handoff

**Files:**
- Verify: `PartA_Q4.ipynb`
- Verify: `PartA_Q5(ChewAikYang.ipynb`
- Verify: `PartB_WELFake_Classification_and_Tuning.ipynb`
- Verify: `docs/report-drafts/txsa-chew-aik-yang-report-sections.md`

**Interfaces:**
- Consumes: all corrected notebooks and report prose.
- Produces: a concise handoff containing ready-to-paste explanations and exact screenshot guidance.

- [ ] **Step 1: Run notebook structural validation**

Parse all three notebooks as JSON and confirm that the required screenshot cells exist and have saved outputs.

- [ ] **Step 2: Review against the assignment brief**

Confirm Q4 implements both unsmoothed and smoothed bigram models, Q5 implements and compares an alternative tokeniser, and Part B Q2 includes at least four supervised text-classification techniques.

- [ ] **Step 3: Deliver the report package**

Provide the three sections, approximate word counts, screenshot positions, and any placement note needed for the existing Word report. State that the Word file itself was not edited.
