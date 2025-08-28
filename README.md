# Technical test - Senior BI Analyst - Ruedata 

This project has as goal, demonstrates an end-to-end Extract, Transform, Load (ETL) process using notebooks and more specifically **PySpark** within a **Microsoft Fabric** environment. Connecting to an external SQL database, ingest data into a Fabric Lakehouse, perform data cleaning and exploratory data analysis (EDA), generate a date dimension table into the data model, and finally load it in a Power BI report connected through a lakehouse connection, where we can see insights about the data, and more specifically about the **invoices** table, all its as part of the selection process to the role `Senior BI Analyst`.

##  Project Description

The project uses data from "SpaceParts," a fictional company that sells spaceship parts. The project is divided into two main notebooks:

1.  **`Load SpaceParts data.ipynb`:** Extracts data from a public SQL Server database, standardizes table and column names, and loads it into a Fabric Lakehouse.
2.  **`EDA.ipynb`:** Reads the data from the Lakehouse, performs a comprehensive exploratory analysis to understand its structure and quality, cleans the data (e.g., removing duplicates), and generates a `Dim_Date` dimension table to facilitate time-based analysis.

## Key Features

- **Data Extraction:** Connects to an external SQL Server database using Spark's built-in JDBC connector.
- **Schema Standardization:** Automatically cleans and standardizes table and column names.
- **Lakehouse Ingestion:** Stores data into the lakehouse in Fabric.
- **Exploratory Data Analysis (EDA):** Includes scripts to review the dimensions, schemas, descriptive statistics, null values, and duplicates for each table.
- **Enrichment:** Creates a dedicated Date Dimension table (`Dim_Date`) from the dates found in the fact tables, enriching it with useful attributes like year, month, quarter, day of the week, etc.
- **Data Cleaning:** Identifies and removes duplicate rows in `invoices` table to ensure data quality.

## About the SpaceParts Database

The **SpaceParts** database is a free, public training database provided by Tabular Editor, through the following link: https://tabulareditor.com/blog/reintroducing-the-spaceparts-dataset.

##  Project Structure and Workflow

The workflow follows a logical sequence across the two notebooks:

1.  **External Source:** The `SpacePartsCoDW` SQL Database.
2.  **Notebook 1: `Load SpaceParts data.ipynb`**
    - Connects to the SQL database.
    - Extracts dimension and fact tables.
    - Standardizes all column names.
    - Saves each table to the **Fabric Lakehouse**.
3.  **Notebook 2: `EDA.ipynb`**
    - Reads the newly created tables from the **Lakehouse**.
    - Performs an explratory data analysis.
    - Creates and writes a new `Dim_Date` table into the **Lakehouse**.
    - Remove duplicates from the `invoices` table.

### Usage Guide

1.  **Upload Notebooks:** Upload both `Load SpaceParts data.ipynb` and `EDA.ipynb` to your Fabric workspace.
2.  **Configure Lakehouse:** Ensure your Lakehouse is created and attached to both notebooks.
3.  **Run the Ingestion Notebook: `Load SpaceParts data.ipynb**
    - Open and run all cells in `Load SpaceParts data.ipynb`.
    - This notebook will connect to the external database and populate your Lakehouse with the initial tables. Wait for all cells to execute successfully.
4.  **Run the Exploratory Data Analysis Notebook: `EDA.ipynb`**
    - Once the ingestion is complete, open and run all cells in `EDA.ipynb`.
    - This notebook will read data from your Lakehouse, perform the analysis, create the date dimension, and apply data cleaning steps (only remove duplicates, in this case).
5.  **Open, see and intercact with the Power BI Report**
    - The file in format .pbix contains a report with different insights about the `invoices` table, you can open it and intreract with it **note: you need to have Power BI desktop installed in your device**   

## Notebook Details

### 1. `Load SpaceParts data.ipynb`

This notebook is the starting point and handles all data ingestion tasks.

- **Key Functions:**
  - `load_data_spark()`: Connects to a specific table in the SQL database and loads it into a Spark DataFrame.
  - `standardize_column_names()`: Converts column names to a clean format.
  - `write_tables_to_lakehouse()`: Iterates through all loaded DataFrames, applies column standardization, and saves them into the Lakehouse.

### 2. `EDA.ipynb`

This notebook focuses on the analysis, cleaning, and transformation of the data already present in the Lakehouse.

- **Data Loading:** Reads all tables from the Lakehouse and stores them in a dictionary of DataFrames for easy access.
- **Date Dimension Creation (`Dim_Date`):**
  - Automatically identifies all date columns across the fact tables (`orders`, `invoices`, `forecast`, `budget`).
  - Determines the complete date range (from the earliest to the latest date).
  - Generates a dimension table with one row for every day in that range.
  - Add useful columns like `Year`, `Quarter`, `MonthName`, `DayOfWeek`, etc.
  - Saves the new `Dim_Date` table back to the Lakehouse.
- **Exploratory Analysis:**
  - Prints the dimensions (rows x columns) and schema for each table.
  - Displays a preview of the data.
  - Includes cells to review descriptive statistics, count null values, and check for duplicates.
- **Data Cleaning:**
  - Identifies that the `invoices` table contains duplicate rows.
  - Applies the `.dropDuplicates()` method to clean the table.
 
## Power BI report Details

### 3. `Prueba Técnica – Senior BI Analyst - Space Parts - Invoice Summary.pbix`

This file allows you to see some insights of the database `invoices` in an interactive way

- **Visualization and interaction**
  - Displays an interactive dashboard showing different insights about the database `invoices`, all databases in this project are available for use, but in this case we only use the database `invoices`

If you need more information, you can reaching out with me
