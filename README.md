# SuperFoodsMax Revenue Growth Analysis

## Project Overview

This project analyzes transactional data from SuperFoodsMax spanning 2019-2022 to identify strategic opportunities for increasing sales revenue by 5% over a two-year period. The analysis focuses on understanding customer loyalty patterns and identifying key drivers of revenue growth, specifically targeting loyal customer retention and first-time customer conversion.

## Business Question

**How can SuperFoodsMax increase revenue by 5% over the next two years by focusing on loyal customer retention and new customer conversion?**

### Key Business Insights from Stakeholders
- Failure to lift average spend of loyal customers is stagnating revenue growth
- First-time customers are not converting into regular (loyal) customers
- Strategy should prioritize existing loyal customers while improving new customer retention rates

---

## Dataset Overview

**File:** `dataset_2019_2022.csv`  
**Time Period:** January 2019 - May 2022  
**Initial Records:** 77,750 transactions  
**Clean Records:** 77,691 transactions (after duplicate removal)  
**Data Retention Rate:** 99.9%

### Data Structure

| Column | Description | Data Type | Sample Values |
|--------|-------------|-----------|---------------|
| `customer_id` | Unique customer identifier | Integer | 15803, 19529, etc. |
| `product_id` | Unique product identifier | Integer | 1131974, 1051516, etc. |
| `basket_id` | Transaction/shopping basket ID | Integer | 57266, 69051, etc. |
| `loyalty` | Customer loyalty classification | Categorical | First Time Buyer, Loyalist, Promiscuous |
| `household_type` | Type of household | Categorical | 1 adult with kids, Couple, etc. |
| `age_band` | Age range of customer | Categorical | 19-24, 25-34, 35-44, etc. |
| `department` | Product department | Categorical | Grocery, Produce, Pharmaceutical, Health & Beauty |
| `brand` | Brand type classification | Categorical | Private, National |
| `commodity` | Product commodity/category | Categorical | Beef, Cheese, Frozen meat, Salad, etc. |
| `store` | Store location identifier | Integer | 374 (single store) |
| `price` | Item price in AUD | Float | Range: $0.10 - $68.97 |
| `transaction_date` | Date of transaction | Date | Format: DD/MM/YYYY |

---

## Data Quality & Cleaning

### Data Quality Checks Performed

✓ **Missing Values:** No null values detected across any columns  
✓ **Duplicates:** 59 duplicate records identified and removed  
✓ **Data Types:** All columns appropriately typed  
✓ **Data Anomalies:** None detected in statistical summary  

### Cleaning Steps Applied

1. **Duplicate Removal**
   - Total rows before: 77,750
   - Duplicate rows found: 59
   - Rows removed: 59
   - Final dataset: 77,691 rows
   - Data retention rate: 99.9%

2. **Date Conversion**
   - Converted `transaction_date` from string (DD/MM/YYYY) to datetime format
   - Verified date range: 2019-01-01 to 2022-05-31

3. **Feature Engineering**
   - Extracted `year` from transaction_date for temporal analysis
   - Extracted `month` from transaction_date for seasonal analysis

---

## Key Findings

### 1. Revenue Analysis

#### Yearly Revenue Performance

| Year | Total Revenue | YoY Change | Status |
|------|---------------|-----------|--------|
| 2019 | $72,623.35 | - | Baseline |
| 2020 | $74,169.00 | +2.13% | Slight growth |
| 2021 | $74,280.04 | +0.15% | Stagnation |
| 2022 | $29,908.08 | -59.74% | Incomplete data (Jan-May only) |

**Key Insight:** Revenue growth has stagnated significantly. Growth from 2019→2020 (+2.13%) declined to near-zero in 2021 (+0.15%), indicating a fundamental business challenge beyond seasonal factors.

#### Monthly Revenue Trends
- Consistent baseline revenue across most months
- Seasonal fluctuations present but minimal year-over-year growth
- 2022 data incomplete (only 5 months of data)

---

### 2. Customer Analysis

#### Total Unique Customers by Year

| Year | Unique Customers | YoY Change | Transactions |
|------|-----------------|-----------|--------------|
| 2019 | 993 | - | 19,316 |
| 2020 | 1,008 | +1.51% | 19,421 |
| 2021 | 1,021 | +1.29% | 19,424 |
| 2022 | 406 | -60.24% | 7,530 |

