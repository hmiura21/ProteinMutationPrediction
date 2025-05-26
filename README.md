# Predicting Functional Effects of Protein Mutations using ESM2 and Active Learning

This project focuses on predicting the functional effects of single-point protein mutations—a key challenge in computational biology with applications in drug discovery, protein engineering, and synthetic biology. Experimental methods such as Deep Mutational Scanning (DMS) can measure these effects but are costly and time-consuming. We address this by building a machine learning model using **ESM2** and **parameter-efficient fine-tuning via LoRA**, combined with an **active learning** querying framework to optimize performance with limited labeled data.

## 💡 Project Goal

Our goal was to develop an accurate and efficient model that predicts DMS scores for single-point mutations of a protein and to recommend the top 10 beneficial mutations that maximize fitness.

---

## 🔍 Problem Setup

- We focused solely on **single-site substitutions**.
- For a protein of length *L*, the number of all possible single-site mutants is **19×L**.
- The challenge was approached as a **simulated active learning scenario**, starting with 10% of experimental data and enabling 3 rounds of query selection.

---

## 🏗️ Model Architecture

- **Base Model**: [ESM2](https://huggingface.co/facebook/esm2_t33_650M_UR50D) (33 layers, 650M parameters).
- **Fine-Tuning**: Implemented with [LoRA](https://arxiv.org/abs/2106.09685), modifying only `q_proj` and `v_proj` with:
  - `rank=4`
  - `alpha=16`
  - `dropout=0.1`
- **Head**: A repurposed `RobertaLMHead` used for regression.

```bash
Loss Function: Mean Squared Error (MSE)
Optimizer: Adam
Learning Rate: 9e-5
Batch Size: 16
Epochs: 25
```
---

## 📁 Repository Structure



