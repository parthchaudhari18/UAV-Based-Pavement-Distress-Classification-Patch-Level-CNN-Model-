# UAV-Based-Pavement-Distress-Classification-Patch-Level-CNN-Model-
This project builds a complete computer vision pipeline for detecting pavement distress (cracks, defects) in UAV runway imagery using deep learning, Python, and TensorFlow. The system automatically parses XML annotations, extracts high-quality training patches, and trains a CNN classifier to distinguish distressed vs healthy pavement tiles.
Project Structure
├── Annotations/        # Pascal VOC XML distress labels
├── JPEGImages/         # UAV runway images
├── patches/
│   ├── positive/       # Distressed patches (160×160)
│   ├── negative/       # Healthy patches
├── notebook.ipynb      # Full training pipeline
└── README.md           # This file

Key Features

Automated XML parsing (Pascal VOC format)

Patch generation with bounding-box–aware sampling

Positive patches extracted from distress annotations

Negative patches mined from non-overlapping areas

Balanced train/val/test creation with stratification

TensorFlow data pipelines with augmentation

Patch-level CNN classifier (lightweight & fast)

Full evaluation with confusion matrix + classification report

Dataset Summary

After preprocessing:

Category	Count
Positive (distressed)	11,946
Negative (healthy)	2,424
Total patches	14,370

Patch size: 160×160 px
Source: UAV pavement images with XML distress annotations.

Model Architecture

A compact CNN optimized for patch-level classification:

Conv2D(32) → MaxPool

Conv2D(64) → MaxPool

Conv2D(128) → MaxPool

GlobalAveragePooling

Dense(64) + Dropout(0.3)

Output: Dense(1, sigmoid)

Total parameters: ~101K.

Training

Loss: binary_crossentropy

Optimizer: Adam

Batch size: 32

Epochs: 5

Augmentation: flip, rotation, zoom

Results

Test Accuracy: 86.13%
Distress Recall: 98%
Healthy Recall: 27%

Confusion matrix:

               Pred 0    Pred 1
True 0           97       267
True 1           32      1760


This means the model:

Almost never misses true cracks (excellent for safety)

Over-flags healthy pavement (expected due to imbalance)

Next Steps / Improvements

Class balancing / weighted loss

Larger patch sizes (256×256)

Multi-class distress types

Sliding-window full-image inference

Integration with mapping / GIS layers

Technologies Used

Python

TensorFlow / Keras

OpenCV

Pandas / NumPy

Scikit-Learn

Google Colab
