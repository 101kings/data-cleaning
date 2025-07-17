# 🧹 Nashville Housing Data Cleaning in SQL

This project focuses on cleaning and preparing the **Nashville Housing** dataset using SQL Server. The goal is to transform raw real estate data into a clean, analysis-ready format.

---

## 📁 Dataset
- **Table:** `PortfolioProject.dbo.NashvilleHousing`
- **Source:** CSV file containing housing records from Nashville, TN.

---

## 🧾 Data Cleaning Steps

### 1. 🗓 Standardize Sale Date Format
Converted `SaleDate` column from text/datetime format to a standardized `DATE` format using:
- `CONVERT(DATE, SaleDate)`
- Added a new column `SaleDateConverted` if direct update failed.

---

### 2. 🏠 Populate Missing Property Addresses
Used a self-join on `ParcelID` to fill in missing values in `PropertyAddress` by matching with rows having the same ID but a non-null address.

---

### 3. 🔍 Split Address Fields into Components

**PropertyAddress** was split into:
- `PropertySplitAddress` (street address)
- `PropertySplitCity` (city)

**OwnerAddress** was split into:
- `OwnerSplitAddress`
- `OwnerSplitCity`
- `OwnerSplitState`

Used `SUBSTRING`, `CHARINDEX`, and `PARSENAME` for parsing.

---

### 4. ✅ Standardize "SoldAsVacant" Values
Replaced inconsistent values in the `SoldAsVacant` column:
- `'Y'` → `'Yes'`
- `'N'` → `'No'`

Applied using a `CASE` statement and an `UPDATE`.

---

### 5. 🧹 Remove Duplicate Records
Implemented a `ROW_NUMBER()` window function to identify duplicate rows based on:
- `ParcelID`, `PropertyAddress`, `SalePrice`, `SaleDate`, `LegalReference`

Filtered rows with `row_num > 1` for review and deletion.

---

### 6. 🗑 Drop Unused Columns
Removed the following columns to reduce noise:
- `OwnerAddress`
- `TaxDistrict`
- `PropertyAddress`
- `SaleDate`

Used `ALTER TABLE ... DROP COLUMN`.

---

## 📦 Optional: Data Import Techniques

**BULK INSERT** and **OPENROWSET** methods were outlined for importing data from a `.csv` file. These require server configuration for:
- `Ad Hoc Distributed Queries`
- `Microsoft.ACE.OLEDB.12.0` provider

---

## 🧠 Skills Demonstrated
- SQL data transformation
- String parsing and cleaning
- Handling NULLs and duplicates
- Schema changes
- Use of common T-SQL functions

---

## 👨‍💻 Author

**Kingsley Momanyi**  
*Data Analyst & SQL Enthusiast*

---

