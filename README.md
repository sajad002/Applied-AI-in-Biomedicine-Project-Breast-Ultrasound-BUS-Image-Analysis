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

## Report Figures (Auto-extracted)

All figures were extracted from the PDF and embedded below in report order. For figure captions and discussion, see the report.

<details>
<summary>Show all figures</summary>

![report-000.png](assets/report_figures/report-000.png)
![report-001.png](assets/report_figures/report-001.png)
![report-002.png](assets/report_figures/report-002.png)
![report-003.png](assets/report_figures/report-003.png)
![report-004.png](assets/report_figures/report-004.png)
![report-005.png](assets/report_figures/report-005.png)
![report-006.png](assets/report_figures/report-006.png)
![report-007.png](assets/report_figures/report-007.png)
![report-008.png](assets/report_figures/report-008.png)
![report-009.png](assets/report_figures/report-009.png)
![report-010.png](assets/report_figures/report-010.png)
![report-011.png](assets/report_figures/report-011.png)
![report-012.png](assets/report_figures/report-012.png)
![report-013.png](assets/report_figures/report-013.png)
![report-014.png](assets/report_figures/report-014.png)
![report-015.png](assets/report_figures/report-015.png)
![report-016.png](assets/report_figures/report-016.png)
![report-017.png](assets/report_figures/report-017.png)
![report-018.png](assets/report_figures/report-018.png)
![report-019.png](assets/report_figures/report-019.png)
![report-020.png](assets/report_figures/report-020.png)
![report-021.png](assets/report_figures/report-021.png)
![report-022.png](assets/report_figures/report-022.png)
![report-023.png](assets/report_figures/report-023.png)
![report-024.png](assets/report_figures/report-024.png)
![report-025.png](assets/report_figures/report-025.png)
![report-026.png](assets/report_figures/report-026.png)
![report-027.png](assets/report_figures/report-027.png)
![report-028.png](assets/report_figures/report-028.png)
![report-029.png](assets/report_figures/report-029.png)
![report-030.png](assets/report_figures/report-030.png)
![report-031.png](assets/report_figures/report-031.png)
![report-032.png](assets/report_figures/report-032.png)
![report-033.png](assets/report_figures/report-033.png)
![report-034.png](assets/report_figures/report-034.png)
![report-035.png](assets/report_figures/report-035.png)
![report-036.png](assets/report_figures/report-036.png)
![report-037.png](assets/report_figures/report-037.png)
![report-038.png](assets/report_figures/report-038.png)
![report-039.png](assets/report_figures/report-039.png)
![report-040.png](assets/report_figures/report-040.png)
![report-041.png](assets/report_figures/report-041.png)
![report-042.png](assets/report_figures/report-042.png)
![report-043.png](assets/report_figures/report-043.png)
![report-044.png](assets/report_figures/report-044.png)
![report-045.png](assets/report_figures/report-045.png)
![report-046.png](assets/report_figures/report-046.png)
![report-047.png](assets/report_figures/report-047.png)
![report-048.png](assets/report_figures/report-048.png)
![report-049.png](assets/report_figures/report-049.png)
![report-050.png](assets/report_figures/report-050.png)
![report-051.png](assets/report_figures/report-051.png)
![report-052.png](assets/report_figures/report-052.png)
![report-053.png](assets/report_figures/report-053.png)
![report-054.png](assets/report_figures/report-054.png)
![report-055.png](assets/report_figures/report-055.png)
![report-056.png](assets/report_figures/report-056.png)
![report-057.png](assets/report_figures/report-057.png)
![report-058.png](assets/report_figures/report-058.png)
![report-059.png](assets/report_figures/report-059.png)
![report-060.png](assets/report_figures/report-060.png)
![report-061.png](assets/report_figures/report-061.png)
![report-062.png](assets/report_figures/report-062.png)
![report-063.png](assets/report_figures/report-063.png)
![report-064.png](assets/report_figures/report-064.png)
![report-065.png](assets/report_figures/report-065.png)

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
