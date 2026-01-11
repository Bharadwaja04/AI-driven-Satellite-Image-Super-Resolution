# 🛰️ AI-Based Satellite Image Super-Resolution using SRCNN

## 📌 Overview

Satellite imagery is essential for applications such as environmental monitoring, agriculture analysis, disaster response, and urban planning. However, acquiring high-resolution satellite images is often limited by sensor capabilities, cost, and revisit frequency.

This project demonstrates an **AI-based super-resolution pipeline** that enhances **10-meter resolution satellite images** to **5-meter resolution** using a **Super-Resolution Convolutional Neural Network (SRCNN)**. The model learns a mapping between low-resolution and high-resolution satellite image pairs using real-world multi-sensor data.

---

## 🎯 Objective

Given a low-resolution satellite image (10m), reconstruct a higher-resolution version (5m) that:
- Preserves spatial structures
- Enhances texture and edges
- Improves visual interpretability over traditional interpolation

---

## 📂 Dataset

We use a real-world satellite dataset containing paired images from:

- **Sentinel-2** (10m resolution)
- **VENµS** (5m resolution)

The dataset provides spatially aligned image patches captured over the same geographic regions and dates.

🔗 **Dataset Link:**  
https://zenodo.org/records/6514159

### Selected Bands
The following spectral bands were used:
- **B2** – Blue  
- **B3** – Green  
- **B4** – Red  
- **B8** – Near Infrared  

These bands are commonly used for land cover and vegetation analysis.

### Dataset Statistics
- Total paired samples used: **805**
- Each sample consists of:
  - Low-resolution image (10m)
  - Corresponding high-resolution image (5m)

---

## 🗂️ Dataset Structure

data/
├── LR/ # Low-resolution Sentinel-2 images (10m)
│ ├── patch_0.tif
│ ├── patch_1.tif
│ └── ...
└── HR/ # High-resolution VENµS images (5m)
├── patch_0.tif
├── patch_1.tif
└── ...


Each `LR/patch_i.tif` corresponds exactly to `HR/patch_i.tif`.

---

## 🧠 Methodology

### Model: SRCNN (Super-Resolution CNN)

SRCNN is a classical deep learning architecture designed for image super-resolution. It learns a direct mapping from low-resolution images to high-resolution outputs using convolutional layers.

**Why SRCNN?**
- Simple and interpretable baseline
- Effective for regression-based image enhancement
- Suitable for real satellite imagery
- Avoids unrealistic hallucination of details

---

## 🏗️ Model Architecture

The SRCNN model consists of three convolutional layers:

1. **Feature Extraction** (9×9 kernel)  
2. **Non-linear Mapping** (5×5 kernel + ReLU)  
3. **Reconstruction** (5×5 kernel)  

**Input:**  
4-channel bicubic-upsampled satellite image  

**Output:**  
4-channel super-resolved satellite image  

---

## ⚙️ Training Details

- Framework: **PyTorch**
- Loss Function: **Mean Squared Error (MSE)**
- Optimizer: **Adam**
- Learning Rate: `1e-4`
- Train / Validation Split: `80% / 20%`
- Epochs: `15`

The model is trained to minimize pixel-wise reconstruction error between predicted and ground-truth high-resolution images.

---

## 📊 Evaluation Metrics

To evaluate model performance, the following metrics are used:

- **PSNR (Peak Signal-to-Noise Ratio)**  
  Measures reconstruction quality (higher is better)

- **SSIM (Structural Similarity Index)**  
  Measures structural similarity between images (range: 0–1)

---

## ✅ Results

### Quantitative Results
- **Validation PSNR:** ~32 dB  
- **Validation SSIM:** ~0.90  

These results indicate a clear improvement over simple bicubic upsampling.

### Qualitative Results
Visual comparisons show:
- Sharper edges
- Improved texture detail
- Better preservation of land structures

---

## 🖼️ Visualization

The following outputs are visualized side by side:
1. Bicubic-upsampled low-resolution image
2. SRCNN super-resolved output
3. Ground truth high-resolution image (VENµS)

This comparison highlights the effectiveness of the CNN-based super-resolution approach.

---

## 🚀 How to Run

1. Clone the repository:
   ```bash
   https://github.com/Bharadwaja04/AI-driven-Satellite-Image-Super-Resolution.git
Install dependencies:
  ```bash
  pip install torch rasterio numpy matplotlib scikit-image
```
Place dataset in the required folder structure.

Run the provided Jupyter notebook (StratoHack.ipynb).


# Future Improvements

Deeper architectures (EDSR, RCAN)

Perceptual or adversarial loss (GAN-based SR)

Multi-temporal or multi-sensor fusion

Training on larger datasets

🏁 Conclusion

This project demonstrates that convolutional neural networks can effectively enhance satellite image resolution using real-world multi-sensor data. Even with a simple SRCNN architecture, meaningful improvements in spatial detail and structural preservation are achieved, highlighting the potential of AI-driven super-resolution for Earth observation.
