# Retail Sales Data Cleaning

This project cleans a deliberately messy retail sales dataset and produces a validated, analysis-ready CSV. The work is documented in a Jupyter notebook, including the reasoning and affected-row count for each cleaning decision.

## Project files

| File | Description |
|---|---|
| [`Task3_Data_Cleaning.ipynb`](./Task3_Data_Cleaning.ipynb) | Data quality assessment, cleaning workflow, validation, and cleaning log |
| [`retail_sales_dataset.csv`](./retail_sales_dataset.csv) | Original dataset (4,310 rows, 21 columns) |
| [`retail_sales_cleaned.csv`](./retail_sales_cleaned.csv) | Cleaned dataset (4,192 rows, 22 columns) |

## Dataset

The source data contains retail order, customer, product, payment, sales, shipping, and satisfaction fields. The cleaned file adds `satisfaction_missing` to preserve which satisfaction ratings were absent in the source.

## Cleaning workflow

The notebook preserves the raw data and performs all work on a copy. Its main steps are:

1. Profile missing values, duplicates, data types, value ranges, and inconsistent formatting.
2. Remove 30 fully empty rows and 80 exact duplicate rows, keeping the first copy.
3. Standardize gender values and order-status capitalization. Parse the three date formats into one date column; slash-separated dates are interpreted as day/month/year based on the data.
4. Remove 8 rows containing the `999` quantity placeholder, whose sales and profit values were consequently unreliable. Convert other impossible values to missing.
5. Review outliers using the IQR method. Cap shipping costs, treat implausibly long shipping times as missing, and retain other flagged values where they are plausible for the product or business context.
6. Fill missing age, quantity, shipping time, discount, and shipping cost values with their medians. Leave missing customer satisfaction ratings untouched and add `satisfaction_missing` rather than guessing customer opinions.
7. Convert identifiers, categories, numeric fields, dates, and flags to appropriate data types; run assertions to validate the cleaned data.
8. Save and reload the cleaned CSV to verify the output.

## Results

- The dataset has **4,192 rows and 22 columns** after cleaning.
- `order_id` values are unique, there are no exact duplicate records, and the standardized gender and order-status values pass validation.
- The cleaned `order_date` values span **2020-01-01 to 2024-12-30**.
- Missing satisfaction ratings are intentionally retained and identified by the added flag column.

These results describe the supplied dataset and cleaning rules; they are not claims about all retail data.

## Requirements

- Python 3
- pandas
- NumPy
- Jupyter Notebook or JupyterLab

Install the dependencies:

```bash
python -m pip install pandas numpy jupyter
```

## Run the notebook

Run these commands from this project directory so the notebook can find the CSV files using their relative paths:

```bash
jupyter notebook
```

Open `Task3_Data_Cleaning.ipynb` and run the cells in order. The final save step writes `retail_sales_cleaned.csv` to this directory.