**Key Insight:** Customer growth is minimal (1-2% annually), and 2022 shows dramatic decline due to incomplete data. This suggests limited customer acquisition strategy.

#### Customer Segmentation by Loyalty

| Loyalty Type | 2019 | 2020 | 2021 | 2022 | Trend |
|--------------|------|------|------|------|-------|
| **First Time Buyer** | 17 | 18 | 12 | 3 | ↓ Declining |
| **Loyalist** | 356 | 399 | 464 | 171 | ↑ Growing (then decline in 2022) |
| **Promiscuous** | 620 | 591 | 545 | 232 | ↓ Declining |

**Critical Findings:**
- **Promiscuous customers** form the largest segment (~60% of customer base)
- **Loyalist segment** growing steadily (+30.9% from 2019-2021)
- **First-time buyers** declining sharply (-70.6% from 2019-2021)
  - Only 3 new customers acquired in 2022 (through May)
  - **This is the PRIMARY ISSUE:** New customers are not being acquired and retained

---

### 3. Revenue Performance by Customer Loyalty

#### Revenue Metrics by Loyalty Type

| Loyalty Type | Total Revenue | Customer Count | % of Customers | Revenue per Customer | % of Total Revenue |
|--------------|---------------|---------------|-----------------|--------------------|-------------------|
| **First Time Buyer** | $3,524.53 | 48 | 3.3% | $73.43 | 1.7% |
| **Loyalist** | $102,222.87 | 1,341 | 92.0% | $76.23 | 49.9% |
| **Promiscuous** | $145,233.07 | 1,879 | 128.8%* | $77.29 | 70.9% |

*Note: Percentages exceed 100% because customers appear across multiple years

**Key Insights:**
1. **Loyalist and promiscuous customers generate 97% of revenue** despite representing smaller customer groups
2. **Revenue per customer is remarkably consistent** ($73-77 across all loyalty types)
   - Problem is NOT spending per customer
   - Problem IS number of customers in each segment
3. **First-time buyers have lowest revenue per customer** ($73.43) and represent only 1.7% of total revenue

---

### 4. Product & Category Performance

#### Top 10 Revenue-Generating Commodities

| Rank | Commodity | Total Revenue | % of Top 10 |
|------|-----------|---------------|-----------|
| 1 | Beef | $17,297.40 | 31.5% |
| 2 | Cheese | $6,368.99 | 11.6% |
| 3 | Frozen meat | $6,235.09 | 11.4% |
| 4 | Deli meats | $5,912.61 | 10.8% |
| 5 | Seafood-frozen | $5,762.80 | 10.5% |
| 6 | Salad | $5,710.09 | 10.4% |
| 7 | Lunch meat | $5,572.08 | 10.1% |
| 8 | Pork | $5,027.56 | 9.2% |
| 9 | Cigarettes | $4,826.62 | 8.8% |
| 10 | Candy | $4,603.99 | 8.4% |

**Key Insights:**
- **Meat/protein products dominate** (Beef, Deli meats, Frozen meat, Lunch meat, Pork, Seafood = 63% of top 10)
- **Top commodity (Beef) represents 31.5%** of revenue from just one product category
- Clear opportunity to leverage high-performing categories in customer retention strategies

#### Department Performance
- **Grocery** is the primary revenue driver
- Consistent performance across multiple departments

#### Brand Performance
- **Both private and national brands** contribute significantly to revenue
- Private label products competitive with national brands

---

### 5. Price Trend Analysis (Top 10 Commodities)

#### Average Price Changes 2019-2022

