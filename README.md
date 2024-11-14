# Data Warehouse Project 1

## Project Description
This project involves using Amazon Redshift as a data warehouse to analyze the **CICIDS 2017 dataset**, a benchmark dataset for intrusion detection. The project implements a **star schema** data model, which optimizes query performance and scalability. By running and analyzing eight complex queries, I explore Redshift-specific optimizations, such as **distribution and sort keys**, to understand how they impact query efficiency, performance, and data storage.

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

