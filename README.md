# YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT

## Overview
This project aims to securely manage, streamline, and perform analysis on the structured and semi-structured YouTube videos data based on the video categories and the trending metrics.
This project uses services like AWS S3, IAM, Glue, Athena, Lambda and QuickSight.

### Key Components Used:

1. #### Data Storage and Security:
Using AWS S3 for scalable storage of YouTube video data.
Employing AWS IAM to ensure secure access control and data protection.

2. #### Data Processing and Transformation:
Leveraging AWS Glue to extract, clean, and transform data for analytical readiness.

3. #### Query and Analysis:
Utilizing Amazon Athena for serverless querying of the processed data.

4. #### Automation:
Employing AWS Lambda to automate data ingestion and transformation tasks, ensuring a seamless and scalable workflow.

5. #### Visualization and Reporting:
Creating interactive dashboards with Amazon QuickSight to visualize trends and metrics, enabling stakeholders to make data-driven decisions.

#### Dataset Used : 
1. https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Data/CA_category_id.json
![Snapshot of Dataset](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/DataSet.JPG)
2. https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/CA_Video_CSV.JPG
![Snapshots_CA_Video_CSV](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/CA_Video_CSV.JPG)
![Snapshot of both](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/dataset_both.JPG)

#### STEPS FOLLOWED : 

1) Create an S3 bucket :   
 ![S3 creation](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/S3%20Created.JPG)

2) Move files to S3 Bucket :
 ![S3_upload](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/moving%20files%20to%20S3.JPG)

3) Created Crawler Job & Ran it to gather stats:
 ![EC2 instance Creation](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/crawler%20running.JPG)

4) Table created by crawler job on AWS Glue Service:
![Glue Database](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/tables%20added%20by%20crawler%20on%20catalog%20databse.JPG)

5) i) Tested Lamda Function code which created parquet file on another S3 location after procesing of data:
   ![a](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/lamda%20function%20environment%20variables.JPG)
  ii) Deployed Lambda Function
   ![b](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/deployed%20lamda%20function.JPG)
   ![c](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/Lamda%20Function%20Test%20Suceeded.JPG)

6) Lamda Function Code :
 
7) Now we can use AWS Athena to Query the processed / cleaned data with cleaned data stats on Glue as well :
 ![d](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/athena%20query.JPG)

 ![e](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/cleansed%20table%20is%20formed.JPG)

4) ETL Script to perform transformation (Schema Change) on one of the fields and also to create partition Key on "Region" field:
![e](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/de-on-youtube-cleansed-csv-to-parquet_1_ETL_script.JPG)


 ![DAG Code](https://github.com/soumyadbt1/reddit_dag_airflow_pipeline/blob/main/Snapshots/reddit_dag_snap.JPG)

5) Running DAG on Airflow UI :

 ![Airflow UI](https://github.com/soumyadbt1/reddit_dag_airflow_pipeline/blob/main/Snapshots/created%20dags.JPG)
 ![Airflow DAG Success](https://github.com/soumyadbt1/reddit_dag_airflow_pipeline/blob/main/Snapshots/reddit_etl_dag%20on%20airflow.JPG)

6) CSV file move to S3 bucket :

![S3 Bucket](https://github.com/soumyadbt1/reddit_dag_airflow_pipeline/blob/main/Snapshots/csv%20on%20S3.JPG)


