# Sales Analytics Lakehouse — Medallion Architecture on Databricks

An end-to-end data engineering and analytics project built on **Databricks**, implementing the **Bronze → Silver → Gold** Medallion Architecture to transform raw sales data into clean, analytics-ready datasets and business-focused Gold tables for reporting and visualization.

## Architecture

```text
Raw Sales Data
      ↓
┌──────────────────────┐
│    BRONZE LAYER      │
│                      │
│ Raw Data Ingestion   │
│ → Delta Tables       │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│    SILVER LAYER      │
│                      │
│ Data Cleaning        │
│ Data Transformation  │
│ Data Quality         │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│     GOLD LAYER       │
│                      │
│ Analytics Tables     │
│ Business Metrics     │
│ Aggregations         │
└──────────┬───────────┘
           ↓
    Power BI / Genie
```

## Project Overview

The project processes sales data through a three-layer **Medallion Architecture** using Databricks and Apache Spark.

Each layer has a specific responsibility:

* **Bronze** stores the raw ingested data.
* **Silver** cleans, validates, and transforms the data.
* **Gold** uses the Silver data to create business analytics, aggregations, and reporting-ready tables.

The final Gold layer contains analytical views designed around different business questions, making the data ready for visualization in **Power BI** and exploration using **Databricks Genie**.

## Data Model

The project uses sales transaction data containing information about customers, products, orders, dates, sales, profit, and geographical regions.

The Silver layer provides the cleaned dataset used as the main source for the Gold analytics.

The Gold layer then transforms the Silver data into focused analytical views for different business requirements.

### Main Data Elements

| Data Element | Role                                         |
| ------------ | -------------------------------------------- |
| Orders       | Sales transaction information                |
| Customers    | Customer purchasing information              |
| Products     | Product-level information                    |
| Categories   | Product category and subcategory information |
| Regions      | Geographic sales information                 |
| Dates        | Time-based analysis                          |
| Sales        | Revenue and sales performance                |
| Profit       | Profitability analysis                       |

## Bronze Layer — Raw Data Ingestion

The Bronze layer is responsible for ingesting the source sales data into Databricks.

### Main Tasks

* Loaded the raw sales dataset into Databricks.
* Created Delta tables for the ingested data.
* Preserved the original data before applying transformations.
* Stored the raw data as the foundation for downstream processing.

The Bronze layer provides a raw and traceable version of the source data.

## Silver Layer — Data Cleaning & Transformation

The Silver layer prepares the Bronze data for analytics by applying data quality checks and transformations.

### Main Tasks

* Inspected the Bronze table schema.
* Checked data types and data quality.
* Cleaned and standardized the data.
* Converted columns to appropriate data types.
* Processed date-related fields.
* Applied required transformations.
* Created calculated fields required for analysis.
* Handled invalid or inconsistent records.
* Validated the transformed dataset.
* Created the final cleaned Silver table.

The Silver layer acts as the **clean and reliable source for the Gold analytics layer**.

## Gold Layer — Analytics & Business Metrics

The Gold layer is built directly from the cleaned Silver data.

Instead of keeping the Silver table at the transaction level only, the Gold layer performs the required **aggregations, calculations, and analytical transformations** to answer specific business questions.

### Gold Analytics Views

Five main analytical views were created:

### 1. Product Performance

Analyzes product-level sales and profitability.

The view can be used to understand:

* Product sales
* Product profit
* Quantity sold
* Number of orders
* Product/category performance

### 2. Customer Behaviour

Analyzes customer purchasing patterns and overall customer performance.

The view includes metrics such as:

* Total sales per customer
* Total profit
* Number of orders
* Quantity purchased
* Average order value
* Customer purchasing behaviour

### 3. Daily Analytics

Provides time-based sales analytics at the daily level.

It can be used to analyze:

* Daily sales
* Daily profit
* Order volume
* Quantity sold
* Sales trends over time

### 4. Region Analytics Dashboard

Provides geographic analysis of sales performance.

The view includes dimensions and metrics such as:

* Region
* Country
* Sales
* Profit
* Orders
* Quantity

This view is designed to support geographic performance analysis and Power BI dashboards.

### 5. Customer–Product Breakdown

Analyzes the relationship between customers and the products they purchase.

It can answer questions such as:

* Which products are purchased by each customer?
* How much does each customer spend on a product?
* How many units were purchased?
* Which customer-product combinations generate the most sales or profit?

## Gold Layer Data Flow

```text
                SILVER TABLE
                     │
                     │
                     ▼
          ┌─────────────────────┐
          │   Gold Analytics    │
          │                     │
          │ Aggregations        │
          │ Calculated Metrics  │
          │ Business Analysis   │
          └──────────┬──────────┘
                     │
          ┌──────────┼──────────┐
          ↓          ↓          ↓
     Product      Customer     Daily
   Performance    Behaviour   Analytics
          │          │          │
          └──────────┼──────────┘
                     ↓
             Region Analytics
                     │
                     ↓
          Customer–Product
             Breakdown
                     │
                     ▼
              Power BI / Genie
```

## Key Business Metrics

The Gold analytics tables support business metrics such as:

| Metric              | Description                   |
| ------------------- | ----------------------------- |
| Total Sales         | Overall sales generated       |
| Total Profit        | Overall profit generated      |
| Total Orders        | Number of orders              |
| Quantity Sold       | Total products sold           |
| Average Order Value | Average sales value per order |
| Profit Margin       | Profit relative to sales      |
| Unique Customers    | Number of distinct customers  |
| Unique Products     | Number of distinct products   |

## Tech Stack

* **Databricks** — Data engineering platform and compute
* **Apache Spark / PySpark** — Distributed data processing
* **Spark SQL** — Data transformation and analytics
* **Delta Lake** — Storage format for the Medallion Architecture
* **Power BI** — Business intelligence and visualization
* **Databricks Genie** — Natural-language data exploration
* **Git / GitHub** — Version control

## Medallion Architecture

```text
                 RAW SALES DATA
                       │
                       ▼
              ┌─────────────────┐
              │     BRONZE      │
              │                 │
              │ Raw Data        │
              │ Ingestion       │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │     SILVER      │
              │                 │
              │ Cleaning        │
              │ Validation      │
              │ Transformation  │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │      GOLD       │
              │                 │
              │ Analytics       │
              │ Aggregations    │
              │ Business KPIs   │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │   CONSUMPTION   │
              │                 │
              │ Power BI        │
              │ Databricks      │
              │ Genie           │
              └─────────────────┘
```

## Repository Structure

```text
sales-analytics-lakehouse-git/
│
├── Bronze/
│   └── Bronze_Layer_Data_Ingestion.ipynb
│
├── Silver/
│   └── Silver_Layer_Data_Transformation.ipynb
│
├── Gold/
│   └── Gold_Layer_Analytics.ipynb
│
└── README.md
```

## Project Highlights

* Implemented an end-to-end **Bronze → Silver → Gold Medallion Architecture** using Databricks.
* Used **PySpark and Spark SQL** for data processing and analytics.
* Applied data cleaning, transformation, and validation in the Silver layer.
* Built the Gold layer directly from the cleaned Silver data.
* Created analytical tables and aggregations based on business requirements.
* Developed five Gold analytics views covering product, customer, daily, regional, and customer-product analysis.
* Prepared analytics-ready data for **Power BI** dashboards.
* Enabled business-focused data exploration through **Databricks Genie**.
* Used **Delta Lake** for reliable storage across the Medallion layers.
* Managed notebooks and project files using **Git and GitHub**.

---

## Author

**Maryam Galal**

Data Engineer | Data & AI

GitHub: `maryam-galal`
