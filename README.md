## 📘 Project Overview

This project builds a complete computer vision pipeline for **pavement distress detection** using high-resolution UAV imagery.  
The goal is to automatically classify small image tiles (patches) as **distressed** (containing cracks/defects) or **healthy**.  
The workflow converts raw UAV images and XML annotations into a fully trainable dataset and trains a CNN-based classifier.

---

## 🛠️ Basic Walkthrough of the Pipeline

### **1. Load Raw UAV Data**
The dataset includes:
- **JPEG runway images**
- **Pascal VOC XML annotation files** marking distress (cracks)

Each XML contains bounding boxes that indicate where pavement defects are located.

---

### **2. Parse XML Annotations**
Every XML file is read to extract:
- Bounding box coordinates  
- All distress regions for each image  

This creates a structured mapping of cracks in the dataset.

---

### **3. Generate Training Patches**
The large UAV images are converted into **160×160 pixel patches**.

Two types of patches are created:

#### ✔ **Positive patches (distressed)**
- Cropped around bounding box centers  
- Guaranteed to contain cracks/distress  

#### ✔ **Negative patches (healthy)**
- Randomly extracted from areas with **no** bounding box overlap  
- Represent clean pavement texture  

This produces a high-quality labeled dataset for supervised learning.

---

### **4. Build a Labeled Dataset**
For each patch, we store:
- The image path  
- The original image source  
- The binary label (1 = distress, 0 = healthy)

Final dataset:
- **11,946 distressed patches**
- **2,424 healthy patches**
- **14,370 total patches**

---

### **5. Split Into Train / Validation / Test**
Using stratified sampling:
- **70% training**
- **15% validation**
- **15% testing**

This maintains class proportions across all splits.

---

### **6. TensorFlow Data Pipeline**
A `tf.data` pipeline was built to:
- Load and decode JPEGs  
- Resize to 160×160  
- Normalize pixel values  
- Apply augmentation (flip, rotation, zoom)  
- Batch and prefetch samples  

This ensures fast and efficient training.

---

### **7. Train the CNN Model**
A lightweight convolutional neural network is trained using:
- Three Conv2D + MaxPooling layers  
- GlobalAveragePooling  
- Dense layer + Dropout  
- Sigmoid output  

Optimizer: **Adam**  
Loss: **Binary crossentropy**  
Epochs: **5**

---

### **8. Evaluate the Model**
Test results:
- **Accuracy:** 86.13%  
- **Distress Recall:** 98% (rarely misses cracks)  
- **Healthy Recall:** 27%  

Confusion matrix shows the model is highly sensitive to cracks, which is preferable for safety.

---

## ✅ Summary

This project implements a full end-to-end pipeline for UAV-based pavement distress detection:
- Annotation parsing  
- Patch extraction  
- Dataset creation  
- Train/val/test preparation  
- CNN training and evaluation  

It serves as a scalable foundation for image-tiling-based pavement analysis, crack heatmaps, and geospatial inspection systems.
