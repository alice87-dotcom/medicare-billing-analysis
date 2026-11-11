# Spotting Unusual Billing in Medicare

**BA780 – Introduction to Data Analytics | Boston University Questrom School of Business | Fall 2026**
Team B01: Ahan Nair, Sree Dandu, Alice Yen, Yuxin Li, Ujjwala Kapoor

---

## Overview

Medicare Part B pays about **1.3 million providers** every year, so auditors can't review everyone. This project asks a simple question:

> **What's the best way to decide whose billing deserves a closer look?**

We combined 2024 Medicare billing data with the government's list of providers excluded from federal health care programs, then compared different ways to spot unusual billing: total payments, services per patient, variety of billing codes, and comparisons with peers in the same specialty.

## Key Findings

- **Spending is highly concentrated:** the top 10% of providers receive about two-thirds (66.5%) of all Part B payments, mostly because of practice size and specialty.
- **Dollar amounts alone aren't enough:** a screen that flags only the highest-paid providers missed **82 of the 83** excluded providers we matched.
- **Services per patient adds signal:** matched providers tended to bill more services per patient, especially among providers with higher-risk patients.
- **Billing-code variety showed no consistent difference** between matched and other providers.
- **Peer comparison matters:** comparing providers with others in the same specialty is fairer and more useful than looking at raw totals.
- **Location affects workload:** providers outside metro areas were flagged more often per 1,000 providers, which helps with planning review work, but location alone is not a risk signal.

## Data

| Dataset | Source | Size |
|---|---|---|
| Medicare Physician & Other Practitioners – by Provider (2024) | [CMS](https://data.cms.gov/provider-summary-by-type-of-service/medicare-physician-other-practitioners/medicare-physician-other-practitioners-by-provider) | 1,296,739 rows × 81 columns |
| List of Excluded Individuals/Entities (LEIE) | [HHS OIG](https://oig.hhs.gov/exclusions/exclusions_list.asp) | 84,001 rows × 18 columns |

The two datasets were joined on each provider's **NPI** (National Provider Identifier).

## Approach

1. **Data cleaning:** standardized NPIs, removed invalid IDs, combined repeated exclusion records into one row per provider, and checked billing values for impossible or zero values
2. **Merging:** one-to-one left join of the Medicare data with the exclusion list
3. **Feature engineering:** payment per patient, services per patient, and payment per service
4. **Analysis:** 15 visualizations comparing billing patterns by specialty, patient risk, practice size, and location

## Tools

Python · pandas · NumPy · Matplotlib · Seaborn · Google Colab

## How to Run

1. Download the two datasets from the links above and save them as:
   - `Medicare_Physician_Other_Practitioners_by_Provider_2024.csv`
   - `LEIE.csv`
2. Open `B01-Medicare-Fraud-Detection.ipynb` in Google Colab or Jupyter.
3. Upload or place both CSV files in the same folder as the notebook.
4. Run all cells from top to bottom.

## Limitations

- The CMS data shows **yearly totals per provider**, not individual claims.
- **Being on the exclusion list does not prove billing fraud.** This project is a screening analysis, not a fraud-prediction model.
- Some groups of matched providers are small, so results should be read with caution.

## Repository Structure

```
├── B01-Medicare-Fraud-Detection.ipynb   # Full analysis notebook
└── README.md
```
