
-----

# RBF - EOD Securities Pricing Analytics Platform

## 📌 Project Overview

The **RBF Analytics Platform** is a fully automated, production-grade End-of-Day (EOD) data pipeline designed for a global investment firm. It replaces fragile, manual CSV-based workflows with a scalable cloud-native architecture.

The platform orchestrates the ingestion, validation, and transformation of U.S. securities pricing and liquidity data, delivering business-ready insights to trading, risk, and research teams via Snowflake and Power BI.

## 💼 Business Context

Before this implementation, RBF analysts faced significant delays and operational risks due to manual data handling. Market movements were often identified too late to inform the next day's trading strategy.

**Key Objectives:**

  * **Automation:** Eliminate manual data collection and formatting.
  * **Reliability:** Ensure high-quality data is available before the market opens.
  * **Scalability:** Build a foundation capable of handling increasing volumes of tickers and historical data.

## 🏗️ Technical Architecture

The platform follows a modular design pattern, ensuring a clear separation of concerns between extraction, storage, and analytics.

1.  **Ingestion:** Python scripts triggered by Airflow extract EOD data from **Polygon.io**, generating standardized CSVs.
2.  **Staging:** Data is pushed to **Amazon S3**, serving as the "Bronze" landing zone.
3.  **Data Warehouse (Snowflake):** A multi-layered architecture transforms raw data into high-performance analytical models.
4.  **Orchestration:** **Apache Airflow (Dockerized)** manages task dependencies, incremental loads, and error handling.
5.  **Analytics:** Curated **Subject Area (SA)** views are exposed to **Power BI** for executive and tactical decision-making.

-----

## ❄️ Snowflake Data Modeling

The Snowflake environment (`SEC_PRICING`) is structured using a Medallion-style approach to ensure data lineage and integrity:

| Layer | Component | Description |
| :--- | :--- | :--- |
| **RAW** | `RAW_EOD_PRICES` | Landed data via External Stages (S3). |
| **CORE** | `EOD_PRICES` | Cleansed, deduplicated, and standardized records. |
| **DM\_DIM** | `DIM_SECURITY`, `DIM_DATE` | Conformed dimensions for attribute-based filtering. |
| **DM\_FACT** | `FACT_DAILY_PRICE` | Central fact table containing OHLCV metrics. |
| **SA** | `VW_SECURITY_PERFORMANCE` | BI-optimized views with pre-calculated 30D returns & liquidity. |

-----

## ⚙️ Pipeline Orchestration (Airflow)

The Airflow DAG manages the end-to-end lifecycle of a data batch:

  * **Extraction:** Fetches daily OHLCV data for the universe of securities.
  * **Validation:** Performs date-level checks to prevent duplicate processing.
  * **Transformation:** Executes SQL `MERGE` statements to update Fact and Dimension tables incrementally.
  * **Monitoring:** Integrated **Slack Alerts** notify the team of successful loads or failures in real-time.

-----

## 📊 Analytics & Insights

The **Subject Area (SA)** layer provides high-value datasets for the following dashboards:

  * **Market Liquidity:** Tracking sector-wise liquidity contribution and ETF trends.
  * **Performance Monitoring:** Rolling 30-day returns and volatility for watchlists.
  * **Volume Analysis:** Identifying top 20 equities by traded value to spot institutional movement.

> 🔗 **[View Live Power BI Dashboard Preview](https://www.google.com/search?q=%23)** *(Replace with your link)*

-----

## 🚀 Key Features & Impact

  * **Fully Automated:** Zero-touch processing from API to Dashboard.
  * **Data Integrity:** Robust validation prevents downstream pollution from missing or malformed API data.
  * **Business Agility:** Reduced the time-to-insight from \~4 hours (manual) to \<15 minutes (automated).
  * **Scalable:** Currently optimized for U.S. Equities; design allows for seamless addition of Crypto or FX data.

-----

## 🛠️ Tech Stack

  * **Languages:** Python, SQL
  * **Data Warehouse:** Snowflake
  * **Cloud:** AWS (S3, IAM)
  * **Orchestration:** Apache Airflow
  * **Containerization:** Docker & Docker Compose
  * **BI:** Power BI
  * **Collaboration:** Slack API (Notifications)

-----

## 📂 Project Structure

```bash
├── airflow/
│   ├── dags/             # Ingestion & Transformation DAGs
│   ├── scripts/          # Python extraction & S3 upload logic
│   └── docker-compose.yaml
├── snowflake/
│   ├── ddl/              # Table & View definitions
│   └── transformations/  # MERGE and Analytics SQL
├── power_bi/             # Dashboard templates and PBIX files
└── README.md
```

## 🙏 Acknowledgements

Special thanks to **Codebasics** for providing the structured framework and real-world engineering principles that informed the design of this platform.

-----

<details>

---



---

  
</details>

























<details>

<img width="901" height="559" alt="image" src="https://github.com/user-attachments/assets/0df5d949-2335-4dd4-b24e-979212bb4552" />

<img width="1296" height="643" alt="image" src="https://github.com/user-attachments/assets/f21d6b45-8ed5-41f5-b837-3c097030439b" />

<img width="1136" height="574" alt="image" src="https://github.com/user-attachments/assets/fd2ad001-3ac7-40aa-a06e-13ffe7075ef1" />
<img width="1166" height="576" alt="image" src="https://github.com/user-attachments/assets/dffc549a-8a5f-459c-8396-f9c81dbdebe0" />
<img width="901" height="566" alt="image" src="https://github.com/user-attachments/assets/c95a4bfb-5307-4541-be3b-17bea099cbb3" />
  
</details>

