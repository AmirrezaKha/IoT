
# IoT Predictive Maintenance Platform

This project is an end-to-end pipeline for real-time IoT sensor data processing, anomaly detection, and model serving using Apache Spark, MinIO, and Parquet-backed Iceberg tables. Designed for scalability, modularity, and cloud/on-prem flexibility.

## 🚀 Features

- **Real-time Data Ingestion** from public IoT APIs or Kafka streams
- **Apache Spark** for distributed processing and data transformations
- **MinIO + Iceberg** for scalable table management in object storage
- **XGBoost** for anomaly detection on sensor metrics (e.g., temperature, vibration)
- **FastAPI** service for serving model predictions
- **Docker-Compose** to orchestrate the platform locally

## 📂 Directory Structure

```
iot-predictive-maintenance/
├── data/
│   ├── raw_data/            # Raw incoming data
│   ├── processed_data/      # Processed Parquet data via Spark
│   └── model_data/          # Training/validation data in Iceberg format
├── docker/
│   ├── kafka/               # Kafka setup
│   ├── spark/               # Spark master/worker
│   └── fastapi/             # FastAPI app
├── scripts/
│   ├── data_pipeline.py     # Pulls and writes data to Iceberg
│   ├── anomaly_detection.py # XGBoost training + scoring
│   ├── model_training.py    # Spark ML training
│   └── model_serving.py     # FastAPI server
├── notebooks/
│   └── data_exploration.ipynb
├── logs/                    # Log files
├── config/                  # Kafka, Spark, API configuration
├── requirements.txt         # Python dependencies
├── docker-compose.yml       # Service orchestration
└── README.md
```

## 🔗 External Dependencies

- **Public Data Stream (Optional)**: [ThingSpeak](https://thingspeak.com/channels/public)
- **Apache Iceberg**: Table format for huge datasets with fast metadata and versioning
- **MinIO**: S3-compatible object storage
- **Apache Spark**: Cluster computing engine

## ⚙️ Setup

### Prerequisites

- Docker & Docker Compose
- Python 3.9+
- Optional: Spark + Iceberg libraries

### Build & Run

```bash
docker-compose up --build
```

Data will be ingested, processed, and stored in MinIO as Iceberg tables. You can connect to Spark UI at `http://localhost:4040` and query tables.

### Train Model

```bash
python scripts/model_training.py
```

### Serve Predictions

```bash
uvicorn scripts.model_serving:app --reload --port 8000
```

## 🧪 Example FastAPI Endpoint

```http
POST /predict
{
  "sensor_id": 1,
  "temperature": 30.5,
  "humidity": 42.0
}
```

Returns:
```json
{
  "anomaly": true,
  "score": 0.873
}
```

## 🛠️ Improvements Roadmap

- Add Prometheus & Grafana for real-time monitoring
- Introduce Apache NiFi for low-code ETL orchestration
- Replace simulated data with real IoT stream (MQTT/Kafka)
- Integrate MLflow or Weights & Biases for model tracking

---

**License**: MIT  
**Maintainer**: Your Name  
