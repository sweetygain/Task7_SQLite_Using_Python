# Task7_SQLite_Using_Python
This project analyzes transactional sales data from a CSV using SQLite and Python. It loads data into a database, performs SQL queries inside Python, and visualizes top products by revenue using Matplotlib and Seaborn.
# 🛍️ Sales Data Analysis Project

This project analyzes transactional sales data using Python and SQLite. It demonstrates how to load data from a CSV, store it in a database, run SQL queries, and visualize key insights using Seaborn and Matplotlib.

---

## 📌 Features

- Import CSV data into SQLite using Pandas
- Run SQL queries inside Python
- Generate:
  - Top 10 Products by Revenue (Bar Chart)
  - Revenue by Region
  - Revenue by Payment Method
  - Monthly Revenue Trend (Optional)
- Save visualizations as `.png` files

---

 Tech Stack:
- Python
- SQLite3
- Pandas
- Matplotlib
- Seaborn
- Jupyter Notebook
---
python :
 Step 1: Import libraries
import sqlite3
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

Step 2: Load data and connect
df = pd.read_csv("trend (1).csv")
conn = sqlite3.connect("sales_data.db")
df.to_sql("sales", conn, if_exists="replace", index=False)

Step 3: SQL query + visualization
query = """
SELECT [Product Name] AS product,
       SUM([Units Sold]) AS total_units,
       SUM([Total Revenue]) AS total_revenue
FROM sales
GROUP BY [Product Name]
ORDER BY total_revenue DESC
LIMIT 10
"""
top_products = pd.read_sql_query(query, conn)

Step 4: Plot
sns.barplot(data=top_products, x="total_revenue", y="product", palette="Blues")
plt.title("Top 10 Products by Revenue")
plt.xlabel("Revenue")
plt.ylabel("Product")
plt.tight_layout()
plt.savefig("top_10_products_revenue.png")
plt.show()
also used 
