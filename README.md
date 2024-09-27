# Weather Data ETL Pipeline Using Apache Airflow and AWS S3
This project is an ETL (Extract, Transform, Load) pipeline that fetches weather data from the OpenWeatherMap API, transforms the data using Python, and stores it in an AWS S3 bucket. The pipeline is orchestrated and automated using Apache Airflow, which allows scheduling the process to run daily, weekly, or monthly.


## Architecture
![Architecture](https://github.com/vighneshbuddhivant/weather-data-etl-pipeline/blob/e274f458189b8519fc1941a8b19774c394081314/weather_pipeline_architecture.png)

## Project Overview
1. **Extract** weather data from the OpenWeatherMap API for Mumbai.
2. **Transform** the extracted data by converting temperature from Kelvin to Fahrenheit and preparing it for storage.
3. **Load** the transformed data as a CSV file into an AWS S3 bucket (data lake).
The pipeline is managed by **Apache Airflow** and hosted on an **AWS EC2 instance**. Data is scheduled to be fetched daily, and the CSV file is uploaded to an S3 bucket.


## Technologies Used
- **Apache Airflow**: Orchestration and automation of the pipeline.
- **AWS S3**: Data lake for storing transformed weather data.
- **AWS EC2**: Instance for running Airflow and Python scripts.
- **OpenWeatherMap API**: Source of weather data.
- **Python**: For data transformation.
- **Pandas**: For data manipulation and storage.


## Project Workflow
### 1. Setting up EC2 Instance
- Create an EC2 instance (t2.small).
- Connect to the EC2 instance via SSH.

### 2. Installing Dependencies
Run the following commands to set up the EC2 environment:

```bash
sudo apt update
sudo apt install python3-pip
sudo apt install python3.12-venv
python3 -m venv airflow_venv
source airflow_venv/bin/activate
pip install pandas s3fs apache-airflow
```

### 3. Running Airflow

```bash
airflow standalone
```

### 4. Connecting Visual Studio Code to EC2
Connect EC2 to Visual Studio Code using SSH for easier code development. Follow the steps from this video tutorial: [Connect VS Code to EC2](https://www.youtube.com/watch?v=sQQjMnEkGjs).

### 5. AWS S3 Setup
- Create an S3 bucket where the transformed weather data will be stored.
- Modify the IAM role of the EC2 instance to grant it access to the S3 bucket.


## Airflow DAG Tasks
1. is_weather_api_ready
Type: HttpSensor
Purpose: Verifies that the OpenWeather API is reachable before attempting data extraction.
2. extract_weather_data
Type: SimpleHttpOperator
Purpose: Makes an HTTP request to fetch weather data for Mumbai.
3. transform_load_weather_data
Type: PythonOperator
Purpose: Transforms the weather data and uploads the CSV to an S3 bucket.


## Conclusion
This project showcases how to build a fully automated weather data pipeline using OpenWeather API, Apache Airflow, and AWS S3. The pipeline efficiently extracts, transforms, and stores weather data, making it suitable for analytics and further insights. The use of Airflow allows for flexible scheduling and scalability of the process.
