**🧠 HFA-Net: Wavelet-based Frequency Analysis with Attention Mechanisms for Precise Brain Tumor Segmentation**

**🧩 Authors**

Akil M, Dilip R, Elango V, Nishanth M

Department of Artificial Intelligence and Data Science

Karpagam Academy of Higher Education, Coimbatore, India

Supervisor: Dr. B. Arun Kumar, Hod, Department of AI & DS

📧 akilmasiv@gmail.com


**📘 Overview**
HFA-Net (Hybrid Frequency-Attention U-Net) is a novel deep learning architecture designed for precise brain tumor segmentation from multimodal MRI (MMRI) scans. 
This network synergistically combines wavelet-based frequency analysis with attention-driven feature fusion to overcome key limitations of traditional U-Net architectures such as boundary degradation, poor high-frequency detail retention, and confusion between tumor and non-tumor tissues.


**🚀 Key Contributions**
1. Integrated Spectral-Spatial Feature Learning
        Introduces a Discrete Wavelet Transform (DWT) module that decomposes MRI slices into complementary frequency sub-bands (LL, LH, HL, HH), capturing both global structure and fine edge details.

2. Dual-Pathway Asymmetric Encoder
        Processes low-frequency (contextual) and high-frequency (detail) information in parallel streams, preserving critical tumor morphology.

3. Attention-Gated Skip Connections
        Implements context-aware feature recalibration, dynamically enhancing tumor-relevant features while suppressing irrelevant background data.

4. Comprehensive Experimental Validation
        Demonstrated superior Dice (0.8795) and IoU (0.7850) scores on the BraTS 2020 dataset, outperforming baseline U-Net and Attention U-Net models.


**🏗️ Network Architecture**
The HFA-Net architecture consists of:
  1. Wavelet-based preprocessing layer using Haar basis.
  2. Dual-pathway encoder for global-local feature fusion.
  3. Attention-gated skip connections replacing naive skip links.
  4. Decoder with transposed convolutions for high-precision mask reconstruction.


**🧪 Dataset and Preprocessing**
Dataset: 
  1. https://www.kaggle.com/datasets/awsaf49/brats20-dataset-training-validation
  2. 369 MRI volumes (T1, T1ce, T2, FLAIR) with expert-labeled tumor regions.
  3. Binary segmentation target: Tumor vs Non-Tumor.
Preprocessing Steps:
  1. Modality Selection: T1ce + FLAIR
  2. Intensity Normalization: Percentile scaling to [0, 1]
  3. Axial Slice Extraction: Retain slices containing tumors (~18,000 slices)
  4. Spatial Resizing: 128×128 pixels
  5. Data Split: 90% training, 10% validation (patient-wise)


**⚙️ Implementation Details**
| Component           | Description                                             |
| ------------------- | ------------------------------------------------------- |
| Framework           | PyTorch 2.0.1                                           |
| GPU Used            | NVIDIA RTX A6000 (48 GB)                                |
| Loss Function       | Dice Loss + 0.6 × Binary Cross Entropy                  |
| Optimizer           | AdamW (LR = 1e-4) with Cosine Annealing                 |
| Batch Size / Epochs | 16 / 25                                                 |
| Augmentations       | Random flips, rotation, brightness, elastic deformation |
| Training Stop       | Early stopping (patience = 7) based on validation Dice  |


**📈 Results**
| Model                 |    Dice    |     IoU    |  Precision |   Recall   | Specificity |
| :-------------------- | :--------: | :--------: | :--------: | :--------: | :---------: |
| U-Net                 |   0.8214   |   0.6959   |   0.8210   |   0.8321   |    0.9947   |
| Attention U-Net       |   0.8559   |   0.7474   |   0.8492   |   0.8685   |    0.9955   |
| DWT-U-Net             |   0.8432   |   0.7286   |   0.8643   |   0.8318   |    0.9959   |
| 🧠 HFA-Net (Proposed) | **0.8795** | **0.7850** | **0.8951** | **0.8951** |  **0.9963** |

Performance Gain:
  1. +7.07% over baseline U-Net
  2. +2.76% over Attention U-Net
  3. +4.30% over DWT-U-Net


**🔍 Ablation Study**
| Model Variant      | DWT Input | Attention Gates |    Dice    |    Gain    |
| ------------------ | :-------: | :-------------: | :--------: | :--------: |
| Baseline U-Net     |     ❌     |        ❌        |   0.8214   |      -     |
| Attention Only     |     ❌     |        ✅        |   0.8559   |   +4.20%   |
| DWT Only           |     ✅     |        ❌        |   0.8432   |   +2.65%   |
| **HFA-Net (Full)** |     ✅     |        ✅        | **0.8795** | **+7.07%** |
✅ The combination of DWT + Attention yields super-additive performance, proving synergistic benefits.


**🖼️ Qualitative Results**
  1. Sharper tumor boundaries
  2. Fewer false positives
  3. Better topological consistency


**📊 Strengths and Limitations**
✅ Strengths:
  1. Preserves high-frequency spatial details
  2. Context-aware dynamic feature fusion
  3. Enhanced tumor region saliency
  4. High robustness to modality variation

**⚠️ Limitations:**
  1. Slightly higher inference time (~23% slower than U-Net)
  2. Small lesion (<5mm) detection sensitivity lower (~15% miss rate)


**🧭 Future Work**
  1. Extend to 3D volumetric segmentation
  2. Integrate Transformer-based attention
  3. Enable multi-class tumor subregion segmentation
  4. Incorporate federated learning for multi-institutional collaboration
  5. Add uncertainty estimation for clinical interpretability
