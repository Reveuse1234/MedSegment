# FLAIR-Only Brain Tumor Segmentation Using Attention U-Net

This repository contains the implementation and result files for a deep learning-based brain tumor segmentation project using the BraTS 2020 dataset. The project uses only the FLAIR MRI modality and performs binary whole-tumor segmentation using Attention U-Net-based models.

## Project Overview

Brain tumor segmentation is an important medical image analysis task used to identify tumor regions from MRI scans. In this project, the BraTS 2020 dataset is used, but only the FLAIR modality is selected as input. The original BraTS labels are converted into a binary whole-tumor mask, where all tumor labels are treated as foreground and the remaining region is treated as background.

The model is trained to predict a binary tumor mask from a FLAIR MRI slice. The final prediction is evaluated using standard segmentation metrics such as Dice score, IoU, sensitivity, and precision.

## Problem Statement

To automatically segment brain tumor regions from FLAIR MRI scans using an Attention U-Net-based deep learning model and evaluate the segmentation performance using Dice score, IoU, sensitivity, and precision.

## Dataset

The project uses the BraTS 2020 dataset.

Only the FLAIR modality is used in this implementation. The full BraTS dataset contains multiple MRI modalities such as T1, T1ce, T2, and FLAIR, but this project is restricted to FLAIR-only segmentation.

The dataset is not included in this repository because of size and access restrictions. Users must download or access the BraTS dataset separately and place it in the required input directory before running the notebook.

## Model Architecture

The project uses Attention U-Net-based segmentation models. Attention mechanisms help the model focus on relevant tumor regions while suppressing less useful background information. The model pipeline follows this general structure:

FLAIR MRI input -> preprocessing -> Attention U-Net -> sigmoid output -> thresholding -> predicted tumor mask -> evaluation

The implemented workflow includes:

- FLAIR image extraction
- Binary whole-tumor mask generation
- Image resizing and normalization
- Train, validation, and test splitting
- Attention U-Net training
- Validation-based checkpoint selection
- Threshold tuning and connected-component post-processing
- Final test evaluation

## Methodology

The BraTS MRI volumes are processed by selecting the FLAIR modality and converting tumor annotations into binary masks. The input images are resized and normalized before being passed to the Attention U-Net model. The model is trained on FLAIR slices and validated after each epoch. The best checkpoint is selected using validation Dice score.

After training, threshold tuning is performed on the validation set to select the best probability threshold and connected-component filtering setting. The selected settings are then applied to the test set for final evaluation.

## Evaluation Metrics

The following metrics are used:

- Dice score: Measures overlap between predicted tumor mask and ground-truth mask.
- IoU: Measures intersection-over-union between prediction and ground truth.
- Sensitivity: Measures how many tumor pixels were correctly detected.
- Precision: Measures how many predicted tumor pixels were actually correct.

## Best Reported Results

The best reported FLAIR-only Attention U-Net run achieved approximately:

| Metric | Value |
|---|---:|
| Validation Dice | 0.878 |
| Test Dice | 0.866-0.867 |
| IoU | 0.774 |
| Sensitivity | 0.861 |
| Precision | 0.889 |

Some individual patient cases achieved Dice scores above 0.90, but the average test Dice remained below 0.90 due to difficult cases with lower sensitivity. This is expected in FLAIR-only segmentation because other MRI modalities such as T1, T1ce, and T2 provide additional tumor boundary and enhancement information that FLAIR alone may not capture.

## Repository Structure

```text
brats-flair-attention-unet/
│
├── notebooks/
│   ├── training_kaggle.ipynb
│   └── inference_demo.ipynb
│
├── results/
│   ├── training_curves.png
│   ├── validation_dice_curve.png
│   ├── prediction_example.png
│   ├── test_summary.json
│   └── patient_wise_metrics.csv
│
├── report/
│   └── project_report.pdf
│
├── README.md
├── requirements.txt
└── .gitignore
```

## How to Run

1. Download or access the BraTS 2020 dataset.
2. Place the dataset in the input directory expected by the notebook.
3. Install the required packages:

```bash
pip install -r requirements.txt
```

4. Open the training notebook in Kaggle or Google Colab.
5. Run the cells in order.
6. After training, run threshold tuning and final test evaluation.
7. Save the result ZIP and figures for report submission.

## Important Notes

- The original BraTS dataset is not included in this repository.
- Large model checkpoints and medical image files should not be uploaded to GitHub.
- Only notebooks, result summaries, figures, and report files should be stored in the repository.
- The project is based on FLAIR-only input, so the performance may be lower than multi-modal MRI segmentation approaches.

## Technologies Used

- Python
- PyTorch
- NumPy
- Pandas
- Matplotlib
- scikit-learn
- NiBabel
- OpenCV
- Kaggle / Google Colab

## Author

Noor ul huda  
AICTE Samartham Intern  
IIITDM Kancheepuram
