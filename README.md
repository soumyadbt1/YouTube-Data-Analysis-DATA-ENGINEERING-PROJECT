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

3) Folders & files created on S3 Bucket :
 ![s3](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/folders%20created%20in%20s3.JPG)

4) Created IAM role for AWS Glue to access S3 bucket :
 ![s3](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/glue%20s3%20access%20role.JPG)

5) Created Crawler Job & Ran it to gather stats:
 ![EC2 instance Creation](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/crawler%20running.JPG)

7) Table created by crawler job on AWS Glue Service:
![Glue Database](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/tables%20added%20by%20crawler%20on%20catalog%20databse.JPG)
![Glue Table](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/Table%20created%20by%20Crawler%20Job%201.JPG)

8) Now its time to view the data in table, for which we used AWS Athena, but to run queries, we need a S3 bucket for output of query run, which is below:
![S3](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/S3%20bucket%20to%20run%20athena%20query%20output.JPG)

9) On running the SQL, we get this error, which means catalog table din't understand how an array needs to be queried.
![error](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/Not%20able%20to%20understand%20this%20JSON%20data.JPG)

10) We need to have some ETL pre-processing to get the items we need from the JSON source data and then use Athena to query it for which we created a Lambda Function using python code.
![lambda fn](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/lamda%20function.JPG)

11) Created Environment variables to test the Lambda Function
![a](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/lamda%20function%20environment%20variables.JPG)

12) Below is the code used to test, which is picking the item json element and then writing to s3 bucket as a transformation:
    
![code](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/Lamda%20Function%20Code.JPG)

Code : https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Code/lambda_function.py

13) i) Tested Lamda Function code which created parquet file on another S3 location after processing of data:
    
   ![c](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/Lamda%20Function%20Test%20Suceeded.JPG)

   ![d](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/function%20test%20created%20the%20parquet%20files.JPG)
      
  ii) Deployed Lambda Function :
  
   ![b](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/deployed%20lamda%20function.JPG)
   

14) Now we can use AWS Athena to Query the processed / cleaned data with cleaned data stats on Glue as well, we can see the lambda function code worked and created the right columns with data types :
   
 ![d](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/athena%20query.JPG)

 ![e](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/cleansed%20table%20is%20formed.JPG)

15) Ran crawler job for csv and partitioned by Region column table got created.
    
![r](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/ran%20crawler%20for%20csv.JPG)

![e](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/Table%20created%20by%20Crawler%20Job%202.JPG)

16) Join of the 2 tables :
    
![join](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/join.JPG)

17) Manual ETL Script to perform transformation (Schema Change) on one of the fields and also to create partition Key on "Region" field:
    
![e](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/de-on-youtube-cleansed-csv-to-parquet_1_ETL_script.JPG)

18) ETL Code used :
     
https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Code/pyspark_code.py

20) The job run created the region file parquet files in each region folder in cleaned S3 :

![r](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/parquet%20files%20created%20by%20job%20run.JPG)

21) Then we created another crawler job to gather stats from the cleaner S3 bucket :
    
![crawler](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/crawler%20job%203.JPG)

22) Then, Created Automated ETL Script via S3 Trigger so that whenever a storage event happens on S3, the trigger should run the ETL job and finally store the Join data to another final S3 location as you can see.
![f](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/added%20Trigger%20to%20Lambda%20Function.JPG)
![g](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/added%20Trigger%20to%20Lambda%20Function%202.JPG)
![i](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/ETL%20Job%20to%20Join%20and%20Save%20the%20data%20to%20S3.JPG)

23) Final S3 location and files after the ETL job run :
![image](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/final%20s3%20reporting%20data.JPG)
![image](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/Final_reporting_parquet_files.JPG)

24) Finally used Amazon Quicksite to use the final data as source for some analytics and reporting:
  
   i) Quicksite Setup : 
    ![image](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/quicksite%20setup.JPG)
  ii) Data Source set up :
    ![d](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/quicksite%20datasource.JPG)
 iii) Final Dashboard :
    ![e](https://github.com/soumyadbt1/YouTube-Data-Analysis-DATA-ENGINEERING-PROJECT/blob/main/Snapshots/Quicksite%20Dashboard.JPG)

