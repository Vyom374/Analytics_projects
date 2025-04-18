# ☕️ Monday Coffee Expansion Project

---

## 🌍 Overview

**Monday Coffee** is a digital-first coffee retailer that began operations in January 2023. As its popularity has grown online, the brand is now exploring opportunities to open physical coffee shop locations in high-demand areas across India. This data-driven SQL project aims to analyze customer behavior, sales performance, and city-level demographics to recommend the top 3 cities for expansion.

---

## 🔧 Problem Statement

Monday Coffee, having operated online since January 2023, is planning to expand its physical store presence. The goal is to:

- Identify cities with the highest coffee consumption potential.
- Analyze real sales and customer data.
- Evaluate profitability by comparing revenue with rent.

---

## 🌎 Dataset Structure

The analysis is based on the following tables:

### `city`
| Column Name       | Description                          |
|-------------------|--------------------------------------|
| `city_id`         | Unique identifier for city           |
| `city_name`       | Name of the city                     |
| `population`      | Total city population                |
| `estimated_rent`  | Monthly rent estimate for a location |

### `customers`
| Column Name       | Description                          |
|-------------------|--------------------------------------|
| `customer_id`     | Unique identifier for customer       |
| `customer_name`   | Customer's full name                 |
| `city_id`         | City where the customer is located   |

### `products`
| Column Name       | Description                          |
|-------------------|--------------------------------------|
| `product_id`      | Unique identifier for product        |
| `product_name`    | Name of the product                  |

### `sales`
| Column Name       | Description                          |
|-------------------|--------------------------------------|
| `sale_id`         | Unique identifier for sale           |
| `product_id`      | Product purchased                    |
| `customer_id`     | Customer who made the purchase       |
| `sale_date`       | Date of the sale                     |
| `total`           | Total transaction value              |
---

## 📊 Key Analyses & SQL Queries

### 1. Coffee Consumers Estimate
```sql
SELECT city_name, ROUND((population * 0.25)/100000, 2) AS Coffee_drinkers_in_lakhs
FROM city
ORDER BY Coffee_drinkers_in_lakhs DESC;
```
**Insight:** Delhi has the highest estimated number of coffee consumers, followed by Mumbai and Kolkata.

---

### 2. Monday Coffee Customers by City
```sql
SELECT city_name AS city, COUNT(DISTINCT customer_name) AS customer_count
FROM sales s
JOIN customers c USING(customer_id)
JOIN city ct USING(city_id)
GROUP BY city_name
ORDER BY customer_count DESC;
```
**Insight:** Bangalore, Chennai, and Pune have the most customers ordering Monday Coffee.

---

### 3. Revenue in Q4 2023
```sql
SELECT EXTRACT(YEAR FROM sale_date) AS Year,
       EXTRACT(QUARTER FROM sale_date) AS Quarter,
       city_name,
       SUM(total) AS revenue
FROM sales s
JOIN customers cu USING(customer_id)
JOIN city ct USING(city_id)
WHERE EXTRACT(YEAR FROM sale_date) = 2023 AND EXTRACT(QUARTER FROM sale_date) = 4
GROUP BY Year, Quarter, city_name
ORDER BY revenue DESC;
```
**Insight:** Pune leads in Q4 2023 revenue followed by Chennai and Bangalore.

---

### 4. Total 2023 Revenue by City
```sql
SELECT EXTRACT(YEAR FROM sale_date) AS Year,
       city_name,
       SUM(total) AS revenue
FROM sales s
JOIN customers cu USING(customer_id)
JOIN city ct USING(city_id)
WHERE EXTRACT(YEAR FROM sale_date) = 2023
GROUP BY Year, city_name
ORDER BY revenue DESC;
```
**Insight:** Pune again tops total revenue for the entire year.

---

### 5. Product Sales Volume
```sql
SELECT p.product_name, COUNT(*) AS Units_sold
FROM products p
LEFT JOIN sales s ON s.product_id = p.product_id
GROUP BY product_name
ORDER BY Units_sold DESC;
```
**Insight:** Cold Brew Coffee Pack (6 Bottles) is the most sold product.

