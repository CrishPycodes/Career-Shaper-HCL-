# Project 10: Banking Transaction Pattern Analysis

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-Preinstalled-013243?logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Preinstalled-150458?logo=pandas&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Google%20Colab-F9AB00?logo=googlecolab&logoColor=white)
![Domain](https://img.shields.io/badge/Domain-Banking%20%2F%20FinTech-success)

An entry-level exploratory data analytics project built in **Google Colab** using **only core Python, NumPy, and Pandas**. This project inspects, cleans, transforms, and analyzes a 1,200-entry synthetic retail banking transaction dataset covering January to December 2025, concluding with cautious, evidence-based operational recommendations.

---

## Project Metadata

| Attribute | Details |
| :--- | :--- |
| **Project Title** | Project 10: Banking Transaction Pattern Analysis |
| **Student Name** | Krishan Pratap |
| **Admission No.** | `2026B01010801` |
| **LMS Naming Format** | `2026B01010801_KrishanPratap_Project10` |
| **Training Program** | Five-Day Engineering Student Training (Year 1, Sem 1) |
| **Industry Domain** | Banking / FinTech |
| **Execution Platform** | Google Colab (Default Python 3 Runtime) |
| **Allowed Libraries** | `numpy` and `pandas` only (no external visualization or ML libraries) |
| **Repository** | [Career-Shaper-HCL-](https://github.com/CrishPycodes/Career-Shaper-HCL-.git) |

---

## Problem Statement & Objectives

Retail banks process continuous credit and debit flows across multiple account types, channels, and cities. Without structured exploratory analysis across a full calendar year, operations teams lack visibility into transaction distribution, missing monetary values, high-value concentration, and alert-flag patterns.

This project achieves five core objectives:
1. **Data Inspection & Cleaning:** Load all 1,200 records, verify date coverage (`2025-01-01` to `2025-12-31`) and `Transaction_ID` uniqueness, impute 20 missing `Amount_INR` values using the median, and export the cleaned dataset.
2. **Monetary Flow & Statistical Summary:** Compute Credit/Debit totals with Pandas and descriptive amount statistics (mean, median, sample standard deviation) with NumPy.
3. **Channel, City & Account Segmentation:** Compare transaction volume across 5 channels, total value across 5 cities, and Credit/Debit totals by `Account_Type`.
4. **Flagged-Record & High-Value Analysis:** Calculate overall and channel-level flagged rates, identify the top 10 largest transactions, categorize amounts into 5 ordered bands, and filter transactions above ₹1,000 using NumPy Boolean indexing.
5. **Cautious Operational Reporting:** Produce five conservative, non-causal operational recommendations dynamically derived from the computed metrics.

---

## Repository Structure

```text
Career-Shaper-HCL-/
├── 10_bank_transactions_1200.csv                          # Raw 1,200-entry synthetic dataset
├── 10_bank_transactions_1200_cleaned.csv                  # Cleaned dataset after median imputation
├── analysis.ipynb                                         # Executed Google Colab notebook (7 steps)
├── analysis.py                                            # Plain Python script version of the notebook
├── 2026B01010801_KrishanPratap_Project10_SRS.docx         # Software Requirements Specification (SRS)
└── README.md                                              # Project documentation
```

---

## Dataset Overview

The raw dataset (`10_bank_transactions_1200.csv`) contains **1,200 rows and 8 columns** spanning 354 unique dates in 2025 (`TX000000` to `TX001199`), with **0 duplicate `Transaction_ID`s** and **20 missing entries (1.67%)**, all in `Amount_INR`.

| Column Name | Data Type | Missing | Unique | Description & Observed Values |
| :--- | :--- | :---: | :---: | :--- |
| `Transaction_ID` | String (`object`) | 0 | 1,200 | Unique identifier (`TX000000` to `TX001199`) |
| `Account_Type` | Categorical (`object`) | 0 | 3 | `Current`, `Savings`, `Student` |
| `Transaction_Date` | Date (`datetime64`) | 0 | 354 | Calendar date (`2025-01-01` to `2025-12-31`) |
| `Transaction_Type` | Categorical (`object`) | 0 | 2 | `Credit` (621), `Debit` (579) |
| `Amount_INR` | Float (`float64`) | 20 | 1,172 | Amount in INR (range ₹25.28–₹6,978.50; median ₹379.88) |
| `Channel` | Categorical (`object`) | 0 | 5 | `NetBanking`, `Branch`, `UPI`, `ATM`, `Card` |
| `City` | Categorical (`object`) | 0 | 5 | `Kolkata`, `Mumbai`, `Delhi`, `Pune`, `Chennai` |
| `Flagged` | Categorical (`object`) | 0 | 2 | Pre-supplied review label: `No` (1,147; 95.58%), `Yes` (53; 4.42%) |

---

## Methodology (7-Step Workflow)

The analysis is organized into seven sequential cells in `analysis.ipynb` (and corresponding blocks in `analysis.py`):

1. **Step 1 — Data Loading & Inspection:** Load `10_bank_transactions_1200.csv`, parse `Transaction_Date` via `pd.to_datetime()`, and inspect shape, data types, date range, and sample rows.
2. **Step 2 — Cleaning, Duplicate Check & Export:** Verify primary-key uniqueness (`duplicated().sum()`), fill the 20 missing `Amount_INR` values with the non-missing median (`₹379.88`), and save `10_bank_transactions_1200_cleaned.csv`.
3. **Step 3 — Monetary & NumPy Statistics:** Compute Credit/Debit counts and totals via `groupby()`, and calculate mean, median, and sample standard deviation (`ddof=1`) using NumPy.
4. **Step 4 — Channel & City Segmentation:** Rank banking channels by transaction volume/share and cities by total transaction value/share.
5. **Step 5 — Flagged-Record Analysis:** Compute overall flagged percentage and channel-level flagged rates using `pd.crosstab()`.
6. **Step 6 — Top 10, Account Totals, Amount Bands & Boolean Indexing:**
   - Extract the 10 largest transactions (`nlargest(10, 'Amount_INR')`).
   - Pivot Credit and Debit totals by `Account_Type`.
   - Segment transactions into 5 ordered bands via `pd.cut()`:
     - **Very Low:** Up to ₹250
     - **Low:** ₹251 to ₹500
     - **Medium:** ₹501 to ₹1,000
     - **High:** ₹1,001 to ₹2,500
     - **Very High:** Above ₹2,500
   - Isolate transactions strictly above ₹1,000 using NumPy Boolean indexing (`amounts[amounts > 1000]`).
7. **Step 7 — Cautious Operational Recommendations:** Print five evidence-based, non-causal recommendations dynamically populated from computed metrics.

---

## How to Run

### Option 1: Google Colab (Recommended)
No `pip install` commands are required—`numpy` and `pandas` come preinstalled in Google Colab.

1. Open [Google Colab](https://colab.research.google.com/) and upload `analysis.ipynb` (or open it directly from this GitHub repository).
2. In the left **Files** sidebar, upload `10_bank_transactions_1200.csv`.
3. Click **Runtime → Run all** to execute all 7 steps from top to bottom.
4. Download the generated `10_bank_transactions_1200_cleaned.csv` from the **Files** sidebar if needed.

> **Note:** Files uploaded to Google Colab are temporary and cleared when the session disconnects. Re-upload `10_bank_transactions_1200.csv` when starting a new session.

### Option 2: Local Python Script
Ensure Python 3.10+, `numpy`, and `pandas` are installed, place `10_bank_transactions_1200.csv` in the same directory as `analysis.py`, and run:

```bash
git clone https://github.com/CrishPycodes/Career-Shaper-HCL-.git
cd Career-Shaper-HCL-
python analysis.py
```

---

## Key Verified Findings (`N = 1,200`)

All metrics below are computed dynamically on the cleaned dataset (**Total Value: ₹735,334.53**):

### 1. Data Cleaning & Monetary Summary
- **Duplicates:** `0` duplicate `Transaction_ID`s (1,200 unique records).
- **Imputation Impact:** Filling 20 missing `Amount_INR` values with the median (`₹379.88`) adjusted the total value from `₹727,736.83` to `₹735,334.53` (`+₹7,597.70`).
- **Credit vs. Debit:**
  - **Credits:** 621 transactions — **₹380,286.40** (51.72% of value)
  - **Debits:** 579 transactions — **₹355,048.13** (48.28% of value)
- **NumPy Distribution Metrics:** Mean **₹612.78** | Median **₹379.88** | Sample Std. Dev. **₹785.92** | Range **₹25.28 – ₹6,978.50**

### 2. Channel Volume, Value & Flagged Rates
| Channel | Transactions | Volume Share | Total Value (₹) | Flagged Count | Flagged Rate |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **NetBanking** | 260 | 21.67% | 171,715.56 | 10 | 3.85% |
| **Branch** | 253 | 21.08% | 150,479.87 | 14 | 5.53% |
| **UPI** | 238 | 19.83% | 146,427.13 | 12 | 5.04% |
| **ATM** | 237 | 19.75% | 152,409.89 | 10 | 4.22% |
| **Card** | 212 | 17.67% | 114,302.09 | 7 | 3.30% |
| **Overall** | **1,200** | **100.00%** | **735,334.53** | **53** | **4.42%** |

### 3. City Value Breakdown
| City | Transactions | Total Value (₹) | Value Share |
| :--- | :---: | :---: | :---: |
| **Kolkata** | 253 | 171,299.91 | 23.30% |
| **Mumbai** | 264 | 170,551.99 | 23.19% |
| **Delhi** | 254 | 146,182.63 | 19.88% |
| **Pune** | 220 | 130,003.56 | 17.68% |
| **Chennai** | 209 | 117,296.45 | 15.95% |

### 4. Account Types, Top 10 & High-Value Concentration
- **Account-Type Totals (Credit / Debit):**
  - **Current:** ₹123,985.45 / ₹121,057.77
  - **Savings:** ₹115,265.96 / ₹116,203.54
  - **Student:** ₹141,035.00 / ₹117,786.83
- **Largest Transaction:** `TX000200` (**₹6,978.50**, Student Debit, UPI, Pune). None of the top 10 transactions are flagged.
- **Amount Bands & High-Value Filter:**
  - **61.92%** of transactions are ₹500 or less (*Very Low*: 387; *Low*: 356).
  - **15.00%** of transactions (**180 records > ₹1,000**) account for **48.21%** of total monetary value (**₹354,540.67**).

---

## Five Cautious Operational Recommendations

1. **Tiered High-Value Review:** Since 15.00% of transactions (> ₹1,000) represent 48.21% of total value and none of the top 10 are flagged, consider stepped review thresholds for high-value transfers while keeping routine small payments (61.92% ≤ ₹500) low-friction.
2. **Digital Scaling & Branch Migration:** NetBanking leads in both volume (21.67%) and value (₹171,715.56), closely followed by Branch volume (21.08%). Prioritize NetBanking availability and encourage migrating routine small Branch transactions to NetBanking or UPI.
3. **Careful Validation of Channel Flag Rates:** Branch (5.53%) and UPI (5.04%) show higher flag rates than Card (3.30%), but channel counts are small (7–14 flagged records each). Validate on a larger production sample before adjusting channel-specific monitoring rules.
4. **Ingestion Schema Validation:** Enforce non-null validation on `Amount_INR` at the transaction-ingestion gateway so incomplete entries (20 in this dataset) do not enter downstream reporting pipelines.
5. **Longitudinal Regional & Account Monitoring:** Kolkata and Mumbai account for 46.49% of total value compared to 15.95% for Chennai, and Student accounts show higher Credit inflows than Debits. Confirm these trends on multi-year production data before adjusting regional liquidity or product strategy.

---

## Assumptions, Limitations & Disclaimer

> **Synthetic Data & Non-Fraud Disclaimer:** `10_bank_transactions_1200.csv` is a synthetic 1,200-entry teaching dataset. The `Flagged` column is a pre-supplied review indicator and **must not** be interpreted as confirmed fraud. All results are descriptive patterns within this sample; correlation does not imply causation.

- **Scope Boundaries:** Advanced visualization (`matplotlib`, `seaborn`, `plotly`), statistical (`scipy`, `statsmodels`), and ML (`scikit-learn`) libraries are intentionally excluded.
- **Modest Flagged Sample:** Only 53 records (4.42%) are flagged overall, making small channel-level differences sensitive to sampling variation.
- **No Customer-Level Context:** The dataset does not contain customer IDs, timestamps, merchant codes, or account balances.
- **Analyst-Defined Bands:** The five amount band cutoffs (₹250, ₹500, ₹1,000, ₹2,500) are chosen for this analysis and can be customized in the notebook.

---

## References

- [Google Colaboratory](https://colab.research.google.com/)
- [Python 3 Official Documentation](https://docs.python.org/3/)
- [NumPy Documentation](https://numpy.org/doc/stable/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)