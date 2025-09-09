# Customer-Interaction-Analysis---SQL-Project

## Creating the Database
```sql
DROP DATABASE IF EXISTS customer_interactions;
CREATE DATABASE customer_interactions;
USE customer_interactions;
```
```sql
-- Customers
CREATE TABLE customers (
    customer_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(150),
    phone VARCHAR(20)
);

-- Interactions
CREATE TABLE interactions (
    interaction_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT,
    channel ENUM('chat','sms','email'),
    message_text TEXT,
    sentiment ENUM('positive','neutral','negative'),
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

-- Tags
CREATE TABLE interaction_tags (
    tag_id INT AUTO_INCREMENT PRIMARY KEY,
    interaction_id INT,
    tag VARCHAR(50),
    FOREIGN KEY (interaction_id) REFERENCES interactions(interaction_id)
);
```


