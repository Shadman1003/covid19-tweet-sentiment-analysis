# Local data setup

Download `Corona_NLP_train.csv` and `Corona_NLP_test.csv` from the [original Kaggle dataset page](https://www.kaggle.com/datasets/datatattle/covid-19-nlp-text-classification) after reviewing the source terms. Place both files here for local Jupyter, or upload them into the Colab session when prompted.

The source listing displays “Data files © Original Authors”; no general redistribution license is assumed. This repository excludes data files, source text, location/account identifiers and derivative data exports. `.gitignore` is a convenience, not permission to redistribute the original data. Do not commit new notebook outputs containing source records.

Expected columns include `Location`, `OriginalTweet`, and `Sentiment`. The notebook fills missing location strings; it does not invent missing sentiment labels. Labels are existing sentiment annotations, not misinformation annotations.

