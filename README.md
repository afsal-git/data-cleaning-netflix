# Netflix Titles Data Cleansing Pipeline

## Project Objective
The objective of this project is to build a robust data-cleansing workflow designed to prepare a raw, highly corrupted dataset of Netflix titles for production-ready analysis. This pipeline systematically tracks and resolves typical real-world data anomalies—such as extensive missing values, duplicate entries, structural format inconsistencies, and corrupted data types—ensuring absolute data integrity and structure.

---

## Technical Toolset Used
* **Environment:** Visual Studio Code (VS Code)
* **Language:** Python
* **Libraries:** Pandas, NumPy

---

## Comprehensive Summary of Preprocessing Operations

The raw dataset (`messy_netflix_titles.csv`) was programmatically cleaned using Python Pandas through the following pipeline stages:

### 1. Column Header Standardization
* Removed all leading and trailing whitespaces from raw headers.
* Standardized all column labels to uniform lowercase syntax.
* Replaced internal whitespace blocks with clean underscores (e.g., converted `SHOW ID` and `DATE_ADDED ` to `show_id` and `date_added`).

### 2. Record Deduplication
* Handled structural data mutations where duplicated rows had minor text variances.
* Utilized subset structural filtering (`subset=['show_id']`) to evaluate unique identifiers.
* Eliminated all duplicate rows, maintaining only the first valid iteration.

### 3. Text and Categorical Normalization
* **Type Column:** Applied `.str.strip().str.title()` to eliminate conflicting classifications like `movie`, `MOVIE`, and ` Movie `, grouping them seamlessly into `Movie` or `TV Show`.
* **Country Column:** Built an architectural standardization mapping structure to normalize regional input variations (e.g., converting variations like `US`, `USA`, `united states`, and trailing whitespaces back to a unified `United States`).

### 4. Mixed-Format Parsing (Date Fields)
* Resolved chaotic structural date formats (e.g., mixing `dd-mm-yyyy`, `yyyy/mm/dd`, `mm/dd/yyyy`, and long-form text strings).
* Leveraged `pd.to_datetime()` with `errors='coerce'` and `format='mixed'` flags to parse variations safely into standard datetime objects.

### 5. Type Casting and Numerical Extraction
* Cleared the `release_year` string variables of literal text noise (e.g., removing `Year:` prefixes).
* Extracted and cast numeric elements from corrupted strings directly into explicit integer types (`.astype(int)`).

### 6. Missing Value (Null) Imputation Strategy
* Imputed structural placeholder labels (`'Unknown Director'`, `'Unknown Cast'`, `'Unknown Country'`) into sparse categorical blocks to maintain dataset layout integrity without dropping rows.
* Imputed numerical entries in the release year field using the calculated data **Median Year (2017)**.
* Standardized unparseable or empty date records cleanly as `'Not Available'`.
* **Result:** Achieved a perfect **0% Missing Values** metric across all 12 columns.

---

## Project Repository Files
* **`messy_netflix_titles.csv`**: The initial, corrupted raw source data containing formatting issues, duplicates, and missing indices.
* **`cleaned_netflix_titles.csv`**: The final, processed structural dataset with pristine layout schemas and zero validation errors.
* **`data_cleaning.ipynb`**: Interactive Jupyter Notebook outlining the precise line-by-line programmatic execution steps.

---

### Verification and Quality Metrics
* **Initial Dataset Size:** 8957 Rows, 12 Columns
* **Final Verified Clean Dataset Size:** 8807 Rows, 12 Columns
* **Final Missing Value Count:** 0
