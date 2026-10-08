# E-commerce Funnel & Product Conversion Analytics

## 📌 Project Overview

This project analyzes e-commerce visitor behavior, product engagement, funnel performance, and transaction activity using **Python, Pandas, and Matplotlib**.

The analysis focuses on understanding where visitors drop off in the purchase journey, which products receive high engagement but generate weak transaction activity, and how visitor engagement is associated with transaction behavior.

The project uses the **Retailrocket e-commerce events dataset**.

---

## 🎯 Business Problem

An e-commerce business is receiving a large volume of product traffic, but it does not have a clear understanding of:

- Where visitors are dropping off in the purchase journey
- How many visitors progress from viewing products to adding them to cart
- How many visitors eventually generate transaction activity
- Which products receive high traffic but have low or zero observed transaction activity
- How visitor engagement relates to transaction behavior
- How conversion performance changes over time

Understanding these patterns can help identify areas for further investigation and potential conversion improvement opportunities.

---

## 🎯 Analytical Objectives

The main objectives of this project are to:

1. Analyze the overall e-commerce conversion funnel.
2. Measure visitor-level funnel progression.
3. Identify major funnel drop-offs.
4. Analyze product-level engagement and transaction performance.
5. Identify high-traffic products with weak conversion.
6. Segment products based on observed conversion performance.
7. Analyze visitor engagement levels.
8. Examine the relationship between engagement and transaction activity.
9. Analyze daily and monthly conversion trends.
10. Generate business insights and recommendations from the analysis.

---

## 🛠️ Tools & Technologies

- **Python**
- **Pandas**
- **Matplotlib**
- **Jupyter Notebook**

---

## 📂 Dataset

### Dataset: Retailrocket E-commerce Dataset

The project uses the `events.csv` file from the Retailrocket e-commerce dataset.

The dataset contains user interaction events such as:

- `view`
- `addtocart`
- `transaction`

### Original Dataset

- Rows: **2,756,101**
- Columns: **5**
- Unique visitors: **1,407,580**
- Unique products: **235,061**

### Columns

| Column | Description |
|---|---|
| `timestamp` | Event timestamp in milliseconds |
| `visitorid` | Unique visitor identifier |
| `event` | Type of visitor interaction |
| `itemid` | Product identifier |
| `transactionid` | Transaction identifier |

---

# 🔍 Data Analysis

## 1. Initial Data Inspection

The dataset was inspected using:

- Dataset dimensions
- First and last records
- Data types
- Missing values
- Duplicate records
- Unique visitors
- Unique products
- Event distribution

---

## 2. Data Quality Assessment

The dataset contained **460 exact duplicate rows**.

A duplicate-free analytical dataset was created by removing these exact duplicate records.

After deduplication:

- Rows: **2,755,641**
- Duplicate rows removed: **460**

The `transactionid` column contains a very high number of missing values.

This is expected because most events are `view` or `addtocart`, where a transaction ID is not applicable.

Therefore, missing transaction IDs were **not treated as a general data-quality problem**.

---

## 3. Timestamp Conversion

The original timestamp was stored in milliseconds.

It was converted into a readable datetime format using Pandas.

The observed event period was approximately:

**May 3, 2015 → September 18, 2015**

This datetime column was later used for daily and monthly trend analysis.

---

# 📊 Event Distribution

After duplicate removal, the event distribution was:

| Event | Count | Share |
|---|---:|---:|
| View | 2,664,218 | 96.68% |
| Add to Cart | 68,966 | 2.50% |
| Transaction | 22,457 | 0.81% |

The dataset is heavily dominated by product-view activity.

---

# 👥 Visitor Analysis

## Unique Visitors

The dataset contains:

**1,407,580 unique visitors**

Visitors were analyzed based on whether they:

- Viewed products
- Added products to cart
- Generated transaction activity

---

# 🛒 Visitor-Level Funnel

The visitor-level funnel was constructed by identifying whether each visitor performed each event type.

| Funnel Stage | Unique Visitors | % of All Visitors |
|---|---:|---:|
| Viewed | 1,404,179 | 100.00% |
| Added to Cart | 37,722 | 2.69% |
| Transacted | 11,719 | 0.83% |

### Funnel Conversion

**View → Add to Cart**

**2.69%**

**View → Transaction**

**0.83%**

**Add to Cart → Transaction**

**31.07%**

The largest observed drop-off occurs between product viewing and add-to-cart activity.

---

# 🔄 Funnel Overlap

Visitor-level overlap was also analyzed.

Key observations:

