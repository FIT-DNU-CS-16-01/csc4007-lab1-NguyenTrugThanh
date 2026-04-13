# Audit AFTER preprocessing

## Schema / Missingness
- **n_rows**: 50000
- **missing_text_count**: 0
- **empty_text_count**: 0
- **missing_label_count**: 0
- **label_counts**: {0: 25000, 1: 25000}

## HTML tags / Entities
- **contains_br_tag_count**: 0
- **contains_any_html_tag_count**: 0
- **contains_html_entity_count**: 11

## Distribution / Length
- **imbalance_ratio_max_over_min**: 1.0
- **len_chars_min**: 32
- **len_chars_median**: 954
- **len_chars_p95**: 3328
- **len_chars_max**: 13593

## Duplicates / Near-duplicates
- **exact_dup_count**: 832
- **exact_dup_ratio**: 0.01664
- **near_dup_pairs_found_in_sample**: 0

## Leakage demo (TF-IDF fit all vs train-only)
- **vocab_size_bad_fit_all**: 20000
- **vocab_size_good_fit_train**: 20000
- **fix**: Split first. Fit preprocessing on train only; transform val/test.

