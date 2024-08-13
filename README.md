-- Retrieve the total number of orders placed.
select count(*) as Total_Order_Placed from orders;

-- Calculate the total revenue generated from pizza sales.
SELECT 
    ROUND(SUM(od.quantity * p.price), 2) AS total_revenue
FROM
    order_details AS od
        JOIN
    pizzas AS p ON p.pizza_id = od.pizza_id;

-- Identify the highest-priced pizza.
SELECT 
    pt.name, p.price
FROM
    pizzas AS p
        JOIN
    pizza_types AS pt ON pt.pizza_type_id = p.pizza_type_id
GROUP BY pt.name , p.price
ORDER BY p.price DESC
LIMIT 1;

-- Identify the most common pizza size ordered.
SELECT 
    p.size, COUNT(quantity) AS total_qty
FROM
    pizzas AS p
        JOIN
    order_details AS od ON p.pizza_id = od.pizza_id
GROUP BY p.size
ORDER BY total_qty DESC;

-- List the top 5 most ordered pizza types along with their quantities.
SELECT 
    pt.name, SUM(od.quantity) AS top_ordered
FROM
    pizzas AS p
        JOIN
    order_details AS od ON p.pizza_id = od.pizza_id
        JOIN
    pizza_types AS pt ON pt.pizza_type_id = p.pizza_type_id
GROUP BY pt.name
ORDER BY top_ordered DESC
LIMIT 5;

-- Join the necessary tables to find the total quantity of each pizza category ordered.
SELECT 
    pt.category, SUM(od.quantity) AS top_ordered
FROM
    pizzas AS p
        JOIN
    order_details AS od ON p.pizza_id = od.pizza_id
        JOIN
    pizza_types AS pt ON pt.pizza_type_id = p.pizza_type_id
GROUP BY pt.category
ORDER BY top_ordered DESC;

-- Determine the distribution of orders by hour of the day.
SELECT 
    HOUR(time_) AS hour, COUNT(order_id) AS order_count
FROM
    orders
GROUP BY HOUR(time_);

-- Join relevant tables to find the category-wise distribution of pizzas.
SELECT 
    category, COUNT(name)
FROM
    pizza_types
GROUP BY category;

-- Group the orders by date and calculate the average number of pizzas ordered per day.
SELECT 
    ROUND(AVG(quantity_), 0) AS avg_pizza_ordered_per_day
FROM
    (SELECT 
        o.date_, SUM(od.quantity) AS quantity_
    FROM
        orders AS o
    JOIN order_details AS od ON o.order_id = od.order_id
    GROUP BY o.date_) AS order_qty;

-- Determine the top 3 most ordered pizza types based on revenue.
SELECT 
    pt.name,
    ROUND(SUM(od.quantity * p.price), 2) AS total_revenue
FROM
    pizzas AS p
        JOIN
    order_details AS od ON p.pizza_id = od.pizza_id
        JOIN
    pizza_types AS pt ON pt.pizza_type_id = p.pizza_type_id
GROUP BY pt.name
ORDER BY total_revenue DESC
LIMIT 3;
