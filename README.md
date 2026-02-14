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
The unsupervised learning method used in this project is K-means clustering. K-means is a distance-based algorithm that divides data into a chosen number of clusters. It groups data so that points in the same cluster are more similar to each other. Similarity is usually measured using Euclidean distance. Because it does not need labelled data, it is suitable for exploratory analysis. K-means assumes the data can be represented by k cluster centres (centroids). The algorithm starts with k initial centroids.

It then repeats two steps: assign points to the nearest centroid, and update each centroid as the cluster mean. The process stops when the centroids change very little. Key elements include k, centroid initialization, distance metric, and iterative updating. K-means is fast, simple, and widely used for multidimensional data clustering.
## GMM Clustering
Gaussian Mixture Models (GMMs) are an unsupervised learning method used to find hidden groups in data. Instead of assuming all data come from one distribution, GMM assumes the data come from several Gaussian (normal) distributions mixed together. Each group has its own mean and variance. By combining these Gaussian components, GMM can describe complex data patterns and is useful for clustering and density estimation.

A GMM mainly includes three parts: the number of Gaussian components, the EM algorithm, and the covariance type. The EM algorithm works in steps: first it estimates how likely each data point belongs to each group, then it updates the group parameters to better fit the data. The covariance type controls the shape and size of each cluster. Unlike hard clustering methods, GMM gives soft probabilities instead of fixed labels, so it can handle clusters with different shapes and spreads. Other common unsupervised methods include K-means and hierarchical clustering.
## Reading in the Necessary Functions
In order to ensure that data is compatible with the chosen analytical model, the data needs to be preprocessed. This includes transforming raw data into variables such as peakiness and stack standard deviation, as well as removing NaN values.
## Running the Clustering Models
1.  **K-Means Clustering**:
The K-Means model is initialized using KMeans from sklearn.cluster. It partitions the data by minimizing the variance within each cluster. By defining the number of clusters (n_clusters) and setting a random_state for reproducibility, the model is fit to the data, and cluster labels are predicted to distinguish between sea ice and leads.

3.  **Gaussian Mixture Model (GMM)**:
The GMM is initialized using GaussianMixture from sklearn.mixture. Unlike K-Means, GMM is a distribution-based model that assumes all data points are generated from a mixture of a finite number of Gaussian distributions with unknown parameters. The model is fit (gmm.fit) to the cleaned data matrix, and cluster labels are predicted (gmm.predict) based on the underlying probability density.
##Result

