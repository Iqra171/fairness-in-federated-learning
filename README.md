# Federated Learning Experiments: Fairness and Robustness

## Overview

This project implements an experimental framework for studying federated learning in a distributed environment. The focus is on evaluating how different client distributions, training conditions, and aggregation strategies affect model performance, stability, and fairness.

The setup simulates multiple clients contributing to a shared global model, allowing controlled experiments under non-IID data distributions and adversarial conditions.

---

## Objectives

- Simulate a federated learning environment with multiple clients  
- Evaluate the impact of non-IID data distributions  
- Analyze model behavior under adversarial or noisy client updates  
- Compare different aggregation strategies  
- Study trade-offs between robustness and fairness  

---

## Key Components

- **Client Simulation**: Multiple clients with distinct data distributions  
- **Global Model Training**: Aggregation of client updates  
- **Aggregation Methods**: Baseline and alternative strategies  
- **Evaluation Metrics**: Accuracy, loss, and performance across clients  
- **Experiment Modules**: Separate runs for synthetic and real datasets  


