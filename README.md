# 👣 Feasibility of Augmenting Gait Analysis with Machine Learning Models

This repository contains the complete code, documentation, and experimental results from the M.Tech thesis project by **Tejas Doypare** at the **Indian Institute of Science (IISc), Bangalore**. The goal is to demonstrate that low-cost, vision-only systems can be used with machine learning models to estimate **Center of Pressure (CoP)** for gait analysis as an affordable and portable alternative to clinical systems like GAITRite.

---

## 🎯 Project Objectives

- Develop a **vision-based gait analysis system** using RGB cameras and pose estimation.
- Perform **spatial registration** of camera-based pose landmarks with real-world CoP coordinates.
- Create a dataset using **interpolation and augmentation** of static frames.
- Train and compare multiple models for CoP prediction:
  - Classical ML: Linear Regression, Random Forest, AdaBoost, MLP
  - Deep Sequence Models: LSTM, Seq2Seq
  - Hybrid: Retrieval-Augmented Generation (RAG)
- Evaluate model accuracy using **Mean Squared Error (MSE)** and visualize performance.

---

## 📆 System Overview

- **Sensors**: 2 RGB Cameras + GAITRite Pressure Mat  
- **Software**: MediaPipe Pose Estimation, PyTorch, OpenCV, FAISS, Transformers  
- **Pipeline**:
  - Extract 33 joint landmarks with MediaPipe
  - Register them to CoP using SVD-based affine transformation
  - Interpolate sparse sequences for continuity
  - Train ML models to predict CoP

---

## 📅 Dataset Overview

- **Input**: 27-dimensional pose vectors (x, y, z) from 9 key joints
- **Output**: CoP (X, Y) trajectory in cm
- **Steps**:
  - 7 valid footstep sequences used (obj1 to obj7)
  - Interpolation used to simulate video-like continuity
  - Sequence models trained with input: [obj1, obj2] → output: obj3 CoP

---

## 📊 Models Implemented

### ✅ Classical Models

- **Linear Regression**
- **Random Forest**
- **AdaBoost**
- **Multilayer Perceptron (MLP)**

### ⏱️ Sequential Models

- **LSTM**: Long-term gait dynamics
- **Seq2Seq**: Encoder-decoder architecture for trajectory prediction

### 🛠️ Retrieval-Augmented Generation (RAG)

- Uses BERT-based embedding and FAISS vectorstore
- Retrieves relevant past sequences to assist CoP prediction

---

## 🔹 Pipeline Summary

1. Data collection via RGB cameras and GAITRite
2. Pose extraction using MediaPipe
3. Affine registration (SVD-based)
4. Interpolation for sequence generation
5. Standardization with `StandardScaler`
6. Model training with PyTorch
7. Evaluation using RMSE and visual plots

---

## 📈 Results Summary

| Model         | RMSE (cm) | Description                         |
|---------------|-----------|-------------------------------------|
| Linear Reg.   | ~5.1      | Simple baseline                     |
| Random Forest | ~3.5      | Ensemble method                     |
| MLP           | ~3.8      | Captures nonlinear spatial relations|
| LSTM          | ~0.85     | Captures time-series dynamics       |
| Seq2Seq       | ~0.50     | Best performance                    |
| RAG           | ~0.45     | Contextual retrieval + sequence gen |

> The Seq2Seq model and RAG retrieval achieved sub-centimeter RMSE, outperforming traditional models.

---

## 🌄 Visualizations

- CoP trajectory comparisons
- Loss vs Epochs (LSTM, Seq2Seq)
- Affine registration plots
- Sequence interpolation visualization

All visual results are stored in the `/figures/` folder.

---

## 🌐 Repository Structure

```bash
.
├── data/              # Raw and processed input data
├── src/               # Core model and training code
├── notebooks/         # Jupyter notebooks
├── utils/             # Helper functions
├── figures/           # Plots and results
├── report/            # Thesis PDF
└── README.md

