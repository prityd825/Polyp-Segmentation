# A Novel Hybrid Deep Learning Model using U-net and Vision Transformer for Polyp Segmentation in medical imaging

**A hybrid deep learning approach combining CNN-based local feature extraction and Vision Transformer-based global contextual modeling for colorectal polyp segmentation.**

## Overview

This research explores a hybrid CNN–Vision Transformer architecture for binary colorectal polyp segmentation using the multi-center PolypDB dataset.

The proposed model integrates:
- **CNN Encoder:** Extracts hierarchical local visual features.
- **Vision Transformer (ViT-B/16):** Captures global contextual information using pretrained weights.
- **Feature Fusion:** Combines CNN and Transformer representations.
- **CNN Decoder:** Reconstructs segmentation masks using skip connections.

## Dataset

Experiments use the Multi-Center PolypDB dataset.

| Modality | Images |
|---|---:|
| BLI | 70 |
| FICE | 70 |
| LCI | 60 |
| NBI | 146 |
| WLI | 3,588 |
| **Total** | **3,934** |

**Preprocessing:**
- Image resizing: 224 × 224
- ImageNet normalization
- Binary mask generation using threshold 128
- Training augmentation: horizontal flipping and random rotation

## Model Architecture

| Component | Configuration |
|---|---|
| CNN Encoder | 32, 64, 128, 256, 384 channels |
| Transformer | Pretrained ViT-B/16 |
| Transformer Features | 768 channels, 14 × 14 |
| Feature Projection | 768 → 256 channels |
| Feature Fusion | 384 + 256 → 640 → 384 channels |
| Decoder | CNN decoder with skip connections |
| Output | Binary segmentation mask |

**Model Parameters:**
- Total: 95,763,329
- Trainable: 9,964,673
- Frozen: 85,798,656

## Training Configuration

| Parameter | Setting |
|---|---|
| Framework | PyTorch |
| Optimizer | AdamW |
| Learning Rate | 1e-4 |
| Weight Decay | 1e-4 |
| Loss | 0.5 Dice + 0.5 BCE |
| Maximum Epochs | 30 |
| Early Stopping | Patience 7 |
| Input Size | 224 × 224 |

## Experimental Results

Preliminary evaluation on the current 617-image test set:

| Metric | U-Net Baseline | Hybrid CNN–ViT |
|---|---:|---:|
| Dice | 0.8014 | **0.8403** |
| IoU | 0.7258 | **0.7768** |
| Precision | 0.8562 | **0.9043** |
| Recall | 0.8342 | **0.8472** |

**Modality-wise Dice Score**

| Modality | U-Net | Hybrid CNN–ViT |
|---|---:|---:|
| BLI | 0.4824 | **0.7554** |
| FICE | 0.7759 | **0.9464** |
| LCI | 0.8815 | **0.9494** |
| NBI | 0.6111 | **0.7076** |
| WLI | 0.8195 | **0.8403** |

**Important evaluation note:** The original hybrid and current U-Net experiments used different data splits. The original hybrid training split has not yet been fully audited against the current test set. Therefore, these results are exploratory and should not be interpreted as a definitive unbiased comparison.

## Research Resources

- **Research Paper:** https://zenodo.org/records/23702821
- **Code:** https://doi.org/10.5281/zenodo.18595415
- **Dataset:** https://doi.org/10.5281/zenodo.18633877
- **GitHub:** https://github.com/prityd825/Polyp-Segmentation

## Author

**Prity Rani Das**  
B.Sc. in Software Engineering  
Noakhali Science and Technology University, Bangladesh

**Research Interests:** Medical Image Analysis, Deep Learning, Computer Vision, and Biomedical Image Segmentation.

---

*This project is intended for academic research and is not a clinically validated diagnostic system.*
