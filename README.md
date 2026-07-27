# Real-Time Happiness Prediction Pipeline

## Overview

This project implements an end-to-end real-time data engineering pipeline that combines Apache Kafka, Machine Learning, and MySQL to predict country Happiness Scores using data from the World Happiness Report (2015–2019).

The solution simulates a production-ready streaming architecture by ingesting data through Kafka, performing real-time machine learning inference, storing predictions in a relational database, and generating interactive analytical dashboards.

---

# Key Features

- Real-time data streaming using Apache Kafka
- Automated ETL pipeline for data normalization
- Machine Learning inference during data consumption
- Persistent storage in MySQL
- Interactive KPI dashboard with Plotly
- Dockerized Kafka environment
- End-to-end workflow from ingestion to visualization

---

# Project Architecture

```text
CSV Files (2015–2019)
          │
          ▼
Kafka Producer
          │
          ▼
Apache Kafka Topic
          │
          ▼
Kafka Consumer
          │
     ┌────┴────────────┐
     │                 │
     ▼                 ▼
ML Prediction     MySQL Storage
          │
          ▼
Interactive Dashboard
```

---

# Project Structure

```text
Real-Time-Happiness-Pipeline/
│
├── csv/
│   ├── 2015.csv
│   ├── 2016.csv
│   ├── 2017.csv
│   ├── 2018.csv
│   └── 2019.csv
│
├── data/
│   └── predictions_streaming.csv
│
├── kafka/
│   ├── kafka_producer.py
│   └── kafka_consumer.py
│
├── kpis/
│   ├── generar_kpis.py
│   └── dashboard_kpis.html
│
├── model_regresion/
│   ├── modelo_regresion_lineal.pkl
│   └── model_utils.py
│
├── notebooks/
│   ├── EDA_Happiness_Report.ipynb
│   └── Modelos_Regresion_Happiness.ipynb
│
├── docker-compose.yml
├── requirements.txt
└── README.md
```

---

# Workflow

1. Historical World Happiness datasets are loaded.
2. Records are streamed into Apache Kafka.
3. A Kafka Consumer receives each message.
4. The trained Machine Learning model generates predictions in real time.
5. Predictions are stored in MySQL.
6. KPI dashboards are generated from the stored results.

---

# Machine Learning

A Multiple Linear Regression model was trained using six numerical features together with the **Country** variable encoded through **One-Hot Encoding**.

The preprocessing pipeline and trained model are serialized into a single `.pkl` artifact, ensuring identical transformations during both training and production inference.

### Model Performance

| Metric | Value |
|---------|------:|
| R² Score | 0.95 |
| MAE | 0.25 |
| RMSE | 0.32 |
| MAPE | 4.2% |

### Features

- GDP per capita
- Social support
- Healthy life expectancy
- Freedom to make life choices
- Generosity
- Perceptions of corruption
- Country (One-Hot Encoding)

---

# KPI Dashboard

The project automatically generates an interactive HTML dashboard containing:

- Overall model performance
- Train vs Test comparison
- Interactive world map
- Top 10 happiest countries
- Temporal evolution
- Regional analysis
- Prediction error distribution

---

# Installation

## Requirements

- Python 3.12+
- Docker
- MySQL
- Git

## Clone the repository

```bash
git clone https://github.com/JuanHoyos329/Workshop-3.git
cd Real-Time-Happiness-Pipeline
```

## Install dependencies

```bash
pip install -r requirements.txt
```

## Start Kafka

```bash
docker-compose up -d
```

## Train the model

```bash
cd model_regresion
python model_utils.py
```

## Start the Kafka Consumer

```bash
cd kafka
python kafka_consumer.py
```

## Start the Kafka Producer

```bash
cd kafka
python kafka_producer.py
```

## Generate the Dashboard

```bash
cd kpis
python generar_kpis.py
```

---

# Technology Stack

| Category | Technologies |
|----------|--------------|
| Programming Language | Python |
| Streaming | Apache Kafka |
| Machine Learning | Scikit-learn |
| Data Processing | Pandas, NumPy |
| Database | MySQL |
| Visualization | Plotly |
| Containerization | Docker |
| Data Source | CSV |

---

# Repository Contents

| Directory | Description |
|-----------|-------------|
| `notebooks/` | Exploratory analysis and model development |
| `model_regresion/` | Model training and serialized artifacts |
| `kafka/` | Producer and Consumer implementation |
| `kpis/` | Dashboard generation |
| `data/` | Generated prediction datasets |

---

# Future Improvements

- Deploy the pipeline on cloud infrastructure.
- Replace CSV ingestion with live API data.
- Integrate model monitoring.
- Add automated retraining workflows.
- Deploy the dashboard as a web application.

---

# Author

**Juan Andrés Hoyos Rodríguez**

Data Engineering & Artificial Intelligence

2025