| Commodity | 2019 Price | 2020 Price | 2021 Price | 2022 Price | Total Change |
|-----------|-----------|-----------|-----------|-----------|--------------|
| Beef | $5.51 | $6.34 | $5.74 | $6.06 | +10.0% |
| Cheese | $3.98 | $4.12 | $3.95 | $3.89 | -2.3% |
| Frozen meat | $4.36 | $4.59 | $4.38 | $4.72 | +8.3% |
| Deli meats | $4.14 | $4.34 | $4.03 | $4.16 | +0.5% |
| Seafood-frozen | $5.67 | $5.85 | $5.54 | $5.71 | +0.7% |
| Salad | $2.91 | $2.98 | $2.89 | $2.86 | -1.7% |
| Lunch meat | $3.57 | $3.74 | $3.49 | $3.68 | +3.1% |
| Pork | $4.38 | $4.63 | $4.41 | $4.72 | +7.8% |
| Cigarettes | $6.92 | $7.27 | $7.42 | $7.61 | +9.8% |
| Candy | $1.61 | $1.67 | $1.61 | $1.60 | -0.6% |

**Key Insight:** Most commodities show modest price stability (±10% variance). Beef and cigarettes show highest price increases (~10%). **Price increases alone are insufficient to drive revenue growth**, confirming that volume (customer acquisition/retention) is the priority.

---

## Strategic Recommendations

### 1. **URGENT: Reverse First-Time Buyer Decline**

**Problem:** First-time buyer segment declining 71% from 2019-2021, only 3 new customers acquired in 2022 (through May)

**Recommended Actions:**
- Implement aggressive new customer acquisition campaign
- Create attractive onboarding incentives (e.g., welcome discounts, loyalty sign-up bonuses)
- Review marketing channels effectiveness
- Analyze barriers to conversion and address them

**Expected Impact:** Stabilize and grow new customer pipeline to 15-20 per month

---

### 2. **Improve Promiscuous→Loyalist Conversion**

**Problem:** 60% of customer base (promiscuous shoppers) makes inconsistent purchases, not generating predictable revenue

**Recommended Actions:**
- Develop targeted personalized offers based on purchase history
- Create loyalty rewards specifically designed for promiscuous buyers
- Implement engagement campaigns during typical purchase windows
- Analyze what makes loyalists different and replicate those behaviors

**Expected Impact:** Convert 10-15% of promiscuous shoppers to loyalist status annually

---

### 3. **Increase Loyalist Engagement & Spending**

**Problem:** Despite being primary revenue drivers, loyalist spending is plateauing

**Recommended Actions:**
- Expand product range in high-performing categories (beef, dairy, proteins)
- Create bundled promotions around top commodities
- Implement tiered loyalty benefits for increased spending
- Communicate new products/promotions to loyalists more frequently

**Expected Impact:** Increase average spend per loyalist from $76.23 to $80+ per transaction (4.9% increase)

---

### 4. **Leverage High-Performing Categories**

**Problem:** Revenue concentrated in meat/protein products; other categories underperforming

**Recommended Actions:**
- Develop marketing campaigns featuring Beef and Meat products
- Cross-sell complementary items (e.g., beef + salad, cheese bundles)
- Ensure consistent stock of top 10 commodities
- Create limited-time promotions in high-margin categories

**Expected Impact:** Increase basket size and frequency of visits

---

### 5. **Investigate 2022 Revenue Decline**

**Problem:** 59.74% revenue drop in 2022, despite only having data through May

**Recommended Actions:**
- Conduct root cause analysis:
  - Store operational changes?
  - Data collection methodology changes?
  - Market disruptions (competitor entry, economic factors)?
  - Product availability issues?
- Compare 2022 (Jan-May) performance against same period in prior years
- Identify specific month of decline

---

## Path to 5% Revenue Growth

**Current Baseline (2021):** $74,280.04  
**Target (2-year growth):** $77,894.04 (5% increase = $3,614 additional revenue)

### Revenue Growth Breakdown

| Strategy | Current Revenue | Projected Uplift | Target Revenue | Confidence |
|----------|-----------------|-----------------|-----------------|------------|
| **New customer acquisition** | $3,524.53 (FTB) | +$900 (↑25.5%) | $4,424.53 | High |
| **Promiscuous→Loyalist conversion** | $145,233.07 (Promiscuous) | +$1,200 (↑0.8%) | $146,433.07 | High |
| **Loyalist spend increase** | $102,222.87 (Loyalist) | +$1,514 (↑1.5%) | $103,736.87 | Medium |
| **Price optimization** | $74,280.04 | Not relied upon | $74,280.04 | - |
| **TOTAL** | $74,280.04 | **+$3,614** | **$77,894.04** | **Medium-High** |

