# Fake vs Real News Headlines — NLP Classifier

This repository contains my **NLP bootcamp project** (Ironhack Data Science & Machine Learning).
The goal is to build a model that classifies **news headlines** as:

- `0` = **Fake**
- `1` = **Real**

The final notebook also generates predictions for the provided test file, where almost all the labels are placeholders (e.g., `2`).

---

## Dataset

For this project I worked with two prepared files:

- `dataset/training_data.csv` — tab-separated: `label<TAB>headline`
- `dataset/testing_data.csv` — tab-separated: `label<TAB>headline` (may include placeholder labels)

**Training set size (raw):** 34,152 headlines
**Duplicates removed:** 1,946 duplicate headlines (to avoid leakage)
**Training set size (deduplicated):** 32,206 unique headlines

---

## Approach 

1. **EDA / signal discovery**
- Duplicate headlines
- Headline length (words and characters) statistics
- Stopword patterns

2. **Text preprocessing (hybrid)**
- Lowercasing, URL/email removal, punctuation cleanup
- Stopword removal **but keeping high-signal words**:
`not, no, never, only, just, very, again, even`
- POS-aware lemmatization (NLTK)

3. **Vectorization**
- Compared **Bag of Words (CountVectorizer)** vs **TF‑IDF**
- Same configuration: 5k features, (1,2)-grams, min_df=2, max_df=0.95

4. **Model development (3 phases)**
- **Phase 1:** baseline models (BoW only)
- **Phase 2:** BoW + engineered features:
`duplication_count`, `stopword_count`, `headline_length`, `word_count`
- **Phase 3:** hyperparameter tuning (RandomizedSearchCV) → final model selection

---

## Results (held-out test set, deduplicated)

Final winner: **Tuned XGBoost (BoW + engineered features)**

- **Accuracy:** ~0.94
- **Weighted F1-score:** ~0.94

(Exact values are printed in the notebook output.)

---

## Repository structure
.
├── main.ipynb # notebook with well-documented Python code that conducts the analysis  
├── datasets/   
│ ├── training_data.csv   
│ └── testing_data.csv  
├── figures/ # saved plots from the notebook  
├── outputs/ # csv summaries + prediction files + accuracy estimation file  
├── models/ # saved models  
├── requirements.txt  
└── README.md   
└── NLP_Project_Julia.pptx # presentation file, presenting the project including analysis  

## Deliverables

1. **Python Code:** main.ipynb
2. **Predictions:** outputs/testing_data_predictions.csv
3. **Accuracy estimation:** outputs/accuracy_estimation.md
4. **Presentation:** NLP_Project_Julia.pptx
