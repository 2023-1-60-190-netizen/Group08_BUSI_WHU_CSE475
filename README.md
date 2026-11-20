# Group08 – CSE475 Machine Learning Project (Fall 2026)

**Repository:** Group08_BUSI_WHU_CSE475  
**Dataset:** BUSI-WHU Breast Cancer Ultrasound Image Dataset  
Source: Mendeley Data, V3, DOI 10.17632/k6cpmwybk3.3 (CC BY 4.0), Renmin Hospital of Wuhan University  
**Track:** Track 3 – CNN + Attention  
**Members:** Maharun Nesa Tanni (2023-1-60-190), Kh. Tania Akter Tamanna (2023-2-60-070)  
**Problem type:** Binary image classification (benign vs malignant) with tumour masks (927 images: 560 benign, 367 malignant; 816 patients)

## Repository layout
```
Group08_BUSI_WHU_CSE475/
  README.md
  report/
    task1/Group08_BUSIWHU_task1_report.pdf   (.docx also included)
    task2/Group08_BUSIWHU_task2_report.pdf   (.docx also included)
  code/
    task1/Group08_BUSIWHU_task1_eda.ipynb
    task1/eda_outputs/                        (EDA figures + tables)
    task2/Group08_BUSIWHU_task2_baselines.ipynb
    task2/Group08_BUSIWHU_task2_proposed_model.ipynb
    task2/task2_outputs/                      (results tables, curves, figures, split file)
  related_work/
    Group08_BUSIWHU_related_work_table.pdf    (.csv also included)
    papers/                                   (the 5 paper PDFs)
```
Task 3 folders (`code/task3`, `report/task3`, `models/`) will be added in the final submission.

## How to run (Kaggle notebook, GPU on, dataset attached)
1. Task 1: `code/task1/Group08_BUSIWHU_task1_eda.ipynb` (Run All).
2. Task 2, step 1: `code/task2/Group08_BUSIWHU_task2_baselines.ipynb` (Run All). It writes everything to `/kaggle/working/task2_outputs`.
3. Task 2, step 2: `code/task2/Group08_BUSIWHU_task2_proposed_model.ipynb` (Run All). To compare with all baselines, add the baseline notebook's output as an input (or copy `baseline_runs.csv` and `baseline_test_probs.npz` into its `task2_outputs` folder); it finds them automatically.
4. Requirements: `torch torchvision scikit-learn pandas numpy pillow matplotlib seaborn openpyxl` (all preinstalled on Kaggle). Pretrained ImageNet weights need Kaggle "Internet" turned on; otherwise the notebooks fall back to random initialisation and say so.

## Task 1 – key findings
- 927 grayscale BMP images, all with masks and labels; no exact duplicates.
- Benign 60.4% / malignant 39.6% (ratio 1.53:1), so macro-F1, per-class recall and ROC/PR are used.
- 38 patients have 2–9 images, so all splits are grouped by patient.
- Malignant tumours are larger (median area 1.25 vs 0.56 cm²) and slightly less convex.
- Gap: BUSI-WHU papers do segmentation only; attention models are rarely evaluated with patient-grouped splits, 5-fold CV, significance tests and Grad-CAM together.

## Task 2 – setup
- Split: patient-wise and stratified, 617 / 155 / 155 images (train / val / test), no patient in two sets; saved as `splits.csv`.
- Preprocessing: grayscale, square letterbox to 224×224, ImageNet normalisation; light augmentation (flip, rotation, shift, scale, brightness/contrast); class-weighted loss.
- Baselines: SimpleCNN (from scratch), ResNet50, DenseNet121, EfficientNet-B0.
- Proposed model: CBAM-ResNet50 (channel + spatial attention after each of the four residual stages), standard and residual variants; the variant with the higher mean validation macro-F1 is the proposed model.
- Every model is trained with 3 seeds (42, 7, 2024) and reported as mean ± std, because a single run on the small test set varies by several points.
- Results: see `code/task2/task2_outputs/` and the Task 2 report.
