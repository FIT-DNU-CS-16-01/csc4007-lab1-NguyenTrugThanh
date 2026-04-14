# Great Expectations — Validation Summary
- evaluated_expectations: 6
- successful_expectations: 5
- unsuccessful_expectations: 1
- success_percent: 83.33333333333334

Nếu FAIL: ghi nguyên nhân và kế hoạch xử lý trong Data Card (Validation Types).

# Báo Cáo Phân Tích Vấn Đề Dữ Liệu - IMDB Dataset

Dựa trên output từ `python run_lab1.py --dataset imdb --seed 42 --use_great_expectations --use_cleanlab`, các vấn đề dữ liệu sau đây đã được phát hiện:

---

## Vấn Đề 1: HTML Tags và HTML Entities Trong Dữ Liệu

### Bằng Chứng Số Liệu
- **Contains `<br>` tags**: 29,200 mẫu (58.4% tổng dữ liệu)
- **Contains any HTML tags**: 29,202 mẫu (58.4% tổng dữ liệu)
- **Contains HTML entities**: 11 mẫu (0.022% tổng dữ liệu)
- **Trạng thái**: HTML tags vẫn tồn tại cả **trước và sau preprocessing**

```
BEFORE: contains_br_tag_count: 29200, contains_any_html_tag_count: 29202, contains_html_entity_count: 11
AFTER:  contains_br_tag_count: 0, contains_any_html_tag_count: 0, contains_html_entity_count: 11 ✓
```

### Vì Sao Vấn Đề Này Nguy Hiểm?

1. **Ảnh hưởng đến chất lượng feature**:
   - HTML tags như `<br>` được coi là tokens riêng biệt trong NLP, làm tăng dimensionality của vocabulary không cần thiết
   - Tỷ lệ 58.4% mẫu chứa HTML tags là rất lớn, tạo bias trong word embeddings

2. **Dẫn tới overfitting vào HTML patterns**:
   - Mô hình có thể học để phát hiện sentiment dựa trên sự hiện diện của `<br>` tags thay vì ngữ nghĩa thực của review
   - Khi deploy trên dữ liệu sạch (không có HTML), performance giảm đáng kể

3. **Leakage giữa train/test**:
   - Nếu một số mẫu trong training set có HTML tags nhưng test set không có (hoặc ngược lại), mô hình sẽ bị confuse

### Phương Hướng Xử Lý

1. **HTML tag removal** (Đã thực hiện sau preprocessing):
   - Sử dụng regex pattern: `re.sub(r'<[^>]+>', '', text)` để loại bỏ tất cả HTML tags
   - ✓ Kết quả: Số mẫu với `<br>` tags giảm từ 29,200 → 0

2. **HTML entity decoding** (Cần cải thiện):
   - Vẫn có 11 mẫu chứa HTML entities sau preprocessing
   - Sử dụng `html.unescape()` để decode: `&amp;` → `&`, `&nbsp;` → ` `, v.v.
   - Nên thêm vào bước preprocessing:
   ```python
   import html
   text = html.unescape(text)
   ```

3. **Kiểm tra chất lượng**:
   - Manual review 10-20 mẫu sau cleaning để đảm bảo logic removal không xóa text quan trọng
   - Validate vocabulary size không bị inflate bởi HTML tokens

---

## Vấn Đề 2: Bản Sao Chính Xác (Exact Duplicates)

### Bằng Chứng Số Liệu
- **Exact duplicates count**: 824 mẫu
- **Exact duplicates ratio**: 0.01648 (1.648% tổng dữ liệu)
- **Trạng thái**: Số lượng duplicates **tăng nhẹ** sau preprocessing
  ```
  BEFORE: exact_dup_count: 824, exact_dup_ratio: 0.01648
  AFTER:  exact_dup_count: 832, exact_dup_ratio: 0.01664 (+8 duplicates)
  ```

### Vì Sao Vấn Đề Này Nguy Hiểm?

1. **Data Leakage giữa train/validation/test**:
   - Nếu cùng một review chính xác xuất hiện ở cả training và test set, là leakage
   - Hiện tại, dữ liệu chưa được split khi phát hiện duplicates
   - Model sẽ "gian lận" bằng cách memorize review thay vì học pattern

2. **Inflated performance metrics**:
   - Khi test trên test set có duplicates từ training, accuracy/precision có thể cao 3-5% hơn reality
   - Nghĩa là performance thực tế khi deploy kém hơn đáng kể
   - Ví dụ: Test accuracy 92% nhưng thực tế chỉ 88% trên unseen data

3. **Không phản ánh generalization**:
   - Duplicates không giúp model học pattern mới
   - Gây lãng phí tài nguyên (CPU, memory, time) với dữ liệu redundant

### Phương Hướng Xử Lý

