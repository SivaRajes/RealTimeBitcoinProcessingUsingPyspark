# 📈 Real-time Bitcoin Data Processing with PySpark

> **Course**: DATA605 – Spring 2025  
> **Project Title**: Real-time Bitcoin Data Processing with PySpark  
> **Student**: Venkata Siva Rajesh Vithanala  
> **Difficulty**: 3

---

## 🚀 Objective

This project demonstrates how to use **Apache Spark (PySpark)** to ingest, process, analyze, and visualize **real-time Bitcoin price data** from the CoinGecko API using a complete **Dockerized pipeline**.

Students and beginners can use this tutorial to learn how to:
- Ingest streaming data
- Apply transformations and aggregations
- Run time-series machine learning (GBT Regression)
- Save results to S3
- Visualize predictions vs actuals

---




## 🚀 What is PySpark?

**PySpark** is the Python API for Apache Spark, a fast and general-purpose engine for large-scale data processing. It enables parallel computation on large datasets across distributed computing environments.

### ✅ Key Features of PySpark:
- Distributed data processing with **RDDs** and **DataFrames**
- Real-time stream processing with **Spark Streaming**
- Built-in **MLlib** for scalable machine learning
- SQL-like querying for structured data
- Easily integrates with cloud storage (e.g., **AWS S3**, **HDFS**)

---

## 🧱 Use Cases of PySpark
- Real-time analytics (e.g., IoT, finance)
- Machine learning on big datasets
- ETL pipelines for massive structured/unstructured data
- Batch jobs over petabytes of data
- Log analysis, clickstream processing, and more

---


## 📊 Architecture Overview

![Architecture Diagram](work/assets/architecture_diagram.png)



## 🔧 Tech Stack

| Component | Description |
|----------|-------------|
| **PySpark** | Distributed data processing and MLlib for time-series regression |
| **Spark Streaming** | Real-time ingestion of Bitcoin data |
| **CoinGecko API** | Source for Bitcoin OHLC data |
| **Boto3** | Upload results to AWS S3 |
| **Matplotlib** | Plot predicted vs actual prices |
| **Docker + Jupyter** | Portable, reproducible environment |

---

## 🧱 Project Structure

```bash
.
├── work/
│   ├── bitcoin_utils.py         # All reusable logic and API calls
│   ├── run_pipeline.py          # End-to-end pipeline that runs automatically
│   ├── Spring2025.API.ipynb     # API usage walkthrough
│   ├── Spring2025.example.ipynb # End-to-end example run
│   ├── Spring2025.API.md        # Markdown doc for API
│   ├── Spring2025.example.md    # Markdown doc for example
├── Dockerfile                   # Spark + Jupyter container
├── docker-compose.yml           # Mounts, ports, and service config
├── .env.example                 # Sample env (exclude real credentials)
├── requirements.txt             # Python packages
```

---

## 🔁 Workflow Overview

```mermaid
graph LR
    A[fetch_price_as_ohlc()] --> B[start_file_producer()]
    B --> C[Stream files to /Data/stream/]
    C --> D[PySpark Streaming reads JSON]
    D --> E[Aggregate + Filter data]
    E --> F[GBTRegressor model]
    F --> G[Evaluate R² and RMSE]
    G --> H[Save as Parquet and ZIP]
    H --> I[Upload to AWS S3 (if env vars set)]
    I --> J[Plot actual vs predicted 📉]
```

---

## ▶️ How to Run

### 1. Clone the Repo

```bash
git clone https://github.com/SivaRajes/RealTimeBitcoinProcessingUsingPyspark.git



```

### 2. Prepare `.env` File

```bash
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
AWS_DEFAULT_REGION=us-east-2
S3_BUCKET_NAME=your_bucket_name

# Then edit it to include your own AWS credentials and bucket name.
```

### 3. Build and Run Dockerized Spark + Jupyter

```bash
docker-compose up --build
```

This will:
- Start pipeline.py
- Ingest Bitcoin prices (90 seconds)
- Run hourly/daily/moving aggregations
- Train GBTRegressor
- Upload results to S3
- Plot the actual vs predicted chart



## ✅ Outputs
- writes stream of json files to the already existed history data
- Spark stream and parses json to Spark 
- prints Aggregation tables (hourly, daily, moving averages)
- Machine Learning Forecasts (GBTRegressor)
- RMSE and R² metrics
- Parquet file and zipped archive
- Upload to AWS S3
- Visualization plot (`output_plot.png`)

---

## 📚 Documentation

| File | Purpose |
|------|---------|
| `Spring2025.API.md` | Details the helper functions and Spark logic |
| `Spring2025.example.md` | Shows full usage with output |
| `bitcoin_utils.py` | All functions: fetch, stream, ML, upload |
| `run_pipeline.py` | Runs everything automatically |

---

## 📝 Notes from Instructor

✔ No need to share credentials — make sure `.env` can be easily edited    

---

## 📎 Useful Commands

```bash
# Check container logs
docker-compose logs -f

# Rebuild container after changes
docker-compose up --build

# Clean up orphan containers
docker-compose down --remove-orphans
```

---



## 🧠 Learn More

- [Apache Spark Docs](https://spark.apache.org/docs/latest/)
- [PySpark MLlib Guide](https://spark.apache.org/docs/latest/ml-guide.html)
- [CoinGecko API](https://www.coingecko.com/en/api)
