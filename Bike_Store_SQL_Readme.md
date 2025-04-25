
# 🏋️ Bike Store SQL Analysis Project

## 📖 Project Overview
This project involves performing exploratory data analysis on a sample retail database called **Bike Store** from Kaggle, which contains transactional and customer information. The analysis is done using SQL in **pgAdmin** (PostgreSQL), and insights are aimed to be later visualized in Power BI.

The project includes:
- Data cleaning (ensuring consistency, integrity, and referential constraints)
- Exploratory SQL queries
- Insight extraction

---

## 📊 Dataset Structure
The database contains **9 tables**:
- **customers**
- **orders**
- **order_items**
- **products**
- **categories**
- **brands**
- **staffs**
- **stores**
- **stocks**

---

## ✍️ Exploratory SQL Queries and Insights

### 1. 💼 Total Revenue Generated
```sql
SELECT SUM(quantity * list_price * (1 - discount)) AS total_revenue
FROM order_items;
```
**Insight**: The total revenue provides a macro-level view of all sales. In this case, the store generated **76,891,116.56**, which is useful for profitability analysis.

---

### 2. 🏢 Revenue by Store
```sql
SELECT s.store_id, s.store_name,
       SUM(oi.quantity * oi.list_price * (1 - oi.discount)) AS store_revenue
FROM order_items oi
JOIN orders o ON oi.order_id = o.order_id
JOIN stores s ON o.store_id = s.store_id
GROUP BY s.store_id, s.store_name
ORDER BY store_revenue DESC;
```
**Insight**: Shows which store locations are most profitable. Helps in strategic decisions like scaling high-performing stores and improving low-performing ones.

---

### 3. 📦 Top 5 Selling Products (by Quantity)
```sql
SELECT p.product_name, SUM(oi.quantity) AS total_sold
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_sold DESC
LIMIT 5;
```
**Insight**: Highlights customer demand. Helps in inventory management and promotional focus.

---

### 4. 👥 Number of Orders by Customer
```sql
SELECT c.first_name || ' ' || c.last_name AS customer_name, COUNT(o.order_id) AS total_orders
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY customer_name
ORDER BY total_orders DESC
LIMIT 5;
```
**Insight**: Identifies high-value customers. Useful for targeted marketing or loyalty programs.

---

### 5. 🗓️ Monthly Revenue Trend
```sql
SELECT DATE_TRUNC('month', o.order_date) AS month,
       SUM(oi.quantity * oi.list_price * (1 - oi.discount)) AS monthly_revenue
FROM orders o
JOIN order_items oi ON o.order_id = oi.order_id
GROUP BY month
ORDER BY month;
```
**Insight**: Detects sales trends across months. Supports seasonal campaign planning and inventory stocking.

---

## 🎯 Next Steps
- Build a **Power BI dashboard** using these queries
- Deploy on GitHub and document

---

## ✅ Status
**Completed:** Data import, cleaning, and exploratory SQL queries.  
**Next Phase:** Power BI Dashboard creation.
