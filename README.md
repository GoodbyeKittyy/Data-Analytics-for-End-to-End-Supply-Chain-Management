# Uber-Data-Analytics-End-To-End-Data-Engineering-Project
Using an Uber dataset, I have built a data model in fact and dimension format and write the transformation code in Python. This code will then be deployed on a compute instance on Google Cloud, where Mage will be installed. We will then load our data onto big query which is in data warehouse and create our final dashboard.

## Architecture
![image](https://github.com/user-attachments/assets/ca575c0d-5448-4d88-9272-99ff878262c0)

## Google Cloud Platform (GCP) Services

### Cloud Storage
Google Cloud Storage is an online file storage service provided by Google as part of its cloud computing platform. It allows you to store and retrieve your data in the cloud, making it accessible from anywhere with an internet connection.

### Compute Engine
Google Compute Enginer is a cloud computing service that provides virtual machines for running applications and services. It allows you to easily create, configure and manage virtual machines with various operating systems and hardware configurations.

### BigQuery
Bigquery is cloud-based data warehouse provided by Google Cloud Platform that allows you to store, analyse, and query large datasets using SQL-like syntax. It is a serverless, highly scalable, and cost-effective solution that can process and analyse terabytes to petabytes of data in real-time.

### Looker
Looker Studio is a web-based data visualization and reporting tool that allows you to create interactive dashboards and reports from various data sources, including Google Analytics, Google Sheets, and BigQuery. It enables you to turn your data into informative and engaging visualisations, which can be easily shared and collaborated on with others.

## Dataset Used
TLC Trip Record Data
Yellow and green taxi trip records include fields capturing pick-up and drop-off dates/times, pick-up and drop-off locations, trip distances, itemized fares, rate types, payment types, and driver-reported passenger counts.

## Data Model

![image](https://github.com/user-attachments/assets/446935c1-7046-4ffd-b3ea-1999d9d5e13d)


## Step 1: Creating Fact & Dimension Table
![image](https://github.com/user-attachments/assets/9ee03830-23d6-4b2d-b655-b03ff45ecf48)


Fact Table:
- Contains the quantitative measures or metrics used for analysis
- Typically contains foreign keys that link to dimension tables
- Contains columns that have high cardinality and change frequently  
- Contains columns that are not useful for analysis by themselves, but are necessary for metric calculation

Dimension Table:
- Contains columns that describe attributes of the data being analysed
- Typically contains primary keys that link to fact tables
- Contains columns that have low cardinality and do not change frequently
- Contains columns that can be used for grouping or filtering data for analysis

Jupyter Notebook (pandas) and the data csv file:


Change Pickup_datetime and dropoff_datetime rom object data type to datetime type. This allows extraction of information from the data.

![image](https://github.com/user-attachments/assets/d58d2083-c0f0-4f9d-9864-4098f5e75335)


Using the data model, reset the index and drop the duplicates. Then extract the required hour, day, month, year, weekday and assign to the new columns created for pick hour, pick day, pick month, etc.

Order the data into the correct format ensuring the correct primary key.

For all required data in the data model, drop dupliclicates, reset the index, assign the index to the required ID column and reorder the information as per the data dimension model.

![image](https://github.com/user-attachments/assets/1d657560-31a7-4980-a979-71a777a91a0b)



For ratecodeID, we require the rate_code_name which is not in the data frame.
Therefore, create a data dictionary, drop the duplicates, reset the index, and assign the index to ratecodeID. Use the rate_code_name and map to the ID so the value is assigned to the standard rate. Finally reorder as per the data model.

![image](https://github.com/user-attachments/assets/48a0e942-9b2b-4802-ad0a-b86e1da63826)



Now that all Dimension Tables created, create the Fact Table by joining the dimension tables based on the common columns between the tables.

![image](https://github.com/user-attachments/assets/d4fa24da-e7a2-45a9-aa71-1dfffc002c83)


