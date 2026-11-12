# Superstore Sales Analysis

A data analysis project on a global retail (Superstore) dataset. I used **Python (Pandas and NumPy)** to clean and analyse the data, and **Power BI** to build an interactive dashboard.

## Problem Statement

A retail chain sells furniture, technology and office supplies in many countries, but management does not clearly know where its sales and profit come from. This project answers:

1. **Which city has the highest sales?**
2. **Which product category has the highest sales?**
3. **Who are the top 10 customers?**
4. How have sales and profit changed over the years?
5. Which markets and customer segments perform best?
6. Do discounts help or hurt profit?

**Objective:** Clean the data, answer these questions with Python, and present the results in a Power BI dashboard so the business can make decisions on stock, customers and discount policy.

## Dataset

- **Global Superstore dataset** (also available on Kaggle), 51,290 order lines, 25,035 orders, 1,590 customers, orders from 2011 to 2014
- Main columns: Order Date, Ship Mode, Customer Name, Segment, City, State, Country, Market, Region, Category, Sub-Category, Sales, Quantity, Discount, Profit, Shipping Cost
- File used: `data/global_superstore.csv` (copy taken from a public GitHub mirror of the dataset). If you reuse this project, please also credit the original Kaggle source.

## Tools Used

- Python: Pandas and NumPy
- Power BI (DAX measures and interactive dashboard)
- Jupyter Notebook

## Project Workflow

1. Load and inspect the data
2. Clean the data: fix mixed date formats, drop unused columns, check missing values and duplicates
3. Create new features: year, month, delivery days, profit margin %, loss flag (`np.where`), discount bands (`np.select`), sales outliers (IQR with `np.percentile`)
4. Calculate KPIs
5. Analyse with `groupby`, `agg`, `pivot` and `corr`
6. Export `data/superstore_cleaned.csv` for Power BI
7. Build the dashboard in Power BI (see `dashboard/POWER_BI_GUIDE.md`)

## Key Results

**Overall:** Total sales 12.64 million, total profit 1.47 million (11.6% margin), 25,035 orders, 1,590 customers.

### 1. Highest sales city: New York City, United States
| Rank | City | Sales | Profit |
|---|---|---|---|
| 1 | New York City, United States | 256,368 | 62,037 |
| 2 | Los Angeles, United States | 175,851 | 30,441 |
| 3 | Manila, Philippines | 120,887 | -11,159 |
| 4 | Seattle, United States | 119,541 | 29,156 |
| 5 | San Francisco, United States | 112,669 | 17,507 |

### 2. Highest sales category: Technology
| Category | Sales | Share of sales | Profit margin |
|---|---|---|---|
| Technology | 4,744,558 | 37.5% | 14.0% |
| Furniture | 4,110,874 | 32.5% | 6.9% |
| Office Supplies | 3,787,070 | 30.0% | 13.7% |

### 3. Top 10 customers by sales
| Rank | Customer | Sales | Profit |
|---|---|---|---|
| 1 | Tom Ashbrook | 35,668 | 6,275 |
| 2 | Greg Tran | 34,472 | 5,165 |
| 3 | Tamara Chand | 34,218 | 8,787 |
| 4 | Sean Miller | 31,125 | -1,084 |
| 5 | Bart Watters | 30,614 | 3,337 |
| 6 | Hunter Lopez | 29,664 | 7,658 |
| 7 | Sanjit Engle | 29,533 | 5,864 |
| 8 | Penelope Sewall | 29,252 | 4,426 |
| 9 | Raymond Buch | 29,198 | 8,524 |
| 10 | Zuschuss Carroll | 28,473 | 453 |

### Other findings
- Sales grew every year: +18.5% (2012), +27.2% (2013) and +26.3% (2014) over the previous year.
- APAC is the largest market by sales, followed by EU and US.
- The top 10 customers together bring only about 2.5% of sales, so revenue is spread across many customers.
- Some high-sales cities lose money (Manila and Philadelphia have negative profit), so high sales alone does not mean high profit.
- **Discounts hurt profit:** the profit margin is 25.3% with no discount, 13.7% with a 1-20% discount, and turns negative above 20% (-17.3% for 21-40%, -74.1% above 40%). About 24.5% of order lines are loss-making.

## Recommendations

- Focus stock and marketing on Technology, and review pricing in Furniture (lowest margin).
- Review discounts above 20%, since they turn orders loss-making.
- Look into loss-making cities such as Manila and Philadelphia (costs, discounts, product mix).
- Run loyalty offers for the top 10 customers, and check why two of them (Sean Miller, Zuschuss Carroll) bring almost no profit.

## Power BI Dashboard

![Dashboard](dashboard/dashboard_screenshot.png)

- KPI cards: Total Sales, Total Profit, Profit Margin %, Total Orders, Total Customers
- Charts: yearly and monthly sales trend, sales by category, top 10 cities, top 10 customers, sales by market, discount band vs profit margin
- Slicers: Year, Market, Category, Segment
- DAX used: `SUM`, `DISTINCTCOUNT`, `DIVIDE`, `CALCULATE`, `FILTER`, `ALL`

## How to Run

```bash
git clone https://github.com/<your-username>/superstore-sales-analysis.git
cd superstore-sales-analysis
pip install -r requirements.txt
jupyter notebook notebooks/superstore_sales_analysis.ipynb
```

Then open Power BI Desktop and load `data/superstore_cleaned.csv`.

## Folder Structure

```
superstore-sales-analysis/
├── data/
│   ├── global_superstore.csv      # raw data
│   └── superstore_cleaned.csv     # output of the notebook, used in Power BI
├── notebooks/
│   └── superstore_sales_analysis.ipynb
├── dashboard/
│   ├── POWER_BI_GUIDE.md
│   ├── superstore_dashboard.pbix  # add your file here
│   └── dashboard_screenshot.png   # add your screenshot here
├── requirements.txt
└── README.md
```

## Future Improvements

- Repeat the same analysis using SQL
- Add hypothesis testing (for example, do customer segments spend differently?)
- Add a simple sales forecast

## Author

Your Name | [LinkedIn](https://linkedin.com/in/your-profile) | [GitHub](https://github.com/your-username)
