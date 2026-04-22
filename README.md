
# 🛍️ Mall Customer Segmentation using K-Means

## 📌 Project Overview
This project applies **K-Means clustering** to the **Mall Customers dataset** to identify distinct customer segments based on their **Annual Income** and **Spending Score**.  
The goal is to help businesses understand customer behavior and tailor marketing strategies accordingly.

---

## 📂 Dataset
- **File:** `Mall_Customers.csv`
- **Columns:**
  - `CustomerID` – Unique identifier for each customer
  - `Gender` – Male/Female
  - `Age` – Age of the customer
  - `Annual Income (k$)` – Annual income in thousands of dollars
  - `Spending Score (1-100)` – Score assigned based on customer behavior and spending nature

---

## ⚙️ Requirements
Install the following Python libraries before running the code:

```bash
pip install pandas matplotlib scikit-learn
```

---

## 🚀 Steps in the Project
1. **Load the dataset** using Pandas.
2. **Select features**: Annual Income and Spending Score.
3. **Apply the Elbow Method** to determine the optimal number of clusters.
4. **Train K-Means model** with the chosen number of clusters.
5. **Visualize clusters** with Matplotlib.

---

## 📊 Visualizations
- **Elbow Method Graph** – Helps decide the optimal number of clusters.
- **Cluster Plot** – Shows customer segments with different colors and centroids.

---

## 📝 Code Example
```python
import warnings
warnings.filterwarnings("ignore")

import pandas as pd
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans

# Load dataset
data = pd.read_csv("Mall_Customers.csv")

# Select features
X = data.iloc[:, [3, 4]].values

# Elbow Method
wcss = []
for i in range(1, 11):
    kmeans = KMeans(n_clusters=i, init='k-means++', random_state=42)
    kmeans.fit(X)
    wcss.append(kmeans.inertia_)

plt.plot(range(1, 11), wcss, marker='o')
plt.title("Elbow Method")
plt.xlabel("Number of clusters")
plt.ylabel("WCSS")
plt.show()

# KMeans with 5 clusters
kmeans = KMeans(n_clusters=5, init='k-means++', random_state=42)
y_kmeans = kmeans.fit_predict(X)

# Visualization
plt.scatter(X[y_kmeans == 0, 0], X[y_kmeans == 0, 1], s=100, c='red', label='Cluster 1')
plt.scatter(X[y_kmeans == 1, 0], X[y_kmeans == 1, 1], s=100, c='blue', label='Cluster 2')
plt.scatter(X[y_kmeans == 2, 0], X[y_kmeans == 2, 1], s=100, c='green', label='Cluster 3')
plt.scatter(X[y_kmeans == 3, 0], X[y_kmeans == 3, 1], s=100, c='cyan', label='Cluster 4')
plt.scatter(X[y_kmeans == 4, 0], X[y_kmeans == 4, 1], s=100, c='magenta', label='Cluster 5')

plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1],
            s=300, c='yellow', marker='*', label='Centroids')

plt.title("Customer Segments using K-Means")
plt.xlabel("Annual Income (k$)")
plt.ylabel("Spending Score (1-100)")
plt.legend()
plt.show()
```

---

## 🎯 Insights
- Customers can be grouped into segments such as:
  - **High income – High spenders**
  - **Low income – Low spenders**
  - **Average income – Moderate spenders**
- These insights can guide **targeted marketing campaigns** and **personalized offers**.

---