- Visitors who viewed and added to cart: **34,401**
- Visitors who added to cart and transacted: **10,576**
- Visitors who viewed and transacted: **11,291**
- Visitors who completed all three observed actions: **10,228**

Approximately **90.25% of transaction visitors also appeared in the add-to-cart visitor group**.

However, these overlaps do not by themselves prove the chronological order of actions.

---

# 📉 Funnel Drop-Off

Based on unique visitors:

### View → Add to Cart

Approximately **97.31%** of viewing visitors did not appear in the add-to-cart visitor group.

### Add to Cart → Transaction

Approximately **68.93%** of add-to-cart visitors did not appear in the transaction visitor group.

### Complete Observed Funnel

Visitors appearing across all three event types represented approximately:

**0.73% of all visitors**

These figures describe observed event participation and should not be interpreted as a causal explanation of customer behavior.

---

# 🧾 Transaction Event Analysis

The dataset contains:

- **22,457 transaction event rows**
- **11,719 unique transaction visitors**
- **12,025 unique products appearing in transaction events**
- **17,672 unique transaction IDs**

An important distinction is made between **transaction event rows** and **unique transaction IDs**.

Therefore, the 22,457 transaction events are **not interpreted as 22,457 individual orders**.

---

# 📦 Product-Level Analysis

Products were analyzed based on:

- Number of views
- Number of add-to-cart events
- Number of transaction events
- View-to-cart rate
- View-to-transaction rate
- Cart-to-transaction rate

Products with at least **100 views** were used for higher-confidence product performance comparisons.

There were:

**3,984 products with at least 100 views**

---

# 📈 Product Performance Segmentation

Products with at least 100 views were segmented into three groups using the average product-level view-to-transaction rate as the benchmark.

| Segment | Products | Views | Add to Carts | Transactions |
|---|---:|---:|---:|---:|
| Above Benchmark | 1,390 | 289,245 | 17,399 | 7,219 |
| Below Benchmark | 972 | 214,295 | 6,192 | 1,424 |
| No Transactions | 1,622 | 290,902 | 2,382 | 0 |

### Segment Performance

| Segment | View → Cart | View → Transaction |
|---|---:|---:|
| Above Benchmark | 6.02% | 2.50% |
| Below Benchmark | 2.89% | 0.66% |
| No Transactions | 0.82% | 0.00% |

The **Above Benchmark** segment generated approximately **83.5% of transaction events** among the products included in this analysis.

---

# 🚨 High-Engagement, Low-Conversion Products

Products with high traffic but weak observed transaction activity were identified.

Examples include:

| Product | Views | Add to Cart | Transactions | View → Transaction |
|---|---:|---:|---:|---:|
| 187946 | 3,410 | 2 | 0 | 0.00% |
| 5411 | 2,325 | 9 | 0 | 0.00% |
| 370653 | 1,854 | 0 | 0 | 0.00% |
| 219512 | 1,740 | 48 | 12 | 0.69% |
| 298009 | 1,642 | 0 | 0 | 0.00% |
| 96924 | 1,633 | 0 | 0 | 0.00% |

These products represent potential areas for further investigation.

Possible areas to investigate could include:

- Product-page experience
- Pricing
- Product availability
- Product information
- Customer intent
- Traffic quality
- Measurement or tracking issues

The analysis identifies an **association/potential opportunity**, not the underlying cause.

---

# 👤 Visitor Engagement Analysis

Visitors were segmented according to the number of recorded events.

| Engagement Segment | Visitors |
|---|---:|
| Very Low | 1,001,591 |
| Low | 347,362 |
| Medium | 52,578 |
| High | 6,049 |

Approximately **95.9% of visitors recorded five or fewer events**.

---

# 🔗 Engagement & Transaction Activity

Transaction activity increased substantially across visitor engagement segments.

| Engagement Segment | Transaction Rate |
|---|---:|
| Very Low | 0.007% |
| Low | 1.49% |
| Medium | 9.42% |
| High | 25.19% |

Highly engaged visitors showed substantially higher transaction activity than low-engagement visitors.

This indicates a **strong association between visitor engagement and transaction activity**.

It should not be interpreted as proof that increasing engagement directly causes purchases.

---

# 🔁 Repeat Transaction Behavior

Transaction visitors were divided into:

- One-time transaction visitors
- Repeat transaction visitors

| Visitor Type | Visitors | Share |
|---|---:|---:|
| One-time | 9,143 | 78.02% |
| Repeat | 2,576 | 21.98% |

Repeat transaction visitors represented approximately **59.3% of transaction event activity**.

This suggests that a relatively small group of highly active visitors generated a substantial share of observed transaction events.

