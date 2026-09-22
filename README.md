# E-Commerce Delivery & Sales Analysis
### Power BI | MySQL | DAX | Statistics

---

## Problem Statement

An E-Commerce company was experiencing
declining customer satisfaction and
increasing late deliveries.

Leadership needed answers:
- Why are deliveries late?
- Which products perform best?
- What is the revenue trend?
- How can we improve ratings?

---

## Dataset

| Detail | Info |
|--------|------|
| Source | Kaggle |
| Rows | 50,000+ |
| Columns | 15+ |
| Period | 2022–2026 |
| Domain | E-Commerce |

**Key columns:**
order_id, order_date,
customer_city, product_category,
sales, shipping_cost,
delivery_days, customer_rating,
payment_method, order_status

---

## Tools Used

| Tool | Purpose |
|------|---------|
| MySQL | Data cleaning + SQL queries |
| Power BI Desktop | Dashboard & visualization |
| DAX | Measures & calculations |
| Excel | Statistical analysis |

---

## Data Cleaning (MySQL)

Issues found and fixed:

- ✅ Duplicate order IDs removed
- ✅ NULL values handled
- ✅ Negative values corrected
- ✅ Mixed date formats standardized
- ✅ Inconsistent text standardized
- ✅ Invalid phone/email flagged
- ✅ Outlier values investigated

```sql
-- Example: Duplicates removed
DELETE t1 FROM orders t1
INNER JOIN orders t2
WHERE t1.order_id = t2.order_id
AND t1.id > t2.id;

-- Example: Category standardized
UPDATE orders
SET product_category =
  UPPER(TRIM(product_category));
```

---

## Dashboard — 4 Pages

### Page 1 — Executive Summary
- Total Sales: 2M
- Shipping Cost: 483.85K
- Promise Days: 7.14
- Actual Delivery: 8.24
- Avg Rating: 3.38
- Delay: 1.24 days
- Map visual — global distribution
- Payment method breakdown
- Order status pie chart
- Month slicer

### Page 2 — Deep Analysis by Month
- Sales by Quarter trend
- Shipping cost by Quarter
- Return reasons breakdown
- Package size distribution
- Rating by customer segment
- Category slicer

### Page 3 — Delivery Insights
- Average hours by warehouse
- Distance vs Delivery days
  (Scatter chart)
- Late delivery: 40.1%!
- Orders by carrier
- Order priority analysis
- Quarter slicer

### Page 4 — Insights & Recommendations
- Written story for stakeholders
- Root cause explanation
- Action plan

---

## Key DAX Measures

```dax
Total Sales =
SUM(orders[sales_amount])

Avg Delivery Days =
AVERAGE(orders[actual_delivery_days])

Late Delivery % =
DIVIDE(
  COUNTROWS(
    FILTER(orders,
      orders[delivery_status]="Late")
  ),
  COUNTROWS(orders)
)

Delay Gap =
[Avg Delivery Days] -
[Avg Promise Days]
```

---

## Key Findings

### 🚨 Finding 1 — Late Delivery Crisis
