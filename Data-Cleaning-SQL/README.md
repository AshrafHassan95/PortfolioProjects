# Nashville Housing Data Cleanup README

This repository contains SQL queries for cleaning data from the Nashville Housing dataset within the PortfolioProject database. The SQL queries perform various data transformations to improve data quality and consistency.

## Excel Data Files

This repository includes the following Excel data files :

- [NashvilleHousingData](https://github.com/AshrafHassan95/PortfolioProjects/blob/main/Data-Cleaning-SQL/Nashville%20Housing%20Data%20for%20Data%20Cleaning%20(reuploaded).xlsx): This file contains the original Nashville Housing dataset before any data cleaning or standardization.

Users can use and download these data files in conjunction with the provided SQL queries to analyze the Nashville Housing data efficiently.

## Queries

### Query 1: Select Data

This query retrieves all records from the `NashvilleHousing` table to provide an overview of the dataset.

### Query 2: Standardize Date Format

This query converts the `SaleDate` column into a standardized date format for consistency.

### Query 3: Populate Property Address Data

This set of queries identifies and populates missing `PropertyAddress` values by matching records with the same `ParcelID`.

### Query 4: Break Out Address into Individual Columns

These queries split the `PropertyAddress` column into separate columns for `Address` and `City`, improving data organization.

### Query 5: Parse Owner Address

This set of queries parses the `OwnerAddress` column into separate columns for `Address`, `City`, and `State`, facilitating analysis.

### Query 6: Change 'Y' and 'N' to 'Yes' and 'No'

This query updates the `SoldAsVacant` column to replace 'Y' and 'N' with 'Yes' and 'No' for readability.

### Query 7: Remove Duplicates

This query removes duplicate records from the dataset based on specific columns, keeping only one instance of each unique record.

### Query 8: Delete Unused Columns

This query deletes columns that are no longer needed in the dataset, improving data simplicity and reducing redundancy.

## Usage

Users can run these SQL queries on the `NashvilleHousing` table within the PortfolioProject database to clean and standardize the data. These transformations enhance data quality, making it more suitable for analysis and reporting.

## Conclusion

The Nashville Housing Data Cleanup project focuses on preparing the dataset for analysis by addressing issues such as missing data, date standardization, and column parsing. By using these SQL queries, users can efficiently preprocess and clean the data for further analysis or visualization.

