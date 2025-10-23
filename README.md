#  Histopathologic Cancer Detection using Deep Learning

This project focuses on detecting **metastatic cancerous tissue** in histopathologic images of lymph node sections.  
The solution uses a **deep convolutional neural network (EfficientNet-B0)** with transfer learning to achieve high accuracy in binary image classification.

---

##  Project Overview

###  Objective
To develop a robust CNN model capable of accurately distinguishing between **cancerous** and **non-cancerous** tissue patches.

###  Highlights
- Built using **PyTorch**
- Used **EfficientNet-B0** as the base model with transfer learning
- Implemented **advanced image augmentations** to enhance generalization
- Employed **AdamW optimizer**, **OneCycleLR scheduler**, and **early stopping**
- Achieved **~97–98% validation accuracy**

---

##  Dataset

- **Source:** [Kaggle - Histopathologic Cancer Detection](https://www.kaggle.com/competitions/histopathologic-cancer-detection)
- **Total Images:** 220,025 labeled patches (96×96 pixels)
- **Labels:**  
  - `1` → Contains cancerous tissue  
  - `0` → Normal tissue  

### Dataset Split
| Split | Percentage | Purpose |
|--------|-------------|----------|
| Training | 90% | Model learning with augmentations |
| Validation | 10% | Performance evaluation |
| Test | Separate Kaggle test set | Final inference/submission |

---

##  Data Pipeline (Summary)

1. **Data Collection**  
   - Images and labels were loaded from the Kaggle dataset using CSV metadata.  
   - Paths were mapped to image IDs for efficient access.

2. **Data Splitting**  
   - Dataset was split into **training (90%)** and **validation (10%)** using stratified sampling to maintain label balance.

3. **Data Augmentation**  
   - Applied strong augmentations to training data for robustness:  
     - Random crops and rotations  
     - Horizontal & vertical flips  
     - Color jitter (brightness, contrast, saturation)  
   - Validation data was only resized and normalized (no random transformations).

4. **Normalization**  
   - All images were standardized using ImageNet mean and standard deviation to align with the pretrained model’s expectations.

5. **DataLoader**  
   - Images were efficiently batched and loaded using PyTorch `DataLoader`, enabling GPU-accelerated training.

---

##  Model Architecture

| Layer | Description |
|--------|--------------|
| **Base Model** | EfficientNet-B0 (pretrained on ImageNet) |
| **Pooling** | Global Average Pooling layer |
| **Regularization** | Dropout for reducing overfitting |
| **Classifier Head** | Fully connected layer for binary classification |
| **Loss Function** | Binary Cross-Entropy with Logits |
| **Optimizer** | AdamW |
| **Learning Rate Scheduler** | OneCycleLR |

---

##  Training Performance

| Epoch | Train Accuracy | Validation Accuracy | Validation Loss |
|--------|----------------|----------------------|-----------------|
| 1 | 91.2% | 95.6% | 0.140 |
| 3 | 95.1% | 96.9% | 0.095 |
| 5 | 96.0% | 97.3% | 0.079 |
| 7 | 96.6% | 97.6% | 0.073 |

 **Final Validation Accuracy:** 97.6%  
 **Overfitting:** Minimal (train ≈ val)

---

##  Results Summary

-  Model generalizes well with minimal overfitting  
-  Strong accuracy and precision in distinguishing cancerous patches  
-  Stable convergence and efficient training  
-  Easily extendable to larger EfficientNet variants (B1–B4)

---