---

### 6. Average Sales per Customer
```sql
SELECT ci.city_name,
       SUM(s.total) AS total_revenue,
       COUNT(DISTINCT s.customer_id) AS total_cust,
       ROUND(SUM(s.total)/COUNT(DISTINCT s.customer_id), 2) AS avg_sale_per_customer
FROM sales s
JOIN customers c ON s.customer_id = c.customer_id
JOIN city ci ON ci.city_id = c.city_id
WHERE EXTRACT(YEAR FROM sale_date) = 2023
GROUP BY ci.city_name
ORDER BY total_revenue DESC;
```
**Insight:** Pune shows high average sales per customer, signaling strong loyalty and buying power.

---

### 7. Top 3 Products per City
```sql
WITH cte AS (
    SELECT city_name, product_name, COUNT(*) AS total_units
    FROM products p
    LEFT JOIN sales s ON s.product_id = p.product_id
    JOIN customers cu USING(customer_id)
    JOIN city ci USING(city_id)
    GROUP BY city_name, product_name
),
cte2 AS (
    SELECT *, ROW_NUMBER() OVER(PARTITION BY city_name ORDER BY total_units DESC) AS rn
    FROM cte
)
SELECT city_name, product_name, total_units
FROM cte2
WHERE rn <= 3;
```
**Insight:** Product preferences vary city-by-city and can be used to stock stores strategically.

---

### 8. Revenue vs Rent (Profitability)
```sql
WITH city_rev AS (
    SELECT ci.city_name, SUM(s.total) AS revenue
    FROM sales s
    JOIN customers cu USING(customer_id)
    JOIN city ci USING(city_id)
    WHERE YEAR(sale_date) = 2023
    GROUP BY city_name
),
rent AS (
    SELECT city_name, estimated_rent * 12 AS yearly_rent FROM city
)
SELECT cr.city_name, revenue, yearly_rent, revenue - yearly_rent AS Profit
FROM city_rev cr
JOIN rent r USING(city_name)
ORDER BY Profit DESC;
```
**Insight:** Pune, Jaipur, and Chennai are the most profitable cities after accounting for rent.

---

### 9. Monthly Sales Growth for 2023
```sql
SELECT DATE_FORMAT(sale_date, '%Y-%m') AS month,
       SUM(total) AS monthly_sales,
       ROUND(SUM(total) - LAG(SUM(total)) OVER(ORDER BY DATE_FORMAT(sale_date, '%Y-%m')), 2) AS change,
       ROUND(((SUM(total) - LAG(SUM(total)) OVER(ORDER BY DATE_FORMAT(sale_date, '%Y-%m')))/LAG(SUM(total)) OVER(ORDER BY DATE_FORMAT(sale_date, '%Y-%m')))*100, 2) AS growth_rate
FROM sales
WHERE YEAR(sale_date) = 2023
GROUP BY month
ORDER BY month;
```
**Insight:** Monthly trends help forecast future store performance and plan marketing campaigns.

---

## 🌟 Recommended Cities for Expansion

Based on the analysis:

1. **Pune**
   - Highest total revenue of 8.5 Lakhs in the year 2023. 
   - Highest Profit of 6.7 Lakhs in the year 2023. 
   - Very Low annual rent (1.8 Lakh).

2. **Delhi**
   - Highest estimated coffee consumers (77.5 Lakhs).
   - Highest customer count (68).
   - Potential for improvement in revenue and profit.

3. **Jaipur**
   - High customer base (69).
   - Low annual rent (1.2 Lakh).
   - Profit in 2023: ₹380,683 and Revenue of 5.1 Lakhs.




## 🔮 Final Conclusion

- **Pune** is the most strategic location with the highest profit and solid average sales.
- **Delhi** brings large untapped market potential due to its large population of coffee drinkers.
- **Jaipur** offers high profitability and low rent with a strong customer base.

This project showcases the power of SQL in strategic decision-making.

---

## 🏆 Tools Used
- SQL (MySQL)
- Excel/CSV for data input
- GitHub for project documentation
