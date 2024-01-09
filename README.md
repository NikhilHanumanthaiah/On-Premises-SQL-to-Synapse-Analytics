# On-Premises SQL to Synapse Analytics
Azure Data Engineering: On-Premises SQL to Synapse Analytics
# Azure Data Engineering Project Documentation

Project Overview:
This end-to-end solution leverages Azure Data Factory for efficient data extraction from on-prem Microsoft SQL Server, Azure Databricks for dynamic transformations, and Azure Synapse Analytics for high-performance analytics. The journey begins with secure data ingestion into Azure Data Lake Storage Gen2, followed by transformative processing in Databricks, and culminates in insightful visualizations through Power BI. Azure Key Vault ensures the security with

### Project Title: Azure Data Engineering: On-Premises SQL to Synapse Analytics

### Project Description:
Provide a brief overview of the project, its objectives, and the problem it aims to solve.
In this project we bring data from on-prem Microsoft SQL to Azure synapse analytics. Data Factory is used to extract and integrate data from on-prem SQL server by using Self Hosted Runtime. Extracted Data from the SQL Server is stored in the Azure Data Lake Gen2 Container called ‘raw’. Containers from ADLS Gen2 is mounted to Databricks and transformed data is stored again in ADLS Gen2 container called ‘Transformed’. Lakehouse concept in Azure synapse analytics to query the data and PowerBI for reporting.
Objective of the project is integrating the data from On-prem SQL server to cloud based Warehouse, Self-Hosted Integration runtime in ADF solves the complexities involved in extracting data form On0prem to Cloud based analytical solutions.
 
1. **Data Extraction (On-Premises SQL Server to ADLS Gen2): **
   - Utilized Azure Data Factory to extract data from the on-premises SQL Server.
      - Created a container and a "raw" folder in ADLS Gen2 to store the extracted data.
   - Used a self-hosted integration runtime for copying data from the on-premises SQL Server to ADLS Gen2.

2. **Data Transformation (Azure Databricks): **
   - Mounted the "raw" folder from ADLS Gen2 into Azure Databricks.
   - Performed data transformations using Databricks and stored the results in the "transformed" container in ADLS Gen2.
   - Used Delta format for storing the transformed data, providing versioning and ACID transactions.

3. **Data Loading (Azure Synapse Analytics): **
   - Created a lake database in Azure Synapse Analytics to organize and structure the data.
   - Loaded the transformed data into Azure Synapse Analytics for further analysis.

4. **Visualization (Power BI): **
   - Connected Power BI to Azure Synapse Analytics to create visualizations and dashboards for data analysis and reporting.

### Security:

- Utilized Azure Key Vault to store sensitive information such as secrets.
- Used Azure IAM rules to provide permissions to create linked Services in ADF and ADLS Gen2.


### Script Descriptions:

- **ADF (Azure Data Factory): **
  - `data_ingestion_pipeline.json` : JSON file describing the data ingestion pipeline in Azure Data Factory.

- **Databricks:**
 - Mounting.py  - Script used to mount the ADLS Gen2 containers to the Databricks.
  - `transformation_script.py`: PySpark script used to transform the raw data in the ADLS Gen2 to container called ‘raw’

## Setup Instructions

1. **Azure Resources: **
   - Azure Data Factory
   - Azure Databricks
  - Azure Synapse Analytics
  - Storage Account – Namespace enabled
  - PowerBI
 -  Azure Key vault
 

## Usage Instructions

1. **Data Ingestion: **
   -Create Azure Data Factory in nearby location.
   -Create Self-Hosted integration runtime and install the Runtime in on-prem network. However, in my case, installed in local system where Microsoft SQL server is installed.
   -Create the Linked Service to connect to on-prem SQL server and use Azure Ky Vault to store the credential.
   -Create pipeline and use the Look Up activity to list all the tables in the on-prem SQL server.
   -Create ForEach activity to take table names from Look Up activity and copy the data from the on-prem SQL Server.
   -Create Notebook Activity in the pipeline to transform the data using the interactive notebook and cluster which is created in the Azure Databricks.
 

2. **Data Transformation: **
   -Create Azure Databricks workspace, and create cluster in the workspace.
   -Create notebook and mount the containers in the ADLS Gen2 to DBFS.
   -Create new notebook and write the code to transform and store the data back to ADLS Gen2.

3. **Data Loading: **
   -Create the Azure Synapse workspace.
   -Create the Database with appropriate database name.
   -Create Lakehouse and create the database using table from ADLS Gen2 from the Create table option in Synapse Analytics Workspace.
 
4. **Visualization: **
   -Load the data from Azure Synapse Analytics to PowerBI.
   -Create required visualization in PowerBI
 
## Conclusion

Successfully completed project for integrating data from on-premises SQL servers to the Azure Synapse Analytics. It's been an adventure, leveraging the power of Azure Data Factory, Databricks, and Synapse Analytics to create a seamless, end-to-end solution. From the secure storage in Azure Data Lake Storage Gen2 to the transformation in Databricks and the beautiful insights in Power BI, this project has not just elevated data engineering capabilities but has also turned data into a storytelling sensation
