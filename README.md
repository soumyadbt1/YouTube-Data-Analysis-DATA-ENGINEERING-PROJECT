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

#### Architecture of Project : 
![Image](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/architecture.jpeg)

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

7) Lambda Function Code :
https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Code/lambda_function.py
 
9) Now we can use AWS Athena to Query the processed / cleaned data with cleaned data stats on Glue as well :
 ![d](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/athena%20query.JPG)

 ![e](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/cleansed%20table%20is%20formed.JPG)

8) Manual ETL Script to perform transformation (Schema Change) on one of the fields and also to create partition Key on "Region" field:
![e](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/de-on-youtube-cleansed-csv-to-parquet_1_ETL_script.JPG)

9) ETL Code used : 
https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Code/pyspark_code.py

10) Then, Created Automated ETL Script via S3 Trigger so that whenever a storage event happens on S3, the trigger should run the ETL job and finally store the Join data to another final S3 location as you can see.
![f](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/added%20Trigger%20to%20Lambda%20Function.JPG)
![g](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/added%20Trigger%20to%20Lambda%20Function%202.JPG)
![i](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/ETL%20Job%20to%20Join%20and%20Save%20the%20data%20to%20S3.JPG)

11) Final S3 location and files after the ETL job run :
![image](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/final%20s3%20reporting%20data.JPG)
![image](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/Final_reporting_parquet_files.JPG)

12) Finally used Amazon Quicksite to use the final data as source for some analytics and reporting:
  
   i) Quicksite Setup : 
    ![image](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/quicksite%20setup.JPG)
  ii) Data Source set up :
    ![d](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/quicksite%20datasource.JPG)
 iii) Final Dashboard :
    ![e](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/Quicksite%20Dashboard.JPG)