---

## Technical Implementation

### Libraries & Tools Used

```python
import pandas as pd          # Data manipulation and aggregation
import numpy as np           # Numerical computations
import matplotlib.pyplot as plt  # Static visualizations
import seaborn as sns        # Statistical data visualization
```

### Analysis Techniques

- **Descriptive Statistics:** Mean, median, standard deviation of key metrics
- **Time-Series Analysis:** Yearly and monthly revenue trends
- **Cohort Analysis:** Customer segmentation by loyalty type
- **Category Performance:** Revenue analysis by department, brand, commodity
- **Price Analysis:** Year-over-year price trend tracking
- **Visualization:** Line plots, bar charts, pie charts for executive communication

---

## How to Use This Repository

### Prerequisites

```bash
pip install pandas numpy matplotlib seaborn
```

### Running the Analysis

1. **Ensure CSV file is in the same directory:**
   ```bash
   dataset_2019_2022.csv
   analysis.py  (or .ipynb)
   ```

2. **Execute the analysis:**
   ```bash
   # Using Jupyter Notebook
   jupyter notebook analysis.ipynb
   
   # Or using Python script
   python analysis.py
   ```

3. **View outputs:**
   - Console tables with key metrics
   - Matplotlib/Seaborn visualizations
   - Data exported to CSV for further analysis (optional)

---

## Project Submission Details

**Assessment Type:** Video presentation with supporting documentation  
**Components:**
- **Part 1:** Slide deck (10 slides, PowerPoint format)
- **Part 2:** Video presentation (3-5 minutes, Canvas Studio)
- **Part 3:** Supporting documentation (this code)

**Marking Criteria:**
- ✓ Define relevant questions for business decision-making
- ✓ Acquire and evaluate relevant data
- ✓ Clean and format data in preparation for analysis
- ✓ Apply analytics using Python and selected libraries
- ✓ Visualize business data using Pandas/Matplotlib/Seaborn
- ✓ Communicate findings to business decision-makers

---

## File Structure

```
business-analytics-project/
├── README.md                          # This file
├── dataset_2019_2022.csv             # Source data (77,691 transactions)
├── analysis.ipynb                     # Jupyter Notebook (fully commented)
├── analysis.py                        # Python script version
├── supporting_documentation.pdf       # Exported code documentation
└── visualizations/                    # Saved charts
    ├── yearly_revenue.png
    ├── monthly_trends.png
    ├── customer_by_loyalty.png
    ├── top_commodities.png
    └── price_trends.png
```

---

## Data Referencing & Sources

- **Data Source:** SuperFoodsMax Transaction Database (2019-2022)
- **Collection Method:** Point-of-sale system export
- **Data Owner:** SuperFoodsMax Decision-Makers/Stakeholders
- **Reference Style:** RMIT Harvard (as per course requirements)

---

## Key Takeaways for Executive Team

1. **Revenue is stagnating, not declining** - 2019-2021 shows minimal growth (2.28% total)
2. **Customer acquisition is broken** - First-time buyers declining 71%
3. **Loyalists are growing but plateauing** - Retention improving, but need to unlock spend
4. **Price increases won't solve the problem** - Revenue per customer is consistent; volume is the issue
5. **Meat/protein products are the engine** - Focus marketing and promotions here
6. **5% growth is achievable** - Target of $3,614 revenue increase is realistic through customer-focused strategies

---

## Questions for Further Analysis

- What causes promiscuous customers to make sporadic purchases?
- Why are first-time customers not converting to loyalists?
- Which marketing channels are most effective for new customer acquisition?
- What products/promotions drive loyalist engagement?
- Is there seasonality in loyalty status changes?
- How do household demographics correlate with loyalty status?
- What is the customer lifetime value by loyalty segment?

---

**Project Author:** Data Analysis Team  
**Organization:** SuperFoodsMax  
**Course:** Data Analysis & Insights (RMIT University)  
**Analysis Period:** 2019-2022  
**Last Updated:** 2026  

---

## License & Confidentiality

This analysis contains proprietary SuperFoodsMax business data and insights. Distribution is restricted to authorized stakeholders only.
