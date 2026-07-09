Federated Learning: Fairness and Robustness under Adversarial Attacks
Overview

This repository contains a comprehensive experimental framework for studying fairness, robustness, and security in Federated Learning (FL). The project evaluates how different adversarial attacks influence both model performance and fairness, and compares several aggregation strategies designed to mitigate malicious client behavior.

Experiments are conducted on both:

Real-world dataset: UCI Adult Income
Synthetic dataset: Generated binary classification data with controlled demographic bias

To ensure statistical reliability, every experiment is repeated across multiple random seeds (42, 100, and 999) and results are reported as mean ± standard deviation.

Repository Structure
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
Project Objectives

The experiments aim to investigate:

Federated learning under heterogeneous (non-IID) client distributions
Robustness against malicious client updates
Fairness-aware aggregation strategies
Trade-offs between prediction accuracy and fairness
Effectiveness of Byzantine-robust defenses
Behavior of adaptive adversarial attacks
Stability across multiple random seeds
Datasets
1. Real Dataset — UCI Adult Income

The Adult Income dataset is used to evaluate fairness on a realistic classification problem.

Properties

48,842 samples
13 input features
Binary classification:
Income > $50K
Income ≤ $50K
Sensitive attribute:
Sex
Split across 6 simulated federated clients
Clients contain heterogeneous data distributions and injected local demographic bias.
2. Synthetic Dataset

A controlled synthetic dataset generated using make_classification().

Properties

2,000 samples
10 features
Binary classification
Artificial sensitive attribute
Controlled demographic bias
Non-IID partitioning across 6 clients
Allows reproducible experiments where fairness violations can be precisely controlled.
Federated Learning Setup

The simulated FL environment contains:

6 clients
2 malicious clients
20 communication rounds
Local training for 5 epochs
Feed-forward neural network
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

Attacks become active beginning at Round 5.

Attack Strategies
Attack	Description
none	Honest client training (baseline)
random	Sends random model parameters
label_flip	Flips labels for part of the sensitive group
gradient_scale	Scales malicious gradients before aggregation
fairness_poison	Intentionally biases predictions against a demographic group
fairness_spoof	Appears fair locally while introducing hidden global bias
adaptive	Stealthy attack that minimizes detection while degrading global fairness
Aggregation Methods (Defenses)
Defense	Description
FedAvg	Standard Federated Averaging
Median	Coordinate-wise median aggregation
Trimmed Mean	Removes extreme client updates before averaging
Krum	Byzantine-robust aggregation using distance-based selection
Fairness Only	Fairness-weighted aggregation based on client DP scores
Robust Fair	Combines robustness and fairness through trust-based weighting
Evaluation Metrics

Each experiment reports:

Performance
Accuracy
Fairness
Demographic Parity (DP) Gap
Equalized Odds (EO) Gap

Lower fairness gaps indicate fairer predictions.

Experiments

Experiments are performed independently on both datasets.

Each experiment evaluates:

Different attacks
Different defenses
Multiple random seeds
Training dynamics over communication rounds

The following attack-defense combinations are analyzed:

Attack vs FedAvg
Fairness Poison vs all defenses
Adaptive vs all defenses
Fairness Spoof vs selected defenses
Baseline (no attack)
Visualizations

Each dataset produces several visualizations.

Training Curves
Accuracy over communication rounds
Demographic Parity Gap over rounds
Equalized Odds Gap over rounds
Multi-Seed Analysis
Mean ± Standard Deviation accuracy
Mean ± Standard Deviation DP Gap
Cross-seed stability comparison
Heatmaps

Attack vs Defense comparison for:

Accuracy
Demographic Parity Gap
Distribution Plots
Accuracy distribution across attacks
DP Gap distribution across defenses
Trade-off Analysis
Accuracy vs Fairness scatter plots
Defense comparison
Robustness comparison
Experimental Findings
Real Dataset (Adult Income)
Baseline FedAvg achieves approximately 85% accuracy.
Fairness poisoning substantially increases fairness disparities while reducing predictive performance.
Robust aggregation methods such as Median and Robust Fair significantly reduce demographic parity gaps under attack.
Adaptive attacks remain difficult to detect because they preserve local fairness while affecting global model behavior.
Byzantine-robust defenses improve fairness at a small cost in overall accuracy.
Synthetic Dataset
Baseline FedAvg achieves approximately 80% accuracy with a DP Gap of around 0.013.
Fairness Poison is the most damaging attack, reducing accuracy and producing the largest demographic parity gap.
Fairness Spoof has minimal impact on accuracy but successfully conceals demographic bias, making it particularly difficult to identify.
Adaptive attacks maintain high predictive performance while subtly influencing fairness metrics.
Krum and Trimmed Mean consistently provide strong robustness against malicious updates.
Robust Fair offers a balanced trade-off between prediction accuracy and fairness across most attack scenarios.
Reproducibility

Experiments are repeated using three random seeds:

42
100
999

Results are reported as:

Mean ± Standard Deviation

to reduce randomness and improve reproducibility.

Results Directory
RealIncomeDataset/
└── experiment_results/
    ├── results_seed_42.png
    ├── results_seed_100.png
    ├── results_seed_999.png
    ├── comparison_across_seeds.png
    ├── heatmap_attack_defense.png
    ├── time_series_comparison.png
    └── ...

SyntheticData/
└── experiment_results/
    ├── results_seed_42.png
    ├── results_seed_100.png
    ├── results_seed_999.png
    ├── comparison_across_seeds.png
    ├── heatmap_attack_defense.png
    ├── time_series_comparison.png
    └── ...
Technologies Used
Python
PyTorch
NumPy
Scikit-learn
Matplotlib
Pandas
Google Colab / Jupyter Notebook
Future Work

Potential extensions include:

Differential Privacy in Federated Learning
Secure Aggregation protocols
Personalized Federated Learning
Graph-based Federated Learning
Transformer-based client models
Additional fairness metrics (Equal Opportunity, Calibration, etc.)
Real-world federated benchmark datasets (COMPAS, CelebA, FEMNIST, etc.)
