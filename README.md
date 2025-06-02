# 🫁 AsthmaCT-Net: CT Feature Extraction for Asthma Stratification Using MedicalNet

This repository implements a pipeline for extracting radiomic embeddings from thoracic CT scans of asthma patients using **MedicalNet**, a pretrained 3D convolutional neural network framework. The goal is to enable **asthma endotyping and therapeutic stratification** by integrating spatial imaging features with transcriptomic and clinical data.

---

## 🎯 Objective
Extract biologically meaningful, low-dimensional CT features from 3D lung volumes to:
- Support asthma subtype classification
- Enable multimodal fusion with omics data (e.g., Geneformer)
- Identify predictive imaging biomarkers in severe or T2-low asthma

---

## 🧠 Why MedicalNet?
Training 3D CNNs from scratch on CT data is often infeasible due to data and annotation limitations. MedicalNet provides:
- Pretrained 3D ResNet models (e.g., ResNet-18, ResNet-34)
- Trained on large, diverse medical datasets (LUNA, LiTS, MSD)
- Proven transferability to various thoracic imaging tasks

---

## 🗂️ Input Data
- Raw thoracic CT scans (NIfTI, DICOM, or converted .npy/.nii.gz formats)
- Optional: associated transcriptomics and clinical metadata for alignment

---

## 🛠️ Methodology

### Step 1: Preprocessing
- Convert to standard voxel spacing (e.g., 1×1×1 mm)
- Normalize voxel intensities (windowing, zero-mean, unit variance)
- Crop or pad to **112×112×80** volume size

### Step 2: CT Embedding with MedicalNet
- Load pretrained **3D ResNet-18 or ResNet-34** from MedicalNet
- Pass preprocessed CT volume through model
- Extract final convolutional layer or global pooled feature as CT embedding

### Step 3: Embedding Matrix Output
- Store patient-level feature vectors in `.csv` or `.npy` format
- Align with omics/clinical data by patient ID

---

## 🔁 Integration Potential
- Combine with **Geneformer embeddings** from transcriptomics
- Fuse imaging and omics for tasks like:
  - Inflammation prediction
  - Subtype discovery (T2-high vs. T2-low)
  - Biologic treatment stratification

---

## 📁 Folder Structure
```
├── data/
│   ├── ct_scans/                 # Preprocessed CT volumes
│   ├── metadata.csv              # Patient IDs and labels
├── models/
│   └── medicalnet_resnet18.pth  # Pretrained weights
├── src/
│   ├── preprocess_ct.py
│   ├── extract_embeddings.py
├── results/
│   └── ct_embeddings.npy
├── notebooks/
│   └── CT_Embedding_Pipeline.ipynb
├── requirements.txt
└── README.md
```

---

## 🧪 Dependencies
```bash
pytorch
monai or nibabel
opencv-python
scikit-image
numpy
scikit-learn
```

---

## 📜 License
MIT License — built upon publicly released MedicalNet weights by Tencent AI Lab.

---

## 📌 Reference
- [MedicalNet GitHub (Tencent)](https://github.com/Tencent/MedicalNet)
- [LUNA16, LiTS, MSD datasets]
