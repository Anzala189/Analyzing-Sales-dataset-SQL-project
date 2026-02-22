# Find out how much Wholesale net revenue each product_line generated per month per warehouse in the dataset.
## The query should be saved as revenue_by_product_line using the SQL cell provided, and contain the following: product_line,month: displayed as 'June', 'July', and 'August', warehouse, and net_revenue: the sum of total minus the sum of payment_fee. The results should be sorted by product_line and month, followed by net_revenue in descending order.

You're working for a company that sells motorcycle parts, and they've asked for some help in analyzing their sales data!

They operate three warehouses in the area, selling both retail and wholesale. They offer a variety of parts and accept credit cards, cash, and bank transfer as payment methods. However, each payment type incurs a different fee.

The board of directors wants to gain a better understanding of wholesale revenue by product line, and how this varies month-to-month and across warehouses. You have been tasked with calculating net revenue for each product line and grouping results by month and warehouse. The results should be filtered so that only `"Wholesale"` orders are included.


![image](https://github.com/Anzala189/Analyzing-Sales-dataset-SQL-project/blob/ded5e4ea4a51f366e9fe76bbe51190893b0c90f0/motorcycle.jpg)

They have provided you with access to their database, which contains the following table called `sales`:

## Sales
| Column | Data type | Description |
|--------|-----------|-------------|
| `order_number` | `VARCHAR` | Unique order number. |
| `date` | `DATE` | Date of the order, from June to August 2021. |
| `warehouse` | `VARCHAR` | The warehouse that the order was made from&mdash; `North`, `Central`, or `West`. |
| `client_type` | `VARCHAR` | Whether the order was `Retail` or `Wholesale`. |
| `product_line` | `VARCHAR` | Type of product ordered. |
| `quantity` | `INT` | Number of products ordered. | 
| `unit_price` | `FLOAT` | Price per product (dollars). |
| `total` | `FLOAT` | Total price of the order (dollars). |
| `payment` | `VARCHAR` | Payment method&mdash;`Credit card`, `Transfer`, or `Cash`. |
| `payment_fee` | `FLOAT` | Percentage of `total` charged as a result of the `payment` method. |


Your query output should be presented in the following format:

| `product_line` | `month` | `warehouse` |	`net_revenue` |
|----------------|-----------|----------------------------|--------------|
| product_one | --- | --- | --- |
| product_one | --- | --- | --- |
| product_one | --- | --- | --- |
| product_one | --- | --- | --- |
| product_one | --- | --- | --- |
| product_one | --- | --- | --- |
| product_two | --- | --- | --- |
| ... | ... | ... | ... |


# SOLUTION

```sql
SELECT product_line,
    CASE WHEN EXTRACT('month' from date) = 6 THEN 'June'
        WHEN EXTRACT('month' from date) = 7 THEN 'July'
        WHEN EXTRACT('month' from date) = 8 THEN 'August'
    END as month,
    warehouse,
	SUM(total) - SUM(payment_fee) AS net_revenue
FROM sales
WHERE client_type = 'Wholesale'
GROUP BY product_line, warehouse, month
ORDER BY product_line, month, net_revenue DESC
```

## Output:

| index | product_line           | month  | warehouse | net_revenue |
|-------|------------------------|--------|-----------|------------|
| 0  | Braking system         | August | Central   | 3039.41 |
| 1  | Braking system         | August | West      | 2500.67 |
| 2  | Braking system         | August | North     | 1770.84 |
| 3  | Braking system         | July   | Central   | 3778.65 |
| 4  | Braking system         | July   | West      | 3060.93 |
| 5  | Braking system         | July   | North     | 2594.44 |
| 6  | Braking system         | June   | Central   | 3684.89 |
| 7  | Braking system         | June   | North     | 1487.77 |
| 8  | Braking system         | June   | West      | 1212.75 |
| 9  | Electrical system      | August | North     | 4721.12 |
| 10 | Electrical system      | August | Central   | 3126.43 |
| 11 | Electrical system      | August | West      | 1241.84 |
| 12 | Electrical system      | July   | Central   | 5577.62 |
| 13 | Electrical system      | July   | North     | 1710.13 |
| 14 | Electrical system      | July   | West      | 449.46  |
| 15 | Electrical system      | June   | Central   | 2904.93 |
| 16 | Electrical system      | June   | North     | 2022.50 |
| 17 | Engine                 | August | Central   | 9528.71 |
| 18 | Engine                 | August | North     | 2324.19 |
| 19 | Engine                 | July   | Central   | 1827.03 |
| 20 | Engine                 | July   | North     | 1007.14 |
| 21 | Engine                 | June   | Central   | 6548.85 |
| 22 | Frame & body           | August | Central   | 8657.99 |
| 23 | Frame & body           | August | North     | 7898.89 |
| 24 | Frame & body           | August | West      | 829.69  |
| 25 | Frame & body           | July   | North     | 6154.61 |
| 26 | Frame & body           | July   | Central   | 3135.13 |
| 27 | Frame & body           | June   | Central   | 5111.34 |
| 28 | Frame & body           | June   | North     | 4910.12 |
| 29 | Frame & body           | June   | West      | 2779.74 |
| 30 | Miscellaneous          | August | North     | 1841.40 |
| 31 | Miscellaneous          | August | Central   | 1739.76 |
| 32 | Miscellaneous          | August | West      | 813.43  |
| 33 | Miscellaneous          | July   | Central   | 3118.44 |
| 34 | Miscellaneous          | July   | North     | 2404.65 |
| 35 | Miscellaneous          | July   | West      | 1156.80 |
| 36 | Miscellaneous          | June   | West      | 2280.97 |
| 37 | Miscellaneous          | June   | Central   | 1878.07 |
| 38 | Miscellaneous          | June   | North     | 513.99  |
| 39 | Suspension & traction  | August | Central   | 5416.70 |
| 40 | Suspension & traction  | August | North     | 4923.69 |
| 41 | Suspension & traction  | August | West      | 1080.79 |
| 42 | Suspension & traction  | July   | Central   | 6456.72 |
| 43 | Suspension & traction  | July   | North     | 3714.28 |
| 44 | Suspension & traction  | July   | West      | 2939.32 |
| 45 | Suspension & traction  | June   | North     | 8065.74 |
| 46 | Suspension & traction  | June   | Central   | 3325.00 |
| 47 | Suspension & traction  | June   | West      | 2372.52 |









