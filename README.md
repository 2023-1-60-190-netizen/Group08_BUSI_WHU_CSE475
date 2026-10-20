# Group08 – CSE475 Machine Learning Project (Fall 2026)

**Repository:** Group08_BUSIWHU_CSE475  
**Dataset:** BUSI-WHU Breast Cancer Ultrasound Image Dataset  
Source: Mendeley Data, V3, DOI 10.17632/k6cpmwybk3.3 (CC BY 4.0), Renmin Hospital of Wuhan University  
**Track:** [Track 2 – GCN  /  Track 3 – CNN + Attention]  
**Members:** Maharun Nesa Tanni (2023-1-60-190), Kh. Tania Akter Tamanna (2023-2-60-070)  
**Problem type:** Binary image classification (benign vs malignant) with tumour masks (927 images: 560 benign, 367 malignant; 816 patients)

## Repository layout
```
Group08_BUSIWHU_CSE475/
  README.md
  report/
    task1/Group08_BUSIWHU_task1_report.pdf   (.docx also included)
  code/
    task1/Group08_BUSIWHU_task1_eda.ipynb
    task1/eda_outputs/                        (EDA figures + tables from the notebook)
  related_work/
    Group08_BUSIWHU_related_work_table.pdf    (.csv also included)
    papers/                                   (put the paper PDFs here)
```
Task 2 and Task 3 folders (`code/task2`, `code/task3`, `report/task2`, `report/task3`, `models/`) will be added in later submissions.

## Task 1 (due 21 Oct 2026)
- **Image EDA (A–G):** `code/task1/Group08_BUSIWHU_task1_eda.ipynb`
- **Related-work table + research gap:** `related_work/Group08_BUSIWHU_related_work_table.pdf`
- **Short report:** `report/task1/Group08_BUSIWHU_task1_report.pdf`

## How to run the EDA notebook
1. Download the dataset from Mendeley Data (`BUSI-WHU.zip` and `Patient_infos_BUSI-WHU.xlsx`) and extract it.
2. Set `BUSI_DIR` (image/mask folder) and `BUSI_XLSX` (patient file) at the top of the notebook, or as environment variables.
3. `pip install pandas numpy pillow matplotlib seaborn plotly scipy scikit-learn scikit-image openpyxl`
4. Run all cells. Figures and tables are saved in `eda_outputs/`.

## Key Task 1 findings
- 927 grayscale BMP images, all with masks and labels; no exact duplicates.
- Benign 60.4% / malignant 39.6% (ratio 1.53:1), so we use macro-F1, per-class recall, ROC/PR.
- Sizes vary (243–2400 px wide) and pixel-per-cm scale varies (57–480), so images are resized with padding.
- 38 patients have 2–9 images, so all splits are grouped by patient (StratifiedGroupKFold).
- Malignant tumours are larger (median area 1.25 vs 0.56 cm²) and slightly less convex.
- Gap: BUSI-WHU papers do segmentation only; graph methods for breast ultrasound use other datasets and whole-image superpixel graphs.
