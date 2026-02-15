# GEOL0069_Week4
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
## Context
Satellite remote sensing provides multiple ways to distinguish between surface types such as sea ice and open water. Optical multispectral imagery captures differences in reflectance across bands, while radar altimetry measures the returned echo waveform from the surface.
In this project, multispectral raster bands and waveform-derived features are processed and clustered using unsupervised learning to explore how well surface classes can be separated automatically.

## unsupervised learning
## K-means Clustering
K-Means is a distance-based clustering method that groups data into k clusters by minimising the variation within each cluster. It works by iteratively assigning each sample to the nearest cluster centre and then updating the centres based on the mean of assigned points.

In this project, K-Means is used to cluster multispectral pixel features and synthetic datasets to explore how different surface types separate in feature space.

**Advantages**
- Fast and simple  
- Easy to interpret  
- Works well for compact clusters

**Limitations**
- Must choose the number of clusters in advance  
- Assumes roughly spherical cluster shapes  
- Sensitive to initial centroid placement  

## GMM Clustering
Gaussian Mixture Models are probabilistic clustering models that represent the data as a mixture of Gaussian distributions. Instead of assigning points strictly to one cluster, GMM estimates the probability of membership for each component.

Model parameters are estimated using the Expectation–Maximization (EM) algorithm. GMM is more flexible than K-Means and can model clusters with different shapes and spreads.

In this project, GMM is applied to waveform and feature datasets to separate likely surface types such as sea ice and leads.

**Advantages**
- Handles overlapping clusters
- Allows different cluster shapes
- Provides probabilistic membership

**Limitations**
- Slower than K-Means
- Requires choosing number of components
- Can overfit if too many components are used

## Reading in the Necessary Functions
In order to ensure that data is compatible with the chosen analytical model, the data needs to be preprocessed. This includes transforming raw data into variables such as peakiness and stack standard deviation, as well as removing NaN values.
## Running the Clustering Models
1.  **K-Means Clustering**:
The K-Means model is initialized using KMeans from sklearn.cluster. It partitions the data by minimizing the variance within each cluster. By defining the number of clusters (n_clusters) and setting a random_state for reproducibility, the model is fit to the data, and cluster labels are predicted to distinguish between sea ice and leads.

3.  **Gaussian Mixture Model (GMM)**:
The GMM is initialized using GaussianMixture from sklearn.mixture. Unlike K-Means, GMM is a distribution-based model that assumes all data points are generated from a mixture of a finite number of Gaussian distributions with unknown parameters. The model is fit (gmm.fit) to the cleaned data matrix, and cluster labels are predicted (gmm.predict) based on the underlying probability density.
##Result
The resulting clusters of functions can then be extracted and plotted using plt from matplotlib.pyplot. The echos (or functions) in the sea ice cluster are been labelled '0' and the lead echos are labelled '1'.
## Result
The clustering models (K-Means and Gaussian Mixture Models) were applied to the waveform / echo feature dataset after preprocessing and cleaning. Results were evaluated using waveform plots, cluster statistics, and confusion matrix comparison against the reference surface-type flags.
### Waveform (Echo) Shape Comparison

Echo waveforms from different clusters show clear structural differences. One cluster is characterised by sharper peak-like returns, while the other shows broader and more gradually decaying signals. This is consistent with the expected physical difference between lead-like and sea-ice-like surfaces.

Example waveform plots were produced for:

- K-Means clusters  
- GMM clusters  
- raw (unaligned) echoes  
- aligned echoes  

This gives four comparison conditions:
- K-Means — raw echoes  
- K-Means — aligned echoes  
- GMM — raw echoes  
- GMM — aligned echoes

### Mean and Standard Deviation Curves
Observations:

- Cluster mean curves show different peak strength and decay behaviour  
- Lead-like clusters generally have higher and sharper mean peaks  
- Sea-ice-like clusters show smoother and lower average return power  
- Standard deviation curves indicate higher variability in the lead cluster  
- After echo alignment, both mean and standard deviation curves become smoother and more physically interpretable  

Aligned results reduce waveform shift effects and improve cluster separability in the statistics.
<img width="572" height="435" alt="image" src="https://github.com/user-attachments/assets/2739a716-33b4-4790-add8-d622ab7bec2d" />
<img width="617" height="435" alt="image" src="https://github.com/user-attachments/assets/6a77fa5a-1bb6-41fa-86b9-0ad1a2a98040" />
<img width="580" height="435" alt="image" src="https://github.com/user-attachments/assets/c19111d8-9efd-4aae-a994-22bbbd4c453a" />
<img width="581" height="435" alt="image" src="https://github.com/user-attachments/assets/4e348ed8-1d97-4263-87f1-885c92887440" />




### Confusion Matrix Comparison
A confusion matrix was computed by comparing the clustering labels with the reference classification flags provided in the dataset.
Below is a confusion matrix comparing the ESA official classification (flags) against k-means and GMM cluster classification：
<img width="662" height="574" alt="image" src="https://github.com/user-attachments/assets/abd38812-f278-4411-857c-e3def129cece" />
<img width="662" height="574" alt="image" src="https://github.com/user-attachments/assets/0cae88c8-f85d-4ebc-ace6-fb86fc1e9b43" />


### Model Comparison Summary

Based on the waveform plots, cluster mean and standard deviation curves, and the confusion matrix results for the unaligned echoes, **Gaussian Mixture Models (GMM)** generally perform better than **K-Means** for this dataset.

GMM produces clusters with more realistic waveform shape separation and smoother statistical profiles. The cluster mean and standard deviation curves are more clearly differentiated, and the confusion matrix shows stronger agreement with the reference surface-type flags. This suggests that GMM handles overlapping and variable echo shapes more effectively.

K-Means still provides reasonable separation and captures the main structure of the data, but its distance-based and hard-boundary clustering leads to more mixed assignments near class transitions.

Overall, for echo-based surface classification in this experiment, **GMM is the more suitable model**, while K-Means serves as a useful and fast baseline method.
