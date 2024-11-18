# Data Warehouse Project 1: Intrusion Detection Analysis

## Project Description
This project involves using Amazon Redshift as a data warehouse to analyze the **CICIDS 2017 dataset**, a benchmark dataset for intrusion detection. The project implements a **star schema** data model, which optimizes query performance and scalability. By running and analyzing ten complex queries, I explored Redshift-specific optimizations, such as **distribution and sort keys**, to understand how they impact query efficiency, performance, and also provided some the issues we faced and how i Overcome those issues.

## Objectives
1. Download the **CICIDS 2017 dataset** and perform data preprocessing.
2. Implement the **ETL process** using Python for data transformation.
3. Upload the transformed data to an Amazon S3 bucket for storage.
4. Set up an Amazon Redshift cluster and use DBeaver to load data from S3 into Redshift, executing complex analytics queries.
5. Analyze the impact of **distribution and sort keys** on query performance in Redshift.

## Tables in the Database
The project schema includes the following tables:

### Dimension Tables:
- **sourc_dim**: Contains details about the source IP and port.
- **dest_dim**: Contains details about the destination IP and port.
- **protocol_dim**: Describes network protocols (e.g., TCP, UDP).
- **packet_dim**: Holds packet-level data, such as packet size, length, and statistics.
- **flag_dim**: Holds information about network flags (e.g., SYN, FIN, ACK).
- **date_dim**: Contains timestamp data, which is used for temporal analysis.
- **flow_dim**: Contains detailed flow metrics (e.g., flow duration, bytes per second).

### Fact Table:
- **fact_table**: This central table links all dimension tables and contains network event data, such as attack labels, source and destination information, and protocol details.

## Dimension Tables with Distribution and Sort Keys:
- **sourc_dim_dist**: Contains details about the source IP and port with a distkey and sortkey.
- **dest_dim_dist**: Contains details about the destination IP and port with a distkey and sortkey.
- **protocol_dim_dist**: Describes network protocols (e.g., TCP, UDP) with a distkey and sortkey.
- **packet_dim_dist**: Holds packet-level data, such as packet size, length, and statistics with a distkey and sortkey.
- **flag_dim_dist**: Holds information about network flags (e.g., SYN, FIN, ACK) with a distkey and sortkey.
- **date_dim_dist**: Contains timestamp data, which is used for temporal analysis with a distkey and sortkey.
- **flow_dim_dist**: Contains detailed flow metrics (e.g., flow duration, bytes per second) with a distkey and sortkey.

### Fact Table with Distribution and Sort Key:
- **fact_table**: This central table links all dimension tables and contains network event data, such as attack labels, source and destination information, and protocol details with a distkey and sortkey.

This project uses two sets of table definitions:
- **Dimension and Fact Tables**:
For detailed code on creating the dimension and fact tables, please refer to the REDSHIFT CODE DOCX file.
- **Tables with Distribution and Sort Keys**:
For table definitions with optimized distribution and sort keys, refer to the REDSHIFT CODE 2 DOCX file.

## Star Schema
<img width="903" alt="Star Schema for the Project" src="https://github.com/user-attachments/assets/882c1a3d-89e1-4004-9e26-85f28ed68b40">



## SQL Queries in the Word Document
The attached Word file contains a set of SQL queries that are designed to analyze the data in the aforementioned tables. Each query serves a specific analytical purpose and is explained in detail. Here's a summary of the types of analysis the queries perform:
1. **FTP-Patator Attack Frequency**: Identifies the frequency of FTP-Patator attacks by source IP and port.
2. **Top Source IPs by Event Count**: Retrieves the top source IPs by event count for each attack label.
3. **Average Packet Size**: Computes the average packet size for each attack type.
4. **Hourly Distribution of Traffic**: Analyzes the hourly distribution of traffic for each attack type.
5. **Top Destination IPs**: Identifies the top 3 destination IPs with the highest traffic count for each label.
6. **Total Packets Forwarded by Source and Protocol**: Computes the total packets forwarded by each source IP and protocol.
7. **Top Packets Forwarded by Source and Protocol**: Retrieves the top packets forwarded by source IP and protocol.
8. **Packet Size Spike Detection**: Detects spikes in packet sizes by source IP based on previous entries.
9. **High Flag Count Combinations**: Identifies source and destination combinations with high flag counts, suggesting potential attack behavior.
10. **Anomaly Detection in Network Traffic Using Flag Count and Hourly Analysis**: Identifies potential network traffic anomalies by analyzing high flag counts and packet lengths for TCP/UDP protocols, grouped by source IP, destination IP, protocol, and hour.

## Query Results
Each query was executed on both versions of the table schema (with and without distribution and sort keys). The results of these queries are available in two separate files:
- **Queries Results 1**: Contains output from queries executed on the initial tables (without distribution and sort key optimizations).
- **Queries Results 2**: Contains output from queries executed on the optimized tables (with distribution and sort keys applied)

## Query Performance Comparison
To evaluate the impact of distribution and sort keys on query performance, we included screenshots showing the query execution times for each table setup:
- **Query Performance 1**: Shows query execution times for the initial tables (without distribution and sort keys).
- **Query Performance 2**: Shows query execution times for the optimized tables (with distribution and sort keys).
These files provide a visual comparison of performance differences between the two table configurations, highlighting the benefits of using distribution and sort keys in Amazon Redshift.

## How to Use This Repository

### Step 1: Set up the Redshift Database
Load the preprocessed data into Amazon Redshift using the provided COPY commands. The CSV files, which contain the modified data after the ETL process, should be accessible from the Google Drive link provided in the Data.md file.

### Step 2: Execute Queries
After setting up the database and tables, execute the queries to analyze the network traffic data.

### Step 3: Review Results
Analyze the results from each query to identify key patterns, such as attack frequencies, packet size anomalies, and flagged traffic behavior.

### Step 4: Reference Word Document
The Word file contains detailed explanations of each query, the metrics involved, and how each query contributes to the overall analysis.

## Data Files
The dataset used in this project (CICIDS 2017) is available in CSV format. The CSV files can be accessed fromshould be accessible from the Google Drive link provided in the Data.md file.

## Challenges and Solutions:
### 1. Surrogate Key Mapping in ETL
#### Problem: 
Mapping surrogate keys to large dimension tables like flow and packet caused overhead due to their size and complexity.
#### Details:
Initially, a mapping function was used, but it was slow and inefficient for high-volume data.
Hash-based mapping was introduced to reduce overhead.
Additional Challenge: Inconsistent hash values between the dimension and fact tables due to data type differences (int vs. float).
#### Solution:
Standardized data types across all relevant attributes to ensure consistent hashing.
### 2. Cluster Availability
#### Problem: 
Redshift clusters were intermittently unavailable, requiring cluster recreation.
#### Details:
This issue disrupted workflows and consumed significant time.
#### Solution:
Switching the cluster's location from Virginia to California resolved the problem. Geographical cluster placement can impact availability and stability.
### 3. File Upload Failures
#### Problem: 
Some files failed to upload consistently, irrespective of file size.
#### Solution:
Retried uploading multiple times, which succeeded eventually.

