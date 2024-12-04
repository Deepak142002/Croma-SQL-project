# Croma-SQL-project
## Project Overview

This project is designed to demonstrate how to manage and analyze an e-commerce platform's data using a relational database. The database includes tables for customers, products, sales, stores, and categories. The project features SQL queries for data retrieval, aggregation, analysis, and data cleansing, all aimed at extracting meaningful insights to support business decision-making.

---

## Database Schema

### **Customers Table**
Stores customer details, including personal information, joining date, and region.

| Column       | Type        | Description                |
|--------------|-------------|----------------------------|
| `customer_id` | INT         | Primary key                |
| `first_name`  | VARCHAR(50) | Customer's first name      |
| `last_name`   | VARCHAR(50) | Customer's last name       |
| `email`       | VARCHAR(100)| Customer's email address   |
| `gender`      | VARCHAR(10) | Customer's gender          |
| `dob`         | DATE        | Customer's date of birth   |
| `join_date`   | DATE        | Date the customer joined   |
| `region`      | VARCHAR(50) | Customer's region          |

### **Products Table**
Stores product details such as name, price, stock quantity, and category.

| Column        | Type        | Description                          |
|---------------|-------------|--------------------------------------|
| `product_id`  | INT         | Primary key                          |
| `product_name`| VARCHAR(100)| Product name                         |
| `category_id` | INT         | Foreign key to Categories table      |
| `price`       | DECIMAL(10,2)| Product price                        |
| `stock_quantity` | INT       | Available stock quantity             |

### **Sales Table**
Records sales transactions, linking customers, products, and stores.

| Column       | Type        | Description                          |
|--------------|-------------|--------------------------------------|
| `sale_id`    | INT         | Primary key                          |
| `customer_id`| INT         | Foreign key to Customers table      |
| `product_id` | INT         | Foreign key to Products table       |
| `store_id`   | INT         | Foreign key to Stores table         |
| `sale_date`  | DATE        | Date of sale                        |
| `quantity_sold`| INT       | Number of items sold                |
| `total_price`| DECIMAL(10,2)| Total price of the transaction      |

### **Stores Table**
Stores information about stores and their managers.

| Column        | Type        | Description                          |
|---------------|-------------|--------------------------------------|
| `store_id`    | INT         | Primary key                          |
| `store_name`  | VARCHAR(100)| Name of the store                    |
| `location`    | VARCHAR(100)| Store location                       |
| `manager_id`  | INT         | Manager responsible for the store    |

### **Categories Table**
Stores product categories (e.g., Electronics, Accessories).

| Column        | Type        | Description                          |
|---------------|-------------|--------------------------------------|
| `category_id` | INT         | Primary key                          |
| `category_name`| VARCHAR(50) | Name of the product category         |

---

## Setting Up the Database

### Step 1: Create Tables

Use the following SQL scripts to create the necessary tables.

```sql
-- Create Customers Table
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    gender VARCHAR(10),
    dob DATE,
    join_date DATE,
    region VARCHAR(50)
);

-- Create Products Table
CREATE TABLE Products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category_id INT,
    price DECIMAL(10, 2),
    stock_quantity INT,
    FOREIGN KEY (category_id) REFERENCES Categories(category_id)
);

-- Create Sales Table
CREATE TABLE Sales (
    sale_id INT PRIMARY KEY,
    customer_id INT,
    product_id INT,
    store_id INT,
    sale_date DATE,
    quantity_sold INT,
    total_price DECIMAL(10, 2),
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id),
    FOREIGN KEY (product_id) REFERENCES Products(product_id),
    FOREIGN KEY (store_id) REFERENCES Stores(store_id)
);

-- Create Stores Table
CREATE TABLE Stores (
    store_id INT PRIMARY KEY,
    store_name VARCHAR(100),
    location VARCHAR(100),
    manager_id INT
);

-- Create Categories Table
CREATE TABLE Categories (
    category_id INT PRIMARY KEY,
    category_name VARCHAR(50)
);
