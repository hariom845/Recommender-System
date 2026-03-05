# Anime Recommendation System (MLOps Pipeline)
A production-ready deep learning–based recommendation system that generates personalized anime recommendations using user–item interaction data. The project demonstrates an end-to-end MLOps pipeline covering data ingestion, model training, experiment tracking, and scalable cloud deployment.

# System Architecture
-
                +-----------------------+
                |   Google Cloud       |
                |   Storage (GCS)      |
                +----------+-----------+
                           |
                           v
                +-----------------------+
                |   Data Ingestion      |
                |   (Download Dataset)  |
                +----------+-----------+
                           |
                           v
                +-----------------------+
                |   Data Processing     |
                |   Feature Engineering |
                +----------+-----------+
                           |
                           v
                +-----------------------+
                |   Model Training      |
                |   TensorFlow Model    |
                +----------+-----------+
                           |
                           v
                +-----------------------+
                | Experiment Tracking   |
                |     Comet-ML          |
                +----------+-----------+
                           |
                           v
                +-----------------------+
                | Model Versioning      |
                |        DVC            |
                +----------+-----------+
                           |
                           v
                +-----------------------+
                |   Flask API Service   |
                +----------+-----------+
                           |
                           v
                +-----------------------+
                |     Docker Image      |
                +----------+-----------+
                           |
                           v
                +-----------------------+
                |   Kubernetes Cluster  |
                |   Scalable Deployment |
                +----------+-----------+
                           |
                           v
                +-----------------------+
                |  Real-Time API Access |
                +-----------------------+
```
# Dataset
The project uses anime interaction datasets stored in a Google Cloud Storage bucket:
- anime.csv  
- anime_with_synopsis.csv  
- animelist.csv  
These datasets contain:
- User IDs  
- Anime IDs  
- Ratings  
- Anime metadata  
- Synopsis information  
The data is automatically downloaded during the data ingestion stage.
---
- Project Workflow
## 1. Data Ingestion
The pipeline begins by retrieving datasets from Google Cloud Storage (GCS).
Key Tasks:
- Connect to the GCS bucket
- Download dataset files
- Store them locally for preprocessing
Configuration is managed through the `config.yaml` file which defines:
- bucket name
- dataset file names
- model parameters
This makes the pipeline configurable and reproducible.
---
## 2. Data Processing
After ingestion, the raw data is processed to prepare it for model training.
Processing steps include:
- Cleaning missing values
- Encoding user and anime IDs
- Preparing interaction pairs
- Creating training features
The processed data is then used to build the user–item interaction dataset.
---
## 3. Model Architecture
The system uses a deep learning–based recommendation model built with embedding layers.
### Model Design
The model learns latent representations for:
- Users
- Anime items
Both embeddings are combined using a dot product similarity to predict the likelihood of user preference.
User ID → User Embedding
Anime ID → Anime Embedding
             ↓
         Dot Product
             ↓
      Preference Score
Key configuration parameters:
- Embedding size: 128  
- Loss function: Binary Crossentropy  
- Optimizer: Adam  
- Metrics: MAE, MSE  
# API Usage Example
Once the system is deployed, recommendations can be accessed through the REST API.
### Endpoint

```
GET /recommend
```

### Example Request

```
http://<server-ip>/recommend?user_id=25
```

### Example Response

```
{
  "user_id": 25,
  "recommended_anime": [
    "Attack on Titan",
    "Death Note",
    "Fullmetal Alchemist",
    "Steins Gate"
  ]
}
```
This endpoint performs:

1. User ID lookup  
2. Model inference  
3. Top recommendation generation  

---

# Project Folder Structure

```
Recommender-System
│
├── config.yaml
├── deployment.yaml
├── requirements.txt
├── Dockerfile
├── dvc.yaml
│
├── data
│   ├── raw
│   └── processed
│
├── src
│   ├── data_ingestion.py
│   ├── data_processing.py
│   ├── model_training.py
│   ├── inference.py
│
├── api
│   └── app.py
│
└── models
    └── trained_model
```

### Folder Description

**config.yaml**  
Contains configuration for data ingestion and model parameters.

**data/**  
Stores raw and processed datasets.

**src/**  
Contains core ML pipeline code including preprocessing and training.

**api/**  
Flask API used to serve model predictions.

**models/**  
Stores trained model artifacts.

**deployment.yaml**  
Kubernetes configuration for deployment.

---

# Containerization

The application is packaged using Docker to ensure consistent runtime environments.

Docker enables:

- Portable deployments
- Environment isolation
- Simplified production setup

The container includes:

- trained model
- API service
- required dependencies

---

# Kubernetes Deployment

The Docker container is deployed on Kubernetes for scalable production serving.

Deployment configuration includes:

- Kubernetes deployment
- multiple replicas for scaling
- LoadBalancer service for external access

```
Deployment
   ├── Replica 1 (ML API)
   └── Replica 2 (ML API)

LoadBalancer
   ↓
External Traffic
```

This ensures:

- High availability
- Scalability
- production-grade serving
---
# Tech Stack
Programming  
- Python
Machine Learning  
- TensorFlow
Data Processing  
- Pandas  
- NumPy  
MLOps  
- DVC  
- Comet-ML  
Cloud  
- Google Cloud Storage (GCS)
Deployment  
- Flask API  
- Docker  
- Kubernetes
Configuration  
- YAML
---
# Key Features
- Deep learning–based recommendation engine  
- End-to-end ML pipeline  
- Experiment tracking and reproducibility  
- Dataset and model version control  
- Scalable API deployment  
- Cloud-native architecture  
---
# Future Improvements
Possible extensions:
- Hybrid recommendation system  
- Real-time streaming recommendations  
- A/B testing framework  
- User feedback loop  
- Feature store integration  
---
