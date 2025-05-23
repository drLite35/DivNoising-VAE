# 📊 DivNoising: Unsupervised Image Denoising with Variational Autoencoders

![DivNoising](https://img.shields.io/badge/Method-Unsupervised-blue) ![VAE](https://img.shields.io/badge/Model-Variational%20Autoencoder-important)

---

## 📌 Overview

This repository presents a **paper presentation and implementation overview of _DivNoising_**, a novel unsupervised image denoising approach based on **fully convolutional Variational Autoencoders (VAEs)**. Unlike conventional restoration methods, _DivNoising_ models the inherent uncertainty in image restoration by generating multiple plausible clean images, explicitly incorporating noise models into its decoding process.

---

## 🎥 Presentation Details

**Title:** _DivNoising: Diversity Denoising via Variational Autoencoders_  
**Course:** Deep Learning Paper Presentation  
**Presented by:**

- Meghana S Seshasai  
- Anurag Singh  
- Ankita Vaishnobi Bisoi  
- Tanishq Jain  
- Chandrika Singh Jadon  
- Advay Burte  

---

## 📖 Abstract

Image denoising traditionally attempts to map noisy images to their clean counterparts — a fundamentally ill-posed task, since multiple clean images could result in the same noisy observation. **DivNoising** addresses this by generating a **distribution of potential clean images**, integrating learned or measured noise models directly within the decoder of a VAE.

---

## 📝 Paper Summary

- **Task:** Unsupervised Image Restoration (denoising without clean data)
- **Approach:** Modifies standard VAEs by replacing pixel-wise Gaussian output with explicit noise models.
- **Noise Models:** 
  - GMM-based for microscopy images.
  - Known models for synthetic datasets.
  - Learned models for specific datasets like W2S.

---

## 📊 Datasets & Setup

- **13 diverse datasets**:
  - **9 microscopy datasets** (e.g., Convallaria, Mouse actin)
  - **4 synthetic noise datasets**
- Benchmarked against:
  - **Supervised:** CARE
  - **Unsupervised:** NOISE2VOID, PN2V, Deep Image Prior, SELF2SELF
- **Networks:** Fully convolutional VAE (200k - 713k parameters)
- **Training:**
  - Optimizer: ADAM
  - Batch Size: 1–4
  - Data Augmentation: 8-fold
  - Epochs: 200
  - Learning Rate: 0.001 (decayed by factor of 0.5 on plateau)

---

## 📈 Results

- Outperforms **SELF2SELF** while using **7× less GPU memory**
- Comparable to supervised **CARE** in many cases — despite not requiring clean data
- Demonstrates robust performance on both synthetic and real-world microscopy datasets (e.g., W2S, DenoiSeg Flywing, BSD68)
- Achieves state-of-the-art unsupervised denoising performance

| Method       | Requires Clean Data | GPU Memory | PSNR Performance |
|--------------|:-------------------|:-----------|:----------------|
| CARE         | ✅                  | High        | Best            |
| SELF2SELF    | ❌                  | High        | Good            |
| DivNoising   | ❌                  | Low         | Excellent        |

---

## 📌 Conclusion

**DivNoising** provides a principled unsupervised image denoising framework by:
- Modeling imaging noise directly in the decoder.
- Capturing uncertainty in image restoration.
- Generating diverse, plausible clean images.
- Delivering performance close to or better than existing unsupervised approaches with reduced computational overhead.

---

## 📄 Reference

**Official Paper:** [DivNoising: Diversity Denoising via Variational Autoencoders](https://github.com/juglab/DivNoising)

---

## 🔬 Examples

This repository includes Jupyter notebooks demonstrating DivNoising on real microscopy data:

### Convallaria Dataset
- **0a-CreateNoiseModel**: Create a GMM noise model with calibration data
- **1-Training**: Train a DivNoising VAE model on Convallaria images
- **2-Prediction**: Generate multiple plausible denoised images

Try it yourself on Google Colab: [Convallaria DivNoising Example](https://colab.research.google.com/drive/1z6qL7erw4OP85Xmu5YZ_kGApMyO7n2Dz?usp=sharing#scrollTo=sCZYSeyaZrZc)

### Mouse Nuclei Dataset
- **0a-CreateNoiseModel**: Adapt the noise model for Mouse Nuclei images
- **1-Training**: Train a dedicated model for the Mouse Nuclei dataset
- **2-Prediction**: Apply the model to denoise nuclei images

Try it yourself on Google Colab: [Mouse Nuclei DivNoising Example](https://colab.research.google.com/drive/1vP3v7ozIa1_5jc8e6Co-No_htVz31gW0?authuser=0#scrollTo=th13RS9FM0Tj)

Navigate to the `examples/` directory to access these notebooks and run them with your own data.

---

## 📂 Structure

```bash
.
├── divnoising/              # Core implementation code
├── examples/                # Example notebooks for different datasets
│   ├── Convallaria/         # Convallaria plant cell examples
│   └── Mouse_nuclei/        # Mouse nuclei microscopy examples
├── nets/                    # Neural network architectures
├── presentation.pdf         # Paper presentation slides/report
├── README.md                # This file
├── requirements.txt         # Python dependencies
└── DivNoising.yml           # Conda environment specification
