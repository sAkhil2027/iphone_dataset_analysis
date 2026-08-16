# 📱 iPhone E-Commerce Sales Analysis

An end-to-end **Exploratory Data Analysis (EDA)** of an iPhone
e-commerce dataset, focused on understanding product demand, pricing,
platform behavior, geographic distribution, seasonality, customer
preferences, and purchasing patterns in the Indian market.

The analysis is implemented in **Python using Pandas, Matplotlib, and
Seaborn** and is available in the accompanying Jupyter Notebook.

------------------------------------------------------------------------

## 📌 Project Overview

This project analyzes **5,843 iPhone records** from an Indian e-commerce
dataset.

The analysis answers questions such as:

-   Which iPhone models and generations receive the most demand?
-   Which storage capacities and colors are most popular?
-   How do prices vary across Amazon, Flipkart, and JioMart?
-   Which Indian states and cities contribute the most orders and
    purchase value?
-   How is demand distributed across months, quarters, and days of the
    month?
-   Are weekday and weekend purchasing patterns different?
-   How strongly do model generation, storage, color, and premium
    variants influence price?

The notebook combines **data cleaning, feature engineering, descriptive
statistics, aggregation, comparative analysis, and visualization** to
extract business-oriented insights.

------------------------------------------------------------------------

## 📂 Project Structure

``` text
.
├── iphone_analysisf.ipynb
├── Iphone_dataset.csv
└── README.md
```

> Place `Iphone_dataset.csv` in the same directory as the notebook
> before running it.

------------------------------------------------------------------------

## 🛠️ Technologies Used

  Technology                        Purpose
  --------------------------------- --------------------------------------------
  Python                            Data analysis and processing
  Pandas                            Data cleaning, transformation, aggregation
  NumPy                             Numerical operations
  Matplotlib                        Data visualization
  Seaborn                           Statistical and categorical visualization
  Jupyter Notebook / Google Colab   Interactive analysis environment

------------------------------------------------------------------------

## 📊 Dataset Overview

The original dataset contains **5,843 records and 17 columns**.

Important fields include:

-   `date` --- date associated with the record
-   `pos_name` --- e-commerce platform / point of sale
-   `product_name` --- complete iPhone product name
-   `generic_name` --- product category
-   `brand` --- brand information
-   `city` --- city associated with the record
-   `state` --- state associated with the record
-   `pincode` --- pincode information
-   `price` --- listed/purchase price in INR

The dataset contains:

-   **347 unique dates**
-   **151 unique product names**
-   **3 platforms**
-   **30 states**
-   **711 city values**
-   **73 distinct prices**

### Data-quality observations

Several columns were found to have little or no analytical value:

-   `country` was completely empty.
-   `gender_name`, `level1_name`, `level2_name`, and `level3_name` each
    had only one unique value.
-   Identifier columns such as extension ID, POS ID, product ID, and
    pincode were not required for the final business analysis.
-   City and state information was available for **2,694 of 5,843
    records**; missing location values were replaced with `Unknown`.

The notebook also identified **2,535 duplicate rows**, with **3,128 rows
involved in duplication**. These duplicates were investigated but were
**not removed in the notebook**, so the reported volumes should be
interpreted as dataset records/listings rather than independently
verified customer transactions.

------------------------------------------------------------------------

## 🧹 Data Cleaning & Preparation

The notebook performs the following preparation steps:

### 1. Date conversion

The `date` column is converted from text to Pandas datetime format.

Additional temporal features are created:

-   Year
-   Month
-   Month name
-   Day of month
-   Day name
-   Weekend flag
-   Quarter

### 2. Missing-location handling

Missing `city` and `state` values are replaced with:

``` text
Unknown
```

This preserves the records while allowing location-based analysis to
explicitly exclude unknown locations when required.

### 3. Redundant-column removal

Columns with no variation, missing values, or limited analytical
usefulness are removed from the working dataset.

### 4. Product feature extraction

The notebook extracts structured attributes from `product_name` using
regular expressions:

-   **Model** --- e.g. iPhone 15, iPhone 15 Plus, iPhone 16 Pro Max
-   **Generation** --- e.g. iPhone 13, iPhone 14, iPhone 15, iPhone 16
-   **Storage** --- 64GB, 128GB, 256GB, 512GB, 1TB
-   **Color** --- Blue, Black, Green, Midnight, Starlight, Titanium,
    etc.

These engineered features make it possible to analyze product demand and
pricing at multiple levels.

------------------------------------------------------------------------

# 🔎 Key Findings

## 1. iPhone 15 is the dominant product

