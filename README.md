# Big-Data-Project-Stocks-prediction-with-SVM

## Project Overview

This project, developed as an academic endeavor for the **BIG DATA ANALYTICS COURSE CS4265**, focuses on building a robust, scalable data pipeline for ingesting, processing, and analyzing NYSE stock market data to predict future stock movements using a **Support Vector Machine (SVM)** model. Leveraging a **Big Data** architecture, the aim is to demonstrate an end-to-end solution for financial data forecasting, highlighting best practices in data engineering and high-performance computing.

The core idea is to transform raw, high-volume stock market data into a clean, feature-rich dataset, train an SVM model for prediction, and integrate this model into a production-ready pipeline for continuous insights.

## Features

* **Automated Data Ingestion:** Securely ingests NYSE stock market data.

* **Big Data Processing:** Handles large volumes of historical and streaming financial data efficiently.

* **Feature Engineering:** Extracts relevant features for predictive modeling from raw time-series data.

* **SVM-Based Prediction:** Utilizes Support Vector Machine for stock price prediction.

* **Scalable Architecture:** Designed to handle increasing data volumes and computational demands.

* **MLOps Integration:** Supports model training, versioning, and potential deployment workflows.

* **High-Performance Computing:** Leverages a campus cluster for distributed processing.

## Technologies Used

* **Programming Languages:** Scala

* **Data Processing:** Apache Spark (with Scala)

* **Compute Environment:** KSU's High Performance Compute Clusters (HPCC)

* **Build Tool:** SBT (Scala Build Tool) or Maven (for FAT Jar creation)

* **Machine Learning:** Spark MLlib (for SVM)

* **Version Control:** Git, GitHub

## Architecture

The project follows a typical Big Data architecture, designed to run on high-performance computing clusters:

1.  **Data Ingestion:** Raw NYSE stock data is ingested from external APIs or historical datasets and staged on the cluster's distributed file system.

2.  **Data Transformation (ETL):** Spark applications written in Scala process the raw data. This involves:

    * Cleaning and validation.

    * Feature engineering (e.g., moving averages, volatility indicators, volume analysis).

    * Data normalization and aggregation.

    * Storing transformed, curated data back into the distributed file system (often in Parquet format).

3.  **Model Training:** The prepared dataset is used to train the SVM model using Spark MLlib. Model training is executed as a Spark job on the cluster.

4.  **Model Evaluation & Versioning:** Trained models are evaluated, and model artifacts (e.g., serialized models, metadata) are stored for reproducibility.

5.  **Prediction Pipeline:** The trained SVM model is integrated into a prediction pipeline, executed as a Spark job on the cluster, to generate stock predictions based on new incoming data.

6.  **Monitoring & Logging:** Standard cluster monitoring tools and Spark's logging capabilities track job health, data quality, and model performance.

The core of the application is packaged as a **FAT Jar** (an executable JAR containing all dependencies), designed for submission to the HPCC using tools like `spark-submit`.

## Installation & Setup

To set up this project for execution on a High Performance Compute Cluster (HPCC):

1.  **Clone the repository:**

    ```bash
    git clone [https://github.com/jreakerian/Big-Data-Project-Stocks-prediction-with-SVM.git](https://github.com/jreakerian/Big-Data-Project-Stocks-prediction-with-SVM.git)
    cd Big-Data-Project-Stocks-prediction-with-SVM
    ```

2.  **Scala and Spark Environment:**

    * Ensure Java Development Kit (JDK) is installed, compatible with your Spark version.

    * Install **SBT (Scala Build Tool)** or **Maven** to manage Scala dependencies and build processes.

    * Access to an Apache Spark cluster, such as KSU's HPCC, is required for running the application.

3.  **Build the FAT Jar:**
    Navigate to the project root directory and build the executable JAR. This will compile your Scala code and package all its dependencies into a single JAR file.

    ```bash
    # If using SBT
    sbt clean assembly
    ```

    *(The FAT Jar will typically be found in `target/scala-X.XX/your-project-name-assembly-X.X.jar`)*

4.  **Data Source Access:**

    * Obtain API keys or access methods for your chosen NYSE stock data provider.

    * *(If using a specific data source, provide brief instructions on how to configure access, e.g., environment variables for API keys, or how data is loaded into the HPCC's distributed file system.)*

## Usage

This project is designed to be compiled into a **FAT Jar** and executed on a **High Performance Compute Cluster (HPCC)**.

1.  **Transfer to HPCC:**
    Copy the generated FAT Jar to the HPCC environment where your Spark cluster can access it.

2.  **Run on HPCC using `spark-submit`:**
    Execute your Spark application on the cluster. The exact `spark-submit` command will depend on your cluster's configuration and your application's main entry point and arguments.

    ```bash
    spark-submit \
      --class com.yourpackage.MainApp \  # Replace with your actual main class
      --master yarn \                    # Or 'spark://master_ip:port' for standalone cluster
      --deploy-mode cluster \            # Or 'client' for client-side deployment
      --executor-memory 8G \             # Adjust based on cluster resources and data size
      --num-executors 20 \               # Adjust based on cluster resources and desired parallelism
      /path/on/hpcc/your-project-assembly-1.0.jar \  # Path to your FAT Jar on HPCC
      --input-data-path /hdfs/user/yourname/nyse_raw_data/ \ # Example HDFS input path
      --output-predictions-path /hdfs/user/yourname/nyse_predictions/ # Example HDFS output path
    ```

    *(Adjust `--class`, JAR name, executor memory/count, and input/output paths based on your specific application logic and cluster setup. Ensure your application accepts these paths as arguments.)*

## Data Source

The project utilizes historical and potentially real-time stock market data from the **New York Stock Exchange (NYSE)**. Specific data acquisition methods may include:

* Historical data dumps from providers.

* Real-time data streams via financial APIs.

## Machine Learning Model: Support Vector Machine (SVM)

A **Support Vector Machine (SVM)** is employed for predicting stock movements. SVMs are powerful, versatile machine learning models capable of performing linear or non-linear classification and regression. In this context, SVM is chosen for its effectiveness in handling complex patterns and its ability to generalize well, even with high-dimensional financial data. The model is trained on engineered features derived from historical stock prices, trading volumes, and potentially other market indicators using Spark MLlib.

## Results & Insights

*(Provide a summary of what your project achieved. Be specific with metrics if possible.)*

This pipeline successfully demonstrates:

* Efficient processing of multi-gigabyte NYSE datasets on a high-performance cluster.

* A robust feature engineering process, yielding \[mention specific features, e.g., 'volatility measures', 'momentum indicators'\].

* An SVM model achieving \[65%\] accuracy / F1-score / MSE on the test dataset for \[e.g., 'daily price direction prediction'\].

* Significant processing time reduction compared to traditional methods.

* Enabling faster analytical queries for \[mention specific use cases, e.g., 'historical backtesting', 'market trend identification'\].

## Future Enhancements

* **Real-time Stream Processing:** Integrate with streaming platforms for true real-time data ingestion and processing on the cluster.

* **Model Serving:** Develop an API layer to serve predictions from the trained model.

* **Advanced Feature Engineering:** Incorporate more complex indicators or sentiment analysis.

* **Deep Learning Models:** Explore more advanced models like LSTMs or Transformers for time-series forecasting within the Spark ecosystem.

* **Dashboarding:** Integrate with BI tools for interactive visualization of predictions and market trends.

* **Cluster Resource Optimization:** Further fine-tune Spark configurations and resource allocation for improved efficiency on the HPCC.
