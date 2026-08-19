# SuperFoodsMax Revenue Growth Analysis and Recommendations

## Project Overview
This project analyses transactional point-of-sale data from **SuperFoodsMax** spanning January 2019 to May 2022. The primary objective is to evaluate historical sales, customer loyalty behaviour, and product pricing dynamics to identify data-driven strategies for achieving a **5% revenue increase over a two-year period**.

## Business Question
> **How can SuperFoodsMax achieve a 5% revenue growth over the next two years by optimising customer loyalty retention, converting new/promiscuous shoppers, and leveraging high-performing product categories?**

## Key Stakeholder Insights
* Overall revenue growth has stagnated from 2019 to 2021.
* First-time buyer acquisition and retention have declined sharply.
* Average revenue spend per customer is consistent across loyalty segments, indicating that growth must be driven by customer volume, tier progression, and basket optimisation rather than direct price hikes alone.

---

## Dataset Overview
* **File:** `dataset_2019_2022.csv`
* **Time Period:** 01 January 2019 – 31 May 2022
* **Total Transactions:** 77,750 (Raw) | 77,691 (Cleaned)
* **Duplicate Rows Removed:** 59
* **Data Retention Rate:** 99.92%
* **Store Scope:** Store #374

### Data Dictionary
| Column | Description | Data Type | Sample Values |
| :--- | :--- | :--- | :--- |
| `customer_id` | Unique customer identifier | Integer | `15803`, `19529` |
| `product_id` | Unique product identifier | Integer | `1131974`, `1051516` |
| `basket_id` | Unique shopping basket ID | Integer | `57266`, `69051` |
| `loyalty` | Customer loyalty tier | Categorical | `First Time Buyer`, `Loyalist`, `Promiscuous` |
| `household_type` | Customer household demographic | Categorical | `1 adult with kids`, `Couple` |
| `age_band` | Age range bracket | Categorical | `19-24`, `25-34`, `35-44` |
| `department` | Product department | Categorical | `Grocery`, `Produce`, `Pharmaceutical` |
| `brand` | Brand classification | Categorical | `National`, `Private` |
| `commodity` | Product commodity category | Categorical | `Beef`, `Cheese`, `Frozen meat` |
| `store` | Store location identifier | Integer | `374` |
| `price` | Item price in AUD | Float | `$0.10` – `$68.97` |
| `transaction_date` | Date of purchase | Date | Parsed with `dayfirst=True` |

---

## Data Quality & Cleaning

### Data Checks Performed
* **Missing Values:** `0` missing values detected across all columns.
* **Duplicate Records:** Identified and removed 59 exact duplicate rows.
* **Date Parsing Correction:** Raw dates stored as `DD/MM/YYYY` were explicitly parsed using `pd.to_datetime(df['transaction_date'], dayfirst=True)`. This corrected standard `MM/DD/YYYY` misparsing that previously inverted days/months, created phantom post-May 2022 data, and obscured true Q4 holiday spikes.

---

## Key Analytical Findings

### 1. Revenue & Seasonality Analysis

#### Full-Year Annual Revenue (2019–2021 Baseline)
*Note: 2022 is excluded from full-year annual comparisons as data concludes on May 31, 2022.*

| Year | Total Revenue (AUD) | YoY Change (%) | Business Performance |
| :--- | :--- | :--- | :--- |
| **2019** | $72,731.76 | — | Baseline year |
| **2020** | $74,212.31 | +2.04% | Modest growth |
| **2021** | $74,335.87 | +0.17% | Growth stagnation |

#### Like-for-Like YTD Comparison (Months 1–5: Jan–May)
To evaluate 2022 performance accurately without partial-year distortion, Months 1–5 were compared across all 4 years:

| Year | Jan–May Revenue (AUD) | YoY Change (%) | Status |
| :--- | :--- | :--- | :--- |
| **2019** | $28,586.81 | — | Baseline |
| **2020** | $29,326.15 | +2.59% | Strongest early-year growth |
| **2021** | $29,720.79 | +1.35% | Moderate growth |
| **2022** | $29,934.94 | +0.72% | Ongoing early-year deceleration |

#### Monthly Seasonality Insights
* **Peak Shifts:** Mid-year revenue peaks have shifted earlier across successive years (moving from August in 2019/2020 toward June/July in 2021).
* **September Trough:** A recurring seasonal sales dip occurs consistently in September (Month 9).
* **End-of-Year Surge:** Strong seasonal spike occurs in November and December (Months 11 & 12).

---

### 2. Customer Loyalty & Retention Dynamics

#### Customer Counts by Loyalty Tier
| Loyalty Tier | 2019 | 2020 | 2021 | 2022 (Jan–May) | 2019–2021 Trend |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **First Time Buyer** | 17 | 18 | 12 | 3 | **Declining (-29.4%)** |
| **Loyalist** | 356 | 399 | 464 | 171 | **Growing (+30.3%)** |
| **Promiscuous** | 620 | 591 | 545 | 232 | **Declining (-12.1%)** |

