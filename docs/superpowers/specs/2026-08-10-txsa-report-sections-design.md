# TXSA Personal Report Sections Design

## Objective

Prepare three evidence-led report sections of approximately 500 words each for Chew Aik Yang's assigned work: Part A Question 4, Part A Question 5, and Part B Question 2. Each section will identify the exact notebook cells to capture and will follow the sequence code screenshot, code explanation, output screenshot, and output interpretation.

## Source Basis

- Assignment brief and marking scheme supplied by the user.
- `PartA_Q4.ipynb` for bigram sentence-probability modelling.
- `PartA_Q5(ChewAikYang.ipynb` for CountVectorizer tokenisation and comparison with NLTK.
- `PartB_WELFake_EDA_and_Preparation.ipynb` and `PartB_WELFake_Classification_and_Tuning.ipynb` for supervised text classification.
- `WELFake_Dataset.csv` as the Part B dataset.
- `TXSA Group Assignment Report.docx` as the existing report structure.

## Report Structure

Each assigned question will contain approximately 500 words in natural British undergraduate English. Figure captions will identify the method or result without repeating the paragraph. Code descriptions will remain concise, while output discussions will explain what the results mean and how they satisfy the question.

### Part A Question 4

Use screenshots showing the corrected training-corpus preparation, MLE and Laplace model construction, the probability-calculation loop, the per-bigram probability table, and the final sentence probabilities. The target sentence must not appear in the training corpus. The explanation will distinguish direct maximum-likelihood estimation from add-one smoothing and interpret why their probabilities differ.

### Part A Question 5

Use the CountVectorizer implementation and token output, followed by the comparison code and output against NLTK `word_tokenize()`. The explanation will make clear that CountVectorizer is the alternative method and NLTK is used only as the Q1 comparison baseline. It will discuss lowercasing, punctuation handling, token-count differences, and suitability for machine-learning feature construction.

### Part B Question 2

Use screenshots covering the stratified train-test split, TF-IDF vectorisation, and the implementation of Multinomial Naive Bayes, Logistic Regression, Linear SVM, and Decision Tree. A combined baseline-results table or chart will serve as the main output screenshot. Discussion will focus on successful implementation and the comparative behaviour of the four classifiers without duplicating the detailed evaluation required by Part B Question 4.

## Verification and Data Integrity

- Correct Q4 so only the three supplied training sentences are used, then rerun all cells.
- Generate `WELFake_processed.csv` from the EDA notebook if it does not exist.
- Run Part B Q2 and preserve genuine outputs before any result-specific prose is drafted.
- Reconcile any class-balance wording with the actual processed class counts.
- Check all screenshot instructions against visible notebook cell content and saved outputs.
- Keep the combined contribution near 1,500 words to respect the 4,000-word group limit.

## Deliverable

Provide the user with three ready-to-paste report sections, approximate word counts, exact screenshot boundaries, and suggested figure captions. The Word document itself will not be edited unless the user separately requests insertion.
