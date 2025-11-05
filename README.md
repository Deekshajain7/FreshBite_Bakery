# 🍞 FreshBite Bakery: Inventory Waste Optimization

## Executive Summary

**Problem**: FreshBite Bakery loses $2,500/month (17% of inventory) to product spoilage across 3 store locations.

**Approach**: Analyzed 9 months of sales, inventory, and product data using Python for data cleaning, SQL for business queries, and statistical visualizations to identify waste patterns.

**Outcome**: Identified top 10 products causing 60% of waste, discovered 23% spoilage rate difference between stores, and provided actionable recommendations to reduce waste by 40% ($1,000/month savings).

**Key Metrics**:
- 📊 Analyzed 21151 sales transactions and 16437 inventory records
- 💰 Identified $3,200 in monthly waste across 45 products
- 🎯 Pinpointed 10 high-impact products for immediate action
- 📈 Discovered seasonal patterns affecting reorder decisions

---

## 🎯 Business Problem & Objective

### Problem Statement
Small bakery chains face significant profit loss due to product spoilage. Unlike large chains with sophisticated inventory systems, small businesses often lack data-driven insights to optimize stock levels.

### Who Benefits?
- **Store Managers**: Daily reorder guidance based on actual waste patterns
- **Business Owners**: Clear ROI on inventory optimization efforts
- **Customers**: Fresher products with better availability

### Success Criteria
- Reduce overall spoilage rate from 17% to under 10%
- Identify top waste-causing products (80/20 rule)
- Provide store-specific recommendations
- Create repeatable analysis framework

---

## 📊 Data & Methodology

### Data Sources
**Synthetic dataset** designed to mirror real bakery operations:

| Dataset | Records | Time Period | Description |
|---------|---------|-------------|-------------|
| Products | 45 items | Static | Product catalog with pricing, categories, shelf life |
| Sales | | ~21,151| | Jan-Sep 2024 | Daily transactions across 3 stores |
| Inventory | ~16,437 | Jan-Sep 2024 | Stock levels and spoilage tracking |

### Process Framework (CRISP-DM)

#### 1️⃣ **Business Understanding** (Day 1)
- Defined stakeholder needs
- Established success metrics
- Created realistic data generation parameters

#### 2️⃣ **Data Understanding** (Day 2 - EDA)
**Key Discoveries**:
- Missing values in 3 locations (shelf life, store location, spoilage)
- Data quality issues: negative spoilage values, outliers (50-100 units)
- Product name inconsistencies ("Sourdough" vs "Sourdough Bread")
- Weekend sales 40% higher than weekdays
- Store spoilage rates vary 15-23%

**Tools Used**: Pandas, Matplotlib, Seaborn

#### 3️⃣ **Data Preparation** (Day 3 - Cleaning)
**Cleaning Decisions**:
- Filled missing shelf life using category averages (business logic)
- Removed sales records with missing store (0.04% of data)
- Fixed negative spoilage → set to 0 (data entry errors)
- Capped outlier spoilage using IQR method (upper bound = Q3 + 3*IQR)
- Filled missing spoilage with median (conservative approach)
- Standardized product names for consistency

**Derived Features Created**:
- `profit_per_unit` = selling_price - unit_cost
- `spoilage_rate` = (stock_spoiled / total_stock) * 100
- `waste_cost` = stock_spoiled * unit_cost
- `is_weekend` = 1 if Saturday/Sunday else 0

**Tools Used**: Pandas, NumPy

#### 4️⃣ **Modeling/Analysis** (Day 4 - SQL Queries)
**Database Design**: 3-table normalized schema (products, sales, inventory) with foreign keys and indexes

**8 Business-Critical Queries**:
1. Top 10 products by spoilage volume
2. Top 10 products by waste cost
3. Spoilage comparison by store location
4. Spoilage breakdown by category
5. Monthly spoilage trend analysis
6. Weekend vs weekday spoilage patterns
7. High waste + low sales products (discontinuation candidates)
8. Comprehensive store performance dashboard

**Tools Used**: SQLite, SQL joins, aggregations, window functions

#### 5️⃣ **Evaluation** (Day 5 - Visualization)
Created 8 visualizations answering specific business questions with actionable recommendations embedded in titles.

**Tools Used**: Matplotlib, Seaborn

---