#### Revenue Contribution by Loyalty Group
| Loyalty Group | Total Revenue (AUD) | Unique Customers | Revenue per Customer | % of Total Revenue |
| :--- | :--- | :--- | :--- | :--- |
| **First Time Buyer** | $3,524.53 | 48 | $73.43 | 1.4% |
| **Loyalist** | $102,324.80 | 1,341 | $76.30 | 40.7% |
| **Promiscuous** | $145,365.55 | 1,879 | $77.36 | 57.9% |

**Key Takeaways:**
* Average revenue per customer is virtually identical across all groups (~$73–$77).
* Growth is a **customer pipeline and volume issue**, not an individual spending deficit.
* The **Loyalist** segment grew by **+30.3%** between 2019 and 2021, proving high retention capability once customers are successfully converted.

---

### 3. Product, Brand & Commodity Performance

#### Top 10 Commodities by Revenue
| Rank | Commodity | Total Revenue (AUD) | Department |
| :---: | :--- | :--- | :--- |
| **1** | Beef | $17,317.96 | Meat / Grocery |
| **2** | Cheese | $6,372.04 | Dairy / Grocery |
| **3** | Frozen meat | $6,244.27 | Frozen |
| **4** | Deli meats | $5,915.40 | Deli |
| **5** | Seafood-frozen | $5,762.80 | Frozen |
| **6** | Salad | $5,722.26 | Produce |
| **7** | Lunch meat | $5,579.82 | Meat / Deli |
| **8** | Pork | $5,030.35 | Meat |
| **9** | Cigarettes | $4,829.58 | Tobacco / Front End |
| **10** | Candy | $4,611.48 | Confectionery |

* **Department Performance:** Grocery, Produce/Meat, and Pharmaceuticals lead total sales volume.
* **Brand Breakdown:** National brands account for the majority of revenue volume over Private label.
* **Pricing Pressures:** Average prices for staple commodities rose significantly between 2019 and 2022 (e.g., Beef rose from $5.52 to $6.05; Frozen meat from $4.36 to $4.72).

---

## Strategic Recommendations (Key Learnings to Actionables)

| # | Key Analytical Learning | Strategic Actionable |
| :--- | :--- | :--- |
| **1** | **Revenue Deceleration & Shifting Seasonality**<br>• Annual growth slowed from +2.04% (2020) to +0.17% (2021).<br>• Seasonal peaks shifted earlier (from August toward June).<br>• Consistent revenue troughs occur in September. | **Campaign Timing & Seasonality Optimisation**<br>• Review and replicate past successful promotional campaigns from peak mid-year periods.<br>• Launch targeted recovery campaigns in **September** to counteract the annual revenue trough. |
| **2** | **Customer Growth Deceleration & Loyalty Potential**<br>• New customer acquisition is falling (only 3 First-Time Buyers in early 2022).<br>• Revenue per customer is consistent across segments (~$73–$77).<br>• Loyalist group grew organically by +30.3% from 2019 to 2021. | **Loyalist Playbook Replication Across All Tiers**<br>• Audit the loyalty programs and nurturing workflows that fueled Loyalist growth.<br>• Replicate onboarding and retention incentives across First-Time Buyers and Promiscuous shoppers to build a reliable conversion pipeline. |
| **3** | **Product Dominance & Inflationary Price Rises**<br>• Top commodities: Beef ($17.3k), Cheese ($6.4k), Frozen meat ($6.2k).<br>• Sharp price increases in protein categories risk driving volume down.<br>• High-volume categories present natural cross-sell synergies. | **Cost-Saving, Price Competitiveness & Product Bundling**<br>• Implement operational/supply chain cost-saving measures to keep staple protein prices competitive.<br>• **Cross-Category Bundles:** Introduce promotional value bundles pairing high-affinity items (e.g., *Meat + Cheese* entertaining bundles or *Beef + Salad* dinner bundles) to increase basket size and overall visit volume. |

---

## Path to 5% Revenue Growth

* **Baseline Revenue (2021):** $74,335.87
* **2-Year Growth Target (+5.0%):** **$78,052.66** (Net uplift of **+$3,716.79**)

| Growth Driver | Strategic Action | Projected Revenue Uplift |
| :--- | :--- | :--- |
| **Loyalty Conversion** | Convert 10–15% of Promiscuous shoppers to Loyalist status | +$1,500.00 |
| **Acquisition & Onboarding** | Stabilize First Time Buyer pipeline with welcome discounts | +$900.00 |
| **Cross-Category Bundles** | Bundle Meat + Cheese / Produce to lift average basket size | +$1,350.00 |
| **Total Projected Uplift** | | **+$3,750.00 (+5.04%)** |

---

## Technical Implementation

### Python Libraries Used
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

## Acknowledgements & Data Source
Data Source: SuperFoodsMax Transaction Database (2019–2022)

Curriculum & Project Framework: Credit and special thanks to RMIT Online (Business Analytics with SQL and Python course).

Reference Style: RMIT Harvard Referencing Standard

## License & Confidentiality
This analysis contains business analysis work completed for academic purposes. Distribution is intended for project evaluation and portfolio demonstration.
