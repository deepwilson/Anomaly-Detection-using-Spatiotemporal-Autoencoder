# Anomaly-Detection-using-Spatiotemporal-Autoencoder

**Pipeline:**

Data preparation

Feature selection

Model identification

Metric identification

Training and testing


**Data:**

For this projecct I use the *UCSD Anomaly Detection Dataset*

It contains two parts:

Peds1

Peds2
As per the site description:

Peds1: clips of groups of people walking towards and away from the camera, and some amount of perspective distortion. Contains 34 training video samples and 36 testing video samples

Peds2: scenes with pedestrian movement parallel to the camera plane. Contains 16 training video samples and 12 testing video samples.

Steps to prepare data:

Resize the image for model ingestion
Store in a Tensor for GPU computation
Create a TF dataset pipeline for effective data augmentation and feed the model
Data augmentation includes taking strides during sampling of the frames from the video e.g. stride 2 would indicate to sample every 2nd frame and so on

**Model Architecture:**

In order to find a suitable architecture I created a vanilla sptial auto-encoder. Individual frames were supplied to the model and the mteric used to identify anomaly was the reconstruction error (L2 norm of model output and input frame[Euclidean distance])

In order to improve the accuracy a spatio-temporal autoencoder was implemented following the paper "Abnormal Event Detection in Videos using Spatiotemporal Autoencoder"

The structure is as follows: 

Based on the reconstruction error a threshold can be set to determine how sensitive the detections are to anomalies (Regularity score)

Once the ground truth can be classified manually into anomaly/non-anomaly frames we can use the area under the receiver operating characteristic (ROC) curve (AUC) to find the perfect threshold (I coudn't get my hands on manually classified frames)

For training I used Adam optimizer to allow it taking the role of setting the learning rate automatically based on the models weight update history

**References:**

Yong Shean Chong, Abnormal Event Detection in Videos using Spatiotemporal Autoencoder (2017)

Mahmudul Hasan, Jonghyun Choi, Jan Neumann, Amit K. Roy-Chowdhury, Learning Temporal Regularity in Video Sequences (2016)

https://github.com/harshtikuu/Abnormal_Event_Detection (regularity score)

Learning Temporal Regularity in Video Sequences Mahmudul Hasan, Jonghyun Choi, Jan Neumann, Amit K. Roy-Chowdhury, Larry S. Davis

Robust Anomaly Detection in Videos Using Multilevel Representations Hung Vu et al (interesting paper but didn't get time to implement)



