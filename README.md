# CKD Predict Model

This project builds a Machine Learning model to predict and diagnose **Chronic Kidney Disease (CKD)** based on biomedical indicators. The project involves a comprehensive comparison of various classification and regression algorithms, applying dimensionality reduction to optimize performance.

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
- [Authors](#authors)

## Introduction
Chronic Kidney Disease is a major global health issue. This project aims to assist in early diagnosis by analyzing patient records. We compare the effectiveness of multiple classification models and utilize PCA/LDA for feature extraction to identify the most critical biomedical markers.

## Dataset
The dataset includes various features such as Age, Blood Pressure, Blood Glucose, etc.
* **Source:** [UCI Machine Learning Repository - Chronic_Kidney_Disease](https://archive.ics.uci.edu/ml/datasets/chronic_kidney_disease)
* **Characteristics:** Mixed dataset containing both **numerical** and **categorical** features.

## Processing Pipeline

### 1. Data Preprocessing
This is a critical step to ensure model performance on the mixed CKD dataset.
* **Handling Missing Values:** Imputed missing numerical data using Mean/Median and categorical data using Mode.
* **Encoding:** Applied Label Encoding and One-Hot Encoding.
* **Normalization:** Min-Max Scaling / Standard Scaling to bring features to a common scale.

### 2. Feature Extraction
Dimensionality reduction was applied to remove noise and improve training speed:
* **PCA (Principal Component Analysis)**
* **LDA (Linear Discriminant Analysis)**

## Models Implemented
We implemented and compared the following algorithms:

**Classification & Regression:**
1.  **K-Nearest Neighbors (K-NN Classifier)**
2.  **Naive Bayes (Mixed Approach)**
3.  **Logistic Regression**
4.  **Linear Regression**
5.  **K-Nearest Neighbors (K-NN Regression)**
6.  **Support Vector Machine (SVM)**

**Unsupervised Learning:**
7.  **K-Means Clustering**

## My Contribution

In this group project, I was the **Lead for Data Engineering** and responsible for building the **Naive Bayes** and **SVM** models.

### 1. Data Preprocessing
* Conducted data cleaning for the raw dataset.
* Performed descriptive statistical analysis to determine optimal imputation strategies for missing values.
* Standardized the input data for distance-based models (like K-NN, SVM, and PCA).

### 2. Mixed Naive Bayes Implementation
Since the CKD dataset contains both **continuous features** (e.g., Blood Pressure, Age) and **discrete features** (e.g., Hypertension, Edema), a standard Gaussian Naive Bayes would not be optimal.

I implemented a **Mixed Naive Bayes** approach:
* **Gaussian Naive Bayes:** Applied to continuous/numerical features.
* **Categorical/Multinomial Naive Bayes:** Applied to discrete/categorical features.
* **Fusion:** Combined the posterior probabilities from both parts to make the final prediction.

### 3. Support Vector Machine (SVM)
I implemented and tuned the SVM model to find the optimal decision boundary:
* **Kernels Tested:** Linear (Hard & Soft Margin) and RBF (Radial Basis Function).
* **Hyperparameter Tuning:** Adjusted `C` (Regularization parameter) to balance margin width and classification error.

## Experimental Results

We evaluated the performance of the models across different Train-Test split ratios and feature extraction techniques.

### 1. Naive Bayes Performance
*Note: LDA results are excluded as they are not relevant for this probabilistic model evaluation.*

| Train:Test Split | Original Data | PCA (6 Components) |
|:---:|:---:|:---:|
| **80:20** | 97.50% | 98.75% |
| **70:30** | 95.83% | 98.33% |
| **60:40** | 94.38% | 98.12% |

**Evaluation of Naive Bayes:**
* **Theoretical Limitation:** Naive Bayes relies on the "Naive" assumption that all features are independent. However, in medical data, biological features are often highly correlated (e.g., Blood Pressure and Heart Disease are linked). This makes Naive Bayes theoretically less suitable for this domain.
* **Practical Outcome:** Despite the theoretical mismatch, because the dataset size is relatively small, the model still managed to produce quite objective and acceptable results (~94-98%).

### 2. Support Vector Machine (SVM) Performance
I tested SVM with three configurations: **Hard Margin**, **Soft Margin**, and **Kernel SVM**.

| Train:Test Split | Original Data (Best of All Kernels) | PCA 6 Components (Best of All Kernels) |
|:---:|:---:|:---:|
| **80:20** | **100.0%** | 98.75% |
| **70:30** | **100.0%** | 98.33% |
| **60:40** | **100.0%** | 98.12% |

**Evaluation of SVM:**
* **Original Data (100% Accuracy):** After performing **One-Hot Encoding**, the feature space became high-dimensional. In this expanded space, the classes (CKD vs. Non-CKD) became **perfectly linearly separable**. This explains why the Linear Kernel (Hard Margin) achieved absolute perfection (100%) on the original data.
* **PCA Data (Accuracy Drop):** When we applied PCA to reduce dimensionality (down to 6 components), the spatial structure of the data changed. The dataset was **no longer perfectly linearly separable** in this reduced space, leading to a slight decrease in accuracy compared to the original high-dimensional data.

## Installation

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/tasdus-117/CKD_Predict_Model](https://github.com/tasdus-117/CKD_Predict_Model)
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
* **[Nguyen Chi Hoang Tu]** - *Data Preprocessing, Naive Bayes & SVM*
* **[Duong Cong Kien]** - *Logistic Regression, Linear Regression & KNN Regression*
* **[Tran Xuan Viet]** - *K-NN Classifier, PCA, LDA & K-Means*
