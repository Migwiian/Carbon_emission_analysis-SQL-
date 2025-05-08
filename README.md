# Analyzing Industry Carbon Emissions with SQL

## Overview

This project analyzes a dataset of product carbon footprints (PCFs) to identify the industries with the highest carbon emissions. The analysis utilizes SQL queries within a Jupyter Notebook environment to explore the `product_emissions` table and determine which industry groups have the largest carbon footprint.

## Motivation

Understanding the distribution of carbon emissions across different industry groups is a critical step in addressing climate change. By identifying the highest emitting industries, we can focus efforts on developing more sustainable practices and policies within those sectors. This project serves as a practical application of SQL for environmental data analysis.

## Skills Demonstrated

* Querying data using `SELECT` and `FROM` statements.
* Filtering data with the `WHERE` clause.
* Aggregating data using `COUNT()` and `SUM()`.
* Grouping data with `GROUP BY`.
* Ordering results with `ORDER BY`.
* Using aggregate functions with aliases (`AS`).
* Examining distinct values.
* Finding minimum and maximum values.
* Using `LOWER()` for case-insensitive grouping.

## Dataset

The analysis is based on the `product_emissions` table, which contains product carbon footprints (PCFs) for various companies. The table includes information such as product ID, year, product name, company, country, industry group, weight, and the carbon footprint (in CO2 equivalent).

## Methodology

1.  **Familiarization with the Data:** The project began by inspecting the first few rows of the `product_emissions` table to understand its structure and sample values.
2.  **Understanding Data Scale and Scope:** Queries were used to determine the total number of records, the distinct industry groups present, and the range of years covered in the dataset (2013 to 2017).
3.  **Data Cleaning Checks:** The analysis included checks for missing `carbon_footprint_pcf` values (none were found) and potential inconsistencies in industry names due to case variations.
4.  **Identifying the Most Recent Year:** The most recent year in the dataset was determined to be 2017.
5.  **Calculating Total Carbon Footprint per Industry in the Most Recent Year:** SQL queries were used to filter the data for the year 2017 and then calculate the sum of `carbon_footprint_pcf` for each `industry_group`.
6.  **Determining the Highest Emitting Industries:** The results were ordered in descending order of the total carbon footprint to identify the industries with the highest emissions in 2017.

## Key SQL Queries
```
Inspect the first 10 rows of the data
SELECT *
FROM public.product_emissions
LIMIT 10;
```
```Calculate the total number of
SELECT COUNT(*) AS total_records
FROM product_emissions;
```
```Identify distinct values in the industry_group column
SELECT DISTINCT industry_group
FROM public.product_emissions
ORDER BY industry_group;
```
```Find the earliest and latest years 
SELECT MIN(year) as earliest_year, MAX(year) as latest_year
FROM product_emissions;
```
```Checking null records
SELECT COUNT(*) AS records_with_missing_emissions
FROM product_emissions
WHERE carbon_footprint_pcf IS NULL;
```
```Checking redundant records
SELECT LOWER(industry_group) AS industry_lowercase, COUNT(*) AS count
FROM product_emissions
GROUP BY LOWER(industry_group)
ORDER BY count DESC;
```
```Most recent years and highest emitting group 
SELECT industry_group, SUM(carbon_footprint_pcf) as pcf_sum
FROM product_emissions
WHERE year=2017
GROUP BY industry_group
ORDER BY pcf_sum DESC;
```
