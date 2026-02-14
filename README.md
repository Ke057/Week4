# Week4
## Getting started
This project focuses on the application of unsupervised learning techniques to classify Sentinel-3 altimetry echoes in the Arctic region. The primary objective is to differentiate between Sea Ice and Leads (narrow channels of open water) based on their unique radar backscatter signatures. We will cover K-means and Gaussian Mixture Models (GMM) clustering.
## Prerequisites
The following software needs to be installed to run the code.
```bash
pip install rasterio
```
```bash
pip install netCDF4
```
* Mounting Google Drive on Google Colab:
```bash
from google.colab import drive
drive.mount('/content/drive')
```
# unsupervised learning
## K-means Clustering
The unsupervised learning method used in this project is K-means clustering. K-means is a distance-based algorithm that divides data into a chosen number of clusters. It groups data so that points in the same cluster are more similar to each other. Similarity is usually measured using Euclidean distance. Because it does not need labelled data, it is suitable for exploratory analysis. K-means assumes the data can be represented by k cluster centres (centroids). The algorithm starts with k initial centroids. It then repeats two steps: assign points to the nearest centroid, and update each centroid as the cluster mean. The process stops when the centroids change very little. Key elements include k, centroid initialization, distance metric, and iterative updating. K-means is fast, simple, and widely used for multidimensional data clustering.
```bash
# Python code for K-means clustering
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt
import numpy as np

# Sample data
X = np.random.rand(100, 2)

# K-means model
kmeans = KMeans(n_clusters=4)
kmeans.fit(X)
y_kmeans = kmeans.predict(X)

# Plotting
plt.scatter(X[:, 0], X[:, 1], c=y_kmeans, cmap='viridis')
centers = kmeans.cluster_centers_
plt.scatter(centers[:, 0], centers[:, 1], c='black', s=200, alpha=0.5)
plt.show()
```
<img width="548" height="413" alt="image" src="https://github.com/user-attachments/assets/83c3022f-061b-4e6c-bbb5-9fa3d9919be0" />

## GMM Clustering
The unsupervised learning method used in this project is Gaussian Mixture Models (GMMs). GMMs are probabilistic models used to describe a dataset as a combination of several normally distributed subpopulations rather than a single distribution. The method assumes that the observed data are generated from multiple Gaussian distributions, each with its own mean and variance. By combining several simple Gaussian components, GMMs can model more complex data structures, which makes them useful for clustering and density estimation. 

The key components of a GMM include the number of Gaussian components, the Expectation–Maximization (EM) algorithm, and the covariance type. The EM algorithm is an iterative procedure that first estimates the probability that each data point belongs to each component, and then updates the component parameters to maximize the likelihood of the observed data. The covariance type controls the shape and flexibility of each cluster. Compared with hard clustering methods, GMM provides soft probabilistic assignments and can better handle clusters with different shapes and spreads. Other unsupervised learning methods include K-means clustering and hierarchical clustering.
