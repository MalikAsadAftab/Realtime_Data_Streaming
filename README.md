
# Realtime Data Streaming

## Table of Contents
1. [Introduction](#introduction)
2. [System Architecture](#system-architecture)
3. [Features](#features)
4. [Installation](#installation)
5. [Usage](#usage)
6. [Generating Random User Data](#generating-random-user-data)
7. [Project Structure](#project-structure)
8. [Contributing](#contributing)
9. [Contact](#contact)

## Introduction
Welcome to the Realtime Data Streaming project! This project aims to provide a robust and scalable data processing pipeline using modern technologies such as Apache Kafka, Apache Airflow, and Apache Spark. The primary goal is to ingest, process, and store large volumes of data efficiently and reliably.

## System Architecture
This section provides an overview of the system architecture used in this project.

### System Architecture Diagram
![System Architecture](https://github.com/MalikAsadAftab/Realtime_Data_Streaming/blob/main/SystemDesign.png?raw=true)

### Data Ingestion
**API**: Acts as the entry point for data into the system. Users or applications send data to the API. The API collects and validates the data before passing it on to the next stage.

### Workflow Orchestration
**Apache Airflow**: Orchestrates the data pipelines, scheduling and managing the workflow of data processing tasks. It ensures that data moves through the system in a controlled and timely manner.

**PostgreSQL**: Stores intermediate data for further processing. This database acts as a staging area where data can be held temporarily before being streamed to Kafka.

### Streaming Platform
**Kafka**: Handles real-time data streaming. It serves as the central hub for data, allowing it to be ingested, processed, and then distributed to various consumers.

**ZooKeeper**: Coordinates and manages Kafka brokers. It ensures that Kafka brokers are synchronized and functioning correctly.

**Control Center**: Monitors and manages Kafka clusters. Provides a user interface for tracking the health, performance, and data flow of Kafka topics.

**Schema Registry**: Manages and enforces data schemas for Kafka topics. Ensures that the data being streamed through Kafka adheres to predefined schemas, enabling consistent data formats and compatibility.

### Data Processing
**Apache Spark**: Processes large-scale data in a distributed manner. Spark performs complex computations and transformations on the data, distributing the workload across its master and worker nodes.

### Final Data Storage
**Cassandra**: Stores processed data for high availability and scalability. Cassandra provides a robust storage solution for the processed data, ensuring it is highly available and can scale with demand.

## Features
- Real-time data ingestion and processing
- Scalable data storage with Cassandra
- Robust workflow orchestration with Apache Airflow
- Real-time data streaming with Apache Kafka
- Distributed data processing with Apache Spark
- Schema enforcement and management with Schema Registry
- Comprehensive monitoring and management with Kafka Control Center

## Installation
### Prerequisites
- Docker and Docker Compose installed
- Git installed

### Installation Steps
1. **Clone the repository**:
   ```bash
   git clone git@github.com:MalikAsadAftab/Realtime_Data_Streaming.git
   ```

2. **Navigate to the project directory**:
   ```bash
   cd Realtime_Data_Streaming
   ```

3. **Build and start the Docker containers**:
   ```bash
   docker-compose up --build
   ```

4. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

## Usage
### Starting the Application
To start the application, run the following command:
```bash
python spark_stream.py
```

### Using the API
You can interact with the API using tools like `curl` or Postman. For example:
```bash
curl -X POST http://localhost:5000/api/data -d '{"key": "value"}' -H "Content-Type: application/json"
```

### Viewing the Dashboard
To view the Airflow dashboard, navigate to `http://localhost:8080` in your web browser.

## Generating Random User Data
We use the [randomuser.me](https://randomuser.me) API to generate random user data for our pipeline.

### Example
To fetch random user data, you can use the following command:
```bash
curl -X GET 'https://randomuser.me/api/?results=10'
```
This command fetches data for 10 random users.

### Integrating with the Pipeline
You can configure your data ingestion script to fetch data from the `randomuser.me` API and send it to the API endpoint for further processing.

Example Python script to fetch data and send to the pipeline:
```python
import requests

# Fetch random user data
response = requests.get('https://randomuser.me/api/')
user_data = response.json()

# Send data to the API endpoint
api_endpoint = 'http://localhost:5000/api/data'
for user in user_data['results']:
    requests.post(api_endpoint, json=user)
```

## Project Structure
```plaintext
├── dags
│   └── __pycache__
│       └── kafka_stream.py
├── env
├── script
│   └── entrypoint.sh
├── .gitignore
├── docker-compose.yaml
├── requirements.txt
├── spark_stream.py
└── SystemDesign.png
```

### Description
- **dags/**: Contains Directed Acyclic Graphs (DAGs) for Apache Airflow.
  - **kafka_stream.py**: Script for Kafka streaming DAG.
- **env/**: Environment-related files (could include virtual environment setups or environment variables).
- **script/**: Shell scripts for various operations.
  - **entrypoint.sh**: Entrypoint script for Docker containers.
- **.gitignore**: Specifies files and directories to be ignored by Git.
- **docker-compose.yaml**: Configuration file for Docker Compose to set up the multi-container Docker application.
- **requirements.txt**: Lists the Python dependencies required for the project.
- **spark_stream.py**: Script for processing data using Apache Spark.
- **SystemDesign.png**: System architecture diagram.

## Contributing
We welcome contributions to this project! Please follow these steps to contribute:

1. **Fork the repository**:
   Click the "Fork" button at the top right corner of the repository page.

2. **Create a new branch**:
   ```bash
   git checkout -b feature/awesome-feature
   ```

3. **Make your changes**:
   Make the necessary changes to the codebase.

4. **Commit your changes**:
   ```bash
   git commit -m "Add awesome feature"
   ```

5. **Push the branch to your fork**:
   ```bash
   git push origin feature/awesome-feature
   ```

6. **Create a Pull Request**:
   Open a pull request from your fork to the original repository.


## Contact
For any questions or feedback, please contact us at:
- Email: asadaftabmalik@gmail.com
- GitHub Issues: [Issue Tracker](https://github.com/MalikAsadAftab/Realtime_Data_Streaming/issues)
