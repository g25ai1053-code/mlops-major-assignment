# End-to-End MLOps Pipeline for Olivetti Face Classification

This repository contains the implementation of an automated, end-to-end Machine Learning Operations (MLOps) pipeline built as part of the MLOps Major Assignment. The pipeline encompasses model development, Continuous Integration (CI) via GitHub Actions, containerization with Docker, and orchestration using Kubernetes with fault-tolerant configurations.

##  Project Links
**GitHub:** https://github.com/g25ai1053-code/mlops-major-assignment

 **Docker Hub:** https://hub.docker.com/u/g25ai1053

---

##  Features & Architecture

1. **Model Development (`dev` branch):** * Trains a `scikit-learn` Decision Tree Classifier on the Olivetti Faces dataset.
   * Dataset is split using a strict 70% train and 30% test partition scheme.
   * Model artifacts are serialized and stored via `joblib` as `savedmodel.pth`.
2. **Continuous Integration (CI):**
   * Configured via GitHub Actions (`.github/workflows/ci.yml`) to automatically trigger on code pushes.
   * Spins up an isolated runner, resolves dependencies, and strictly executes the training and evaluation steps to ensure code health.
3. **Containerization (`docker_cicd` branch):**
   * Packages a Flask web application server inside a lightweight, highly optimized Docker container image (`python:3.9-slim`).
   * Provides an interactive UI for users to upload facial images and retrieve real-time subject classification IDs.
4. **Orchestration & Resiliency:**
   * Uses Kubernetes configuration templates (`k8s-deployment.yaml`) to enforce high availability with a strict **3-replica minimum** setup.
   * Implements automated self-healing capabilities to instantly recover from pod failures or manual disruptions.

---

##  Repository Structure & Branch Strategy

The project utilizes a strict multi-branch Git workflow strategy without cross-merging to maintain production isolation:

* **`main`:** Contains base project setup metadata (`README.md`, `.gitignore`).
* **`dev`:** Contains the primary machine learning code base (`train.py`, `test.py`) and the GitHub Actions automation logic.
* **`docker_cicd`:** Contains delivery files including the Flask web application backend (`app.py`), environmental `Dockerfile`, and the Kubernetes architecture manifests (`k8s-deployment.yaml`).

```text
.
├── .github/
│   └── workflows/
│       └── ci.yml             # GitHub Actions automation pipeline
├── app.py                     # Flask web app backend controller
├── train.py                   # Model ingestion & training lifecycle script
├── test.py                    # Inference validation & scoring test script
├── requirements.txt           # Environment execution dependency manifest
├── Dockerfile                 # Container image packaging instructions
├── k8s-deployment.yaml        # Kubernetes deployment & NodePort service manifest
├── .gitignore                 # Tracked path exclusion instructions
└── README.md                  # Project documentation overview
```
```
Code Push (GitHub)
    ↓
GitHub Actions (CI/CD)
    ├─ Train Model
    ├─ Run Tests
    ├─ Build Docker Image
    └─ Push to Docker Hub
    ↓
Deploy Options:
    ├─ Local: python app.py
    ├─ Docker: docker-compose up
    └─ Kubernetes: kubectl apply -f k8s-deployment.yaml
    ↓
User Interface (Port 5000)
    ├─ Upload Face Image
    ├─ Get Real-time Prediction
    └─ View Classification ID (0-39)
```


