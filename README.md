# YouTube Comment Sentiment Analysis

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![MLflow](https://img.shields.io/badge/MLflow-Tracking-0194E2.svg)](https://mlflow.org/)
[![DVC](https://img.shields.io/badge/DVC-Data%20Version%20Control-945DD6.svg)](https://dvc.org/)
[![Flask](https://img.shields.io/badge/Flask-API-000000.svg)](https://flask.palletsprojects.com/)

## 🎯 Project Overview

An end-to-end machine learning system that performs real-time sentiment analysis on YouTube comments using Natural Language Processing (NLP) and a LightGBM classifier. The project features a complete MLOps pipeline with experiment tracking, model versioning, and REST API deployment.

### Key Features

- **Advanced NLP Pipeline**: Text preprocessing with lemmatization, stopword removal, and TF-IDF vectorization
- **Production-Ready ML Model**: LightGBM classifier optimized for sentiment classification
- **MLOps Best Practices**: 
  - Experiment tracking with MLflow
  - Data version control with DVC
  - Pipeline orchestration with DVC
  - Model registry integration
- **REST API**: Flask-based API for real-time predictions with CORS support
- **Visualization**: Word clouds and temporal sentiment analysis
- **AWS Integration**: Deployment-ready with Docker and AWS CodeDeploy

## 🛠️ Technology Stack

- **ML/DL**: LightGBM, Scikit-learn, NLTK
- **MLOps**: MLflow, DVC, DagHub
- **API**: Flask, Flask-CORS
- **Cloud**: AWS (S3, EC2, CodeDeploy)
- **Containerization**: Docker
- **Visualization**: Matplotlib, Seaborn, WordCloud

## 📁 Project Structure

```
├── src/
│   ├── data/               # Data ingestion and preprocessing
│   │   ├── data_ingestion.py
│   │   └── data_preprocessing.py
│   ├── model/              # Model building, evaluation, and registration
│   │   ├── model_building.py
│   │   ├── model_evaluation.py
│   │   └── register_model.py
│   └── visualization/      # Visualization scripts
│
├── flask_app/              # Flask API for predictions
│   ├── app.py
│   └── requirements.txt
│
├── deploy/                 # Deployment scripts
│   └── scripts/
│       ├── install_dependencies.sh
│       └── start_docker.sh
│
├── notebooks/              # Jupyter notebooks for EDA
├── dvc.yaml               # DVC pipeline configuration
├── params.yaml            # Hyperparameters and configuration
├── Dockerfile             # Container configuration
├── appspec.yml            # AWS CodeDeploy specification
└── requirements.txt       # Python dependencies
```

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- pip
- (Optional) AWS account for deployment
- (Optional) MLflow tracking server

### Installation

1. Clone the repository:
```bash
git clone https://github.com/AshutoshMishra-UJ/Comment_Sentiment_Analysis.git
cd Comment_Sentiment_Analysis
```

2. Create and activate virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Download NLTK data:
```python
python -c "import nltk; nltk.download('stopwords'); nltk.download('wordnet')"
```

## 💻 Usage

### Training Pipeline

Run the complete ML pipeline using DVC:

```bash
# Initialize DVC (first time only)
dvc init

# Run the entire pipeline
dvc repro

# Run specific stages
dvc repro data_ingestion
dvc repro model_building
```

### Flask API

Start the Flask API server:

```bash
cd flask_app
python app.py
```

API Endpoints:
- `POST /predict`: Single comment sentiment prediction
- `POST /predict_with_timestamps`: Batch predictions with timestamps
- `GET /wordcloud`: Generate word cloud visualization
- `GET /sentiment_over_time`: Temporal sentiment analysis

Example API request:
```python
import requests

url = "http://localhost:5000/predict"
data = {"comment": "This video is amazing!"}
response = requests.post(url, json=data)
print(response.json())
```

### Model Training

Customize hyperparameters in `params.yaml`:

```yaml
model_building:
  ngram_range: [1, 3]
  max_features: 10000
  learning_rate: 0.09
  max_depth: 20
  n_estimators: 367
```

## 📊 Model Performance

The LightGBM model achieves competitive performance on YouTube comment sentiment classification with:
- Optimized hyperparameters through MLflow experiments
- TF-IDF feature extraction (1-3 grams, 10k features)
- Comprehensive evaluation metrics tracked in MLflow

## 🔧 Configuration

### MLflow Setup

Configure MLflow tracking URI in your code or environment:

```python
mlflow.set_tracking_uri("http://your-mlflow-server:5000/")
```

### DVC Remote Storage

Set up DVC remote (S3 example):

```bash
dvc remote add -d myremote s3://your-bucket/path
dvc push
```

## 🐳 Docker Deployment

Build and run the Docker container:

```bash
docker build -t yt-sentiment-api .
docker run -p 5000:5000 yt-sentiment-api
```

## 📈 MLOps Pipeline

The project implements a complete MLOps workflow:

1. **Data Ingestion**: Load and split data
2. **Preprocessing**: Clean and transform text data
3. **Model Building**: Train LightGBM with TF-IDF features
4. **Evaluation**: Generate metrics and confusion matrix
5. **Model Registry**: Register best models in MLflow
6. **Deployment**: Serve via Flask API

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 👤 Author

**Ashutosh Mishra**
- GitHub: [@AshutoshMishra-UJ](https://github.com/AshutoshMishra-UJ)

## 🙏 Acknowledgments

- Project structure based on [Cookiecutter Data Science](https://drivendata.github.io/cookiecutter-data-science/)
- MLflow for experiment tracking
- DVC for data version control

---

*For questions or support, please open an issue in the GitHub repository.*
