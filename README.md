HAM10000 Skin Lesion Image Classifier

An educational deep learning project that classifies dermoscopic skin lesion images from the HAM10000 dataset using EfficientNetB0 and TensorFlow.

Disclaimer: This project was created for educational and research purposes only. It is not a medical diagnostic system and should never be used to make healthcare decisions.

Live results page: https://shashankpadala43267.github.io/HAM10000-Skin-Lesion-Classifier/

Project Overview

This project explores medical image classification using transfer learning with EfficientNetB0.

The complete machine learning workflow includes:

Downloading the HAM10000 dataset
Exploring metadata and class distribution
Mapping image paths
Leakage-aware train/validation/test splitting (split by lesion ID, not image ID)
TensorFlow data pipelines
Image augmentation
Class weighting for imbalance
EfficientNetB0 transfer learning
Initial training with a frozen base
Fine-tuning the final EfficientNet layers
Model evaluation
Confusion matrix analysis
Per-class recall analysis
High-confidence error analysis
Dataset

Dataset: HAM10000 (Human Against Machine with 10,000 Training Images)

Number of classes: 7

Classes:

akiec — Actinic keratoses
bcc — Basal cell carcinoma
bkl — Benign keratosis-like lesions
df — Dermatofibroma
mel — Melanoma
nv — Melanocytic nevi
vasc — Vascular lesions

Dataset Split (split by lesion ID, using a 70/15/15 lesion-grouped split, so the same lesion never appears in more than one split):

Training Images: 7,002
Validation Images: 1,519
Testing Images: 1,494
Model

Architecture:

EfficientNetB0
TensorFlow / Keras
Transfer learning (frozen-base training, then fine-tuning)
Data augmentation
Class weighting
Evaluation Results (Final Model, After Fine-Tuning)
Metric	Value
Test Accuracy	72.49%
Balanced Accuracy	66.76%
Macro Precision	50.06%
Macro Recall	66.76%
Macro F1 Score	53.52%
Weighted F1 Score	74.41%
Macro ROC-AUC	92.39%

Reading these numbers: Balanced accuracy (66.76%) and macro F1 (53.52%) diverge because macro precision (50.06%) is noticeably lower than macro recall — the model still over-predicts majority classes like nv somewhat, even with class weighting applied, which drags precision down for minority classes. The high macro ROC-AUC (92.39%) shows the model separates classes well by confidence ranking, even where the final hard-threshold decision is sometimes wrong. Out of 1,494 test images, the model made 411 errors.

This task is genuinely difficult: 7 visually similar classes, a heavily imbalanced dataset, and images from multiple clinical sources. The project prioritizes an honest, fully-documented ML workflow over inflating results — see MODEL_CARD.md for the full breakdown and discussion of limitations.

Training

Initial Training (Frozen Base)

Show Image Show Image

Fine-Tuning

Show Image Show Image

Confusion Matrix

Show Image

Recall by Lesion Class

Show Image

High-Confidence Incorrect Predictions

Show Image

Reviewing confident mistakes helps identify class confusion, dataset limitations, and areas for future improvement. The most common confusions are between visually similar classes such as nv and mel, and nv and vasc.

Repository Structure
HAM10000-Skin-Lesion-Classifier/
│
├── docs/                    # GitHub Pages live results site
│   └── assets/
├── figures/                 # Charts referenced in this README
│   ├── confusion_matrix.png
│   ├── fine_tuning_accuracy.png
│   ├── fine_tuning_loss.png
│   ├── high_confidence_mistakes-2.png
│   ├── initial_accuracy.png
│   ├── initial_loss.png
│   └── per_class_recall.png
├── notebook/
│   └── HAM10000_Skin_Lesion_Classifier_jpynb.ipynb
├── results/
│   ├── HAM10000_results.json
│   ├── HAM10000_mistakes.csv
│   ├── HAM10000_error_pairs.csv
│   └── HAM10000_test_predictions.csv
│
├── MODEL_CARD.md
├── README.md
└── requirements.txt
Technologies Used
Python
TensorFlow
Keras
EfficientNetB0
NumPy
Pandas
Matplotlib
Scikit-learn
Google Colab
KaggleHub
Skills Demonstrated
Computer Vision
Deep Learning
Transfer Learning
Fine-Tuning
TensorFlow
Data Preprocessing
Leakage-Aware Dataset Splitting
Medical Image Analysis
Model Evaluation
Error Analysis
Confusion Matrix Interpretation
Machine Learning Documentation
Project Limitations
The HAM10000 dataset is highly imbalanced.
Performance varies significantly across lesion classes.
The model produces some high-confidence incorrect predictions.
Results may not generalize outside the HAM10000 dataset.
The model has not been clinically validated.
Predictions are based only on images and do not include patient history or clinical information.

Full discussion in MODEL_CARD.md.

Future Improvements
Grad-CAM visual explanations
Further handling of class imbalance (e.g., focal loss)
Hyperparameter optimization
Additional CNN architectures (ResNet50, MobileNetV2) for comparison
Precision-recall curves per class
Interactive web application / hosted demo
Model comparison experiments
Author

Shashank Padala

High school student interested in:

Artificial Intelligence
Computer Vision
Biomedical Engineering
Medicine
Machine Learning
Software Engineering
Educational Disclaimer

This repository is an educational machine learning project created to demonstrate deep learning techniques using publicly available data.

It must not be used for:

Medical diagnosis
Clinical decision making
Patient screening
Treatment recommendations
Replacing a licensed healthcare professional

Always consult a qualified medical professional for medical advice.
