# ELE489-HW2-DecisionTree

# 🧠 ELE489 Homework 2 – Decision Tree on Banknote Authentication Dataset

## 📌 Project Overview

In this project, we apply a **Decision Tree Classifier** to the [Banknote Authentication Dataset](https://archive.ics.uci.edu/dataset/267/banknote+authentication) to distinguish real and fake banknotes based on four statistical features. The goal is to analyze how hyperparameters such as `max_depth`, `min_samples_split`, and `criterion` affect both **model performance** and **interpretability**.

---

## 📁 Repository Structure

- `decision_tree.ipynb`: Google Colab notebook with full code, visualizations, and comments
- `report.pdf` *(optional)*: Final written report (same content as below)
- `README.md`: This file

---

## 🔍 Dataset Description

- Total samples: 1372
- Features:
  - `Variance`: Spread of pixel values
  - `Skewness`: Asymmetry of distribution
  - `Kurtosis`: Sensitivity to outliers
  - `Entropy`: Complexity / disorder in the image
- Target label: `0 = Fake`, `1 = Real`

---

## 📊 Feature Interpretations

| Feature   | Description & Interpretation |
|-----------|------------------------------|
| **Variance** | Real notes have more consistent patterns; high variance is expected |
| **Skewness** | Asymmetric patterns might suggest forgery |
| **Kurtosis** | Sensitivity to outliers; may signal suspicious distributions |
| **Entropy**  | Higher entropy = more randomness, common in fake banknotes |

---

## ⚙️ Model Experiments

We tested 9 different models with varying `max_depth`, `min_samples_split`, and `criterion`:

| Model | Criterion | Depth | Split | Accuracy | Precision | Recall | F1 Score |
|-------|-----------|-------|-------|----------|-----------|--------|----------|
| 1     | Gini      | 3     | 2     | 0.909    | 0.925     | 0.874  | 0.899    |
| 2     | Gini      | 5     | 5     | 0.967    | 1.000     | 0.929  | 0.963    |
| 3     | Gini      | 7     | 10    | 0.982    | 1.000     | 0.961  | 0.980    |
| 4     | Gini      | 9     | 2     | 0.982    | 1.000     | 0.961  | 0.980    |
| 5     | Gini      | 12    | 2     | 0.982    | 1.000     | 0.961  | 0.980    |
| 6     | Entropy   | 5     | 5     | 0.978    | 0.992     | 0.961  | 0.976    |
| 7     | Entropy   | 7     | 10    | 0.982    | 0.992     | 0.969  | 0.980    |
| 8     | Entropy   | 9     | 2     | 0.985    | 1.000     | 0.969  | 0.984    |
| 9     | Entropy   | 12    | 2     | 0.985    | 1.000     | 0.969  | 0.984    |

### 🔎 Observations:
- Performance improves with depth up to 7–9, then plateaus.
- `entropy` slightly outperforms `gini` in recall.
- Deeper trees are more accurate but **less interpretable**.
- Depths of 5–7 provide **optimal trade-off** between performance and readability.

---

## 🌳 Tree Depth & Interpretability

Using `plot_tree()` from `sklearn.tree`, we visualized how increasing depth:
- Improves prediction but
- Decreases explainability.

Shallow trees (depth 3–5) are **simple and readable**. Deeper trees (9–12) become **complex and hard to follow**, despite higher accuracy.

---

## 🔬 Feature Importance (from trained model)

```plaintext
variance   → ~60%  
skewness   → ~23%  
kurtosis   → ~15%  
entropy    → ~2%
