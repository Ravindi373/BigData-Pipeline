# Big Data Pipeline: Bronze–Silver–Gold Architecture
### (CCS3309) Big Data Assignment 02

A PySpark + MongoDB Atlas pipeline that turns raw e-commerce transaction data into analytics-ready insights, using the Bronze–Silver–Gold (Medallion) architecture.

## Overview

- **Bronze** – Raw CSV data ingested into Spark, stored as partitioned Parquet
- **Silver** – Data cleaned: nulls, negative quantities, cancelled invoices, invalid prices, and duplicates removed
- **Gold** – Feature-engineered data (revenue, RFM metrics, time-based features) written to MongoDB Atlas

## Tech Stack

- **PySpark 3.5.1** – distributed processing
- **MongoDB Atlas** – Gold layer storage
- **Google Colab** – execution environment
- **Parquet** – partitioned storage format

## Dataset

Retail transaction data with fields: `Invoice`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `Price`, `Customer ID`, `Country`.

## Pipeline Steps

1. **Setup & Ingestion** – install dependencies, connect to MongoDB, load raw CSV
2. **Data Cleaning** – handle missing values, remove invalid/duplicate records, generate a Data Quality Report
3. **Feature Engineering** – calculate revenue, time-based features, basket metrics, and RFM (Recency, Frequency, Monetary)
4. **MongoDB Modeling** – write three Gold-layer collections: `fact_invoices`, `dim_customers`, `dim_products`
5. **Indexing** – create indexes on `CustomerID`, `InvoiceDate`, `customer_segment`, and `total_product_revenue` to speed up queries
6. **Analytics** – run Spark and MongoDB queries covering monthly revenue trends, top customers, top products, country sales, and return patterns
7. **Performance Optimization** – partitioning, caching, and broadcast joins to improve pipeline speed

## Key Insights

- Revenue peaks sharply in November (holiday seasonality)
- A small group of high-value customers drives most revenue
- The Netherlands has an unusually high revenue-per-invoice ratio, suggesting wholesale buyers
- A handful of products account for a large share of returns

## Getting Started

1. Open the notebook in Google Colab
2. Add `MONGO_URI` and `MONGO_DATABASE` as Colab Secrets (enable notebook access)
3. Run the notebook cells in order

## Security

MongoDB credentials are never hardcoded — they're pulled from Colab Secrets at runtime.

## Files

```
├── BigData_Assignment2.ipynb     # Main pipeline notebook
├── data_quality_report.csv       # Data cleaning summary
├── Technical-Report.pdf          # Full report with appendices
├── Online_retail.csv             # Raw dataset
└── README.md
```

## References

1. Google, "Secrets in Google Colab," Google Colaboratory Documentation, 2023.
2. Apache Software Foundation, "Data Types – Spark SQL and DataFrames," 2023.
3. MongoDB Inc., "Analyze Query Performance," MongoDB Manual, 2024.
4. MongoDB Inc., "Explain Results," MongoDB Manual, 2024.
