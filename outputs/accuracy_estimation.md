# Accuracy estimation (expected performance)

**Model:** Tuned XGBoost with Bag-of-Words (5k, 1–2 grams) + engineered features (duplication_count, stopword_count, headline_length, word_count).
**Evaluation setup:** 80/20 stratified split on training data, duplicates removed to reduce leakage.
**Observed performance (held-out set):** Accuracy ≈ 0.9404, F1 ≈ 0.9420.
**Expected performance on testing file:** around 94% accuracy (if the evaluation data is similar).

**Notes:** If evaluation data contains duplicates/overlap with training, accuracy may be slightly higher; if the evaluation data is from a different distribution (domain shift), performance may be lower.