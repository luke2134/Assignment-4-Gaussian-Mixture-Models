# Assignment-4-Gaussian-Mixture-Models

Analysis Report: Gaussian Mixture Models on Olivetti Faces Dataset

1. Introduction
This analysis explores the use of Gaussian Mixture Models (GMM) for clustering and anomaly detection on the Olivetti Faces dataset. The dataset contains 400 grayscale images of 40 individuals, with 10 images per person. The main objectives of this assignment were to apply dimensionality reduction using Principal Component Analysis (PCA), train a GMM model to perform clustering, generate new synthetic images, and detect anomalies.

2. Dataset Preparation
The Olivetti Faces dataset was retrieved using fetch_olivetti_faces from sklearn. The dataset was then split into training (60%), validation (20%), and test (20%) sets using stratified sampling to ensure that each set had an equal number of images per person.

Outcome: The dataset was successfully split into 240 training samples, 80 validation samples, and 80 test samples.

3. Dimensionality Reduction using PCA
PCA was applied to the dataset to reduce its dimensionality while preserving 99% of the variance. This step reduced the number of features from 4096 (each image is 64x64 pixels) to 178 principal components. This reduction maintains most of the data's variability while making the dataset more manageable for the GMM model.

Outcome: The number of features was reduced to 178 components, significantly improving the efficiency of the subsequent GMM training.

4. Selecting the Best Covariance Type
Gaussian Mixture Models were trained using four different covariance types: full, tied, diag, and spherical. The BIC (Bayesian Information Criterion) was used to evaluate which covariance type performed best. The model with the lowest BIC score was selected as the optimal configuration.

Outcome: The spherical covariance type had the lowest BIC score, indicating it provided the best fit for the data.

5. Determining the Optimal Number of Clusters
To determine the best number of clusters, I trained GMM models with varying numbers of components (1 to 50) and evaluated them using both AIC and BIC scores. The plots of AIC and BIC showed that around 10 clusters produced the best scores, balancing model complexity and performance.

Outcome: The optimal number of clusters was determined to be around 10, as both AIC and BIC reached their minimum at this point.

6. Clustering Assignments
The GMM model was used to assign each test image to a cluster. Both hard clustering (assigning a cluster label) and soft clustering (probabilities of belonging to each cluster) were performed. This probabilistic approach allowed for a more flexible assignment of images to clusters, accounting for uncertainty in the data.

Outcome: Hard clustering labels and soft clustering probabilities were successfully assigned to each test image.

7. Generating New Faces
Using the GMM model, new faces were generated by sampling from the Gaussian distributions of the clusters. These generated samples were then transformed back to the original image space using the inverse transform from PCA. The new images resemble the original dataset's faces, demonstrating that the GMM learned the distribution of the data effectively.

Outcome: The GMM successfully generated plausible new face images that resembled the original dataset.

8. Image Modifications
To test anomaly detection, some images were modified. I applied three transformations: rotating the image by 45 degrees, flipping it horizontally, and darkening the image by reducing its brightness by 50%. These modifications created anomalies that were used to test the GMM’s ability to detect outliers.

Outcome: The modifications were applied correctly, resulting in visibly altered versions of the test images.

9. Anomaly Detection
The GMM’s score_samples() method was used to detect anomalies by comparing the log-likelihood scores of normal and modified images. The GMM assigns higher scores to images that fit well within the learned distribution and lower scores to anomalies. As expected, the modified (anomalous) images received significantly lower scores than the normal images.

Outcome: The anomaly detection process was successful, with modified images receiving much lower scores compared to the normal images, indicating they were recognized as anomalies.

10. Conclusion
This analysis demonstrated the application of Gaussian Mixture Models for clustering and anomaly detection on the Olivetti Faces dataset. Through the use of PCA, the dataset's dimensionality was reduced without significant loss of information, which made the GMM training more efficient. The GMM was able to cluster the images, generate new face images, and detect anomalies based on modifications made to the test data. The spherical covariance type and around 10 clusters were found to be optimal for this dataset, as determined by the BIC and AIC metrics.
