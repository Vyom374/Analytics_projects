# **Stock Data Pipeline: Web Scraping, Cleaning, and MySQL Ingestion**

## **Project Overview**

This project demonstrates an end-to-end data pipeline where live stock market data is:

- Web scraped from Yahoo Finance using **Selenium**  
- Cleaned and transformed using **Pandas**  
- Ingested into **MySQL** using **SQLAlchemy**  

The goal of this project is to simulate a real-world **data engineering and data analyst workflow**.

---

## **Tech Stack**

- **Python**  
- **Selenium** (Web Scraping)  
- **Pandas** (Data Cleaning and Transformation)  
- **SQLAlchemy** (Database Connection)  
- **MySQL Workbench** (Data Storage)  

---

## **Features**

- Automated scraping of live stock data from Yahoo Finance  

- Data cleaning, including:
  - Conversion of string columns to numeric where applicable  
  - Handling of values with units such as **M (Million), B (Billion), and T (Trillion)**  
  - Removal of commas and formatting issues  

- Data ingestion into a MySQL database  

- Automatic table replacement if it already exists  
