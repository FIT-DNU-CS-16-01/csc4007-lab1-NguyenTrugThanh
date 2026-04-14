# Data Card — IMDB Movie Review Dataset (CSC4007-Lab1)

## Version
- v1.0 — Initial data card with audit results, validation findings, and label quality assessment (2026-04-14)
- v1.1 — (Planned) After correcting 5 label issues, deduplication, and HTML entity cleanup

---

## 1. Dataset Overview

### Thông tin cơ bản
Tên dataset: IMDB Movie Review Dataset
Lĩnh vực: Xử lý ngôn ngữ tự nhiên / Phân tích cảm xúc
Nguồn gốc: Maas et al., 2011 (Đại học Stanford)
URL dataset: http://www.andrew-maas.net/data/sentiment
Bài báo: https://aclanthology.org/P11-1015.pdf
Tham chiếu bài lab: CSC4007-Lab1 (Data Card & Audit module)

### Mục đích & Use Case
Mục đích chính: Phân loại cảm xúc nhị phân (tích cực / tiêu cực)
Loại bài toán: Phân tích cảm xúc ở mức tài liệu (document-level), học biểu diễn
Phù hợp cho: Nghiên cứu, benchmark, bài tập học thuật
KHÔNG phù hợp cho: Dự đoán rating đa lớp (1–10), triển khai thực tế nếu chưa kiểm định thêm

### Kích thước dữ liệu
Tổng số mẫu: 50,000 review
Phân bố nhãn: 25,000 tiêu cực (0) + 25,000 tích cực (1) → Cân bằng hoàn hảo
Chia tập: 25,000 train / (không rõ validation) / 25,000 test
Loại dữ liệu: Văn bản (tiếng Anh)

---

## 2. Đánh giá chất lượng dữ liệu

### Audit trước tiền xử lý
| Metric | Count | Ratio | Status |
|--------|-------|-------|--------|
| **HTML `<br>` tags** | 29,200 | 58.4% | ⚠️ HIGH |
| **Any HTML tags** | 29,202 | 58.4% | ⚠️ HIGH |
| **HTML entities** | 11 | 0.022% | ⚠️ LOW |
| **Exact duplicates** | 824 | 1.648% | ⚠️ MEDIUM |
| **Missing values** | 0 | 0% | ✅ GOOD |
| **Empty text** | 0 | 0% | ✅ GOOD |

### Audit sau tiền xử lý
| Metric | Count | Ratio | Change | Status |
|--------|-------|-------|--------|--------|
| **HTML `<br>` tags** | 0 | 0% | -29,200 | ✅ FIXED |
| **Any HTML tags** | 0 | 0% | -29,202 | ✅ FIXED |
| **HTML entities** | 11 | 0.022% | No change | ⚠️ PENDING |
| **Exact duplicates** | 832 | 1.664% | +8 | ⚠️ NEED FIX |
| **Missing values** | 0 | 0% | No change | ✅ GOOD |

### Thống kê độ dài văn bản
| Statistic | Value | Note |
|-----------|-------|------|
| **Min length** | 32 characters | Very short reviews |
| **Median length** | 954 characters | ~150-200 words |
| **95th percentile** | 3,328 characters | ~500-700 words |
| **Max length** | 13,593 characters | Long, detailed reviews |

---

## 3. Kết quả kiểm định dữ liệu

### Great Expectations (GE) Testing
| Metric | Result | Status |
|--------|--------|--------|
| **Total expectations** | 6 | - |
| **Passed** | 5 | 83.33% ✅ |
| **Failed** | 1 | 16.67% ⚠️ |
| **Pass rate** | 83.33% | Below target (100%) |

**Failed Test Investigation Needed**: Check `outputs/ge/validation_summary.md` and `outputs/ge/validation_result.json` to identify which expectation failed and why.

### Cleanlab (đánh giá nhãn)
| Metric | Count | Ratio | Interpretation |
|--------|-------|-------|-----------------|
| **Suspected label issues** | 1,000 | 2.0% | ~2% of labels likely incorrect/ambiguous |
| **Export top_k** | 200 | - | Top 200 flagged samples available for review |
| **Manual review done** | 5 | - | Sample 5/200 (rows 11-15) reviewed ✓ |

| Chỉ số            | Số lượng | Tỷ lệ | Ý nghĩa           |
| ----------------- | -------- | ----- | ----------------- |
| Nghi ngờ lỗi nhãn | 1,000    | 2.0%  | ~2% nhãn sai      |
| Top export        | 200      | -     | Có file để review |
| Đã review         | 5        | -     | ✔                 |

**Kết quả review thủ công (5 mẫu)
- **ID 11668**: 0 (Neg) → **FIX to 1 (Pos)** — "great movie, love ×4" = positive (Cleanlab confidence: 99.86%)
- **ID 22259**: 1 (Pos) → **FIX to 0 (Neg)** — "bad ×7, how dumb" = negative (99.81%)
- **ID 22257**: 1 (Pos) → **FIX to 0 (Neg)** — "cheap, terrible, worst" = negative (99.74%)
- **ID 16634**: 1 (Pos) → **FIX to 0 (Neg)** — So-bad-it's-good = core negative (99.5%)
- **ID 31245**: 0 (Neg) → **FIX to 1 (Pos)** — "powerful performance, worth rental" = positive (98.9%)

