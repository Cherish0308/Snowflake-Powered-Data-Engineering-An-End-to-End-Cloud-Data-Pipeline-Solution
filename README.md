# Snowflake-Powered Data Engineering: An End-to-End Cloud Data Pipeline Solution

## Introduction
This project focuses on building a comprehensive end-to-end data engineering pipeline using the **Snowflake Cloud Data Platform**. It covers everything from extracting data via APIs, ingesting it into Snowflake, performing data transformation, modeling using a star schema design, to visualizing the output with **Streamlit**. Additionally, the project includes automation of workflows using **GitHub Actions**, providing a complete real-world data engineering solution.

![Pipeline Overview](./images/pipeline-overview.png)

## Database and Schema Setup
I created a `dev_db` database with four schemas: `stage`, `clean`, `consumption`, and `publish`. These schemas transform data from the raw stage to the final, ready-for-reporting phase.

![Database and Schema Setup](./images/schema-setup.png)

## Virtual Warehouses Setup
I configured several virtual warehouses for different tasks:
- **Load Warehouse**: For data loading.
- **Transform Warehouse**: For data transformation.
- **Streamlit Warehouse**: For reporting.

This setup helps in managing workloads efficiently.

## Role and Permissions
All resources (databases, warehouses) were created under the **System Admin role** to ensure proper permissions and control.

## Setting Up the Bronze Layer: Loading and Staging Raw Data in Snowflake

### Loading JSON Files into Snowflake
- Set up a staging location in Snowflake.
- Created a stage and defined a file format for handling JSON files.
- Uploaded JSON files containing air quality data into the internal stage using Snowflake's data loader.

![Loading JSON Files](./images/json-loading.png)

### Querying and Processing Data
Queried the JSON data directly from the stage using the defined file format.

![Querying JSON Data](./images/query-json.png)

## Automating Data Ingestion
Created a `raw_AQI` table and used the **COPY command** to load the staged data into this table.

![Data Ingestion Automation](./images/data-ingestion.png)

## Setting Up the Silver Layer: Cleaning and Transforming Raw Data

### Cleaning and Deduplication
Handled duplicate records using a **window function** to rank rows and retain the most recent data.

![Data Deduplication](./images/data-deduplication.png)

### Flattening JSON Data
Transformed nested JSON data into a structured tabular format using **Snowflake’s lateral flatten function**.

## Transposing Rows to Columns in the Clean Layer
Used SQL to transpose rows into columns, consolidating multiple pollutant entries into one row per station per hour.

![Transposing Data](./images/transpose.png)

## Calculating the Air Quality Index (AQI)
Wrote Python functions to calculate the AQI based on pollutant measurements and converted missing/null values to zero during transposition.

## Building Fact and Dimension Tables
Created **fact and dimension tables** for air quality data modeling. The model is built on a **dimensional modeling approach**, making it scalable for more complex use cases.

![Fact and Dimension Tables](./images/fact-dim-tables.png)

## Creating Aggregated Fact Tables for Air Quality Index (AQI)
Grouped AQI data to calculate the average AQI values across stations within the same city and recomputed prominent pollutants.

![Aggregated Fact Tables](./images/aggregated-fact.png)

## Deploying a Streamlit Application for Monitoring AQI Trends
Deployed a simple Streamlit app within Snowflake to monitor city-level AQI trends.

![Streamlit App](./images/streamlit.png)

## Automating JSON Data Ingestion into Snowflake Using Python and Snowpark
Automated the process of downloading JSON data from the **Data.gov.in** portal and loading it into Snowflake using Python and **Snowpark**.

## Automating Daily Weather Data Refresh and Aggregation in Snowflake
Integrated weather data with air quality data by building an **aggregated daily fact table**.

![Weather Data Integration](./images/weather-integration.png)

## Next Steps: Dashboard Creation
Build a dashboard on top of the dataset for real-time monitoring of air quality and weather trends.

---

## License
This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.

## Contributing
Contributions are welcome! Please fork this repository and submit a pull request.
