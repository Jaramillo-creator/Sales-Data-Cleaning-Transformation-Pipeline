## Sales Data Cleaning & Standardization Project

## 📌 Project Overview
This project focuses on performing data cleaning, text standardization, outlier treatment, and data type conversion on a messy sales dataset (`Messy_data (1).csv`). Using **Python** and **Pandas** in Google Colab, the raw dataset was audited, cleaned of quality defects, and transformed into a standardized, analysis-ready dataset saved as `cleaned_sales_dataset.csv`.

---

## 🛠️ Data Quality Issues Identified & Resolved

| Data Quality Issue | Examples Found in Raw Data | Action Taken / Resolution Strategy |
| :--- | :--- | :--- |
| **Duplicate Records** | 5 duplicate rows | Removed using `drop_duplicates()`. |
| **Extra Spaces** | Leading/trailing spaces in names, cities, products | Trimmed whitespace across string columns using `.str.strip()`. |
| **Text Standardization** | Mixed casing (e.g., `delhi`, `DELHI`, `Delhi`) | Standardized using `.str.title()` and `.str.capitalize()`. |
| **Data Type Errors** | Text numbers (`"three"`, `"forty"`), units (`"2 pcs"`), commas (`"18,500"`), and invalid values (`"unknown"`) | Custom parsing logic applied to extract numbers, remove punctuation/text, and re-cast columns to numeric types (`int`/`float`). |
| **Outliers** | Negative quantities, prices like `999,999`, and ages like `185` | Flagged as invalid data (`NaN`) based on domain thresholds and imputed using column medians. |
| **Date Inconsistencies** | Mixed formats (`YYYY-MM-DD`, `DD/MM/YYYY`) and string errors (`"not a date"`) | Converted to datetime objects using `pd.to_datetime(errors='coerce')` and missing timestamps filled via forward fill (`ffill`). |
| **Missing Values** | Missing entries in names, cities, dates, prices, and quantities | Imputed text columns with `"Unknown"` or `"Pending"`; imputed numeric columns with median values. |

---

## 📊 Summary of Cleaning & Transformation Steps

1. **Inspection:** Assessed dataset shape, column datatypes, and missing value counts using `df.info()`, `df.shape`, and `df.isnull().sum()`.
2. **Deduplication & Whitespace Removal:** Dropped exact row duplicates and stripped extraneous spacing from all text columns.
3. **Parsing Numeric Fields:**
   - **`Quantity`:** Mapped text numbers (e.g., `"three"`) and extracted numeric digits from strings like `"2 pcs"`.
   - **`UnitPrice`:** Removed commas (e.g., `"18,500"` $\rightarrow$ `18500`) and coerced invalid string tokens (`"unknown"`) to null values.
   - **`CustomerAge`:** Converted word numbers (`"forty"`) to integers and filtered out unrealistic ages outside the 18–100 range.
4. **Missing Value Imputation:**
   - Numerical missing values and cleared outliers (`Quantity`, `UnitPrice`, `CustomerAge`) were imputed with their respective **median values** to avoid skewing distributions.
   - Categorical missing values (`CustomerName`, `City`, `OrderStatus`) were imputed with clear placeholder tags (`"Unknown"` or `"Pending"`).
5. **Feature Engineering:** Created the calculated field:
   $$\text{TotalAmount} = \text{Quantity} \times \text{UnitPrice}$$
6. **Export:** Exported the final cleaned dataset as `cleaned_sales_dataset.csv`.

---

## 📁 Repository Contents

* `Messy_data (1).csv`: Original raw dataset containing deliberate quality issues.
* `cleaned_sales_dataset.csv`: Processed dataset ready for analysis.
* `sales_data_cleaning.ipynb`: Google Colab Jupyter Notebook with step-by-step Python execution.
* `README.md`: Overview documentation and data cleaning summary report.

---

## 🚀 How to Run

1. Open **Google Colab** or any Jupyter Notebook environment.
2. Clone this repository or upload `sales_data_cleaning.ipynb` and `Messy_data (1).csv`.
3. Execute all cells in the notebook to reproduce the cleaned dataset output.
