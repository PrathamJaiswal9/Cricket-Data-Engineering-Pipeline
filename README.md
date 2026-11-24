# Cricket Data Engineering Pipeline

An end-to-end data engineering project that ingests live cricket match data from a REST API and processes it using PySpark and Databricks. The project follows the Medallion Architecture (Bronze, Silver, and Gold) to transform raw JSON data into structured datasets and analytical insights.

## Project Architecture

**Data Flow:**

Cricket API → Python API Ingestion → Bronze Layer → Silver Layer → Gold Layer → Analytics

## Technologies Used

- **Python** – API integration and JSON processing
- **REST API** – Cricket match data ingestion
- **PySpark** – Distributed data processing and transformation
- **Databricks** – Data engineering and notebook execution environment
- **Delta Lake** – Storage format for Bronze and Silver tables
- **Spark SQL** – Analytical queries
- **Unity Catalog** – Catalog, schema, and volume management

## Project Workflow

### 1. Bronze Layer – Raw Data Ingestion

- Connects to the Cricket REST API using Python Requests.
- Retrieves current cricket match information in JSON format.
- Stores the raw API response in a Databricks Unity Catalog Volume.
- Creates a Bronze Delta table containing the source endpoint, raw JSON response, and ingestion timestamp.

### 2. Silver Layer – Data Transformation

- Reads raw JSON data from the Bronze table.
- Extracts relevant match information from nested JSON structures.
- Applies an explicit PySpark schema.
- Structures match details such as:
  - Match ID and match name
  - Match type and status
  - Venue and match date
  - Participating teams
  - Team scores
  - Match start and end indicators
- Stores the transformed records in a Silver Delta table.

### 3. Gold Layer – Analytics

Uses PySpark and Spark SQL to generate analytical insights, including:

- Match distribution by match type.
- Venue-wise match count.
- Team-wise match participation.
- Overall match statistics, including total matches and distinct match types and venues.

## Repository Structure

```text
Cricket-Data-Engineering-Pipeline/
│
├── 1_API Ingestion and Bronze Layer.py
├── 2_BronzetoSilverCleanMatchTable.py
├── 3_GoldLayerAnalyticsPrepration.py
├── Flow of Project.drawio
└── README.md
```

## Setup and Execution

1. Create a Databricks workspace with Unity Catalog enabled.
2. Configure a Cricket API account and obtain an API key.
3. Store the API key securely using Databricks Secrets.
4. Configure the secret scope and key referenced in the Bronze notebook:
   - Scope: `cricket-api`
   - Key: `cricapi-key`
5. Import the three Python notebooks into Databricks.
6. Execute the notebooks in the following order:

   - `1_API Ingestion and Bronze Layer.py`
   - `2_BronzetoSilverCleanMatchTable.py`
   - `3_GoldLayerAnalyticsPrepration.py`

**Note:** The project requires a compatible Databricks environment with the necessary Unity Catalog permissions and API access.

## Acknowledgements
This project was recreated and adapted as a guided learning project based on the original work by [Anurag](https://github.com/anuanurag2410/cricket-big-data-project).
