# Advanced Data Mining Project - Deliverable 1
## Data Collection, Cleaning, and Exploration

### Project Overview
This repository contains the first deliverable of the Advanced Data Mining project, focusing on data collection, cleaning, and exploratory data analysis using the UCI Online Retail Dataset. The project demonstrates comprehensive data preprocessing techniques and insights extraction from real-world e-commerce transaction data.

### Dataset Summary
- **Dataset**: UCI Online Retail Dataset (ID: 352)
- **Source**: UCI Machine Learning Repository
- **Original Records**: 541,909 transactions
- **Cleaned Records**: 406,829 valid transactions (after removing missing CustomerID and data quality issues)
- **Attributes**: 8 original features + 5 engineered features
- **Time Period**: December 1, 2010 to December 9, 2011
- **Business Domain**: UK-based non-store online retail (unique all-occasion gifts)

### Dataset Features
| Feature | Type | Description |
|---------|------|-------------|
| InvoiceNo | Categorical | 6-digit transaction identifier (cancellations start with 'C') |
| StockCode | Categorical | 5-digit product identifier |
| Description | Categorical | Product name |
| Quantity | Integer | Number of items per transaction |
| InvoiceDate | DateTime | Transaction timestamp |
| UnitPrice | Float | Product price per unit in GBP |
| CustomerID | Integer | 5-digit customer identifier |
| Country | Categorical | Customer country |
| TotalAmount | Float | Calculated total transaction value (Quantity × UnitPrice) |
| Year | Integer | Extracted year from InvoiceDate |
| Month | Integer | Extracted month from InvoiceDate |
| DayOfWeek | Integer | Day of week (0=Monday, 6=Sunday) |
| Hour | Integer | Hour of transaction |

### Data Cleaning Steps Performed

#### 1. Missing Value Treatment
- **CustomerID Missing**: 135,080 transactions (24.9%) without customer identification
- **Action**: Removed transactions without CustomerID for customer-focused analysis
- **Description Missing**: Minimal missing values removed
- **Rationale**: Customer analysis requires valid customer identification

#### 2. Data Quality Issues
- **Cancellation Transactions**: Identified transactions with InvoiceNo starting with 'C'
- **Negative Quantities**: Found and analyzed return/refund transactions
- **Zero/Negative Prices**: Removed 1,454 transactions with invalid pricing
- **Action**: Focused analysis on positive transactions for initial exploration

#### 3. Data Type Conversions
- **CustomerID**: Converted to integer for consistency
- **InvoiceDate**: Converted to datetime for temporal analysis
- **Description**: Standardized to uppercase and trimmed whitespace

#### 4. Feature Engineering
- **TotalAmount**: Created calculated field (Quantity × UnitPrice)
- **Temporal Features**: Extracted Year, Month, DayOfWeek, Hour from InvoiceDate
- **Purpose**: Enable time series analysis and temporal pattern identification

#### 5. Outlier Management
- **Detection**: Used IQR method to identify outliers in Quantity, UnitPrice, TotalAmount
- **Treatment**: Capped extreme outliers (>99th percentile) in UnitPrice and TotalAmount
- **Impact**: Preserved data integrity while reducing skewness from extreme values

### Key Insights from Exploratory Data Analysis

#### Business Performance Metrics
- **Total Revenue**: £9,747,748 over 11-month period
- **Total Transactions**: 22,190 unique invoices
- **Average Order Value**: £439.45
- **Average Items per Transaction**: 18.3 units
- **Customer Base**: 4,372 unique customers across 38 countries

#### Customer Analysis
- **Average Customer Lifetime**: 91 days between first and last purchase
- **Average Orders per Customer**: 5.1 transactions
- **Average Customer Value**: £2,231 total spending
- **Geographic Distribution**: UK dominates with 91.5% of sales
- **Customer Segments**: Clear patterns for RFM (Recency, Frequency, Monetary) segmentation

#### Product Performance
- **Product Catalog**: 3,958 unique products (StockCode)
- **Best-Selling Product**: WHITE HANGING HEART T-LIGHT HOLDER (2,159 units)
- **Highest Revenue Product**: PAPER CRAFT, LITTLE BIRDIE (£168,469 total)
- **Price Range**: £0.001 to £38,970 (wide variety from small gifts to bulk orders)
- **Average Product Price**: £4.61