1. **Deduplication trước splitting**:
   - **Bước 1**: Identify exact duplicates: `df[df.duplicated(subset=['text'], keep=False)]`
   - **Bước 2**: Giữ lại 1 bản, xóa 824 bản copy
   - **Bước 3**: **Sau đó** mới chia train/val/test
   ```python
   # Remove duplicates BEFORE train/test split
   df_dedup = df.drop_duplicates(subset=['text'], keep='first')
   # Then split: train (67%), val (16%), test (17%)
   ```

2. **Thay vì**: Tách sau khi split (hiện tại):
   - ❌ Nếu bạn split trước: duplicates có thể nằm ở cả train và test
   - ✓ Đúng: Deduplicate trước, split sau

3. **Near-duplicate detection** (Optional):
   - Báo cáo cho thấy `near_dup_pairs_found_in_sample: 0` 
   - Nhưng nên kiểm tra lại với fuzzy matching để tránh near-duplicates (ví dụ: cùng review nhưng khác vài ký tự)

---

## Vấn Đề 3: Label Issues - Nhãn Sai Và Ambiguous

### Bằng Chứng Số Liệu
- **Suspected label issues count**: 1,000 mẫu
- **Suspected label issues ratio**: 0.0200 (2% tổng dữ liệu)
- **Export top_k for review**: 200 mẫu (được export vào `cleanlab_label_issues.csv`)

```
From cleanlab_summary.md:
- suspected_label_issues_count: 1000
- suspected_label_issues_ratio: 0.0200
- export_top_k: 200
```

### Vì Sao Vấn Đề Này Nguy Hiểm?

1. **Label noise giảm performance**:
   - 2% label noise tiêu chuẩn có thể giảm model accuracy 2-5% tùy thuộc vào model complexity
   - Ví dụ: Nếu expected accuracy là 90%, nhưng có 2% label noise, thực tế là ~87-88%
   - Càng phức tạp model, càng dễ overfit lên wrong labels

2. **Ambiguous labels - khó học**:
   - Một số reviews có thể là borderline (e.g., review trung lập nhưng được gán positive/negative)
   - Model sẽ confuse và không thể học consistent pattern
   - Các features từ ambiguous samples **trái chiều** với clear samples

3. **Deployment risk**:
   - Khi deploy, model sẽ predict không chính xác vì đã học từ wrong/ambiguous labels
   - Customer satisfaction giảm nếu sentiment predictions không chính xác

4. **Expensive to detect thủ công**:
   - Không thể manual review hết 1,000 mẫu → cần prioritize 200 mẫu top confidence từ Cleanlab

### Phương Hướng Xử Lý

1. **Manual review & correction** (Primary approach):
   ```
   Task (từ Cleanlab summary):
   "Student task: chọn 5 mẫu trong cleanlab_label_issues.csv để review 
   (giữ/sửa/ambiguous) và ghi vào Data Card."
   ```
   - Mở `outputs/logs/cleanlab_label_issues.csv` → xem top 200 mẫu flagged
   - Chọn 5-10 mẫu có confidence cao nhất (most likely wrong)
   - Quyết định: **KEEP** (correct), **FIX** (relabel), hoặc **REMOVE** (ambiguous)

2. **Stratified removal/relabeling**:
   - Nếu fix: Relabel với human judgment, rerun training
   - Nếu remove: Xóa các samples ambiguous, retrain với clean data
   - Nếu keep: Giữ nguyên nếu judge nó đúng

3. **Document decisions trong Data Card**:
   - Ghi rõ: mẫu số nào fix sang label nào, tại sao
   - Ghi rõ: mẫu nào remove, tại sao
   - Ghi impact: "Sau khi fix X label, test accuracy tăng từ 87.2% → 89.1%"

4. **Iterative improvement**:
   - Sau khi fix top issues, rerun `run_lab1.py` để detect new issues từ Cleanlab
   - Lặp lại đến khi `suspected_label_issues_ratio < 0.005 (0.5%)`

---

## Tóm Tắt & Hành Động Tiếp Theo

| Vấn Đề | Severity | Status | Action |
|--------|----------|--------|--------|
| HTML tags/entities | 🔴 HIGH | Partially Fixed | Thêm `html.unescape()`, validate |
| Exact duplicates (1.65%) | 🔴 HIGH | Pending | Deduplicate trước split, validate train-test disjoint |
| Label issues (2.0%) | 🟡 MEDIUM | Pending | Manual review 5-10 mẫu từ CSV, document decisions |

**Ưu tiên**: 
1. Dedupplication → Split → Retrain
2. Fix label issues via manual review → Retrain
3. Improve HTML entity decoding

---

## Tham Khảo Log Files
- `outputs/logs/audit_before.md` - Kiểm tra dữ liệu trước preprocessing
- `outputs/logs/audit_after.md` - Kiểm tra dữ liệu sau preprocessing  
- `outputs/logs/cleanlab_summary.md` - Label issues summary
- `outputs/logs/cleanlab_label_issues.csv` - Chi tiết top 200 mẫu có issues
- `outputs/ge/validation_summary.md` - Great Expectations validation results
