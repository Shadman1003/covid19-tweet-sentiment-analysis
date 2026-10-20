# COVID-19 Tweet Sentiment Classification

A Python academic team project exploring classical NLP, text preprocessing and binary sentiment classification. The workflow compares a scikit-learn TF-IDF/logistic-regression baseline with a small NumPy implementation of logistic regression and includes an optional notebook prediction interface.

**Academic team:** Shadman Al Muksit, MD Tarek Hossen and Sariful Islam. The academic report lists these contributors; it does not establish separate individual implementation roles. This repository presents that team project, not a new research method or a peer-reviewed publication.

## Task and workflow

The target is **sentiment**, not misinformation, factual accuracy or medical advice:

- Positive and Extremely Positive map to `1`.
- Negative and Extremely Negative map to `0`.
- Neutral samples are excluded from the binary exercise.

The notebook loads two CSV files, combines them, constructs binary labels, fills missing location strings, combines location with tweet text, and removes URLs, mentions, digits, punctuation and English stop words. It removes empty texts and exact duplicates of `(clean_text, label)`, then creates stratified 70/15/15 training/validation/test partitions with fixed random seeds.

TF-IDF is fitted only on training text. The library baseline uses up to 5,000 unigram/bigram features and L2 logistic regression. The NumPy teaching implementation uses 600 unigram features with sigmoid activation, binary cross-entropy, L2 regularization and gradient descent. Additional cells explore vocabulary size and regularization and provide an `ipywidgets` input interface.

## Files

```text
notebooks/covid19_tweet_sentiment.ipynb  Clean publication notebook
requirements.txt                        Required Python libraries
.gitignore                              Excludes data and generated artifacts
data/README.md                          Data setup and rights information
```

No raw data, tweet examples, reports, screenshots, trained models or saved notebook outputs are included. The private academic source files remain separate.

## Data source and rights

Download `Corona_NLP_train.csv` and `Corona_NLP_test.csv` from the original [Coronavirus tweets NLP - Text Classification dataset page on Kaggle](https://www.kaggle.com/datasets/datatattle/covid-19-nlp-text-classification). Its public file listing confirms these two filenames. The source listing displayed **Data files © Original Authors** when checked on 20 October 2026; that label is not treated here as a general redistribution license.

Review the source terms and any applicable platform conditions before use. The dataset is not redistributed by this repository, and no additional license is asserted over it. No blanket project license has been selected; public access alone does not grant a separate reuse license for the team code.

The local academic archive used this file pair and sentiment schema. Exact equivalence to a currently downloaded dataset version has not been independently established by hashes. Downloaded versions may produce different counts or scores.

## Run in Google Colab

1. Open `notebooks/covid19_tweet_sentiment.ipynb` in Google Colab using its file-upload or GitHub notebook interface.
2. Install missing libraries if necessary with `pip install numpy pandas matplotlib scikit-learn ipywidgets`.
3. Run cells in order. At the upload prompt, select both CSV files. A second prompt appears only if one is still missing.
4. Review printed counts and metrics. The manual gradient-descent section can take longer than the library baseline.

## Run locally

A Python virtual environment is recommended. The original academic environment was not recorded, so `requirements.txt` lists dependencies without claiming an exact historical version lock.

```bash
python -m venv .venv
# Ubuntu / WSL / macOS
source .venv/bin/activate
# Windows PowerShell alternative:
# .venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m jupyterlab
```

Place the two downloaded CSVs in `data/`, open the notebook and run cells in order. Dataset lookup supports starting Jupyter from either the repository root or `notebooks/`. No Google account connection is required for local use. Do not commit downloaded data or newly generated notebook outputs containing source text or identifiers.

## Recorded academic results

The original notebook saved the following results. They are **historical outputs**, not experiments re-executed for this publication copy:

| Measure | Recorded value |
|---|---:|
| Combined raw observations | 44,955 |
| Binary observations before cleaning | 36,623 |
| Cleaned observations | 36,547 |
| New train / validation / test rows | 25,582 / 5,482 / 5,483 |
| TF-IDF/logistic baseline test accuracy | 0.8377 |
| TF-IDF/logistic baseline positive-class F1 | 0.8510 |
| Manual logistic model test accuracy | 0.6719 |
| Manual logistic model positive-class F1 | 0.7502 |

F1 above uses the positive class; it is not macro F1. The library/manual comparison changes the feature space as well as the implementation, so it does not isolate implementation quality alone. The clean notebook intentionally contains no saved outputs. Only static syntax and packaging checks were performed while preparing this repository; a full data/model rerun remains to be done in the reader's environment.

## Evaluation limitations

- The original benchmark training and test files were merged before creating a **new random split**. These numbers are not results on the benchmark's original held-out test set.
- The original regularization sweep calculates test F1 for multiple `C` values. If those scores inform model selection, the test set is no longer untouched. A stronger follow-up should tune on training/validation partitions and evaluate once on an independent final holdout.
- Splitting is stratified by label, not grouped by author or ordered by time. Near duplicates, author overlap, location effects and temporal/domain shift can affect generalization.
- Deduplication uses the cleaned-text/label pair; it does not resolve identical text with conflicting labels. English stop-word removal may also discard negation cues.
- Removing neutral tweets narrows the task to two polarities. The model does not detect misinformation, explain causes of sentiment or establish clinical/public-health validity.
- No external dataset validation, novel architecture, production deployment or research publication is claimed.

## Publication preparation

This copy derives from the original academic notebook. Publication edits remove outputs, execution counts, notebook/account metadata, raw-text previews, example sentences and a repeated UI cell. Small file-loading changes support local Jupyter as well as Colab; the modeling experiments are preserved, with their limitations stated explicitly. Repository cleanup and documentation were prepared with AI assistance and should be reviewed by the academic team.