#### Temporal Patterns
- **Peak Sales Period**: November 2011 (seasonal gift buying)
- **Weekly Pattern**: Thursday shows highest transaction volume
- **Daily Pattern**: Peak activity between 12:00-15:00 GMT
- **Seasonal Trends**: Strong Q4 performance indicating gift seasonality

#### Geographic Insights
- **Primary Market**: United Kingdom (91.5% of revenue)
- **International Presence**: 37 additional countries served
- **Top International Markets**: Germany, France, EIRE, Spain
- **Market Opportunity**: Strong European focus with expansion potential

### Correlation Analysis Results
Strong correlations identified in numerical features:
- **TotalAmount ↔ Quantity**: r = 0.631 (expected relationship)
- **Month ↔ Year**: r = 0.421 (temporal correlation)
- **Hour ↔ DayOfWeek**: r = -0.301 (business hours pattern)

### Challenges Encountered and Solutions

#### Challenge 1: Large Dataset Size
- **Issue**: 541K records requiring efficient processing
- **Solution**: Implemented chunked processing and optimized pandas operations
- **Impact**: Successful handling of large-scale retail data

#### Challenge 2: Missing Customer Information
- **Issue**: 25% of transactions without CustomerID
- **Solution**: Separated customer-focused analysis from transaction-level analysis
- **Impact**: Maintained data integrity while enabling customer behavior modeling

#### Challenge 3: Data Quality Variations
- **Issue**: Cancellations, returns, and pricing inconsistencies
- **Solution**: Implemented systematic cleaning pipeline with business logic
- **Impact**: Created clean dataset suitable for multiple modeling approaches

#### Challenge 4: Temporal Complexity
- **Issue**: Date/time features requiring multiple analytical perspectives
- **Solution**: Engineered comprehensive temporal features for trend analysis
- **Impact**: Enabled robust time series and seasonal analysis capabilities

### Implications for Future Deliverables

#### Deliverable 2: Regression Modeling
- **Sales Forecasting**: Time series regression for revenue prediction
- **Customer Value Prediction**: Regression models for lifetime value estimation
- **Price Optimization**: Demand elasticity modeling using price-quantity relationships
- **Inventory Planning**: Quantity prediction models by product and season

#### Deliverable 3: Classification and Clustering
- **Customer Segmentation**: RFM-based clustering for marketing personalization
- **Churn Prediction**: Classification models using purchase recency patterns
- **Product Categorization**: Clustering analysis for inventory management
- **Geographic Segmentation**: Country-based customer classification

#### Deliverable 4: Association Rule Mining
- **Market Basket Analysis**: Product affinity analysis for cross-selling
- **Customer Behavior Patterns**: Purchase sequence mining
- **Seasonal Association Rules**: Time-based product relationships
- **Geographic Purchasing Patterns**: Location-based buying behavior analysis

### Technical Approach Validated
- **Data Volume**: Successfully processed 541K+ transaction records
- **Feature Richness**: 13 features enabling comprehensive analysis
- **Business Relevance**: Real e-commerce data with practical applications
- **Modeling Diversity**: Dataset supports all required analytical techniques

### Files in Repository
- `online_retail_analysis.ipynb` - Complete data analysis and cleaning notebook
- `cleaned_online_retail_dataset.csv` - Processed transaction data
- `customer_metrics.csv` - Customer-level aggregated metrics
- `rfm_analysis.csv` - RFM segmentation analysis results
- `README.md` - Project documentation
- `/screenshots/` - Analysis visualizations and results

### Technical Requirements Compliance
- Dataset Size: 541,909 records >> 500+ requirement
- Feature Count: 13 total features >> 8-10+ requirement  
- Data Cleaning: Comprehensive preprocessing pipeline implemented
- EDA: Multiple visualization types and statistical analysis completed
- Business Insights: Actionable findings for retail optimization identified
- Documentation: Professional repository structure maintained

### Usage Instructions
1. Install required packages: `pip install pandas numpy matplotlib seaborn scikit-learn ucimlrepo`
2. Clone repository and navigate to project directory
3. Run Jupyter notebook: `online_retail_analysis.ipynb`
4. Review generated visualizations and analysis outputs
5. Use exported CSV files for subsequent deliverable development

### Dataset Access
```python
from ucimlrepo import fetch_ucirepo
online_retail = fetch_ucirepo(id=352)
df = online_retail.data.features
```

Alternative: Download directly from UCI ML Repository at https://archive.ics.uci.edu/dataset/352/online+retail

