# Chronic Kidney Disease Prediction

This project builds a Machine Learning model to predict and diagnose **Chronic Kidney Disease (CKD)** based on biomedical indicators. The project involves a comprehensive comparison of various classification algorithms and applies dimensionality reduction techniques to optimize performance.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Scikit-Learn](https://img.shields.io/badge/Library-Scikit--Learn-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)

## Table of Contents
- [Introduction](#introduction)
- [Dataset](#dataset)
- [Processing Pipeline](#processing-pipeline)
- [Models Implemented](#models-implemented)
- [My Contribution](#my-contribution)
- [Experimental Results](#experimental-results)
- [Installation](#installation)

##  Introduction
Chronic Kidney Disease is a major global health issue. This project aims to assist in early diagnosis by analyzing patient records. We compare the effectiveness of multiple classification models and utilize PCA/LDA for feature extraction.

##  Dataset
The dataset includes various features such as Age, Blood Pressure, Blood Glucose, etc.
* **Source:** [UCI Machine Learning Repository - Chronic_Kidney_Disease](https://archive.ics.uci.edu/ml/datasets/chronic_kidney_disease)
* **Characteristics:** Mixed dataset containing both **numerical** and **categorical** features.

##  Processing Pipeline

![Văn bản thay thế](đường_dẫn_hoặc_URL_của_ảnh)

### 1. Data Preprocessing
This is a critical step to ensure model performance on the mixed CKD dataset.
* **Handling Missing Values:** Imputed missing numerical data using Mean/Median and categorical data using Mode.
* **Encoding:** Applied Label Encoding and One-Hot Encoding.
* **Normalization:** Min-Max Scaling / Standard Scaling to bring features to a common scale.

### 2. Feature Extraction
Dimensionality reduction was applied to remove noise and improve training speed:
* **PCA (Principal Component Analysis)**
* **LDA (Linear Discriminant Analysis)**

##  Models Implemented
We implemented and compared the following algorithms:
1.  **K-Nearest Neighbors (K-NN)**
2.  **Naive Bayes (Mixed Approach)**
3.  **Logistic Regression**
4.  **Linear Regression**
5.  **Random Forest**

##  My Contribution

In this group project, I was the **Lead for Data Engineering** and the **Naive Bayes Model Architect**.

### 1. Data Preprocessing
* Conducted data cleaning for the raw dataset.
* Performed descriptive statistical analysis to determine optimal imputation strategies for missing values.
* Standardized the input data for distance-based models (like K-NN and PCA).

### 2. Mixed Naive Bayes Implementation
Since the CKD dataset contains both **continuous features** (e.g., Blood Pressure, Age) and **discrete features** (e.g., Hypertension, Edema), a standard Gaussian Naive Bayes would not be optimal.

I implemented a **Mixed Naive Bayes** approach:
* **Gaussian Naive Bayes:** Applied to continuous/numerical features.
* **Categorical/Multinomial Naive Bayes:** Applied to discrete/categorical features.
* **Fusion:** Combined the posterior probabilities from both parts to make the final prediction.

## Experimental Results

We evaluated the performance of the **Naive Bayes** model across different Train-Test split ratios and feature extraction techniques.

The table below summarizes the **Accuracy** scores:

| Train:Test Split | Original Data | PCA (6 Components) | LDA (1 Component) |
|:---:|:---:|:---:|:---:|
| **80:20** (4:1) | 97.50% | 98.75% | **100.0%** |
| **70:30** (7:3) | 95.83% | 98.33% | **100.0%** |
| **60:40** (6:4) | 94.38% | 98.12% | **100.0%** |

### Key Findings
1.  **LDA Superiority:** Using Linear Discriminant Analysis (LDA) with just 1 component resulted in **perfect accuracy (100%)** across all data splits. This indicates that the classes (Chronic Kidney Disease vs. Non-CKD) are linearly separable when projected onto the LDA axis.
2.  **PCA Improvement:** PCA (reduced to 6 components) consistently outperformed the Original Data model, proving that dimensionality reduction helped eliminate noise and improve generalization.
3.  **Stability:** The model performance remains robust even when the training set size is reduced (e.g., 60:40 split).

## Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/tasdus-117/CKD_Predict_Model
    ```
2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Run the Project:**
    ```bash
    jupyter notebook MachineLearning_Project.ipynb
    ```

## Authors
* **[Nguyen Chi Hoang Tu]** - *Data Preprocessing & Naive Bayes*
* [Duong Cong Kien] - *Logistic Regression, Linear Regression &  Random Forest*
* [Tran Xuan Viet] - *K-NN, PCA, & LDA*
