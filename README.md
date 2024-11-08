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

Here are the setup instructions specifically for MySQL Workbench, including steps to import the `.csv` file.

---

## Setup Instructions

To set up and run the Layoffs Data Cleaning and EDA project through MySQL Workbench, follow these steps:

### 1. Install MySQL and MySQL Workbench
Ensure you have both **MySQL Server** and **MySQL Workbench** installed on your system. MySQL Workbench is a GUI that will allow you to manage the database, execute SQL scripts, and import the `.csv` file.

### 2. Create a New Database in MySQL Workbench
1. Open **MySQL Workbench** and connect to your MySQL server.
2. In the **Navigator** panel, right-click on the **Schemas** area and select **Create Schema**.
3. Name the schema (for example, `LayoffsDB`) and click **Apply**.
4. Confirm by clicking **Apply** again to create the new database.

### 3. Set Up the Database Structure
1. Open a new SQL file in MySQL Workbench by navigating to **File > Open SQL Script** and select the `Data Cleaning SQL.sql` file provided for this project.
2. Once loaded, select your newly created schema (e.g., `LayoffsDB`) in the **Schemas** panel to set it as the default database.
3. Run the SQL script by clicking the **Execute** button (lightning icon) to set up the necessary table structure and constraints.

### 4. Import the `.csv` File into the Layoffs Table
1. Go to **Server > Data Import** in MySQL Workbench.
2. Choose **Import from Self-Contained File** and select the `layoffs.csv` file.
3. In the **Default Target Schema** dropdown, select your newly created database schema (e.g., `LayoffsDB`).
4. Under **Import Options**, select the option to create a new table if necessary, or choose the `layoffs` table if it already exists in your schema.
5. Start the import process by clicking **Start Import**.

### 5. Run the EDA SQL Script
1. Once the data is imported, open the `Data EDA SQL.sql` file by navigating to **File > Open SQL Script**.
2. Ensure that your `LayoffsDB` schema is selected as the active database in the **Schemas** panel.
3. Run the EDA SQL script by clicking the **Execute** button to analyze the data using predefined queries.

### 6. Verify and Start Querying
With the data structure set up and data imported, you can now run custom SQL queries in MySQL Workbench to further analyze the data or gain additional insights.

## Usage

With the database set up, you can execute SQL queries for additional analysis or to customize insights for specific requirements. This allows you to build custom reports and dashboards, providing valuable insights into layoff trends and patterns across sectors.

## License

This project is open-source and licensed under the MIT License. Feel free to use, modify, and distribute this code as per the terms of the license.
