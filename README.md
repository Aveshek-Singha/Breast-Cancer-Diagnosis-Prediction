# Breast Cancer Diagnosis using KNN and K-Means

## Overall Project Overview

This project applies two different machine learning techniques to the Breast Cancer dataset in order to understand tumor characteristics and predict cancer diagnosis. The two techniques serve different but complementary purposes:

* **K-Means Clustering** is used as an unsupervised learning method to explore natural groupings in the data.
* **K-Nearest Neighbors (KNN)** is used as a supervised learning method to predict whether a tumor is malignant or benign.

The dataset consists of numerical features extracted from breast tumor images, along with a diagnosis label indicating whether the tumor is **Malignant (M)** or **Benign (B)**.

---

## Dataset and Preprocessing Approach

Before applying any machine learning algorithm, the dataset is preprocessed to ensure reliable and fair results.

### Steps Performed

* Removed identifier and empty columns: `id`, `Unnamed: 32`
* Removed low-impact features: `fractal_dimension_mean`, `fractal_dimension_se`, `fractal_dimension_worst`
* Encoded the diagnosis column:

  * Malignant (M) → 1
  * Benign (B) → 0
* Applied **Min-Max Normalization** to scale all feature values between 0 and 1

Feature scaling is essential because both K-Means and KNN rely on distance calculations. Without normalization, features with larger numeric ranges would dominate the distance measurement.

---

## K-Means Clustering Approach (Unsupervised Learning)

### Purpose

The goal of K-Means clustering is not prediction, but **pattern discovery**. The algorithm groups tumors based solely on feature similarity, without using diagnosis labels during training.

### How the Code Works

1. Only the feature set is used as input (diagnosis labels are excluded).
2. All features are normalized using Min-Max scaling.
3. K-Means is applied with **k = 2**, assuming two natural groups in the data.
4. After clustering, the diagnosis labels are used only to analyze how benign and malignant cases are distributed across clusters.

### Clustering Results

| Cluster | Benign (0) | Malignant (1) |
| ------- | ---------- | ------------- |
| 0       | 6          | 180           |
| 1       | 351        | 32            |

### Interpretation

* One cluster is dominated by malignant tumors
* The other cluster is dominated by benign tumors
* This indicates that tumor features naturally separate into meaningful groups

K-Means successfully reveals structure in the data, but it **does not classify or predict diagnoses**.

---

## K-Nearest Neighbors (KNN) Classification Approach (Supervised Learning)

### Purpose

KNN is used to **predict the diagnosis** of a tumor based on labeled training data.

### How the Code Works

1. The dataset is split into features (X) and labels (y).
2. Min-Max normalization is applied to all features.
3. The data is split into training (80%) and testing (20%) sets.
4. A KNN classifier with **k = 5** neighbors is trained using the training data.
5. Predictions are made on the test set.
6. Model performance is evaluated using standard classification metrics.

### Evaluation Results

| Metric    | Value  |
| --------- | ------ |
| Accuracy  | 95.61% |
| Precision | 93.18% |
| Recall    | 95.35% |
| F1-Score  | 94.25% |

### Interpretation

* High accuracy indicates strong overall classification performance
* High recall shows effective identification of malignant tumors
* Balanced precision and recall produce a strong F1-score

KNN demonstrates excellent reliability for breast cancer diagnosis prediction.

---

## Key Differences Between K-Means and KNN

* K-Means is **unsupervised** and does not use labels during training
* KNN is **supervised** and requires labeled data
* K-Means is used for exploration and pattern discovery
* KNN is used for actual diagnosis prediction

The two algorithms are independent and serve different analytical goals.

---

## Technologies Used

* Python
* Pandas
* Scikit-learn
* Google Colab / Jupyter Notebook

---

## Conclusion

This project demonstrates how unsupervised and supervised learning techniques can be applied to the same medical dataset for different purposes. K-Means provides insight into the natural structure of tumor data, while KNN delivers accurate and dependable predictions. Together, they offer a comprehensive understanding of breast cancer diagnosis using machine learning.
