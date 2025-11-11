# 🧠 HFA-Net: Wavelet-based Frequency Analysis with Attention Mechanisms for Precise Brain Tumor Segmentation

[![Python](https://img.shields.io/badge/Python-3.10-blue.svg)]()
[![PyTorch](https://img.shields.io/badge/Framework-PyTorch-red)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)]()
[![Paper](https://img.shields.io/badge/ArXiv-Preprint-orange.svg)]()

---

## 🧩 Authors
**Akil M**, **Dilip R**, **Elango V**, **Nishanth M**  
*Department of Artificial Intelligence and Data Science*  
Karpagam Academy of Higher Education, Coimbatore, India  
**Supervisor:** Dr. B. Arun Kumar, Professor & HoD, Department of AI & DS  
📧 **Contact:** akilmasiv@gmail.com  

---

## 📘 Overview

**HFA-Net (Hybrid Frequency-Attention U-Net)** introduces a multi-domain feature learning approach that fuses **wavelet-based frequency analysis** with **attention mechanisms** for accurate **brain tumor segmentation** from MRI scans.  

The model preserves high-frequency boundary information and dynamically recalibrates features for **clinical-grade segmentation precision**.

---

## 🚀 Key Features

- 🌀 **Wavelet Transform (DWT):** Extracts spatial-frequency details from MRI slices.  
- 🔀 **Dual-Path Encoder:** Processes low-frequency (context) and high-frequency (edge) features in parallel.  
- 🎯 **Attention-Gated Skip Connections:** Enhances tumor saliency and suppresses noise.  
- 🧪 **Validated on BraTS 2020:** Outperforms U-Net and Attention U-Net baselines.


---

## 🧪 Dataset and Preprocessing

**Dataset:** [BraTS 2020 - Kaggle Link](https://www.kaggle.com/datasets/awsaf49/brats20-dataset-training-validation)

**Details:**
- 369 MRI volumes (T1, T1ce, T2, FLAIR)
- Expert-labeled tumor subregions
- Binary segmentation (Tumor / Non-Tumor)

**Preprocessing:**
1. Select T1ce & FLAIR modalities  
2. Percentile intensity normalization ([0, 1])  
3. Extract axial slices (~18k)  
4. Resize to 128×128 pixels  
5. 90/10 train-validation patient split  

---

## ⚙️ Implementation Details

| Component | Description |
|------------|-------------|
| Framework | PyTorch 2.0.1 |
| GPU Used | NVIDIA RTX A6000 (48 GB) |
| Loss Function | Dice Loss + 0.6 × Binary Cross Entropy |
| Optimizer | AdamW (LR = 1e-4, Cosine Annealing) |
| Batch Size / Epochs | 16 / 25 |
| Augmentations | Flip, Rotate, Brightness, Elastic Deformation |
| Early Stop | Patience = 7 (Validation Dice) |

---

## 🧩 Performance

| Model | Dice | IoU | Precision | Recall | Specificity |
|-------|------:|----:|----------:|--------:|-------------:|
| **U-Net** | 0.8214 | 0.6959 | 0.8210 | 0.8321 | 0.9947 |
| **Attention U-Net** | 0.8559 | 0.7474 | 0.8492 | 0.8685 | 0.9955 |
| **DWT-U-Net** | 0.8432 | 0.7286 | 0.8643 | 0.8318 | 0.9959 |
| 🧠 **HFA-Net (Proposed)** | **0.8795** | **0.7850** | **0.8951** | **0.8951** | **0.9963** |

---

## 🔍 Ablation Study

| Variant | DWT Input | Attention | Dice | Gain |
|----------|:----------:|:----------:|:------:|:------:|
| U-Net | ❌ | ❌ | 0.8214 | - |
| Attention Only | ❌ | ✅ | 0.8559 | +4.2% |
| DWT Only | ✅ | ❌ | 0.8432 | +2.6% |
| **HFA-Net (Full)** | ✅ | ✅ | **0.8795** | **+7.07%** |

✅ The combination of **DWT + Attention** achieves **super-additive performance**.

---

## 🖼️ Qualitative Insights

- Sharper tumor boundaries  
- Fewer false positives  
- Topologically consistent segmentation masks  

---

## 🧭 Future Work

- Extend to **3D volumetric segmentation**
- Add **Transformer-based attention**
- Multi-class tumor subregion segmentation
- **Federated learning** for privacy-preserving collaboration
- **Explainable AI** integration with uncertainty estimation  
