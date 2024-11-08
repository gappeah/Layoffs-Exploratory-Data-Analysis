# Layoffs Data Cleaning and Exploratory Data Analysis (EDA) Project

This project uses MySQL to perform data cleaning and exploratory data analysis (EDA) on a dataset detailing company layoffs. The primary goal is to process, clean, and explore the data to gain insights into trends and patterns related to layoffs across various sectors. The project demonstrates best practices for handling missing values, duplicates, and inconsistencies, followed by performing in-depth EDA.

## Database Schema

The Layoffs database comprises a single primary table that encapsulates details about company layoffs. Below is a summary of the structure of this table.

### Layoffs Table
- **Columns:**
  - `company_name` (varchar): The name of the company where layoffs occurred.
  - `industry` (varchar): The industry category of the company.
  - `layoff_date` (date): The date on which layoffs were reported.
  - `total_layoffs` (integer): Total number of employees laid off.
  - `location` (varchar): Location of the company's headquarters or main operational region.
  - `cause` (text): Description of the primary cause of layoffs, if available.
  
### Constraints and Relationships
- **Primary Keys:** The `company_name` column acts as a unique identifier when combined with `layoff_date` to ensure each entry is unique.
- **Constraints:** Proper data types and constraints are applied to ensure the integrity and reliability of the data, such as non-null constraints on crucial columns like `company_name` and `layoff_date`.

## Data Cleaning Process

The data cleaning process focuses on identifying and addressing data quality issues. Below are some of the key cleaning operations:

1. **Handling Missing Values:** Missing values in essential columns, such as `company_name` and `layoff_date`, are removed. Non-essential columns, like `cause`, have missing values replaced where possible.
2. **Duplicate Removal:** Duplicate entries based on `company_name` and `layoff_date` are detected and removed.
3. **Data Type Consistency:** Ensuring consistent data types for columns, especially for numerical values such as `total_layoffs` to enable quantitative analysis.
4. **Standardization:** Standardizes text entries in columns like `industry` and `location` for consistency.

## Exploratory Data Analysis (EDA)

The EDA phase utilizes SQL queries to uncover insights into the layoff trends across industries, dates, and regions. Some of the analyses performed include:

- **Industry Trends:** Analyze which industries experienced the highest layoffs.
- **Geographical Analysis:** Evaluate layoffs by location to identify any region-specific trends.
- **Temporal Trends:** Track the increase or decrease in layoffs over time to identify potential correlation with global events.
- **Cause Analysis:** Examine patterns in the reported causes of layoffs to see if specific triggers are associated with certain industries or time periods.

### Example Queries

Here are a few example SQL queries used in the project:

1. **Get Total Layoffs by Industry:**
   ```sql
   SELECT industry, SUM(total_layoffs) AS total_layoffs
   FROM layoffs
   GROUP BY industry
   ORDER BY total_layoffs DESC;
   ```
   
2. **Identify Layoffs in a Specific Location:**
   ```sql
   SELECT company_name, total_layoffs, layoff_date
   FROM layoffs
   WHERE location = 'San Francisco'
   ORDER BY layoff_date DESC;
   ```

3. **Determine Monthly Layoff Trends:**
   ```sql
   SELECT EXTRACT(YEAR_MONTH FROM layoff_date) AS month, SUM(total_layoffs) AS total_layoffs
   FROM layoffs
   GROUP BY month
   ORDER BY month;
   ```

4. **Top Causes of Layoffs:**
   ```sql
   SELECT cause, COUNT(*) AS frequency
   FROM layoffs
   WHERE cause IS NOT NULL
   GROUP BY cause
   ORDER BY frequency DESC;
   ```

## Setup Instructions

To set up the Layoffs database in MySQL:

1. **Install MySQL:** Ensure MySQL is installed on your system.
2. **Create Database:** Use the `CREATE DATABASE` command to create a database for layoffs.
3. **Execute SQL Scripts:** Run the provided SQL files for data cleaning and EDA using the following commands:
   ```sql
   mysql -u [username] -p layoffs < Data\ Cleaning\ SQL.sql
   mysql -u [username] -p layoffs < Data\ EDA\ SQL.sql
   ```
4. **Load Dataset:** Import the `layoffs.csv` file into MySQL as the primary data source for the analysis.
5. **Connect to Database:** Start querying the database for EDA once the setup is complete.

## Usage

With the database set up, you can execute SQL queries for additional analysis or to customize insights for specific requirements. This allows you to build custom reports and dashboards, providing valuable insights into layoff trends and patterns across sectors.

## License

This project is open-source and licensed under the MIT License. Feel free to use, modify, and distribute this code as per the terms of the license.
