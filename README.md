# Polyp-Segmentation: Hybrid U-Net and Vision Transformer (ViT)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
Code : [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18591131.svg)](https://doi.org/10.5281/zenodo.18595415)
Research Paper : [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18591131.svg)](https://doi.org/10.5281/zenodo.18591131)

This repository contains the official implementation of the research paper: **"A Novel Hybrid Deep Learning Model using U-net and Vision Transformer for Polyp Segmentation in medical imaging"**.

## 📌 Abstract
Early detection of polyps is critical for colorectal cancer prevention. We propose a hybrid architecture that integrates **U-Net** as an encoder for local feature extraction and **Vision Transformer (ViT)** as a bottleneck module for global contextual information. The model is trained on the multicenter **PolypDB** dataset.

## 🚀 Key Features
- **Hybrid Architecture:** Combines CNN's spatial inductive bias with Transformer's global attention.
- **Data Augmentation:** Robust preprocessing including rotations and flips to improve generalization.
- **High Performance:** Achieved an **IoU score of 0.966** with pretrained weights.

## 🛠 Methodology
The model utilizes a compound loss function:
$$Loss = DiceLoss + BinaryCrossEntropyLoss$$

1. **Encoder (U-Net):** Extracts fine-grained local features.
2. **Bottleneck (ViT):** Captures long-range dependencies.
3. **Decoder:** Refines segmentation through skip connections.

## 📂 Dataset
The study uses **PolypDB**, which includes 3,934 images from multiple modalities (BLI, FICE, LCI, NBI, WLI) and centers in Norway, Sweden, and Vietnam.

## 📊 Results
| Configuration | IoU Score |
| :--- | :--- |
| **Hybrid Model (Pretrained + Augmentation)** | **0.966** |
| Hybrid Model (Custom Weight) | 0.802 |
| Hybrid Model (Base) | 0.771 |

## 💻 How to Run
1. **Clone the repository:**
   ```bash
   git clone [https://github.com/prityd825/Polyp-Segmentation.git](https://github.com/prityd825/Polyp-Segmentation.git)
