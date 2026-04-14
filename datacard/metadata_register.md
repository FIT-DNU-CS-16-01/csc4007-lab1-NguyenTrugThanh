# Metadata Register — Verified / Estimated / To be measured

## Verified ✅
**Data Dimension & Distribution:**
- **N (total samples)**: 50,000 (source: `outputs/datacard_stats.json`)
- **Label distribution**: 25,000 negative (0) + 25,000 positive (1) → Perfectly balanced (imbalance_ratio = 1.0)
- **Label counts verified by**: `outputs/logs/audit_before.md` & `outputs/logs/audit_after.md`

**Text Length Statistics:**
- **Min chars**: 32
- **Median chars**: 954
- **95th percentile**: 3,328
- **Max chars**: 13,593
- (Source: `outputs/datacard_stats.json`)

**Data Quality — Before Preprocessing:**
- **HTML `<br>` tags**: 29,200 mẫu (58.4%) contain
- **Any HTML tags**: 29,202 mẫu (58.4%) contain
- **HTML entities**: 11 mẫu (0.022%) contain
- **Exact duplicates**: 824 mẫu (1.648%)
- (Source: `outputs/logs/audit_before.md`)

**Data Quality — After Preprocessing:**
- **HTML `<br>` tags removed**: ✓ 0 mẫu (100% clean)
- **Any HTML tags removed**: ✓ 0 mẫu (100% clean)
- **HTML entities remaining**: ⚠️ 11 mẫu (0.022%) still present
- **Exact duplicates**: ⚠️ 832 mẫu (1.664%) — *INCREASED by 8*
- (Source: `outputs/logs/audit_after.md`)

**Data Validation (Great Expectations):**
- **Total expectations evaluated**: 6
- **Passed**: 5 tests (83.33%)
- **Failed**: 1 test (16.67%)
- (Source: `outputs/ge/validation_summary.md`)

**Label Quality (Cleanlab):**
- **Suspected label issues**: 1,000 mẫu (2.0%)
- **Export top_k for review**: 200 mẫu (CSV ready)
- (Source: `outputs/logs/cleanlab_summary.md`)

**Data Splits Generated:**
- ✓ `outputs/splits/train.csv` — training set
- ✓ `outputs/splits/val.csv` — validation set
- ✓ `outputs/splits/test.csv` — test set

---

## Estimated 📊
**Expected Model Performance (Based on Data Quality):**
- **Baseline accuracy estimate**: 85-87% (given 2% label noise + 1.65% duplicates)
- **Confidence interval**: If clean, could reach 90%+

**Data Quality Issues Impact:**
- **HTML artifacts**: ~1-2% accuracy hit (residual 11 entities)
- **Exact duplicates**: ~1-2% inflated metrics (1.65% will artificially boost performance)
- **Label noise (2%)**: ~2-3% accuracy reduction

**Fairness/Bias Estimate:**
- **Estimated demographic bias**: Low risk (movie reviews assumed to be from diverse users)
- **Domain bias**: High risk (IMDB overrepresents movie enthusiasts; may not generalize to casual viewers)

**Estimated Remediation Effort:**
- **Fix HTML entities**: ~10 minutes (script: `html.unescape()`)
- **Deduplicate**: ~15 minutes (script: `drop_duplicates()` + rerun)
- **Manual label review (5 samples)**: ~30 minutes (read + decide KEEP/FIX/REMOVE)
- **Total**: ~1 hour

---

## To be measured ⏳
**Model Performance (Need to Train & Evaluate):**
- [ ] Train/test accuracy on current dataset
- [ ] Train/test accuracy AFTER fixes (dedup + HTML entity fix)
- [ ] Cross-validation F1-score
- [ ] Class-wise precision/recall (positive vs negative)

**Human Agreement & Label Quality:**
- [ ] Manual review of 5 samples from `cleanlab_label_issues.csv` → record KEEP/FIX/REMOVE decisions
- [ ] If FIXED: how many labels changed? (delta from original to corrected)
- [ ] Estimated human inter-rater agreement (if multiple annotators review same 5 samples)

**Data Leakage & Split Integrity:**
- [ ] Verify NO exact duplicates between train/val/test after deduplication
- [ ] Check for near-duplicates (fuzzy matching) across splits
- [ ] Confirm: Did preprocessing happen BEFORE or AFTER split? (critical for avoiding leakage)

**Great Expectations Failed Test:**
- [ ] **Which expectation failed?** (investigate `outputs/ge/expectation_suite.json`)
- [ ] **Why did it fail?** (check validation_result.json details)
- [ ] **Fix/adjust expectation or data?** (decision needed)

**Downstream Performance:**
- [ ] Real-world test: deploy model on fresh IMDB reviews → measure actual accuracy
- [ ] Bias audit: check if positive/negative predictions are balanced across demographics (if data available)
- [ ] Robustness: test on out-of-domain data (e.g., Amazon reviews, Yelp) → generalization

**Privacy & Security:**
- [ ] Scan for PII (emails, phone numbers, names) in review text
- [ ] Check if usernames/account IDs leaked in dataset
- [ ] Assess re-identification risk from free-text content
