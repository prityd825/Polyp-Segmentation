# 🏥 Polyp Segmentation: Hybrid U-Net and Vision Transformer (ViT)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Research Paper](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.18591131-blue)](https://doi.org/10.5281/zenodo.18591131)
[![Code DOI](https://img.shields.io/badge/Code-Zenodo-green)](https://doi.org/10.5281/zenodo.18595415)
[![Dataset](https://img.shields.io/badge/Data-Zenodo-lightgrey)](https://doi.org/10.5281/zenodo.18633877)
![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat\&logo=pytorch\&logoColor=white)

> **A Hybrid Deep Learning Framework Combining U-Net-Style Convolutional Learning and Vision Transformer-Based Global Feature Modeling for Polyp Segmentation**

This repository contains the implementation and experimental results associated with the research work:

**“A Novel Hybrid Deep Learning Model using U-Net and Vision Transformer for Polyp Segmentation in Medical Imaging.”**

---

## 📌 Overview

Accurate polyp segmentation is an important task in computer-aided medical image analysis and may support the early identification of abnormalities associated with colorectal cancer.

This project investigates a **hybrid CNN–Transformer architecture** for binary polyp segmentation. The model combines:

* A **U-Net-style convolutional encoder** for hierarchical local feature extraction
* A **Vision Transformer (ViT)** component for global feature modeling
* A decoder with **skip connections** for reconstructing the segmentation mask

The project evaluates multiple experimental configurations to investigate the effect of **pretrained initialization and different weight/training configurations** on segmentation performance.

The model is optimized using a combined **Dice Loss + Binary Cross-Entropy Loss** objective and evaluated primarily using the **Intersection over Union (IoU)** metric.

---

# 🎯 Research Motivation

Convolutional neural networks are effective at learning local spatial patterns, while Transformer-based architectures can model longer-range relationships between image regions.

This project investigates whether combining these two approaches can improve polyp segmentation performance.

The main research questions include:

1. Can a hybrid U-Net–Transformer architecture effectively segment colorectal polyps?
2. How does pretrained initialization affect segmentation performance?
3. How does the hybrid model perform under different experimental configurations?

---

# ✨ Key Features

* 🧠 Hybrid CNN–Transformer segmentation architecture
* 🏗️ Custom U-Net-style encoder and decoder
* 🔍 Vision Transformer (ViT) for global feature modeling
* 🔗 Skip connections between encoder and decoder stages
* ⚖️ Combined Dice + Binary Cross-Entropy Loss
* 🔄 Training-time data augmentation
* 📏 Standardized input resolution of `224 × 224`
* 📊 IoU-based evaluation
* 🖼️ Input, ground-truth, and predicted mask visualization
* 🧪 Comparison of pretrained and non-pretrained configurations

---

# 🏗️ Model Architecture

The proposed model follows an **Encoder → Transformer → Decoder** design.

```text
Input Image
(3 × 224 × 224)
        │
        ▼
┌─────────────────────────┐
│ U-Net-Style CNN Encoder │
│ Local Feature Extraction│
└────────────┬────────────┘
             │
             ▼
      Deep Feature Map
             │
             ▼
      Feature Projection
             │
             ▼
┌─────────────────────────┐
│ Vision Transformer (ViT)│
│ Global Feature Modeling │
└────────────┬────────────┘
             │
             ▼
     Feature Projection
             │
             ▼
┌─────────────────────────┐
│ Decoder + Skip          │
│ Connections             │
└────────────┬────────────┘
             │
             ▼
      Segmentation Output
             │
             ▼
      Binary Polyp Mask
```

## 🔬 Architecture Components

### 1. U-Net-Style Encoder

The convolutional encoder extracts hierarchical spatial features from the input image through multiple convolutional stages.

The encoder features are preserved and later incorporated into the decoder through **skip connections**, helping the model recover fine spatial details.

### 2. Vision Transformer

The deep feature representation is processed by a Vision Transformer component to model broader contextual relationships.

The project includes experiments with both:

* **Pretrained Transformer initialization**
* **Training without pretrained Transformer weights**

### 3. Decoder

The decoder progressively reconstructs the spatial representation using upsampling and encoder skip connections.

The final layer produces a binary segmentation output representing the predicted polyp region.

---

# ⚖️ Loss Function

The model is trained using a compound loss function:

$$
\mathcal{L}_{Total} =
\mathcal{L}_{Dice} +
\mathcal{L}_{BCE}
$$

## Dice Loss

Dice Loss encourages strong overlap between the predicted segmentation region and the ground-truth mask.

## Binary Cross-Entropy Loss

Binary Cross-Entropy provides pixel-level supervision for foreground and background classification.

Combining these losses helps optimize both **regional overlap** and **pixel-wise segmentation accuracy**.

---

# 📂 Dataset

The experiments use the **PolypDB dataset**, containing colonoscopy images and corresponding segmentation masks.

The project supports experiments on the available dataset modality structure and pairs each image with its corresponding ground-truth mask.

For the notebook configuration reviewed in this project, the data is split into training and test sets using a fixed random seed.

> **Note:** Dataset usage and modality configuration may vary between experimental notebooks. The exact dataset paths and experimental settings should be checked in each notebook.

---

# 🔄 Data Augmentation

Data augmentation is applied during training to increase data diversity and improve generalization.

The augmentation pipeline includes transformations such as:

* Horizontal flipping
* Vertical flipping
* Rotation

Images and masks are resized to:

```text
224 × 224
```

The evaluation/test data is processed without random augmentation.

---

# ⚙️ Training Configuration

The implementation uses PyTorch-based training with the following core configuration:

| Parameter        | Configuration        |
| ---------------- | -------------------- |
| Input Resolution | `224 × 224`          |
| Optimizer        | Adam                 |
| Learning Rate    | `1e-4`               |
| Loss Function    | Dice Loss + BCE Loss |
| Training Epochs  | 20                   |
| Primary Metric   | IoU                  |
| Random Seed      | 42                   |

The model uses GPU acceleration when CUDA is available.

---

# 📊 Experimental Results

The project includes multiple experiments investigating the effect of pretrained initialization and different model configurations.

| Model Configuration                              | IoU Score |
| ------------------------------------------------ | --------: |
| **Hybrid Model (Pretrained ViT + Augmentation)** | **0.966** |
| Hybrid Model (Custom Weight Configuration)       |     0.802 |
| Hybrid Model (Without Pretrained Weights / Base) |     0.771 |

## 🏆 Best Result

The strongest reported configuration was:

> **Hybrid U-Net–ViT with pretrained ViT initialization and data augmentation**, achieving an **IoU score of 0.966**.

### Experimental Observation

The results suggest that the pretrained configuration substantially outperformed the base configuration in these experiments.

However, the results should be interpreted within the context of the specific dataset split, preprocessing, augmentation, and training configuration used in each experiment.

> ⚠️ For a scientifically fair comparison, the same evaluation protocol and test split should be used when comparing configurations.

---

# 📈 Evaluation

The primary segmentation evaluation metric is **Intersection over Union (IoU)**.

IoU measures the overlap between the predicted mask and the ground-truth mask:

$$
IoU =
\frac{|Prediction \cap GroundTruth|}
{|Prediction \cup GroundTruth|}
$$

Predicted probability maps are converted into binary masks using a segmentation threshold before calculating overlap.

The project also provides qualitative visualization of:

* 🖼️ Original input image
* 🎯 Ground-truth segmentation mask
* 🧠 Predicted segmentation mask

This allows visual inspection alongside quantitative IoU evaluation.

---

# 🖼️ Qualitative Prediction Visualization

The notebooks include visualization utilities for examining segmentation results.

```text
Input Image
     │
     ├──────────────► Ground-Truth Mask
     │
     ▼
Hybrid U-Net–ViT Model
     │
     ▼
Predicted Probability Map
     │
     ▼
Binary Predicted Mask
```

These visualizations help examine where the model successfully segments the polyp and where prediction errors may occur.

---

# 🧪 Experimental Configurations

The repository contains experiments exploring different initialization and training configurations.

### 🔹 Pretrained Configuration

The pretrained experiment uses pretrained initialization for the Transformer component and includes data augmentation.

**Reported IoU:** **0.966**

### 🔹 Custom Weight Configuration

This experiment represents a separate configuration using the custom weight/training setup implemented in its corresponding notebook.

**Reported IoU:** **0.802**

> The exact meaning of “Custom Weight” should remain consistent with the implementation in the corresponding notebook.

### 🔹 Base / Without Pretrained Weights

This configuration initializes the model without pretrained Transformer weights.

**Reported IoU:** **0.771**

---

# 🚀 How to Run

This repository follows a **notebook-based research workflow**.

1. Clone the repository.
2. Install the required dependencies.
3. Configure the dataset paths in the notebook.
4. Select the experiment you want to reproduce.
5. Run the notebook cells in order.
6. Train or load the corresponding model configuration.
7. Evaluate the model using IoU.
8. Visualize predicted segmentation masks.

The experiment notebooks should be run independently because different notebooks may use different initialization or training configurations.

---

# 📁 Repository Structure

```text
Polyp-Segmentation/
│
├── polyp-segmentation-with-pretrained.ipynb
│   └── Hybrid U-Net–ViT experiment using pretrained
│       Transformer initialization and augmentation
│
├── polyp-segmentation-without-pretrain.ipynb
│   └── Hybrid U-Net–ViT experiment without
│       pretrained Transformer weights
│
├── polyp-segmentation-with-custom-weight.ipynb
│   └── Hybrid model experiment with the custom
│       weight/training configuration
│
├── README.md
│   └── Project documentation
│
└── Additional experiment files
    └── Model configurations, results, and visualizations
```

> **Note:** This repository is intentionally organized as a notebook-based research project. Each notebook may represent a separate experiment and should be interpreted according to its own configuration.

---

# 🛠️ Technologies Used

* Python
* PyTorch
* Torchvision
* Vision Transformer (ViT)
* OpenCV
* Albumentations
* NumPy
* Scikit-learn
* Matplotlib
* ImageIO

---

# ⚠️ Limitations

This project is an experimental research implementation and has several limitations:

* Results may depend on the dataset split and random seed.
* Different experimental configurations should ideally be evaluated under identical conditions for a direct comparison.
* External validation on independent datasets has not yet been established.
* The model is not clinically validated.
* High experimental IoU does not guarantee real-world clinical performance.

---

# 🚧 Future Improvements

* [ ] Evaluate all configurations using the same fixed test set
* [ ] Perform cross-validation
* [ ] Add Dice Score alongside IoU
* [ ] Add Precision, Recall, and F1-score for segmentation
* [ ] Compare against standard U-Net and U-Net++ baselines
* [ ] Evaluate across additional PolypDB modalities
* [ ] Add external dataset validation
* [ ] Add attention-based visualization
* [ ] Investigate more efficient Transformer architectures
* [ ] Add model checkpointing and early stopping
* [ ] Perform statistical significance testing between configurations

---

# 👩‍💻 Author

**Prity Rani Das**

* **GitHub:** https://github.com/prityd825

---

# 📚 Citation

If you use this work, please consider citing the associated research paper, code, and dataset:

* **Research Paper:** https://doi.org/10.5281/zenodo.18591131
* **Code:** https://doi.org/10.5281/zenodo.18595415
* **Dataset:** https://doi.org/10.5281/zenodo.18633877

---
# 📄 Research Disclaimer

This repository is intended for **research and educational purposes only**.

The model is **not a clinical diagnostic system** and should not be used for real-world medical diagnosis or treatment decisions without additional clinical validation and regulatory evaluation.


⭐ **If you find this project useful, please consider giving the repository a star!**