---

# 📅 Time-Based Analysis

Daily and monthly trends were analyzed to understand changes in:

- Product views
- Add-to-cart activity
- Transaction activity
- View-to-transaction conversion

---

# 📆 Monthly Conversion

| Month | Views | Add to Cart | Transactions | View → Cart | View → Transaction |
|---|---:|---:|---:|---:|---:|
| May | 571,655 | 14,318 | 4,611 | 2.50% | 0.81% |
| June | 590,239 | 15,031 | 5,043 | 2.55% | 0.85% |
| July | 674,797 | 17,250 | 5,802 | 2.56% | 0.86% |
| August | 533,880 | 14,725 | 4,632 | 2.76% | 0.87% |
| September* | 293,647 | 7,642 | 2,369 | 2.60% | 0.81% |

\*September represents a partial month through September 18.

### Key Observation

August recorded the highest monthly view-to-transaction conversion rate at approximately **0.87%**.

July recorded the highest number of transaction events.

---

# 📊 Visualizations

The project includes seven Matplotlib visualizations.

### 1. Monthly Conversion

Shows monthly view-to-transaction conversion performance.

### 2. Visitor Funnel

Shows visitor progression across viewing, add-to-cart, and transaction stages.

### 3. Product Performance Segments

Compares the number of products across performance segments.

### 4. Product Conversion

Compares view-to-transaction rates across product performance segments.

### 5. Monthly Views & Transactions

Shows monthly product views and transaction activity.

### 6. Monthly Transactions

Shows the monthly transaction trend.

### 7. Engagement vs Transaction Rate

Shows the relationship between visitor engagement level and transaction activity.

---

# 💡 Key Business Insights

### 1. Major funnel drop-off occurs at the view-to-cart stage

Only **2.69% of viewing visitors appeared in the add-to-cart visitor group**.

This represents the largest observed funnel drop-off.

---

### 2. Transaction activity is strongly concentrated among engaged visitors

High-engagement visitors had a transaction rate of approximately **25.19%**, compared with only **0.007%** among very-low-engagement visitors.

---

### 3. Some high-traffic products show weak transaction activity

Several products received thousands of views but generated few or zero observed transaction events.

These products should be investigated further rather than immediately assuming a product or pricing problem.

---

### 4. Above-benchmark products contribute most transaction activity

The Above Benchmark product segment generated approximately **83.5% of transaction events** among the products included in the performance segmentation.

---

### 5. July had the highest transaction volume

July recorded approximately **5,802 transaction events**, the highest monthly total in the analyzed period.

---

### 6. August recorded the highest monthly conversion rate

August had the highest monthly view-to-transaction conversion rate at approximately **0.87%**.

---

# 💼 Business Recommendations

Based on the observed patterns, the following areas could be prioritized for further investigation:

### 1. Improve product-page engagement

Investigate why a large proportion of product viewers do not proceed to add-to-cart.

Potential areas include:

- Product information
- Images
- Pricing visibility
- Availability
- User experience

---

### 2. Investigate high-traffic, low-conversion products

Review products receiving substantial traffic but generating few or no observed transactions.

These products can be prioritized for:

- Product-page review
- Pricing analysis
- Inventory checks
- Customer feedback analysis
- Controlled experiments

---

### 3. Study highly engaged visitors

Highly engaged visitors demonstrate substantially higher transaction activity.

Further analysis could examine:

- Products viewed
- Number of sessions
- Add-to-cart behavior
- Repeat visits
- Product categories

---

### 4. Monitor funnel performance over time

Monthly conversion trends can be monitored to identify periods of stronger or weaker performance.

---

# ⚠️ Limitations

This analysis has several limitations:

- The dataset contains event-level interactions rather than complete customer sessions.
- Event overlap does not guarantee chronological sequence.
- Transaction event rows are not equivalent to individual orders.
- Product metadata was not used as a core part of the analysis.
- September represents only a partial month.
- The analysis identifies associations and patterns, not causal relationships.
- No A/B testing or experimental data was available to establish causality.
- Traffic source and marketing-channel information were not included in the core dataset.

---

# 🔄 Analytical Workflow

```text
Raw E-commerce Data
        ↓
Data Inspection
        ↓
Data Quality Assessment
        ↓
Duplicate Handling
        ↓
Timestamp Conversion
        ↓
Event Analysis
        ↓
Visitor Funnel Analysis
        ↓
Product Performance Analysis
        ↓
Visitor Engagement Analysis
        ↓
Time-Based Analysis
        ↓
Visualization
        ↓
Business Insights
        ↓
Recommendations
