---
layout: post
title: Toy Models of Superposition
date: 2024-05-06
categories: [AGI Safety Fundamentals, AI Alignment, Interpretability, Project]
---

# Summary of Toy Models of Superposition

## **Model Configuration and Instantiation**

- **Configuration**:
  - Features (`n_features`): 200
  - Hidden units (`n_hidden`): 20
  - Instances (`n_instances`): 20

- **Model Parameters**:
  - **Feature Importance**: Presumed constant across features (not explicitly set in the provided snippets).
  - **Feature Probability**: Defined to decrease exponentially from 1 (fully dense) to 1/20 (highly sparse) across instances, potentially affecting the sparsity of input data and model training dynamics.

## **Training and Optimization**

- **Optimization**: The `optimize` function trains the model using an AdamW optimizer, likely adjusting weights to minimize a loss function.

## **Weight Analysis Functions**

- **`compute_dimensionality`**:
  - Computes a dimensionality metric for the weights that quantifies how independently each feature can represent information, based on the interference (overlap) of normalized weight vectors.

## **Visualization and Analysis**

1. **Feature Sparsity vs. Weight Concentration**
   - **Plot**: Relationship between the inverse of feature probability (`1/(1-S)`) and the ratio of the number of hidden units to the squared Frobenius norm of the weight matrix (`m/||W||_F^2`).
   - **Findings**: The plot showed a decreasing trend, indicating more concentrated or less uniformly distributed weights as feature sparsity increased.

2. **Dimensionality Fractions Visualization**
   - **Plot**: Scatter plot of dimensionality fractions against the inverse of feature probability with reference lines at specific fractional values.
   - **Observations**:
     - Data points spread indicates variability in feature independence across different sparsity levels.
     - Clustering near specific reference lines suggests thresholds of feature independence.

## **Interpretations**

- **Impact of Feature Density on Independence**:
  - Lower feature density (higher sparsity) tends to reduce the independence of feature representations, potentially leading to overfitting on the fewer available features.
  
- **Model Capacity and Generalization**:
  - The visualizations and metrics calculated offer insights into the model's capacity to differentiate feature representations and its potential to generalize across varying levels of feature availability.

## **Conclusions**

The series of analyses provides valuable insights into the behavior of neural network weights under varying conditions of feature availability. By examining the distribution of weights and their independence across features, one can infer crucial aspects of model behavior, such as susceptibility to overfitting and generalization capabilities. These findings can guide further model refinement and experimentation to enhance performance and robustness.