The base **iPhone 15** is the strongest product in the dataset with:

**3,472 records**

This is substantially higher than premium variants and newer-generation
products.

The analysis suggests that the base model provides a strong value
proposition compared with higher-priced Pro/Pro Max variants.

------------------------------------------------------------------------

## 2. 128GB is the preferred storage capacity

The **128GB** configuration dominates the dataset with:

**5,353 records**

This indicates that the majority of observed demand is concentrated
around the entry-level storage configuration.

Higher-capacity variants such as 512GB and 1TB appear much less
frequently and are associated with substantially higher prices.

------------------------------------------------------------------------

## 3. iPhone 16 has very low observed demand

The analysis reports only:

**72 records for the iPhone 16 generation**

This is far below the observed volume for the iPhone 15 generation.

Based on this dataset, the newer generation did not achieve comparable
observed adoption.

------------------------------------------------------------------------

## 4. Blue is the most popular color

The analysis identifies **Blue** as the leading color with:

**2,114 records**

For the iPhone 15 generation specifically, Blue and Black account for a
large share of the observed volume.

For iPhone 13, Starlight and Midnight are among the strongest color
choices.

------------------------------------------------------------------------

# 💰 Platform Pricing Analysis

The dataset contains records from:

-   Amazon
-   Flipkart
-   JioMart

### Platform volume

  Platform     Records
  ---------- ---------
  Flipkart       4,561
  Amazon         1,278
  JioMart            4

Flipkart represents the overwhelming majority of records in the dataset.

### Platform price statistics

  ---------------------------------------------------------------------------
  Platform        Records      Average Median Price      Minimum      Maximum
                                 Price                           
  ---------- ------------ ------------ ------------ ------------ ------------
  Amazon            1,278   ₹48,312.08      ₹43,999      ₹22,990     ₹154,900

  Flipkart          4,561   ₹63,863.85      ₹59,999      ₹35,496     ₹184,900

  JioMart               4   ₹71,445.00      ₹71,445      ₹69,990      ₹72,900
  ---------------------------------------------------------------------------

### Main observation

Amazon has a lower median price than Flipkart, while Flipkart shows a
wider high-price range.

JioMart appears to have the most tightly controlled price range, but
this conclusion must be treated cautiously because **only four JioMart
records are present**.

The notebook's boxplot analysis also highlights substantial outliers on
Amazon and Flipkart, suggesting that the same broad platform can contain
both discounted and premium product configurations.

------------------------------------------------------------------------

# 🗺️ Geographic Analysis

Location analysis was performed after excluding records where the state
or city was `Unknown`.

## Top States by Record Volume

    Rank State              Records
  ------ ---------------- ---------
       1 Maharashtra            356
       2 Uttar Pradesh          303
       3 Karnataka              222
       4 Haryana                214
       5 Delhi                  201
       6 Telangana              199
       7 West Bengal            173
       8 Tamil Nadu             131
       9 Madhya Pradesh         124
      10 Rajasthan              121

### State revenue / purchase value

Maharashtra leads with approximately:

**₹2.25 Cr**

followed by:

**Uttar Pradesh --- ₹1.97 Cr**

Other major markets include Karnataka, Haryana, Delhi, Telangana, and
West Bengal.

The analysis shows a clear concentration of observed purchase value
among the leading states.

------------------------------------------------------------------------

# 🏙️ City-Level Analysis

The strongest cities by observed record volume are:

    Rank City          Records   Purchase Value
  ------ ----------- --------- ----------------
       1 New Delhi         175         ₹1.17 Cr
       2 Hyderabad         154         ₹1.00 Cr
       3 Bengaluru         138         ₹89.27 L
       4 Pune               69         ₹42.96 L
       5 Chennai            52         ₹34.82 L
       6 Mumbai             51         ₹31.97 L
       7 Gurugram           45         ₹28.95 L
       8 Lucknow            40         ₹25.28 L
       9 Jaipur             38         ₹25.89 L
      10 Ahmedabad          38         ₹23.11 L

New Delhi and Hyderabad are the only two cities in the analysis to reach
or exceed the **₹1 Crore** purchase-value level.

There is also a sharp drop after the top three cities: Bengaluru has 138
records while Pune has only 69.

------------------------------------------------------------------------

# 📅 Seasonality & Time Analysis

One of the strongest patterns in the notebook is the concentration of
activity in **Q3**.

### Quarter-level finding

Q3 records:

**3,582**

This is more than the combined volume of the other three quarters
according to the notebook's analysis.

### September peak

September accounts for:

**3,211 records**

