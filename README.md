# Customer Sales Data: Cleaning and EDA

A data cleaning and exploratory data analysis project on a raw customer sales file with many data quality problems. The raw data is cleaned step by step, then explored to answer basic business questions about sales by city, age group, gender and time.

**Tools:** Python (Pandas, NumPy, Matplotlib, Seaborn), Jupyter Notebook

---

## Project Files

| File | Description |
|------|-------------|
| `DataCleaning.ipynb` | Jupyter notebook with the full cleaning and analysis |
| `messy_customer_sales_data.csv` | Raw input data |
| `Report_EDA.pdf` | Final written report with charts and findings |

---

## Dataset

- **Size:** 10,400 rows and 10 columns in the raw file. 10,197 rows after cleaning
- **Columns:** Customer_ID, Name, Gender, Age, City, Signup_Date, Last_Purchase_Date, Purchase_Amount, Feedback_Score, Email
- **Signup dates:** 1 Jan 2018 to 31 Dec 2023
- **Last purchase dates:** 1 Jan 2023 to 31 Dec 2025
- **Cities:** 12 Indian cities (Chennai, Mumbai, Pune, Hyderabad, Bangalore, Jaipur, Delhi, Kolkata, Surat, Nagpur, Ahmedabad, Lucknow)

---

## Goals

- Find and fix the quality problems in the raw data
- Build a clean dataset that can be used for analysis
- Look at purchase amount by city, age group, gender and month
- Calculate basic KPIs and a feedback split

---

## Data Problems Found

- **Duplicate rows:** 203 exact duplicates
- **Missing values:** Name (504), Gender (495), Age (756), City (742), Last_Purchase_Date (591), Purchase_Amount (652), Feedback_Score (509), Email (655)
- **Age stored as text:** values like "46 years" (1,453 values)
- **Gender written many ways:** male, female, m, f, MALE, FEM, with mixed case and extra spaces
- **City spelling and case:** values like "ahmedabad" and "JAIPUR"
- **Dates stored as text:** Signup_Date and Last_Purchase_Date
- **Impossible dates:** 276 rows with last purchase date earlier than signup date
- **Customer_ID problem:** 2,542 of 6,204 IDs (about 41%) are linked to more than one name

---

## Cleaning Steps

1. Extracted the number from Age text using a regular expression and removed ages outside 0 to 100
2. Converted both date columns to proper dates
3. Trimmed spaces, lowercased Gender and mapped everything to Male or Female
4. Trimmed spaces and applied title case to City
5. Removed 203 duplicate rows (10,400 down to 10,197)
6. Filled missing Name, City, Gender and Email with "Unknown"
7. Checked emails, negative purchase amounts and the feedback range
8. Set the 276 impossible last purchase dates to blank and flagged them in a `Date_Issue` column
9. Created `Age_Group` with three equal-sized bands: Young (18 to 35), Adult (35 to 53), Senior (53 to 70)
10. Left missing Age, Purchase_Amount, Feedback_Score and Last_Purchase_Date blank on purpose, so no made-up values enter the analysis
11. Checked outliers using box plots and the IQR rule

---

## Key Findings

- **Total purchase amount:** 408.6 million, with an average of about 42,750 per record
- **Purchase range:** 5,009 to 79,998
- **Top cities:** Chennai, Mumbai and Pune lead with about 37 million each
- **Lower cities:** Surat, Nagpur, Ahmedabad and Lucknow sit at 22.6 to 24.5 million each
- **Why those four are lower:** they have fewer records (574 to 612 against 818 to 941 elsewhere), while the average amount per record is almost the same in every city (about 41,600 to 43,900). The gap comes from volume, not from lower spending
- **Age and gender:** female and male records are almost equal (4,856 vs 4,855). Median purchase is about 42,800 to 43,600 across age groups, and the correlation between age and amount is about -0.01
- **Yearly amount (by last purchase date):** 2023: 121.1M, 2024: 125.8M, 2025: 126.4M
- **Year on year growth:** +3.86% in 2024 and +0.49% in 2025
- **Feedback split:** Detractors 40.2%, Passives 30.3%, Promoters 29.5%
- **Feedback vs spending:** correlation between feedback score and purchase amount is about -0.01
- **Customer_ID:** found to be linked to multiple names, which is why the analysis is done at record level

---

## Business KPIs

| KPI | Value |
|-----|-------|
| Total purchase amount | 408,560,586.60 |
| Average purchase amount | 42,749.88 |
| Highest purchase | 79,997.70 |
| Lowest purchase | 5,009.30 |
| Year on year growth | 2024: +3.86%, 2025: +0.49% |
| Average days from signup to last purchase | About 1,318 (median 1,309) |

---

## How to Run

1. Clone this repository
2. Install the libraries:
   ```
   pip install pandas numpy matplotlib seaborn jupyter
   ```
3. Open `DataCleaning.ipynb` in Jupyter Notebook
4. Make sure `messy_customer_sales_data.csv` is in the same folder
5. Run all cells from top to bottom

---

## Author

**Mohammed Naveed**

- Email: mohammednaveed1222@gmail.com
- GitHub: [github.com/NaveedSultan](https://github.com/NaveedSultan)
