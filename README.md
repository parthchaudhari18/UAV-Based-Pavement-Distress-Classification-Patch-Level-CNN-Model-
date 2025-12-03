# 📘 UAV-Based Pavement Distress Classification (Patch-Level Deep Learning Model)

This project implements a complete computer vision and machine learning pipeline for **detecting pavement distress** (cracks, defects) from UAV runway imagery.  
Using Pascal VOC XML annotations and raw aerial images, the system automatically generates labeled training patches and trains a TensorFlow CNN classifier to distinguish **distressed** vs **healthy** pavement tiles.

---

## 🚀 Project Summary

- Parses **XML annotations** to extract distress bounding boxes  
- Generates **positive patches** (distress-centered) and **negative patches** (non-overlapping)  
- Creates a **balanced patch-level dataset**  
- Builds TensorFlow `tf.data` pipelines with augmentation  
- Trains a **compact CNN (101k params)** for binary classification  
- Achieves **86.13% test accuracy** with **98% recall** on distressed patches  

The goal is to replicate real-world workflows used in UAV inspection systems and digital twin pipelines.

---

## 📂 Project Structure

