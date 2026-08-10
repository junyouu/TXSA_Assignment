# TXSA Part A Q5 CountVectorizer Design

## Objective

Populate `PartA_Q5(ChewAikYang.ipynb` with Chew Aik Yang's individual Q5 solution. The notebook will implement a common alternative tokenisation approach that is distinct from the other members' BERT WordPiece, spaCy, and Gensim solutions and from the group's `split()`, regular-expression, and NLTK methods.

## Selected Approach

Use scikit-learn's `CountVectorizer` analyser as the alternative tokenizer. This is a familiar text-analytics tool, requires no pretrained language model, and connects naturally to supervised text classification. Its default analysis pipeline lowercases text, selects word tokens, ignores punctuation, and produces a vocabulary suitable for document-term features.

## Notebook Structure

1. Title and rubric mapping for Q5's 3-mark implementation, 2-mark comparison, and 5-mark evaluation.
2. Environment setup using scikit-learn, NLTK, pandas, and regular expressions.
3. The exact `Data_1.txt` corpus embedded in the group Q1/Q2 notebook so the comparison uses identical evidence and does not depend on a machine-specific path.
4. `CountVectorizer` tokenisation with the complete ordered token output and token count.
5. Reproduction of the group's `split()`, regex, and NLTK tokenisation methods on the same corpus.
6. Evidence tables comparing token counts, case handling, punctuation handling, and the treatment of `open-class`.
7. A balanced discussion explaining where CountVectorizer is better, worse, or simply different, based only on observed output and intended use.
8. Executable assertions covering non-empty output, lowercase normalisation, punctuation removal, vocabulary construction, and consistency between the analyser tokens and vectorised feature counts.

## Data Flow

The embedded corpus is passed to `CountVectorizer.build_analyzer()` to obtain ordered tokens. The fitted vectorizer then converts the same corpus to a document-term matrix. The group methods process the identical corpus independently. Results are assembled into pandas tables for direct comparison, followed by interpretation grounded in those values.

## Error Handling and Reproducibility

- Download only NLTK's `punkt` and `punkt_tab` resources when required for the comparison baseline.
- Avoid absolute local paths and external datasets.
- Use deterministic text and parameters so rerunning the notebook produces the same tokens, counts, vocabulary, and tables.
- Keep the implementation self-contained in the requested notebook and do not change other members' files.

## Verification

- Validate the notebook JSON and cell order.
- Execute it from top to bottom in a clean temporary directory.
- Confirm every code cell completes without an exception and produces saved output.
- Confirm the assertions pass and the final comparison and conclusion cover all three Q5 marking components.
- Re-open the executed notebook and scan outputs for tracebacks or missing results.

## Scope

Only `PartA_Q5(ChewAikYang.ipynb` and the required design/plan documentation will be added or changed. No Part A group answers, Part B notebooks, datasets, or other members' Q5 files will be modified.