and represents nearly 90% of Q3 volume.

The most extreme daily spike occurs on:

**September 25 --- approximately 1,465 records**

followed by:

**September 26 --- approximately 1,060 records**

The analysis therefore identifies a very strong late-September
concentration.

------------------------------------------------------------------------

# 📈 Day-of-Month Pattern

The September analysis shows an unusual pattern:

-   Days 1--24: almost no observed activity
-   Day 25: extreme spike
-   Day 26: another major spike
-   Following days: sharp decline

The September 25 peak is reported as more than **8.5×** the highest
daily peak observed during the rest of the year.

Outside September, the notebook identifies recurring activity peaks
around days **2, 6, 13, and 20**, with daily volumes generally much
lower than the September flash-sale spike.

------------------------------------------------------------------------

# 🗓️ Weekday vs Weekend

The notebook compares Monday--Friday against Saturday--Sunday.

  Day Type     Records    Share   Average Price   Purchase Value
  ---------- --------- -------- --------------- ----------------
  Weekday        4,722   80.81%      ₹60,762.69        ₹28.69 Cr
  Weekend        1,121   19.19%      ₹59,224.10         ₹6.64 Cr

### Key takeaway

Observed demand is heavily concentrated on weekdays, with approximately:

**80.8% weekday volume**

versus:

**19.2% weekend volume**

The average weekday price is also slightly higher than the weekend
average.

> The notebook suggests this pattern may align with promotional or
> early-access sales behavior, but the dataset itself does not establish
> the exact cause.

------------------------------------------------------------------------

# 💎 Price Analysis by Product Attributes

The notebook analyzes price distributions using boxplots and violin
plots.

## Model

The **Pro Max** variants, particularly:

-   iPhone 15 Pro Max
-   iPhone 16 Pro Max

occupy the highest price segment, with median prices above approximately
**₹1.2 lakh**.

The iPhone 14 Plus shows unusually large internal price variation.

## Generation

The analysis reports:

-   **iPhone 13:** lowest and most tightly clustered pricing, around
    ₹43,000
-   **iPhone 14:** two major price clusters around ₹50,000 and ₹70,000
-   **iPhone 15:** strong concentration around ₹60,000 with a long
    premium tail
-   **iPhone 16:** widest observed price dispersion, reaching above ₹2
    lakh
-   **iPhone 11/12:** limited observed price variation below ₹60,000

## Storage

Higher storage tiers show substantially greater prices and price
dispersion.

The pivot table shows, for example:

  Generation          128GB          256GB          512GB            1TB
  ------------ ------------ -------------- -------------- --------------
  iPhone 13      ₹43,960.90     ₹53,649.00            ---            ---
  iPhone 14      ₹57,500.21     ₹68,291.46     ₹89,582.38            ---
  iPhone 15      ₹61,702.97     ₹85,393.22   ₹1,36,368.60   ₹1,37,797.75
  iPhone 16      ₹77,881.78   ₹1,08,943.48   ₹1,50,400.00   ₹1,77,900.00

This demonstrates a strong relationship between storage capacity and
observed price.

## Color

The notebook finds that **Titanium** is strongly associated with the
highest price brackets because it appears on premium Pro models.

Meanwhile, colors such as Midnight, Starlight, and Red are concentrated
in lower-priced product configurations.

Therefore, color should not be interpreted as an independent causal
price driver; it also acts as a proxy for product variant.

------------------------------------------------------------------------

# 🛒 Product & Consumer Preference Insights

The analysis reveals a strong preference for mainstream configurations:

### Most important observed preferences

-   **iPhone 15** dominates model demand.
-   **128GB** dominates storage demand.
-   **Blue** is the most frequently observed color.
-   Premium **Pro/Pro Max** variants have relatively low record volumes.
-   iPhone 16 has only **72 observed records**.
-   Higher storage configurations have higher prices and much greater
    price dispersion.

Overall, the observed demand is concentrated around **affordable,
mainstream configurations rather than premium configurations**.

------------------------------------------------------------------------

# 🔄 Platform × Product Comparison

The notebook also compares average prices for the most frequently
observed products across platforms.

Examples include:

-   Apple iPhone 13 (128GB) - Midnight --- Amazon: **₹43,499**
-   Apple iPhone 13 (128GB) - Starlight --- Amazon: **₹43,999**
-   Apple iPhone 15 (Black, 128 GB) --- Flipkart: **₹59,999**
-   Apple iPhone 15 (Blue, 128 GB) --- Flipkart: **₹59,999**
-   Apple iPhone 15 (Green, 128 GB) --- Flipkart: **₹59,999**

