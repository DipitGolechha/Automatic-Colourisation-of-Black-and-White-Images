# Automatic Colorization of Black and White Images

### Deep Learning Project  
By Devansh Upadhyaya, Dipit Golechha, Krishnav Mahansaria, Vardan Vij, and Yashvi Maheshwari  

---

## Overview
This project presents a **deep learning-based approach** for **automatic colorization of grayscale images**. The model generates realistic, vibrant, and contextually coherent colorizations without human intervention.  
Applications include **photo restoration**, **media enhancement**, and **digital forensics**.

---

## Key Objectives
- Produce visually realistic and vibrant image colorizations  
- Maintain **spatial consistency** and **semantic alignment**  
- Optimize model performance using advanced loss metrics  

---

## Core Challenges
- Preserving spatial coherence across complex scenes  
- Understanding global semantic context within images  
- Mapping grayscale inputs to consistent and contextually correct color palettes  

---

## Dataset
- Source: **ImageNet**
- Total Images: **10,000** (80% training, 20% validation)
- Image Size: **256 × 256 pixels**
- Preprocessing:  
  - Converted to **CIE Lab** color space  
  - `L` channel (lightness) used as input  
  - `a`, `b` color channels used as ground truth  
  - Normalization to range **[-1, 1]**  
  - Standard data augmentation with random horizontal flips  

---

## Model Architectures

### Model 1: Baseline UNet + PatchGAN
- **Generator:** UNet predicting `a` and `b` channels from `L` input  
- **Discriminator:** PatchGAN — distinguishes real from generated colorizations  
- **Loss Functions:**  
  - `L1 Loss` for pixel-level accuracy  
  - `GAN Loss` for perceptual realism  

### Model 2: Enhanced Conditional GAN
- **Generator:** UNet enhanced with:
  - **Multiscale inputs** (original, half-res, and double-res grayscale)  
  - **Self-attention layers** for spatial consistency  
  - **ResNet-18** semantic features to incorporate global context  
- **Discriminator:** Conditional PatchGAN with semantic conditioning inputs  
- **Loss Functions:** Combined `GAN + L1` losses with tuned weights  

---

## Key Features
- **Multiscale Inputs:** Captures both local textures and global semantics  
- **Self-Attention Mechanisms:** Enables color continuity across image regions  
- **Semantic Conditioning:** Aligns colorization with object-specific cues using ResNet features  

---

## Training Workflow
1. **Pre-train the generator** using only L1 loss to stabilize early learning  
2. **Adversarial training** — alternate optimization of generator and discriminator  
3. **Evaluation and checkpoint saving** — log training metrics and save best weights  

---

## Evaluation Metrics

| Metric | Definition | Goal |
|:-------|:------------|:----|
| **MSE** | Mean Squared Error – measures pixel-wise difference | Lower is better |
| **PSNR** | Peak Signal-to-Noise Ratio – evaluates image quality | Higher is better |
| **SSIM** | Structural Similarity Index – measures structural fidelity | Closer to 1 is better |
| **FID** | Frechet Inception Distance – evaluates perceptual realism | Lower is better |

---

## Results

| Metric | Model 1 | Model 2 |
|:------|:--------:|:--------:|
| **MSE** | 0.0060 | **0.0053** |
| **PSNR (dB)** | 23.78 | **23.85** |
| **SSIM** | 0.9108 | **0.9224** |
| **FID** | **34.41** | 36.33 |

Model 2 achieved superior perceptual and structural consistency, balancing vividness and realism, with marginally better quantitative metrics.

---

## Limitations
- Training limited to 10,000 images due to GPU constraints  
- Pretrained ResNet features depend on semantic correctness of ImageNet labels  
- Evaluation metrics (MSE, PSNR, SSIM) fail to capture subjective color realism  

---

## Conclusion
The **Enhanced Conditional GAN** demonstrates significant improvement in output vibrancy, consistency, and semantic alignment over baseline models.  
Model 2 is **recommended** for producing the most realistic and context-aware colorizations.

---

## References
1. Isola, P., Zhu, J. Y., Zhou, T., & Efros, A. A. (2017). *Image-to-Image Translation with Conditional Adversarial Networks*.  
2. Zhang, R., Isola, P., & Efros, A. A. (2016). *Colorful Image Colorization*.  
3. Sarapu, R., Viswanadam, A., Devulapally, S., Nenavath, H., & Ashwini, K. (2020). *Automatic Colorization of Black and White Images Using CNNs*.  

---
