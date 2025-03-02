# tokyo-olympics-az-da
Azure end to end project for tokyo olympics data analysis using  Azure cloud.
**Tokyo Olympics Analytics Project Documentation**
**1. Project Overview**
The Tokyo Olympics Analytics Project is a comprehensive data engineering solution designed to process, analyze, and visualize data related to the Tokyo Olympics. This project leverages Azure services—Azure Data Lake Storage Gen2, Azure Databricks, Azure Synapse Analytics—and Power BI to create an interactive analytics platform. The goal is to provide stakeholders with insights into medal distributions, athlete participation, coaching performance, and team events.

**2. Architecture and Major Components**
**2.1 Data Ingestion and Storage**
Azure Data Lake Storage Gen2 (ADLS Gen2):
Purpose: Store raw data related to athletes, coaches, teams, entries by gender, and medals.
Resource Name: [tokyoolympics_proj1]
Container Name: [tokyoolympics_1]
**2.2 Data Transformation Using Azure Databricks**
Azure Databricks Service:

Purpose: Perform data transformation and processing.
Service Name: [tokyoolympics_1db]
Compute Cluster:

Type: General-purpose DS3_V2
Cluster Name: [tokyoolympics_1dbclus]
Notebook Development:

Language: Apache Spark (PySpark)
Operations:
Reading data from ADLS Gen2 using spark.read
Inspecting schema with printSchema()
Previewing data using show()
Applying transformations: filtering, selecting, renaming, and adding calculated columns
Writing transformed data back to ADLS Gen2
Authentication and Connection:

App Registration:
Tenant ID: [TENANT_ID]
Client ID: [CLIENT_ID]
Secret Generation: Utilized for OAuth2 authentication.
Role Assignment: Assigned Storage Blob Data Contributor role to the app.
Mounting ADLS Gen2: Mounted the container to Databricks workspace.
Mount Point: /mnt/transformed_data
Output Location:

Container: [TRANSFORMED_DATA_CONTAINER]

**2.3 Data Analytics Using Azure Synapse Analytics**
Azure Synapse Workspace:

Purpose: Provide a scalable analytics environment.
Workspace Name: [SYNAPSE_WORKSPACE_NAME]
Lake Database:

Name: [tokyo-olympics-lakedb]
Significance: Serves as a unified interface to query data stored in ADLS Gen2 using serverless SQL pools.
External Tables:

Description: Five external tables referencing transformed data in ADLS Gen2.
Creation: Utilized linked services within Synapse.
Serverless SQL Pool:

Usage: Executed SQL queries for analytics on medal counts, athlete participation, and team performance.
**2.4 Reporting and Visualization Using Power BI**
Data Connection:

Method: Connected Power BI directly to Azure Synapse Analytics.
Server Name: [SYNAPSE_SERVER_NAME]
Database Name: [tokyo-olympics-lakedb]
Report Structure:

**Page 1: Medal Analysis**
Visuals: Clustered bar chart, matrix, line chart, map visualization.
**Page 2: Sports & Participation Analysi**s
Visuals: Column chart, stacked bar chart, treemap.
**Page 3: Coaches & Team Events Analysis**
Visuals: Treemap, bar chart, slicers/filters.
DAX Measures and Calculated Columns:

Example Measure:
DAX
**Total Medals = SUM(medals[Gold]) + SUM(medals[Silver]) + SUM(medals[Bronze])**
Purpose: Enabled dynamic analysis and interactivity.
Publishing:

Workspace Name: tokyoolympicsdata-analysis
Description: Published the report to Power BI Service with scheduled data refreshes.
**2.5 Interactivity and User Experience**
Slicers and Filters: Implemented for dynamic data exploration.
Drill-Through Capabilities: Enabled detailed views from high-level summaries.
User Impact: Empowered stakeholders to make data-driven decisions through interactive dashboards.
**3. Summary of Technologies and Resources**
Service/Tool ---->	Purpose	Resource 
Azure Data Lake Storage Gen2 ---->	Store raw and transformed data	[ADLS_GEN2_NAME], [RAW_DATA_CONTAINER], [TRANSFORMED_DATA_CONTAINER]
Azure Databricks ---->	Data transformation and processing	[DATABRICKS_SERVICE_NAME], [DATABRICKS_CLUSTER_NAME]
Azure Synapse Analytics---->Data warehousing and on-demand querying	[SYNAPSE_WORKSPACE], [tokyo-olympics-lakedb], [SYNAPSE_SERVER_NAME]
Power BI---->	Reporting and interactive dashboards:	[tokyoolympicsdata-analysis]
Azure Active Directory---->	Authentication and access control
