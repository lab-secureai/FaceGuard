# FaceGuard: Proactive Identity Perturbation for Protecting Facial Images Against Deepfake Face-Swapping

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)]()
[![PyTorch](https://img.shields.io/badge/PyTorch-2.x-red.svg)]()
[![License](https://img.shields.io/badge/License-MIT-green.svg)]()

Official implementation of **FaceGuard**, a proactive facial image protection framework that reduces identity transfer in deepfake face-swapping by applying bounded identity-space adversarial perturbations.

> **Paper:** FaceGuard: Proactive Identity Perturbation for Protecting Facial Images Against Deepfake Face-Swapping

---

# Overview

Deepfake face-swapping systems can synthesize realistic fake images by extracting the identity representation from a publicly available facial image. Instead of detecting fake images after generation, **FaceGuard** protects facial images **before publication** by introducing an imperceptible perturbation that disrupts identity extraction.

Unlike traditional adversarial attacks, FaceGuard is designed as a **proactive privacy protection method**:

- preserves human visual perception;
- disrupts machine identity extraction;
- reduces source identity transfer in face-swapping models.

---

# Pipeline

```
Source Image
      │
      ▼
Face Detection & Alignment
      │
      ▼
Identity Encoder (ArcFace)
      │
      ▼
Masked PGD Optimization
      │
      ▼
Protected Source Image
      │
      ▼
Face-Swapping Model (InSwapper)
      │
      ▼
Protected Fake Output
```

---

# Features

- Identity-space adversarial perturbation
- Facial-mask constrained optimization
- Projected Gradient Descent (PGD)
- InsightFace InSwapper evaluation
- Quantitative and qualitative evaluation
- PSNR / SSIM / LPIPS evaluation
- Attack Success Rate (ASR)
- Protection Success Rate (PSR)

---

# Experimental Results

| Metric | No Defense | FaceGuard |
|---------|------------|-----------|
| Identity Similarity | 0.4761 | **0.0003** |
| Identity Distance | 0.5239 | **0.9997** |
| Attack Success Rate | 44.15% | **0.20%** |
| Protection Success Rate | — | **99.80%** |
| Source PSNR | — | 36.44 |
| Source SSIM | — | 0.948 |
| Source LPIPS | — | 0.037 |

Attack reduction:

```
44.15%  →  0.20%

Reduction = 99.54%
```

---

# Qualitative Example

The protected image remains visually similar to the original image.

However, after face-swapping, the generated fake is **no longer recognized as the original source identity by the face recognition model**, which is the primary objective of FaceGuard.

```
Original Source
        │
        ▼
Protected Source
        │
        ▼
FaceSwap
        │
        ▼
Looks Similar to Humans ✓
Different Identity for AI ✓
```

---

# Repository Structure

```
FaceGuard/
│
├── notebook/
│     Deepfake_Protective.ipynb
│
├── models/
│
├── data/
│
├── figures/
│
├── outputs/
│
├── README.md
│
└── requirements.txt
```

---

# Installation

```bash
git clone https://github.com/lab-secureai/FaceGuard.git

cd FaceGuard

pip install -r requirements.txt
```

---

# Usage

Launch the notebook:

```bash
jupyter notebook notebook/Deepfake_Protective.ipynb
```

or

```bash
python main.py
```

(if a standalone script is provided)

---

# Evaluation

The evaluation protocol compares two settings.

### No Defense

```
Source Image
        ↓
FaceSwap
        ↓
Generated Fake
```

### FaceGuard

```
Source Image
        ↓
FaceGuard
        ↓
Protected Source
        ↓
FaceSwap
        ↓
Protected Fake
```

Identity similarity is computed using cosine similarity between the source identity embedding and the generated fake embedding.

---

# Citation

If you find this work useful, please cite:

```bibtex
@inproceedings{faceguard2026,
  title={FaceGuard: Proactive Identity Perturbation for Protecting Facial Images Against Deepfake Face-Swapping},
  author={Hoang Phuc Dang, Anh Tu Tran},
  booktitle={VCRIS},
  year={2026}
}
```

---

# License

MIT License

---

# Acknowledgements

This project uses:

- InsightFace
- ArcFace
- InSwapper
- PyTorch

---

# Disclaimer

FaceGuard is intended **solely for privacy protection and academic research**.

The proposed method is designed to reduce the risk of unauthorized identity transfer in deepfake face-swapping systems. It should not be interpreted as providing absolute protection against all deepfake attacks.
