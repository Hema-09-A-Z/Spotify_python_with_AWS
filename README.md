✅ **Project Title:**
 
Spotify Data Ingestion and Analytics on AWS using Serverless Architecture
 
 
---
 
🎯 **Objective:**
 
To build a serverless data pipeline that extracts data from the Spotify API, processes and stores it in Amazon S3, and finally performs analysis using Amazon Athena, with automation using Lambda, CloudWatch, and Glue Catalog.
 
 
---
 
🔧**Tools and Services Used:**
 
Spotify API
 
AWS Lambda
 
Amazon CloudWatch
 
Amazon S3
 
AWS Glue Crawler & Data Catalog
 
Amazon Athena
 
 
 
---
 
🧱 **Architecture Stages:**
 
🔹 **EXTRACT**
 
**1. Spotify API + Python Script:**
 
A Python script is written to call the Spotify API.
 
It fetches music-related metadata (e.g., song name, artist, duration, popularity, etc.).
 
 
 
**2. Amazon CloudWatch (Scheduler):**
 
A CloudWatch Event Rule is scheduled (e.g., daily trigger) to invoke the extraction Lambda function.
 
Ensures automated and periodic data fetching.
 
 
 
**3. AWS Lambda (Data Extraction):**
 
This Lambda function:
 
Calls the Spotify API.
 
Extracts raw data (JSON format).
 
Stores the raw JSON data into Amazon S3 (raw data folder).
 
 
 
 
 
 
---
 
🔹**TRANSFORM**
 
**4. S3 Trigger (Object Put):**
 
When raw data is uploaded to the S3 bucket, it automatically triggers another Lambda.
 
 
 
**5. AWS Lambda (Data Transformation):**
 
Cleans and transforms the raw data:
 
Remove unwanted columns
 
Normalize nested JSON
 
Rename fields or convert types
 
 
Writes the processed data to a different S3 location (e.g., s3://bucket-name/processed/).
 
 
 
 
 
---
 
🔹 **LOAD**
 
**6. Amazon S3 (Transformed Data):**
 
Now holds clean, structured data in a format like Parquet/CSV/JSON.
 
 
 
**7. AWS Glue Crawler:**
 
Periodically or manually run to scan the transformed data folder.
 
Infers schema and updates the AWS Glue Data Catalog with table definitions.
 
 
 
**8. AWS Glue Data Catalog:**
 
Acts as the metadata store for the transformed datasets.
 
Enables querying from Athena by providing table structure.
 
 
 
**9. Amazon Athena (SQL Analytics):**
 
Used to run SQL queries on the transformed data stored in S3.
 
No need to move data; Athena reads directly from S3 using the Glue catalog.
 
 
 
 
 
---
 
📁 Folder Structure in S3 (Example):
 
s3://spotify-pipeline/
  ├── raw/
  │     └── spotify_data_2025-07-09.json
  └── processed/
        └── spotify_data_2025-07-09_clean.csv
 
 
---
 
📌 **Summary:**
 
Step Service Action
 
1 Spotify API Source of the data
2 Lambda Extracts data using Python and saves to S3
3 S3 Stores raw and transformed data
4 Lambda Transforms raw data to clean format
5 Glue Crawler Infers schema from processed data
6 Glue Data Catalog Holds table definitions
7 Athena Runs SQL queries on S3 data
 
 
 
---
 
🔄 **Automation & Triggers:**
 
CloudWatch: Schedules extraction Lambda.
 
S3 Trigger: Automatically calls transform Lambda on new data.
 
Glue Crawler: Can be scheduled or run manually to update catalog.
 
 
 
---
 
**💡 Use Cases:**
 
Analyzing user listening patterns.
 
Trending songs or artist popularity.
 
Building dashboards using tools like QuickSight (optional extension).

![image](https://github.com/user-attachments/assets/e709ddf4-c2d1-46ae-8cbd-a634a39b087b)
