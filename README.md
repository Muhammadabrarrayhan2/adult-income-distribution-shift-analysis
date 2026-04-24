# Analyzing Model Stability and Generalization under Distribution Shift in Real-World Machine Learning Applications

A complete machine learning study on **model stability**, **generalization**, and **distribution shift** using the **UCI Adult / Census Income dataset** as a real-world tabular classification case study.

---

## Table of Contents

- [Overview](#overview)
- [Research Objective](#research-objective)
- [Paper Title](#paper-title)
- [Dataset](#dataset)
- [Problem Definition](#problem-definition)
- [Models Evaluated](#models-evaluated)
- [Distribution Shift Scenarios](#distribution-shift-scenarios)
- [Evaluation Metrics](#evaluation-metrics)
- [Methodology Summary](#methodology-summary)
- [Main Findings](#main-findings)
- [Repository Structure](#repository-structure)
- [Requirements](#requirements)
- [Installation](#installation)
- [How to Run](#how-to-run)
- [Expected Outputs](#expected-outputs)
- [Research Significance](#research-significance)
- [Authors](#authors)
- [Citation](#citation)
- [License](#license)

---

## Overview

Machine learning models are often evaluated under the assumption that training and testing data follow the same distribution. In practice, this assumption is frequently violated. Real-world deployment environments may differ from the original training environment due to changes in age distribution, education level, subgroup composition, sampling strategy, or other population characteristics.

This repository contains the code, experiment design, and supporting research materials for a study that analyzes how different machine learning models behave under controlled **distribution shift**. The project focuses on **tabular classification**, using the **UCI Adult / Census Income dataset** and comparing both a linear baseline and modern gradient boosting methods.

The study evaluates whether strong in-distribution performance also translates into robust performance under subgroup-based shift, and whether single-metric evaluation is sufficient for measuring model stability.

---

## Research Objective

The main objective of this project is to analyze how predictive models behave when the test distribution differs from the training distribution.

More specifically, this study aims to:

1. compare multiple machine learning models under standard in-distribution evaluation,
2. measure performance under subgroup-based distribution shift,
3. quantify performance change across scenarios,
4. evaluate model stability using multiple metrics rather than relying on a single performance score.

---

## Paper Title

**Analyzing Model Stability and Generalization under Distribution Shift in Real-World Machine Learning Applications**

---

## Dataset

This study uses the **UCI Adult / Census Income dataset**, a well-known tabular benchmark for binary income classification.

### Dataset summary
- **Dataset name:** Adult / Census Income
- **Number of records:** 48,842
- **Number of predictive features:** 14
- **Task type:** Binary classification
- **Prediction target:** Annual income greater than USD 50,000 (`>50K`) or not (`<=50K`)

### Features include
- age
- workclass
- fnlwgt
- education
- education-num
- marital-status
- occupation
- relationship
- race
- sex
- capital-gain
- capital-loss
- hours-per-week
- native-country

The dataset is especially suitable for shift analysis because it contains interpretable demographic and socioeconomic features that allow controlled subgroup partitioning.

---

## Problem Definition

The task is to predict whether an individual's annual income exceeds USD 50,000.

This study does **not** focus only on maximizing predictive accuracy. Instead, it investigates:

- whether a model remains reliable when evaluated on a shifted subgroup,
- whether higher baseline performance implies better real-world generalization,
- and how different evaluation metrics can lead to different conclusions about robustness.

---

## Models Evaluated

This project compares four classification models:

### 1. Logistic Regression
Used as a simple and interpretable linear baseline.

### 2. XGBoost
A gradient boosting decision tree method known for strong tabular performance.

### 3. LightGBM
A highly efficient boosting framework optimized for speed and accuracy.

### 4. CatBoost
A gradient boosting method designed to handle categorical structure effectively.

This model selection allows the project to compare:
- a classical linear model,
- and three strong modern tabular learners.

---

## Distribution Shift Scenarios

The experimental design includes **three evaluation scenarios**.

### Scenario 1 — In-Distribution
A standard stratified random split is used to simulate the conventional i.i.d. evaluation setting.

- **Train/Test split:** 80/20
- **Purpose:** baseline performance comparison

### Scenario 2 — Age Shift
The dataset is split by age group.

- **Training domain:** individuals aged under 40
- **Testing domain:** individuals aged 40 and above

This scenario simulates a demographic shift in which the deployed model encounters a different age profile from the one it was trained on.

### Scenario 3 — Education Shift
The dataset is split by educational attainment.

- **Training domain:** non-degree holders
- **Testing domain:** degree holders

This scenario simulates a subgroup distribution shift with a substantial change in population composition and class prevalence.

---

## Evaluation Metrics

The following metrics are used in this project:

- **Accuracy**
- **Precision**
- **Recall**
- **F1-score**
- **Performance Change**
- **Average Stability Change**
- **Stability Rank**

### Why multiple metrics matter
A central motivation of this repository is that **single-metric evaluation can be misleading under distribution shift**. In some settings, one metric may improve while another deteriorates, making multi-metric analysis essential for valid conclusions.

---

## Methodology Summary

The full workflow of the study is as follows:

### 1. Data loading
- Load the Adult dataset
- Merge and standardize target labels if needed

### 2. Data cleaning
- Convert question-mark tokens (`?`) to missing values
- Strip inconsistent whitespace
- normalize binary target labels

### 3. Preprocessing
A shared preprocessing pipeline is used for all models:

#### Numerical features
- median imputation
- standardization using z-score scaling

#### Categorical features
- mode imputation
- one-hot encoding with unknown-category handling

### 4. Modeling
Train the four models under identical preprocessing conditions.

### 5. Scenario-based evaluation
Evaluate model performance under:
- in-distribution
- age shift
- education shift

### 6. Stability analysis
Compute:
- metric values per scenario
- scenario-wise performance change
- average performance change
- stability ranking

### 7. Result export
Save:
- performance tables
- stability summary
- comparison figures

---

## Main Findings

This project is designed to reveal how predictive behavior changes under controlled distribution shift.

Key findings from the accompanying study include:

- gradient boosting models perform strongly in the standard in-distribution setting,
- subgroup-based distribution shift can alter metric behavior substantially,
- F1-score may improve under some shifted settings even when accuracy declines,
- model stability must be evaluated using multiple complementary metrics,
- high in-distribution performance does not automatically imply strong real-world robustness.

In other words, this project argues that **distribution-aware validation is necessary for trustworthy machine learning evaluation**.