These comparisons illustrate that platform coverage differs by product
and that platform-level price comparisons should account for product
mix.

------------------------------------------------------------------------

# 📊 Visualizations Included

The notebook includes multiple visual analyses covering:

### Platform

-   Number of records by platform
-   Price distribution by platform

### Geography

-   Top 10 states by record volume
-   Top 10 states by purchase value
-   Top 10 cities by record volume
-   Top 10 cities by purchase value
-   State × platform order-volume heatmap

### Product

-   Price distribution by model
-   Price distribution by generation
-   Price distribution by storage
-   Price distribution by color
-   Record volume by model
-   Record volume by generation
-   Record volume by storage
-   Record volume by color
-   Generation × color breakdown
-   Generation-wise price density

### Time

-   Quarterly record volume
-   Monthly record volume
-   Day-of-month record volume
-   September vs rest-of-year daily pattern
-   Weekday vs weekend comparison

------------------------------------------------------------------------

# 🧠 Business Insights

From the analysis, several practical observations emerge:

### 1. Value-oriented configurations dominate

The strongest observed demand is concentrated around the standard iPhone
15 and 128GB storage, suggesting that mainstream buyers prioritize a
balance between price and product capability.

### 2. Premium variants occupy a different market segment

Pro and Pro Max models command much higher prices but have substantially
lower observed record volumes.

### 3. Promotions can create extreme temporal concentration

The late-September spike demonstrates how promotional periods can
dominate annual observed demand.

### 4. Platform pricing is heterogeneous

Amazon and Flipkart exhibit significant price ranges and outliers.
JioMart has a narrow range in this dataset, but the sample is too small
for a reliable platform-wide conclusion.

### 5. Geographic demand is concentrated

Maharashtra, Uttar Pradesh, Karnataka, Haryana, Delhi, and Telangana are
among the strongest observed markets.

At the city level, New Delhi, Hyderabad, and Bengaluru form a
particularly strong group before a sharp decline in volume.

------------------------------------------------------------------------

# ⚠️ Important Data Limitations

This analysis should be interpreted with the following limitations:

1.  **Duplicate records exist.**\
    The notebook found 2,535 duplicate rows. They were not removed
    before the main analysis.

2.  **The dataset may represent listings/records rather than verified
    customer transactions.**\
    Therefore, terms such as "orders" should be understood in the
    context of the dataset structure.

3.  **Location coverage is incomplete.**\
    Only 2,694 of 5,843 records have known city/state values.

4.  **JioMart has only four records.**\
    Its price statistics are therefore not directly comparable in
    reliability with Amazon or Flipkart.

5.  **The country column is completely empty.**

6.  **The dataset does not establish causality.**\
    For example, the September spike is clearly visible, but the exact
    business reason behind it cannot be proven from this dataset alone.

7.  **Price outliers may reflect different product variants.**\
    Premium models, higher storage configurations, and different product
    variants can naturally produce large price differences.

------------------------------------------------------------------------

# 🚀 How to Run

## 1. Clone the repository

``` bash
git clone <your-repository-url>
cd <your-repository-folder>
```

## 2. Install dependencies

``` bash
pip install pandas numpy matplotlib seaborn jupyter
```

## 3. Place the dataset

Make sure the following files are in the same directory:

``` text
iphone_analysisf.ipynb
Iphone_dataset.csv
```

## 4. Start Jupyter Notebook

``` bash
jupyter notebook
```

Open:

``` text
iphone_analysisf.ipynb
```

and run the cells sequentially.

------------------------------------------------------------------------

# 📌 Project Takeaway

The analysis reveals a highly concentrated iPhone market within the
observed dataset.

The strongest demand is centered around the **base iPhone 15, 128GB
storage, and mainstream colors**, while premium Pro/Pro Max
configurations occupy the high-price but lower-volume segment.

Demand is also strongly concentrated in **Q3 and particularly late
September**, with an exceptional spike around September 25--26. Weekdays
account for approximately **80.8% of observed records**, while
Maharashtra and Uttar Pradesh lead the state-level market.

The overall picture is that **mainstream configurations, promotional
timing, platform pricing, and geographic concentration are the major
patterns visible in the dataset**.

------------------------------------------------------------------------

## 👨‍💻 Author

**Akhil Vikram Singh**

B.Tech --- Mechatronics and Automation Engineering\
Indian Institute of Information Technology Bhagalpur

------------------------------------------------------------------------

## ⭐ If you found this analysis useful

Feel free to star the repository and explore the notebook for the
complete EDA, transformations, tables, and visualizations.
