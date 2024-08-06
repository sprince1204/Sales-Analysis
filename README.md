# Pizza Sales Analysis

This project involves analyzing pizza sales data using SQL. The analysis is divided into three categories: Basic, Intermediate, and Advanced. Each category addresses specific questions related to sales, revenue, and customer preferences.

## Table of Contents
- [Project Description](#project-description)
- [Basic Analysis](#basic-analysis)
- [Intermediate Analysis](#intermediate-analysis)
- [Advanced Analysis](#advanced-analysis)
- [Technologies Used](#technologies-used)
- [Setup and Installation](#setup-and-installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Project Description

The goal of this project is to analyze pizza sales data to gain insights into customer preferences, sales performance, and revenue distribution. The analysis is performed using SQL queries, and the results are used for inventory management, resource allocation, and sales strategy development.

## Basic Analysis

1. **Total Number of Orders Placed**
    ```sql
    SELECT COUNT(*) AS total_orders FROM orders;
    ```

2. **Total Revenue Generated from Pizza Sales**
    ```sql
    SELECT SUM(price) AS total_revenue FROM sales;
    ```

3. **Highest-Priced Pizza**
    ```sql
    SELECT name, MAX(price) AS highest_price FROM pizzas;
    ```

4. **Most Common Pizza Size Ordered**
    ```sql
    SELECT size, COUNT(*) AS order_count 
    FROM orders 
    GROUP BY size 
    ORDER BY order_count DESC 
    LIMIT 1;
    ```

5. **Top 5 Most Ordered Pizza Types**
    ```sql
    SELECT pizza_type, COUNT(*) AS quantity 
    FROM orders 
    GROUP BY pizza_type 
    ORDER BY quantity DESC 
    LIMIT 5;
    ```

## Intermediate Analysis

1. **Total Quantity of Each Pizza Category Ordered**
    ```sql
    SELECT category, SUM(quantity) AS total_quantity 
    FROM pizzas 
    JOIN orders ON pizzas.id = orders.pizza_id 
    GROUP BY category;
    ```

2. **Distribution of Orders by Hour of the Day**
    ```sql
    SELECT HOUR(order_time) AS order_hour, COUNT(*) AS order_count 
    FROM orders 
    GROUP BY order_hour 
    ORDER BY order_count DESC;
    ```

3. **Category-Wise Distribution of Pizzas**
    ```sql
    SELECT category, COUNT(*) AS order_count 
    FROM pizzas 
    JOIN orders ON pizzas.id = orders.pizza_id 
    GROUP BY category;
    ```

4. **Average Number of Pizzas Ordered Per Day**
    ```sql
    SELECT order_date, AVG(quantity) AS avg_quantity 
    FROM orders 
    GROUP BY order_date;
    ```

5. **Top 3 Most Ordered Pizza Types Based on Revenue**
    ```sql
    SELECT pizza_type, SUM(price) AS total_revenue 
    FROM orders 
    JOIN pizzas ON orders.pizza_id = pizzas.id 
    GROUP BY pizza_type 
    ORDER BY total_revenue DESC 
    LIMIT 3;
    ```

## Advanced Analysis

1. **Percentage Contribution of Each Pizza Type to Total Revenue**
    ```sql
    SELECT pizza_type, 
           SUM(price) * 100.0 / (SELECT SUM(price) FROM sales) AS revenue_percentage 
    FROM orders 
    JOIN pizzas ON orders.pizza_id = pizzas.id 
    GROUP BY pizza_type;
    ```

2. **Cumulative Revenue Generated Over Time**
    ```sql
    SELECT order_date, 
           SUM(price) OVER (ORDER BY order_date) AS cumulative_revenue 
    FROM orders 
    JOIN pizzas ON orders.pizza_id = pizzas.id;
    ```

3. **Top 3 Most Ordered Pizza Types Based on Revenue for Each Pizza Category**
    ```sql
    SELECT category, pizza_type, SUM(price) AS total_revenue 
    FROM orders 
    JOIN pizzas ON orders.pizza_id = pizzas.id 
    GROUP BY category, pizza_type 
    ORDER BY category, total_revenue DESC 
    LIMIT 3;
    ```

## Technologies Used
- SQL
- Database Management System (DBMS)