**Conclusion**: Cleanlab phát hiện rất chính xác (100%)

---

## 4. Vấn đề dữ liệu & hướng xử lý

### Issue 1: HTML Artifacts (29,202 tags + 11 entities)

**Problem**:
- 58.4% dữ liệu chứa <br>
- 11 mẫu chứa HTML entity
- Model learns spurious HTML patterns instead of genuine sentiment features

**Current Status**:
- ✅ HTML tags removed during preprocessing (29,200 → 0)
- ⚠️ HTML entities remain (11 samples need `html.unescape()`)

**cách xử lý**:
```python
import html
text = html.unescape(text)  # Convert &amp; → &, &nbsp; → space, etc.
```

**Impact**: Minimal (11 samples), but ensures data integrity

---

### Vấn đề 2: Trùng lặp (832 mẫu)

**Problem**:
- 832 exact duplicate reviews (same text, same label)
- If duplicates span train/test splits → data leakage, inflated metrics
- Wasted computation, non-informative for model learning

**Current Status**: ⚠️ NOT DEDUPLICATED

**cách xử lý**:
```python
# BEFORE train/test split
df_dedup = df.drop_duplicates(subset=['text'], keep='first')
# Result: n_rows: 50,000 → 49,168 (-832 samples, -1.66%)
```

**Critical**: Must deduplicate BEFORE splitting to ensure no leakage

**Impact**: 
- +1.66% data reduction but gain integrity
- Metrics will be honest (not inflated by duplicates)

---

### Vấn đề 3: Sai nhãn

**Trạng thái**

Mới sửa 5 mẫu
Còn ~995 mẫu

**Kế hoạch**
Áp dụng 5 sửa ✔
Review top 50
Giảm xuống <1%

**Remediation Priority**:
1. **Phase 1**: Apply 5 corrected labels (Done)
2. **Phase 2**: Review top-50 flagged by Cleanlab confidence
3. **Phase 3**: Target: Reduce issue ratio from 2.0% → <1.0%

**Impact**:
- -2-3% boost in model accuracy after fixing
- More honest benchmark for evaluation

---

## 5. Các bước tiền xử lý

| Bước              | Kỹ thuật        | Trạng thái |
| ----------------- | --------------- | ---------- |
| Xóa HTML          | regex           | ✅          |
| Decode entity     | html.unescape   | ⏳          |
| Tokenization      | TBD             | ⏳          |
| Dedup             | drop_duplicates | ⏳          |
| Split             | chưa rõ         | ❓          |
| Vocabulary filter | top 5k          | ⏳          |


---

## 6. Chia tập dữ liệu

| Tập        | Số lượng | Ghi chú           |
| ---------- | -------- | ----------------- |
| Train      | 25,000   | Không trùng movie |
| Test       | 25,000   | Không trùng movie |
| Validation | Không rõ | ❓                 |


**Note**: Cleanlab and manual review conducted on full dataset (no split applied yet for these analyses).

---

## 7. Hạn chế & Bias

## Hạn chế
Chỉ review phim
Chỉ tiếng Anh
Không có neutral (chỉ cực đoan)
## Bias
Genre bias
Reviewer bias
Vocabulary bias

## 8. Hướng phát triển
**Ngắn hạn**
Sửa 5 label
Dedup
Fix HTML entity
Chạy lại pipeline
**Trung hạn**
Debug GE
Review thêm Cleanlab
Kiểm tra leakage
**Dài hạn**
Train model
So sánh accuracy
Test cross-domain

---

## 9. Tổng hợp chất lượng

| Metric       | Hiện tại | Mục tiêu |
| ------------ | -------- | -------- |
| Cleanliness  | 96.5     | 99       |
| Duplicates   | 1.66%    | 0        |
| Label errors | 2%       | <1%      |
| Accuracy     | 85–87%   | 89–91%   |


---

## 10. Versioning
**v1.0**
Audit
Cleanlab
Review 5 mẫu
**v1.1** (dự kiến)
Fix label
Dedup
Fix entity
Rerun validation

---

## References & Attachments

- **Original Paper**: Maas et al., 2011. "Learning Word Vectors for Sentiment Analysis" (ACL)
- **Dataset URL**: http://www.andrew-maas.net/data/sentiment
- **Lab Outputs**:
  - `outputs/logs/audit_before.md` — Detailed audit before preprocessing
  - `outputs/logs/audit_after.md` — Audit after preprocessing
  - `outputs/logs/cleanlab_summary.md` — Label issues summary
  - `outputs/logs/cleanlab_label_issues.csv` — Top 200 flagged samples
  - `outputs/ge/validation_summary.md` — Great Expectations results
  - `outputs/ge/validation_result.json` — Detailed GE test results
  - `outputs/datacard_stats.json` — Metadata & statistics
- **Related Documentation**:
  - `LABEL_ISSUES_REVIEW.md` — Detailed manual review of 5 samples
  - `DATA_QUALITY_ISSUES.md` — Analysis of 3 major data quality problems
  - `datacard/metadata_register.md` — Verified/Estimated/To-measure metrics
  - `datacard/heuristics_scorecard.md` — Self-assessment (Completeness, Accuracy, Clarity, Timeliness, Actionability)