## 🔍 Results & Business Insights

### Finding #1: Top 10 Products Drive 60% of Waste
![Top Spoilage Products](viz1_top_spoilage_products.png)

**Insight**: Cinnamon Roll, Croissant, and Blueberry Muffin account for 35% of all spoilage despite being only 6.7% of product catalog.

**Recommendation**: Reduce daily stock levels by 30% for top 3 products. Implement made-to-order system for Cinnamon Rolls.

---

### Finding #2: $3,200 Monthly Waste Concentrated in 10 Products
![Waste Cost](viz2_top_waste_cost.png)

**Insight**: High-cost items (Pain au Chocolat, Eclair) create disproportionate financial impact despite moderate spoilage volume.

**Recommendation**: Prioritize waste reduction for top 5 products = potential $1,000/month savings.

---

### Finding #3: 23% Spoilage Rate Difference Between Stores
![Store Comparison](viz3_spoilage_by_store.png)

**Insight**: Westside location has 23% higher spoilage rate than Eastside despite similar sales volume.

**Recommendation**: 
- Audit Westside inventory management practices
- Share Eastside best practices (training opportunity)
- Investigate temperature control and FIFO compliance

---

### Finding #4: Pastry & Bread Categories Account for 65% of Waste
![Category Breakdown](viz4_spoilage_by_category.png)

**Insight**: Short shelf-life categories (1-2 days) naturally have higher waste, but current stock levels don't account for this.

**Recommendation**: Implement category-specific reorder formulas based on shelf life and demand patterns.

---

### Finding #5: Seasonal Pattern - Summer Peak in Waste
![Monthly Trend](viz5_monthly_trend.png)

**Insight**: Spoilage peaked in June-July (vacation season = unpredictable customer traffic).

**Recommendation**: Reduce base inventory 15-20% during summer months. Use weather data for daily adjustments.

---

### Finding #6: Weekend Spoilage 12% Higher Despite Higher Sales
![Weekend vs Weekday](viz6_weekend_weekday.png)

**Insight**: Weekend overstocking occurs despite demand spike. Monday inventory shows highest waste.

**Recommendation**: Increase weekend production but with tighter batch controls. Reduce Monday opening stock.

---

### Finding #7: 15 Products Are Discontinuation Candidates
![High Waste Low Sales](viz7_high_waste_low_sales.png)

