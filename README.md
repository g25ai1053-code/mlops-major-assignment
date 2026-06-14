# mlops-major-assignment
Olivetti Face Classification Web Application (MLOps Major Assignment)
 Overview
This repository hosts the containerized web application built as part of an end-to-end Machine Learning Operations (MLOps) pipeline. The project bridges the gap between machine learning development and production deployment by wrapping a trained predictive model inside a web service, containerizing the runtime environment, and orchestrating it for high availability.

The core application utilizes a scikit-learn Decision Tree Classifier trained on the Olivetti Faces dataset to predict and output human subject identities (Subject IDs) based on user-uploaded facial images.

 Features
Optimized Base Layer: Built using a lightweight python:3.9-slim base image to maintain a minimal container footprint.
Embedded Inference Weights: The model training script (train.py) is executed during the container build stage, safely embedding the serialized weights artifact (savedmodel.pth) directly within the image.
Interactive Interface: Serves a clean HTML upload form on port 5000 that handles image pre-processing (grayscale conversion and resizing to $64 \times 64$) dynamically before passing matrices to the model.
Orchestration Ready: Fully configured to deploy seamlessly onto Kubernetes clusters using a fault-tolerant, self-healing 3-replica state configuration.
