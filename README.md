# 🗽 New York Airbnb 2024 — Exploratory Data Analysis

## 📌 Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Project Workflow](#project-workflow)
- [Key Findings](#key-findings)
- [Visualizations](#visualizations)
- [Tech Stack](#tech-stack)
- [How to Run](#how-to-run)
- [Future Work](#future-work)

---

## Overview

This project uses a 20,765-row dataset. My separate [NYC Airbnb cleaning and modeling project](https://github.com/Talhax55z/airbnb-nyc-eda-modeling) uses a different, 102,599-row dataset.

This project performs end-to-end EDA on New York Airbnb 2024 data. The goal is to go beyond surface-level charts and extract **actionable insights** for both guests and hosts — understanding what drives prices, how availability correlates with reviews, and where the real value listings are hiding.

---

## Dataset

| Property | Detail |
|---|---|
| Source | [Inside Airbnb](http://insideairbnb.com/get-the-data/) |
| Rows | 20,765 listings |
| Columns | 22 features |
| Year | 2024 |

**Key columns used:**

- `neighbourhood_group` — Borough (Manhattan, Brooklyn, Queens, Bronx, Staten Island)
- `room_type` — Entire home/apt, Private room, Shared room, Hotel room
- `price` — Nightly rental price (USD)
- `availability_365` — Number of available days per year
- `number_of_reviews` — Total reviews received
- `reviews_per_month` — Average monthly review rate
- `beds` — Number of beds in the listing
- `latitude` / `longitude` — Geolocation for mapping

---

## Project Workflow

### 1. 🧹 Data Cleaning
- Identified and dropped null values in `price`, `neighbourhood`, and `beds`
- Converted `last_review` to `datetime` format
- Removed duplicate rows
- Cast `id` and `host_id` to object type (non-numeric identifiers)
- Capped prices at **$1,000/night** to remove extreme outliers from visualizations

### 2. 🔧 Feature Engineering
- Created `price per bed` = `price / beds` to normalize for listing size

### 3. 📊 Exploratory Data Analysis

**Univariate:**
- Price distribution (histogram + KDE)
- Availability distribution across the year

**Bivariate:**
- Price vs neighbourhood group broken down by room type
- Number of reviews vs price by borough
- Geographical scatter plot of all listings by room type

**Multivariate:**
- Pairplot across price, minimum nights, reviews, and availability
- Correlation heatmap across all numerical features

---

## Key Findings

### 💰 Pricing
- **Manhattan** has the highest average prices — entire homes average **$250+/night**
- **Brooklyn** offers the best balance of quality and cost — the smart pick for budget-conscious guests
- **Entire homes/apartments** cost significantly more than private or shared rooms across every borough
- The majority of listings are priced between **$50–$300/night**, but a handful of extreme outliers exceed $10,000+

### 🏠 Room Types
- **52% of listings** are entire homes or apartments — the most common type by far
- **Private rooms** are the budget-friendly alternative, especially in Brooklyn and Queens
- Shared rooms account for less than 5% of total listings

### 📅 Availability & Reviews
- Listings with **higher year-round availability** tend to accumulate more reviews
- More reviews generally correlates with better guest experience and repeat bookings
- Low-availability listings are often managed by part-time hosts or seasonally rented properties

### 🏘️ Host Behaviour
- A subset of hosts manage **multiple listings simultaneously** — a clear trend toward professional hosting
- These multi-listing hosts tend to cluster in Manhattan and Brooklyn

---

## Visualizations

| Chart | What it shows |
|---|---|
| 📍 Geo Map | Spatial distribution of all listing types across NYC |
| 🍩 Room Type Donut | Breakdown of listing types by proportion |
| 📊 Price by Borough & Room Type | Average nightly price across all boroughs and room categories |
| 📈 Price Distribution | Full price spread with mean and median markers |
| 🔥 Correlation Heatmap | Relationships between all numerical features |

> All visualizations were built with a custom Airbnb-inspired color palette using Matplotlib and Seaborn.

---

## Tech Stack

```
Python 3.10+
├── pandas        — data loading, cleaning, and manipulation
├── numpy         — numerical operations and outlier handling
├── matplotlib    — base plotting and chart customization
└── seaborn       — statistical visualizations (histplot, barplot, heatmap, pairplot)
```

---

## How to Run

**1. Clone the repository**
```bash
git clone https://github.com/Talhax55z/Air-BNB-1.git
cd Air-BNB-1
```

**2. Install dependencies**
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

**3. Launch the notebook**
```bash
jupyter notebook day23_note.ipynb
```

**4. Add the dataset**

The repository includes `datasets.csv`, which is the filename loaded by the notebook.

---

## Future Work

- [ ] **Price prediction model** — use regression (Linear, Random Forest) to predict nightly price from location, room type, and availability
- [ ] **Sentiment analysis** — NLP on guest reviews to surface what actually drives satisfaction
- [ ] **Interactive dashboard** — rebuild the key charts in Plotly or Streamlit for a live, filterable view
- [ ] **Time-series analysis** — track how prices and availability shift across seasons

