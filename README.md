#  Quick Commerce Analysis

An exploratory data analysis (EDA) project on the **quick commerce industry in India**, comparing 6 platforms — **Blinkit, Swiggy Instamart, Zepto, BigBasket Now, Dunzo, and JioMart Now** — across revenue, delivery performance, customer satisfaction, and operational efficiency.

---

##  Dataset

- **File:** `quick_commerce_data_raw.csv`
- **Columns:** `Order_ID`, `Company`, `City`, `Customer_Age`, `Product_Category`, `Order_Value`, `Items_Count`, `Delivery_Time_Min`, `Distance_Km`, `Customer_Rating`, `Delivery_Partner_Rating`, `Discount_Applied`

---

##  Data Cleaning Steps

| Step | What was done |
|------|---------------|
| Missing values | Dropped rows with null `City`; filled `Items_Count` with **mode**; filled `Customer_Rating` with **group-wise mean by Company**; filled `Delivery_Partner_Rating` with **group-wise mean by Delivery_Time_Min** |
| Outlier removal | Filtered `Order_Value <= 2500` using the **filtering method** (boxplot analysis) |
| Data types | Rounded float columns → converted to `int`; `Order_ID` converted to `string` |

---

##  Business Questions & Approach

**Q1. Which quick commerce platform has the highest revenue?**
- Grouped `Order_Value` by `Company`, found max and min
- Visualised with a **combined bar + line chart** (green = highest, red = lowest)

**Q2. Which platform has the highest Average Order Value (AOV)?**
- Computed mean `Order_Value` per company
- Visualised with a **stem chart**

**Q3. How does customer rating vary across platforms?**
- Computed mean `Customer_Rating` per company
- Visualised with a **box plot** (rating distribution) + **grouped bar chart** (rating counts)

**Q4. Does delivery time affect delivery partner rating?**
- Computed **Pearson correlation** between `Delivery_Time_Min` and `Delivery_Partner_Rating`
- Created delivery time buckets: `Very fast (<10)`, `Fast (10–20)`, `Normal (20–30)`, `Slow (30–40)`, `Very slow (40–50)`
- Visualised with a **line chart** of avg partner rating per bucket

**Q5. Most popular product category on Swiggy Instamart for age 30–40 in Mumbai?**
- Applied **3-condition filter**: Company = Swiggy Instamart, City = Mumbai, Age 30–40
- Used `value_counts()` on `Product_Category`

**Q6. Which cities should companies expand into?**
- Grouped by `Company` + `City`, computed orders, avg rating, avg delivery time, revenue
- Filtered cities meeting all 3 criteria: `Avg_rating >= 3.5`, `Avg_delivery_time <= 15 min`, `Total_orders > median`
- Visualised shortlisted cities with a **grouped bar chart**

**Q7. Are discounts increasing order volume or decreasing revenue?**
- Compared avg `Order_Value` and total `Items_Count` for discounted vs non-discounted orders
- Visualised with **side-by-side bar charts**

**Q8. Which company has the best operational efficiency?**
- Aggregated `Total_orders` and `Avg_delivery_time` per company
- Normalised both using **MinMaxScaler (0–1)**
- Computed `Efficiency_Score = Total_Orders_Scaled - Avg_Delivery_Time_Scaled`
- Visualised with a **bar chart** + interactive **Plotly bubble scatter plot**

---

##  Mini Dashboard

A single-figure dashboard built with **Matplotlib + Seaborn** showing:

**KPI Cards**
-  Total Orders
-  Total Revenue (₹)
-  Avg Delivery Time (min)
-  Avg Customer Rating

**Company-level Charts**
- Orders by Company
- Revenue by Company
- Avg Delivery Time by Company
- Avg Customer Rating by Company

---

##  Libraries Used

| Library | Purpose |
|---------|---------|
| `pandas` | Data loading, cleaning, grouping |
| `numpy` | Rounding, array operations |
| `matplotlib` | All static charts and dashboard |
| `seaborn` | Bar plots, box plots, styling |
| `plotly.express` | Interactive bubble scatter plot (Q8) |
| `sklearn.preprocessing` | MinMaxScaler for efficiency score (Q8) |

---


