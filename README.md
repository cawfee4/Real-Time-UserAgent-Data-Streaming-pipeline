## This project was made to ingest UserAgent data from a website for cleaning, transformation and Analytics using several services from Azure and Power BI for Visualization
### The project follows this architecture
 ![image](https://github.com/cawfee4/Real-Time-UserAgent-Data-Streaming-pipeline/assets/94046123/64349e78-a52a-4be3-9d03-424ac203b0e7)
## 1. Ingestion (Thu thập dữ liệu) 
UserAgent Data from website is sent to Azure Event Hubs by calling API. Event Hubs is an event ingestion service that can handle millions of events per second.
## 2. Website data 
The data sent includes:
- Browser: Browser type of the user
- deviceType: Device type of the user
- ip: User's IP
- os: User's operating system
- path: The path the user accesses
## 3. Data Storage (Lưu trữ dữ liệu)
Data from Event Hubs is then temporarily stored in Azure Data Lake Storage (ADLS) in Delta Lake Format. ADLS is a highly scalable data store that allows for the storage and management of large amounts of unstructured data. Data will be stored and processed in 3 tiers: bronze, silver, gold according to Medallion Architecture
## 4. ETL (Extract, Transform, Load)
Azure Data Factory (ADF) is used to plan and coordinate ETL jobs. ADF supports connecting, transforming, and moving data between different systems. ADF can connect to Azure Databricks to perform complex data transformation tasks. Azure Databricks is an analytics platform based on Apache Spark that enables efficient big data computation.
## 5. Data Processing
In Azure Databricks, data is cleaned, transformed, and aggregated. These data processing steps can range from filtering and cleaning data to complex statistical calculations and analysis
- In the bronze layer, raw data will be ingested in Delta Lake format.
- In the silver layer, data will be cleaned, renamed and columns such as Timestamp (specific date and time the data was added) will be added.
- In the gold layer, data will be aggregated to produce meaningful data for data analysis and data mining.
![image](https://github.com/cawfee4/Real-Time-UserAgent-Data-Streaming-pipeline/assets/94046123/506b6763-a0ea-4190-aef0-9cf7e1074d24)
## 6. Dimension Modeling
The transformed data in the gold layer is then used in Data factory for dimension modeling, the gold layer table is transformed into fact and dimensions table
![image](https://github.com/cawfee4/Real-Time-UserAgent-Data-Streaming-pipeline/assets/94046123/89dd6573-d368-469c-b756-47c54af15f86)
## 7. Data Analysis and Reporting
The transformed and stored data can be accessed by BI (Business Intelligence) tools like Power BI for analysis and reporting
![image](https://github.com/cawfee4/Real-Time-UserAgent-Data-Streaming-pipeline/assets/94046123/aeaa8370-a6dc-40ac-877e-120c888582f9)
