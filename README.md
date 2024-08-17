Pizza Sales Database Analysis:

    This repository contains SQL queries designed to analyze a pizza sales database. The queries retrieve important business metrics
    such as total orders, revenue, most popular pizza types, and time-based ordering patterns.

Database Structure

    The analysis assumes a database with the following structure:

    orders: Stores order details such as order ID, date, and time.

    order_details: Contains information about individual pizzas in each order, including quantity.

    pizzas: Contains pizza-specific data such as pizza ID, type, and price.

    pizza_types: Stores types and categories of pizzas.


Relationships:

    orders (1) ↔ (N) order_details

    pizzas (1) ↔ (N) order_details

    pizza_types (1) ↔ (N) pizzas
