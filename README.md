# ⚽ FIFA 21 Data Cleaning & Analysis Project

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Pandas](https://img.shields.io/badge/Library-Pandas-orange)
![Status](https://img.shields.io/badge/Status-Completed-green)

## 📖 Project Overview

In the world of data analytics, raw data is rarely ready for immediate analysis. It often contains inconsistencies, formatting errors, and mixed data types.

This project focuses on the **end-to-end data cleaning pipeline** of a raw dataset containing information on over 18,000 professional football players from the FIFA 21 video game. The goal was to transform a "messy" raw dataset into a pristine, structured format suitable for high-level analysis, visualization, or Machine Learning modeling.

By utilizing Python and the Pandas library, this project demonstrates how to handle complex string manipulation, unit conversion, and data type standardization.

---

## 📂 Data Scale and Scope

The dataset comprises detailed attributes for players across various leagues and nationalities.

*   **Volume:** Approximately **19,000 rows** (individual players) and **77 columns** (attributes).
*   **Source:** Scraped data from SoFifa (Kaggle).
*   **Key Attributes:**
    *   **Identity:** Name, Nationality, Club, ID.
    *   **Performance:** Overall Rating (OVA), Potential (POT), Best Position.
    *   **Physical:** Height, Weight, Foot Preference.
    *   **Financial:** Market Value, Weekly Wage, Release Clause.
    *   **Contractual:** Contract Start/End, Loan Status.

---

## 🎯 Research Questions & Objectives

The primary objective was to render the data computationally useful. Raw text cannot be aggregated or mathematically analyzed.

**Key Challenges Solved:**
1.  **Normalization:** How do we compare player salaries when some are in Millions ('M') and others in Thousands ('K')?
2.  **Unit Standardization:** How do we perform statistical analysis on physical attributes when Height is stored as `5'7"` (Imperial string) and Weight as `170lbs`?
3.  **Data Type Integrity:** How do we convert object-type columns (strings with special characters like `€` or `★`) into numerical floats and integers?
4.  **Temporal Analysis:** How do we extract the length of a player's tenure from a free-text "Joined" column?

---

## 🧹 Data Cleaning & Preprocessing Steps

The raw data contained significant inconsistencies. Below is a detailed breakdown of the cleaning logic applied:

### 1. Handling Height & Weight (Unit Conversion)
*   **Issue:** Heights were stored as strings (e.g., `5'9"`), and Weights included units (e.g., `172lbs`).
*   **Solution:**
    *   Parsed the feet and inches.
    *   Converted all Heights to **Centimeters (cm)**.
    *   Converted all Weights to **Kilograms (kg)**.
    *   *Result:* Columns are now clean integers ready for correlation analysis.

### 2. Financial Cleaning (Value, Wage, Release Clause)
*   **Issue:** Financial data was stored as strings with currency symbols and suffixes (e.g., `€100.5M`, `€50K`).
*   **Solution:**
    *   Stripped the Euro (`€`) symbol.
    *   Wrote a custom function to detect suffix types:
        *   Multiplied values with **'M'** by **1,000,000**.
        *   Multiplied values with **'K'** by **1,000**.
    *   Converted the final output to **Float**.

### 3. 'Hits' Column Transformation
*   **Issue:** This column represents player profile views. It contained mixed formats (e.g., `1.6K`) and hidden newline characters (`\n`).
*   **Solution:**
    *   Removed newline characters.
    *   Standardized 'K' notation into absolute numbers (e.g., `1.6K` $\rightarrow$ `1600`).

### 4. Date & Contract Management
*   **Issue:** The 'Joined' column was a standard date string, while 'Contract' contained ranges (e.g., `2019 ~ 2024`) or text (e.g., `Free`).
*   **Solution:**
    *   Converted 'Joined' to datetime objects.
    *   Extracted **Year**, **Month**, and **Day** into separate columns for temporal analysis.

---

## 📊 Before vs. After (Transformation)

| Attribute | Raw Data (Before) | Cleaned Data (After) | Data Type |
| :--- | :--- | :--- | :--- |
| **Height** | `5'7"` | `170` | `int` |
| **Weight** | `159lbs` | `72` | `int` |
| **Value** | `€103.5M` | `103500000.0` | `float` |
| **Wage** | `€560K` | `560000.0` | `float` |
| **Hits** | `1.6K` | `1600.0` | `float` |

---

## ⚙️ Methodology

1.  **Import & Inspection:** Loaded the raw CSV using Pandas and inspected the `head()`, `info()`, and `dtypes` to identify dirty data.
2.  **Iterative Cleaning:** Created specific Python functions for each cleaning task (e.g., `convert_height()`, `clean_money()`).
3.  **Application:** Applied these functions using the Pandas `.apply()` method for vectorization and efficiency.
4.  **Verification:** Checked unique values and data types after every step to ensure accuracy.
5.  **Export:** Saved the processed dataframe to `fifa21_cleaned_data.csv`.

---

## 🚀 Usage Instructions

To replicate this analysis on your local machine:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/YourUsername/YourRepoName.git
    ```
2.  **Install dependencies:**
    ```bash
    pip install pandas numpy
    ```
3.  **Run the Notebook:**
    Open `FIFA_Cleaning_Code.ipynb` in Jupyter Notebook or VS Code and run all cells.

---

## 🔮 Future Work & Contributions

This project sets the foundation for deeper analysis. Future expansions could include:

*   **Visualization Dashboard:** creating a PowerBI or Tableau dashboard to visualize the best value-for-money players.
*   **Machine Learning:** Using the now-clean numerical data to predict a player's Market Value based on their stats (Regression Model).
*   **Clustering:** Grouping players into "Play Styles" based on their physical and technical attributes.

Contributions are welcome! If you find a more efficient way to clean the 'Contract' column, please submit a Pull Request.

---

**Author:** Neelam
**Tools:** Python, Pandas, Jupyter