**Insight**: Products like Pumpernickel Bread and Spinach Quiche have waste-to-sales ratios above 0.50 (waste more than half of what's sold).

**Recommendation**: 
- Discontinue bottom 3 performers immediately
- Switch next 5 to "weekly special" rotation (not daily stock)
- Consider customer pre-order system

---

### Finding #8: Store Performance Dashboard Reveals Operational Gaps
![Store Dashboard](viz8_store_dashboard.png)

**Insight**: Downtown has highest sales but also highest absolute waste. Westside has worst spoilage rate. Eastside is most efficient.

**Recommendation**: 
- Downtown: Waste is proportional to volume (acceptable but improvable)
- Westside: Needs immediate operational review
- Eastside: Model for other stores

---

## 💼 Business Impact Summary

### Quantified Savings Potential

| Action | Monthly Savings | Implementation |
|--------|----------------|----------------|
| Reduce stock for top 10 products by 30% | $1,000 | Immediate |
| Discontinue bottom 3 performers | $180 | Week 1 |
| Fix Westside operational issues | $400 | Week 2-4 |
| Implement seasonal adjustments | $220 | Ongoing |
| **Total Potential Savings** | **$1,800/month** | **$21,600/year** |

### Spoilage Rate Projection
- **Current**: 17% average spoilage rate
- **Target**: 9-10% (after recommendations)
- **Industry Benchmark**: 8-12% for small bakeries

---

## 🚧 Limitations & Next Steps

### Current Limitations
1. **Synthetic Data**: Real-world data may have more complex patterns (holidays, events, weather)
2. **No Customer Demand Forecasting**: Analysis is reactive, not predictive
3. **Limited Time Granularity**: Daily data misses intra-day patterns (morning vs evening)
4. **No External Factors**: Weather, local events, competitor actions not included
5. **Single Chain**: Findings may not generalize to other bakery types

### Recommended Next Steps

**Phase 1 - Quick Wins (Week 1-2)**
- [ ] Implement top 10 product stock reductions
- [ ] Audit Westside store operations
- [ ] Discontinue bottom 3 products

**Phase 2 - System Improvements (Month 2-3)**
- [ ] Build automated daily reorder recommendations
- [ ] Integrate weather API for demand adjustments
- [ ] Create manager dashboard with real-time spoilage alerts
- [ ] Implement FIFO tracking system

**Phase 3 - Advanced Analytics (Month 4-6)**
- [ ] Deploy time-series forecasting model (ARIMA/Prophet)
- [ ] Add customer pre-order system
- [ ] Test dynamic pricing for near-expiry items
- [ ] Expand analysis to other bakery chains

**Technical Enhancements**:
- Migrate from SQLite to PostgreSQL for production scale
- Build Streamlit dashboard for non-technical stakeholders
- Automate weekly reporting pipeline
- Add anomaly detection for sudden waste spikes

---

## 🛠️ Technical Stack

| Component | Tool | Purpose |
|-----------|------|---------|
| Data Generation | Python (Faker, NumPy) | Create realistic synthetic data |
| Data Cleaning | Pandas | Handle missing values, outliers, standardization |
| Database | SQLite | Relational data storage and queries |
| Analysis | SQL | Business logic queries and aggregations |
| Visualization | Matplotlib, Seaborn | Static charts with business insights |
| Documentation | Markdown | Professional project presentation |

---

## 📁 Project Structure

```
inventory_waste_project/
│
├── data/
│   ├── raw/                          # Original generated data
│   │   ├── products.csv
│   │   ├── sales_transactions.csv
│   │   └── inventory_records.csv
│   │
│   ├── cleaned/                      # Processed data & query results
│   │   ├── products_clean.csv
│   │   ├── sales_clean.csv
│   │   ├── inventory_clean.csv
│   │   ├── query1_top_spoilage_products.csv
│   │   └── ... (8 query result files)
│   │
│   └── freshbite_bakery.db          # SQLite database
│
├── notebooks/
│   ├── 01_eda.ipynb                 # Exploratory Data Analysis
│   ├── 02_cleaning.ipynb            # Data Cleaning Pipeline
│   ├── 03_sql_analysis.ipynb        # SQL Queries & Database
│   └── 04_visualization.ipynb       # Business Visualizations
│
└── README.md                         # This file
```

---

## 🚀 How to Run This Project

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn sqlite3
```

### Step-by-Step Execution

**Day 1**: Generate data
```python
python data_generator.py  # Creates 3 CSV files
```

**Day 2**: Explore data
```bash
jupyter notebook notebooks/01_eda.ipynb
```

**Day 3**: Clean data
```bash
jupyter notebook notebooks/02_cleaning.ipynb
```

**Day 4**: SQL analysis
```bash
jupyter notebook notebooks/03_sql_analysis.ipynb
```

**Day 5**: Visualize insights
```bash
jupyter notebook notebooks/04_visualization.ipynb
```

---

## 📚 Key Learnings

### Technical Skills Demonstrated
✅ **Data Quality Assessment**: Identified and documented 6 types of data issues  
✅ **Strategic Data Cleaning**: Made business-driven decisions (not just technical fixes)  
✅ **SQL Proficiency**: Complex joins, aggregations, window functions  
✅ **Business-Focused Visualization**: Every chart answers "so what?"  
✅ **End-to-End Workflow**: From raw data to actionable insights  

### Business Skills Demonstrated
✅ **Stakeholder Communication**: Translated technical findings to business language  
✅ **ROI Quantification**:  annual savings potential identified  
✅ **Actionable Recommendations**: Specific, measurable, time-bound suggestions  
✅ **Risk Assessment**: Acknowledged limitations and mitigation strategies  

---

## 👤 About This Project

**Author**: Deeksha Jain  
**Role**: Data Analyst  
**Project Type**: Portfolio Project - Data Analytics  
**Duration**: 7 days (learning project)  
**Date**: October 2025

**Contact**: deekshadineshjain@gmail.com
 |           https://www.linkedin.com/in/deekshajain7

---

## 📄 License

This project uses synthetic data and is intended for educational/portfolio purposes.

---

**⭐ If this project helped you, please star the repository!**"# FreshBite_Bakery" 
"# FreshBite_Bakery" 
