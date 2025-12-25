# Breast Lesion Segmentation and Classification  
### A Hybrid Two-Stage Pipeline Using UNet with Transfer-Learning Encoders (VGG16 & ResNet50)

---

## 📌 Project Overview

This project presents a **hybrid two-stage deep learning pipeline** for **breast lesion segmentation and classification** using ultrasound images. The pipeline integrates **UNet-based segmentation** with **transfer-learning encoders (VGG16 and ResNet50)**, followed by **segmentation-guided classification** into three clinical categories:

- **Benign**
- **Malignant**
- **Normal**

The core motivation is that **accurate lesion localization (segmentation) improves downstream diagnostic classification**, especially in noisy and low-contrast ultrasound images.

---

## 🎯 Key Objectives

- Design and implement **UNet with VGG16 encoder** for lesion segmentation  
- Design and implement **UNet with ResNet50 encoder** for lesion segmentation  
- Build a **two-stage learning pipeline**:
  - Stage 1: Lesion segmentation
  - Stage 2: Classification using segmented lesion regions (ROI)
- Perform a **comparative ablation study** between VGG16 and ResNet50 encoders
- Evaluate performance using **quantitative metrics** and **qualitative visual analysis**

---

## 🧠 Methodology Overview

### 🔹 Two-Stage Learning Pipeline

Input Ultrasound Image
↓
Stage 1: UNet-based Segmentation
↓
Predicted Lesion Mask
↓
ROI Extraction (Image × Mask)
↓
Stage 2: Classification Network
↓
Final Prediction (Benign / Malignant / Normal)

yaml
Copy code

This design ensures that the classifier focuses only on clinically relevant lesion regions, reducing background noise and improving robustness.

---

## 🗂 Dataset

- **Dataset:** Breast Ultrasound Images (BUSI)
- **Classes:**
  - Normal
  - Benign
  - Malignant
- **Data Characteristics:**
  - Ultrasound images with corresponding ground-truth masks (for benign & malignant cases)
  - Normal images contain no lesion masks
- **Preprocessing Includes:**
  - Image resizing and normalization
  - Mask binarization
  - ROI alignment between images and masks

---

## 🏗 Model Architecture

### 1️⃣ Segmentation Models (Stage 1)

Two UNet variants were implemented:

- **UNet + VGG16 Encoder**
  - Strong low-level feature extraction
  - Faster convergence
  - Higher tendency to overfit

- **UNet + ResNet50 Encoder**
  - Deep residual learning
  - Improved gradient flow
  - Better generalization and robustness

Skip connections are used to preserve spatial details critical for medical image segmentation.

---

### 2️⃣ Classification Model (Stage 2)

- Input: **Segmentation-guided ROI images**
- Output: Three-class prediction (Benign / Malignant / Normal)
- The classifier leverages the segmented lesion region to improve diagnostic accuracy.

---

## 📊 Performance Evaluation

### 🔹 Segmentation Metrics
- **Dice Coefficient**
- **Intersection over Union (IoU)**

### 🔹 Classification Metrics
- **Accuracy**
- **F1-score**

---

## 🔬 Ablation Study: Encoder Comparison

| Model | Dice | IoU | Classification Accuracy |
|------|------|-----|--------------------------|
| UNet + VGG16 | 0.865 | 0.812 | 94.2% |
| UNet + ResNet50 | **0.892** | **0.845** | **96.8%** |

### 📌 Key Findings
- ResNet50-based UNet consistently outperforms VGG16 across all metrics
- Residual connections and Batch Normalization improve training stability
- Better generalization observed on unseen test data

---

## 🧪 Robustness & Overfitting Analysis

- **UNet + VGG16** shows faster convergence but a growing gap between training and validation performance, indicating overfitting.
- **UNet + ResNet50** demonstrates stable validation behavior and a smaller generalization gap.
- Residual mappings act as a natural regularizer, improving robustness against ultrasound noise and irregular lesion geometry.

---

## 🖼 Qualitative Results

The project includes visual comparisons showing:
- Original ultrasound image
- Ground-truth segmentation mask
- Predicted mask from UNet + VGG16
- Predicted mask from UNet + ResNet50

ResNet50-based segmentation produces smoother and more accurate lesion boundaries, especially for malignant cases with irregular shapes.

---

## 📁 Repository Structure

├── breast-lesion-segmentation-and-classification.ipynb
├── final_report.pdf
├── README.md
└── requirements.txt

yaml
Copy code

- The **notebook** contains full implementation, training, evaluation, and visualization
- The **PDF report** provides detailed explanation, figures, and experimental analysis

---

## 🚀 How to Run

1. Clone the repository:
```bash
git clone https://github.com/Tanvir284/breast-lesion-segmentation-and-classification-using-transfer_learning-encoder-decoder-network.git
Install dependencies:

bash
Copy code
pip install -r requirements.txt
Open the notebook:

bash
Copy code
jupyter notebook
Run all cells sequentially to reproduce results.

🧾 Conclusion
This project demonstrates that segmentation-guided classification significantly improves diagnostic performance in breast ultrasound imaging. Among the evaluated encoders, UNet with ResNet50 provides superior segmentation accuracy, classification performance, and robustness.

The proposed two-stage pipeline effectively handles challenges such as speckle noise, low contrast, and irregular lesion geometry, making it a strong baseline for automated breast cancer screening systems.

👤 Author
Md Tanvir Islam
B.Sc. in Computer Science and Engineering
Bangladesh University of Business and Technology

📧 Email: (add your email here)
