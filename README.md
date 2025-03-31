# Polyp-Segmentation
Polyp Segmentation using a Hybrid Model U-net and Vision Transfer in medical Imaging  

# Introduction: 
Medical image segmentation is a crucial task in medical diagnosis, particularly for detecting polyps in colonoscopy images. This project integrates UNet (a CNN-based segmentation model) with Vision Transformer (ViT) to improve feature extraction and segmentation accuracy. The methodology involves data preprocessing, augmentation, feature extraction, model training, and evaluation.

# About Dataset: 
PolypDB is a large-scale, multi-center, and multi-modality dataset designed for the development of advanced AI algorithms in colonoscopy. The dataset comprises 3,934 polyp images from various imaging modalities and medical centers, offering a rich resource for research in polyp detection and segmentation.

PolypDB addresses the critical need for robust and generalizable data for developing computer-aided diagnosis (CAD) systems. 

# Features
Multi-Modality Data: Includes images from BLI, FICE, LCI, NBI, and WLI modalities.
Multi-Center Data: Sourced from three medical centers in Norway, Sweden, and Vietnam.
High-Quality Annotations: Verified by a team of 10 gastroenterologists with over 10 years of experience.

# Methodology :
## Data Preprocessing:
### Dataset: 
The dataset consists of colonoscopy images and their corresponding segmentation masks (which highlight the polyp regions).
The dataset is divided into:
1.80% Training Data
2.20% Testing Data

### Data Augmentation (augment_data function)
To improve the model's ability to generalize, the images and masks undergo the following augmentations:
1.Horizontal Flip → Flips images left-right.
2.Vertical Flip → Flips images upside-down.
3.Rotation → Randomly rotates images up to 45°.
Each image and mask is resized to 224×224 pixels, ensuring consistency for the model input.

After augmenting data: 

100%|██████████| 2870/2870 [02:24<00:00, 19.83it/s]
100%|██████████| 718/718 [00:17<00:00, 40.49it/s]



