# Daily Pandas + SQL Practice with ChatGPT, Claude & Meta AI (WhatsApp) 07th October 2026
<b>For each category, among only orders with</b> ```quantity >= 3;```</br>
<ul>
   <li> Find <b>the number of orders</b>
   <li> Find <b>the total quantity</b>
   <li> Find <b>the average unit price</b>
</ul></br>
<b>SQL concept</b><br>
You will need:</br>

```
WHERE
GROUP BY
COUNT()
SUM()
AVG()
```

<b>Pandas concept</b></br>
You will need:</br>
```
filtering
groupby()
count()
sum()
mean()
```

```SQL
sqlite> SELECT
   ...> category,
   ...> COUNT(order_status),
   ...> SUM(quantity),
   ...> MAX(unit_price),
   ...> MIN(unit_price)
   ...> FROM orderz
   ...> WHERE quantity >= 3 AND
   ...> order_status = 'Completed'
   ...> GROUP BY category;
╭────────────────┬─────────────────────┬───────────────┬─────────────────┬─────────────────╮
│    category    │ COUNT(order_status) │ SUM(quantity) │ MAX(unit_price) │ MIN(unit_price) │
╞════════════════╪═════════════════════╪═══════════════╪═════════════════╪═════════════════╡
│ Books          │                   7 │            28 │          284.36 │           38.81 │
│ Clothing       │                   6 │            27 │          226.42 │           29.71 │
│ Electronics    │                   6 │            24 │          226.77 │           80.72 │
│ Home & Kitchen │                   8 │            31 │          295.43 │           88.57 │
│ Sports         │                   6 │            28 │          252.07 │           33.78 │
╰────────────────┴─────────────────────┴───────────────┴─────────────────┴─────────────────╯
```
```Python
import pandas as pd
df = pd.read_csv('orders.csv')
df1 = df[(df["quantity"] >= 3) & (df["order_status"]== "Completed")].groupby("category")["order_status"].count().reset_index()
df2 = df[(df["quantity"] >= 3) & (df["order_status"]== "Completed")].groupby("category")["quantity"].sum().reset_index()
df3 = df[(df["quantity"] >= 3) & (df["order_status"]== "Completed")].groupby("category")["unit_price"].max().reset_index()
df4 = df[(df["quantity"] >= 3) & (df["order_status"]== "Completed")].groupby("category")["unit_price"].min().reset_index()
df5 = df1.merge(df2,on="category").merge(df3,on="category").merge(df4,on="category")
print(df5)

PS C:\Users\hp\Downloads\sql_practice(0)> & C:\Users\hp\AppData\Local\Programs\Python\Python313\python.exe "c:/Users/hp/Downloads/sql_practice(0)/test2.py"
         category  order_status  quantity  unit_price_x  unit_price_y
0           Books             7        28        284.36         38.81
1        Clothing             6        27        226.42         29.71
2     Electronics             6        24        226.77         80.72
3  Home & Kitchen             8        31        295.43         88.57
4          Sports             6        28        252.07         33.78
PS C:\Users\hp\Downloads\sql_practice(0)> 
```
