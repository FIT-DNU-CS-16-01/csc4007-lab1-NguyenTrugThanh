[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/RS4ROckR)
# CSC4007 — Lab 1 Starter Kit Template (GE + Cleanlab + Data Card Playbook)

Template repo cho sinh viên, kèm **GitHub Actions CI**.

## Chạy trên máy cá nhân
```bash
conda activate csc4007-nlp
pip install -U typing_extensions

python run_lab1.py --dataset imdb --seed 42 --use_great_expectations --use_cleanlab
```

## CI làm gì?
- Cài deps
- Chạy `run_lab1.py` với `--max_rows` nhỏ (smoke test)
- Check các file output bắt buộc tồn tại

## Nộp bài
- `data_card.md` (copy từ Google Docs template)
- `datacard/heuristics_scorecard.md`, `datacard/metadata_register.md`
- `outputs/*` theo yêu cầu lab
