# Applied AI in Biomedicine - Breast Ultrasound Project

This repository contains our Applied AI in Biomedicine final project on breast ultrasound (BUS) image analysis. We implement two complementary pipelines for lesion classification and segmentation, following the assignment specifications and reported in the project report.

Team: Bikini Bottom Team (Ali Mehdipour, Sajjad Shaffaf)

<p align="center">
  <img src="assets/report_figures/report-002.png" alt="report-002.png" width="400">
</p>

## Assignment Objectives (Summary)

**Task A (classification-first):**
- A.1: 3-class classification of breast ultrasound images (Normal / Benign / Malignant).
- A.2: 2-class lesion segmentation for Benign and Malignant cases.

**Task 2 (segmentation-first):**
- 2a: 3-class lesion segmentation (Normal / Benign / Malignant as lesion presence).
- 2b: 2-class classification (Benign vs Malignant) using the segmentation-masked ROI.

## Dataset

- 1,531 images from 968 patients (460 Normal, 706 Benign, 365 Malignant).
- Patient-level splits are used to prevent data leakage.
- Data folder includes `training_images/` and `training_metadata.xlsx`.

Download (assignment link):
- https://drive.google.com/drive/folders/1EkuEi0h2G_-nVuD08Z3dUJpXl63sgY79?usp=drive_link

## Requirements (From Notebooks)

Exact versions explicitly printed in notebook outputs:
- segmentation-models-pytorch==0.5.0

Packages installed/imported in notebooks (versions not pinned in notebook cells):
- torch, torchvision
- timm
- albumentations
- scikit-learn
- numpy, pandas
- matplotlib, seaborn
- pillow
- opencv-python
- openpyxl

## Methods (High Level)

**Task A.1 (3-class classification)**
- Transfer learning with EfficientNet-B0 (best model).
- Weighted cross-entropy to address class imbalance.
- Data augmentation (affine transforms, blur, brightness/contrast, speckle noise).
- Hyperparameter grid search + stratified 5-fold ensembling.
- Grad-CAM for interpretability.

**Task A.2 (lesion segmentation)**
- Encoder-decoder models: U-Net, U-Net++, DeepLabV3+, Attention U-Net.
- Loss: BCE + Dice.

**Task 2 (segmentation-first pipeline)**
- Stage 1: segmentation produces ROI mask.
- Normal filter: if mask area < 50 pixels, classify as Normal.
- Stage 2: classify Benign vs Malignant on the masked image.
- 5-fold ensemble + test-time augmentation for classification stage.

## Results (From the Report)

| Task | Metric | Value | Notes |
| --- | --- | --- | --- |
| Task A.1 (classification) | Balanced accuracy | 0.8432 | EfficientNet-B0 5-fold ensemble |
| Task A.2 (segmentation) | Dice (validation) | ~0.80 | Best model |
| Task 2 (segmentation-first pipeline) | Balanced accuracy | 0.7879 | Best configuration |

### Per-class Metrics (Task 2 Pipeline)

| Class | Precision | Recall | F1 | Support |
| --- | --- | --- | --- | --- |
| Benign | 0.7597 | 0.8417 | 0.7986 | 139 |
| Malignant | 0.7846 | 0.6000 | 0.6800 | 85 |
| Normal | 0.8659 | 0.9221 | 0.8931 | 77 |

### Confusion Matrices (Task 2 Pipeline)

<p align="center">
  <img src="assets/report_figures/report-051.png" alt="Task 2 pipeline confusion matrices (raw counts and row-normalized)" width="800">
</p>

## Report Figures (Auto-extracted)
<p align="center">
  <img src="assets/report_figures/report-038.png" alt="report-038.png" width="400">
</p>
All figures were extracted from the PDF and embedded below in report order. For figure captions and discussion, see the report.

<details>
<summary>Show all figures</summary>

<p align="center">
  <img src="assets/report_figures/report-003.png" width="32%" />
  <img src="assets/report_figures/report-006.png" width="32%" />
  <img src="assets/report_figures/report-018.png" width="32%" />
  <img src="assets/report_figures/report-004.png" width="32%" />  
  <img src="assets/report_figures/report-010.png" width="32%" />
  <img src="assets/report_figures/report-012.png" width="32%" />
  <img src="assets/report_figures/report-014.png" width="32%" />
  <img src="assets/report_figures/report-016.png" width="32%" />
  <img src="assets/report_figures/report-008.png" width="32%" />
  <img src="assets/report_figures/report-020.png" width="32%" />
  <img src="assets/report_figures/report-022.png" width="32%" />
  <img src="assets/report_figures/report-024.png" width="32%" />
  <img src="assets/report_figures/report-026.png" width="32%" />
    <img src="assets/report_figures/report-034.png" width="32%" />
  <img src="assets/report_figures/report-030.png" width="32%" />
  <img src="assets/report_figures/report-028.png" width="32%" />
  <img src="assets/report_figures/report-032.png" width="32%" />
  <img src="assets/report_figures/report-036.png" width="32%" />
  <img src="assets/report_figures/report-039.png" width="32%" />
  <img src="assets/report_figures/report-041.png" width="32%" />
  <img src="assets/report_figures/report-048.png" width="32%" />
  <img src="assets/report_figures/report-045.png" width="32%" />
  <img src="assets/report_figures/report-043.png" width="32%" />
  <img src="assets/report_figures/report-049.png" width="32%" />
  <img src="assets/report_figures/report-051.png" width="32%" />
  <img src="assets/report_figures/report-053.png" width="32%" />
  <img src="assets/report_figures/report-055.png" width="32%" />
  <img src="assets/report_figures/report-062.png" width="32%" />
  <img src="assets/report_figures/report-064.png" width="32%" />
  <img src="assets/report_figures/report-060.png" width="32%" />
  <img src="assets/report_figures/report-056.png" width="32%" />
  <img src="assets/report_figures/report-058.png" width="32%" />
</p>

</details>

## Notebooks

- `t1_TASKA.ipynb` - Task A pipeline (classification-first) experiments.
- `t2_1_data_splitting.ipynb` - patient-aware splitting.
- `t2_2_modular-task2-experiment-2b-efficientnetb0.ipynb` - Task 2 training experiments.
- `t2_3_inference-evaluation-task2.ipynb` - single-model Task 2 inference/evaluation.
- `t2_4_ensemble-inference-5fold-task2.ipynb` - 5-fold ensemble inference for Task 2.
- `t2_5_blind_test_inference.ipynb` - blind test inference pipeline.

## Model Weights

Pretrained model checkpoints are available here:
- https://drive.google.com/drive/folders/1Y_FJ20fPWVEXtZ79zlhs4wnvlODzZFcf

## How To Run (Typical Order)

1. Download the dataset and place it in the expected folders.
2. Run the patient-level split notebook.
3. Train or load model checkpoints.
4. Run inference notebooks (single-model or 5-fold ensemble).
5. Use the blind test notebook for final submission predictions.

## Report

See `Applied_AI_in_Biomedicine___Project_report.pdf` for full methodology, experiments, and discussion.
