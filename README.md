# Federated Learning: Fairness and Robustness under Adversarial Attacks

> A comprehensive experimental framework for evaluating fairness-aware and Byzantine-robust federated learning on **real-world** and **synthetic** datasets.

---

## 📖 Table of Contents

- [Overview](#overview)
- [Repository Structure](#repository-structure)
- [Objectives](#objectives)
- [Datasets](#datasets)
- [Federated Learning Setup](#federated-learning-setup)
- [Attack Strategies](#attack-strategies)
- [Defense Strategies](#defense-strategies)
- [Evaluation Metrics](#evaluation-metrics)
- [Experiments](#experiments)
- [Results](#results)
- [Key Findings](#key-findings)
- [Technologies Used](#technologies-used)
- [Future Work](#future-work)

---

# Overview

This repository presents a comprehensive framework for studying **fairness**, **robustness**, and **security** in Federated Learning (FL).

The project evaluates how different adversarial attacks affect both model performance and fairness, while comparing multiple aggregation strategies designed to defend against malicious clients.

Experiments are performed on:

- 📊 **Real Dataset:** UCI Adult Income Dataset
- 🧪 **Synthetic Dataset:** Controlled binary classification dataset

To ensure reproducibility, every experiment is repeated across **three random seeds (42, 100, 999)**, with results reported as **Mean ± Standard Deviation**.

---

# Repository Structure

```text
Federated-Learning-Fairness/
│
├── RealIncomeDataset/
│   ├── RealIncomeDataset.ipynb
│   ├── experiment_results/
│   └── README.md
│
├── SyntheticData/
│   ├── SyntheticData.ipynb
│   ├── experiment_results/
│   └── README.md
│
├── images/
│
└── README.md
```

---

# Objectives

The project investigates:

- Federated learning under non-IID client distributions
- Byzantine robustness against malicious clients
- Fairness-aware aggregation strategies
- Trade-offs between robustness, fairness, and accuracy
- Adaptive adversarial attacks
- Multi-seed reproducibility

---

# Datasets

## 📊 Real Dataset — UCI Adult Income

| Property | Value |
|----------|-------|
| Samples | 48,842 |
| Features | 13 |
| Task | Binary Income Classification |
| Sensitive Attribute | Sex |
| Clients | 6 |
| Distribution | Non-IID |

The dataset is partitioned across six simulated clients with heterogeneous data distributions and injected demographic bias.

---

## 🧪 Synthetic Dataset

Synthetic data is generated using `sklearn.make_classification()`.

| Property | Value |
|----------|-------|
| Samples | 2,000 |
| Features | 10 |
| Task | Binary Classification |
| Sensitive Attribute | Artificial Binary Group |
| Clients | 6 |
| Distribution | Non-IID |

The synthetic dataset provides complete control over demographic bias, making it useful for reproducible fairness experiments.

---

# Federated Learning Setup

| Parameter | Value |
|------------|------|
| Clients | 6 |
| Adversaries | 2 |
| Communication Rounds | 20 |
| Local Epochs | 5 |
| Attack Start | Round 5 |

### Model Architecture

```text
Input
 ↓
Linear (64)
 ↓
ReLU
 ↓
Dropout
 ↓
Linear (32)
 ↓
ReLU
 ↓
Linear (1)
```

---

# Attack Strategies

| Attack | Description |
|---------|-------------|
| **none** | Honest client training |
| **random** | Sends random model weights |
| **label_flip** | Flips labels for part of the sensitive group |
| **gradient_scale** | Amplifies malicious gradients |
| **fairness_poison** | Introduces demographic bias |
| **fairness_spoof** | Appears locally fair while introducing hidden global bias |
| **adaptive** | Evades detection while degrading fairness |

---

# Defense Strategies

| Defense | Description |
|----------|-------------|
| **FedAvg** | Standard Federated Averaging |
| **Median** | Coordinate-wise Median |
| **Trimmed Mean** | Removes extreme updates |
| **Krum** | Byzantine-robust aggregation |
| **Fairness Only** | Fairness-weighted aggregation |
| **Robust Fair** | Trust-based fairness + robustness aggregation |

---

# Evaluation Metrics

The following metrics are recorded during every communication round.

### Performance Metrics

- Accuracy

### Fairness Metrics

- Demographic Parity (DP) Gap
- Equalized Odds (EO) Gap

> Lower DP Gap and EO Gap indicate fairer predictions.

---

# Experiments

Experiments are independently conducted on both datasets.

Each experiment evaluates:

- Different attack strategies
- Different aggregation methods
- Multiple random seeds
- Communication round dynamics

The following attack-defense combinations are included.

| Attack | Defenses Evaluated |
|---------|-------------------|
| None | FedAvg, Median, Fairness Only, Robust Fair |
| Random | FedAvg |
| Label Flip | FedAvg |
| Gradient Scale | FedAvg |
| Fairness Poison | All Defenses |
| Fairness Spoof | FedAvg, Median, Robust Fair |
| Adaptive | FedAvg, Median, Krum, Fairness Only, Robust Fair |

---

# Results

Each dataset produces:

✅ Training Curves

- Accuracy over communication rounds
- Demographic Parity Gap
- Equalized Odds Gap

✅ Multi-Seed Analysis

- Mean ± Standard Deviation Accuracy
- Mean ± Standard Deviation DP Gap
- Cross-seed comparison

✅ Heatmaps

- Attack vs Defense Accuracy
- Attack vs Defense DP Gap

✅ Distribution Plots

- Accuracy Distribution
- DP Gap Distribution

✅ Trade-off Analysis

- Accuracy vs Fairness
- Defense Comparison

---

# Key Findings

## 📊 Real Dataset

- Baseline FedAvg achieves approximately **85% accuracy**.
- Fairness poisoning significantly degrades both fairness and predictive performance.
- Robust aggregation methods (Median and Robust Fair) reduce demographic disparity while maintaining competitive accuracy.
- Adaptive attacks remain difficult to detect because they preserve local fairness while affecting the global model.

---

## 🧪 Synthetic Dataset

- Baseline FedAvg achieves approximately **80% accuracy** with a DP Gap around **0.013**.
- Fairness Poison causes the largest fairness degradation.
- Fairness Spoof maintains accuracy while concealing demographic bias.
- Adaptive attacks remain highly stealthy.
- Krum and Trimmed Mean consistently improve robustness.
- Robust Fair provides a balanced trade-off between fairness and predictive performance.

---

# Results Directory

```text
RealIncomeDataset/
└── experiment_results/
    ├── results_seed_42.png
    ├── results_seed_100.png
    ├── results_seed_999.png
    ├── comparison_across_seeds.png
    ├── heatmap_attack_defense.png
    └── ...

SyntheticData/
└── experiment_results/
    ├── results_seed_42.png
    ├── results_seed_100.png
    ├── results_seed_999.png
    ├── comparison_across_seeds.png
    ├── heatmap_attack_defense.png
    └── ...
```

---

# Technologies Used

- Python
- PyTorch
- NumPy
- Pandas
- Scikit-learn
- Matplotlib
- Jupyter Notebook / Google Colab

---

# Future Work

Potential extensions include:

- Differential Privacy
- Secure Aggregation
- Personalized Federated Learning
- Transformer-based FL
- Graph Federated Learning
- Additional fairness metrics
- Larger real-world federated datasets


---

## ⭐ Acknowledgement

This repository was developed for research on **Fairness and Robustness in Federated Learning**, exploring how adversarial attacks influence machine learning systems and how fairness-aware defenses can mitigate their effects.
