MLOps Pipeline using Apache Airflow and MLflow
Project Overview

This project implements an end-to-end Machine Learning pipeline using Apache Airflow and MLflow for predicting survival on the Titanic dataset.

The goal of the project is to demonstrate a production-style MLOps workflow where machine learning tasks are automated and reproducible. Apache Airflow is used to orchestrate the pipeline tasks through a Directed Acyclic Graph (DAG), while MLflow is used to track experiments, log model parameters and metrics, and manage model versions.

The pipeline automates the entire machine learning workflow including data ingestion, validation, preprocessing, feature engineering, model training, evaluation, and model registration.

Pipeline Architecture

The system integrates two major MLOps tools:

Apache Airflow

Apache Airflow manages the workflow orchestration using a DAG. Each stage of the machine learning pipeline is implemented as a task in the DAG. Airflow ensures that tasks execute in the correct order while also supporting parallel processing and retry mechanisms in case of failures.

MLflow

MLflow is used for experiment tracking and model management. During model training and evaluation, parameters and performance metrics are logged to the MLflow server. The best performing model is automatically registered in the MLflow Model Registry.

DAG Workflow

The pipeline consists of the following stages:

Data Ingestion
Loads the Titanic dataset and logs dataset information.

Data Validation
Checks missing value percentages and demonstrates Airflow retry behavior through intentional failure.

Parallel Processing

Handling missing values

Feature engineering

Data Encoding
Encodes categorical variables and removes unnecessary columns.

Model Training
Trains machine learning models such as Random Forest and Logistic Regression while logging parameters to MLflow.

Model Evaluation
Calculates evaluation metrics including accuracy, precision, recall, and F1-score.

Branching Logic
If the model accuracy is greater than or equal to 0.80, the model is registered. Otherwise, it is rejected.

Model Registration
Approved models are stored in the MLflow Model Registry.

Parallel Task Execution

The pipeline demonstrates parallel processing where:

Missing value handling

Feature engineering

are executed simultaneously using Airflow task parallelization.

Experiment Tracking

Three experiments were executed with different model configurations.

Run	Model	Accuracy
Run 1	Random Forest (100 trees)	0.79
Run 2	Random Forest (200 trees)	0.83 (Best)
Run 3	Logistic Regression	0.79

The Random Forest model with 200 estimators achieved the best performance and was registered in the MLflow Model Registry.

Retry Mechanism

The pipeline demonstrates Airflow’s retry capability. The data validation task intentionally fails on its first attempt to simulate a real-world failure scenario. Airflow automatically retries the task after a specified delay until the task succeeds.

Repository Structure
mlops-airflow-mlflow-titanic
│
├── dags
│   └── mlops_airflow_mlflow_pipeline.py
│
├── data
│   └── titanic.csv
│
├── screenshots
│   ├── airflow_graph_view.png
│   ├── airflow_retry_logs.png
│   ├── mlflow_runs.png
│   └── mlflow_model_registry.png
│
├── reports
│   └── technical_report.pdf
│
├── requirements.txt
└── README.md
How to Run the Project
1 Install dependencies
pip install -r requirements.txt
2 Start MLflow server
mlflow ui
3 Start Airflow services
airflow scheduler
airflow webserver
4 Trigger the DAG

Open Airflow UI:

http://localhost:8080
Trigger the DAG mlops_titanic_pipeline to execute the pipeline.

Technologies Used

Apache Airflow
MLflow
Python
Scikit-learn
Pandas
Docker

Author

Abdul Wasay
