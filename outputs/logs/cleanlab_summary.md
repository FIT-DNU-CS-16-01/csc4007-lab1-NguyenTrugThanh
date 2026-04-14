# Cleanlab — Label Issues Summary
- suspected_label_issues_count: 1000
- suspected_label_issues_ratio: 0.0200
- export_top_k: 200

Student task: chọn 5 mẫu trong cleanlab_label_issues.csv để review (giữ/sửa/ambiguous) và ghi vào Data Card.

---

## Manual Label Review Results (5 Samples)

| Sample | Original Label | Decision | Lý Do | Confidence |
|--------|---|---|----|---|
| ID 11668 | 0 (Neg) | **FIX → 1** | "great movie, love ×4" = positive | 99.86% |
| ID 22259 | 1 (Pos) | **FIX → 0** | "bad ×7, how dumb" = negative | 99.81% |
| ID 22257 | 1 (Pos) | **FIX → 0** | "cheap, terrible, worst" = negative | 99.74% |
| ID 16634 | 1 (Pos) | **FIX → 0** | So-bad-it's-good → core negative | 99.5% |
| ID 31245 | 0 (Neg) | **FIX → 1** | "powerful performance, worth rental" = positive | 98.9% |

**Summary**: 5/5 samples (100%) required relabeling (FIX decision). All have high Cleanlab confidence (98.9-99.86%) that original labels were incorrect.

**Status**: ✅ PENDING IMPLEMENTATION — Decisions ready to merge into dataset
