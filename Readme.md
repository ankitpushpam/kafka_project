# Kafka, Spark, and Airflow Data Generation, Streaming, and Processing Project

This repository contains a comprehensive data processing project that encompasses data generation, streaming, and processing using Apache Airflow, Kafka, Apache Spark, Cassandra, and Docker. This project follows a specific architecture designed to handle these tasks efficiently.

## Project Overview

### Data Generation
- The project starts with an API that generates random user data. To achieve this, it utilizes the [Random User Generator API](https://randomuser.me/api/).

### Data Streaming
1. An Apache Airflow Directed Acyclic Graph (DAG) periodically fetches data from the Random User Generator API.
2. The retrieved data is streamed into a Kafka queue.
3. Apache Airflow operates on a PostgreSQL database.

### Kafka
- Data is streamed into Kafka, which is managed by Apache ZooKeeper. ZooKeeper oversees multiple Kafka brokers.
- The Kafka Control Center provides a user interface to visualize data within Kafka brokers.
- The Schema Registry aids in visualizing the schema of the records within Kafka streams.

### Apache Spark
- Data from Kafka is streamed into Apache Spark, which utilizes a master-worker architecture.
- Apache Spark determines which worker handles a job and runs the data processing task.
- Once processed, the data is streamed into Cassandra.

### Cassandra
- A listener retrieves data from Kafka via Apache Spark and streams it directly into Cassandra.

### Docker
- The entire architecture operates within Docker containers.
- A single Docker Compose file orchestrates the deployment of all the necessary components.

## Getting Started

1. Install the required Python packages:

   ```bash
   pip3 install apache-airflow kafka-python cassandra-driver pyspark
   ```

2. Create a keyspace in Cassandra to store the data.

3. Ensure that Docker is installed and running on your system.

4. Deploy the complete architecture by executing the provided Docker Compose file:

   ```bash
   docker-compose up -d
   ```

5. Confirm the health and availability of all services:

   - ZooKeeper: [localhost:2181](http://localhost:2181)
   - Kafka broker: [localhost:9092](http://localhost:9092)
   - Schema Registry: [localhost:8081](http://localhost:8081)
   - Control Center: [localhost:9021](http://localhost:9021)

6. Start the Apache Airflow and Control Center web interface:

   - airflow: [localhost:8080/home](http://localhost:8080/home)
   - control center: [localhost:9021](http://localhost:9021)

7. Configure Apache Spark master and workers according to your requirements.

8. Once the environment is up and running, execute the provided Python scripts to initiate data streaming and processing.

## Project Structure

The project comprises the following components and files:

### Python Scripts

1. **airflow_dags.py**: Python script containing Apache Airflow DAG definitions for data streaming.

2. **pyspark_stream.py**: Python script responsible for streaming data from Kafka to Cassandra using Apache Spark.

These components work together to implement data generation, streaming, and processing in the project.


