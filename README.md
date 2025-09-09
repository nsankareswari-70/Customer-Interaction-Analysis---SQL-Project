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

```sql
-- ================================
-- Sample Data
-- ================================

-- Customers
INSERT INTO customers (name, email, phone) VALUES
('Alice Johnson', 'alice@example.com', '555-111-2222'),
('Bob Smith', 'bob@example.com', '555-222-3333'),
('Charlie Lee', 'charlie@example.com', '555-333-4444'),
('Diana Perez', 'diana@example.com', '555-444-5555'),
('Ethan Brown', 'ethan@example.com', '555-555-6666'),
('Fiona Adams', 'fiona@example.com', '555-666-7777'),
('George King', 'george@example.com', '555-777-8888'),
('Hannah Davis', 'hannah@example.com', '555-888-9999');

-- Interactions (~50 rows)
INSERT INTO interactions (customer_id, channel, message_text, sentiment, created_at) VALUES
(1,'chat','I can’t log in to my account','negative','2025-09-01 09:15:00'),
(2,'email','Thanks for resolving my issue quickly','positive','2025-09-01 10:05:00'),
(3,'sms','When will my order arrive?','neutral','2025-09-02 14:20:00'),
(1,'chat','Still waiting on password reset link','negative','2025-09-02 15:10:00'),
(2,'email','Great support, very happy!','positive','2025-09-03 11:30:00'),
(4,'sms','My payment didn’t go through','negative','2025-09-03 16:00:00'),
(5,'chat','Do you ship internationally?','neutral','2025-09-04 09:45:00'),
(6,'email','Order arrived damaged','negative','2025-09-04 12:10:00'),
(7,'chat','Your support was excellent','positive','2025-09-05 13:25:00'),
(8,'sms','I want to cancel my subscription','negative','2025-09-05 14:00:00'),
(1,'email','Password reset finally worked','positive','2025-09-06 08:30:00'),
(2,'chat','Can I change my delivery address?','neutral','2025-09-06 09:20:00'),
(3,'email','Thank you for the prompt response','positive','2025-09-06 10:15:00'),
(4,'chat','My payment keeps failing','negative','2025-09-06 11:40:00'),
(5,'sms','When will product X be restocked?','neutral','2025-09-07 12:25:00'),
(6,'chat','This is the best service ever','positive','2025-09-07 13:50:00'),
(7,'email','Shipping delay is unacceptable','negative','2025-09-07 14:30:00'),
(8,'chat','Cancel my subscription now','negative','2025-09-08 09:10:00'),
(1,'sms','Login issue resolved quickly','positive','2025-09-08 10:00:00'),
(2,'email','Support was helpful','positive','2025-09-08 11:15:00'),
(3,'chat','Order hasn’t shipped yet','negative','2025-09-08 12:40:00'),
(4,'sms','Payment issue fixed, thanks','positive','2025-09-09 13:55:00'),
(5,'email','Please update me on my order','neutral','2025-09-09 15:05:00'),
(6,'chat','Product arrived on time','positive','2025-09-09 16:30:00'),
(7,'sms','Support ignored my request','negative','2025-09-09 17:45:00'),
(8,'email','I am happy with my subscription','positive','2025-09-10 09:10:00'),
(1,'chat','Forgot password again','negative','2025-09-10 10:30:00'),
(2,'sms','Order delayed another week?','negative','2025-09-10 11:50:00'),
(3,'email','Good communication from support','positive','2025-09-10 13:05:00'),
(4,'chat','Still can’t pay with my card','negative','2025-09-11 14:20:00'),
(5,'sms','When will I get a tracking number?','neutral','2025-09-11 15:45:00'),
(6,'chat','Very happy with your service','positive','2025-09-11 17:00:00'),
(7,'email','Shipping took too long','negative','2025-09-12 09:15:00'),
(8,'sms','Cancel process was smooth','positive','2025-09-12 10:30:00'),
(1,'chat','Login fixed, thank you','positive','2025-09-12 12:05:00'),
(2,'email','I appreciate the fast response','positive','2025-09-12 13:25:00'),
(3,'chat','Order not updated in system','negative','2025-09-12 14:40:00'),
(4,'sms','Payment gateway error again','negative','2025-09-13 09:55:00'),
(5,'chat','Will product X be available soon?','neutral','2025-09-13 11:10:00'),
(6,'email','Package came earlier than expected','positive','2025-09-13 12:20:00'),
(7,'chat','I need better support','negative','2025-09-13 13:45:00'),
(8,'sms','Subscription service is great','positive','2025-09-14 09:30:00'),
(1,'email','Still having login issues','negative','2025-09-14 10:40:00'),
(2,'chat','Delivery address updated successfully','positive','2025-09-14 12:00:00'),
(3,'sms','Order finally shipped','positive','2025-09-14 13:10:00'),
(4,'email','Thanks for fixing payment','positive','2025-09-14 14:25:00'),
(5,'chat','Can you notify me about restock?','neutral','2025-09-15 09:15:00'),
(6,'sms','Customer service was very friendly','positive','2025-09-15 10:20:00'),
(7,'chat','Still no reply from support','negative','2025-09-15 11:30:00'),
(8,'email','I love my subscription','positive','2025-09-15 12:45:00');

-- Tags (linking to interactions)
INSERT INTO interaction_tags (interaction_id, tag) VALUES
(1,'login'),(4,'login'),(11,'login'),(19,'login'),(27,'login'),(35,'login'),(43,'login'),
(3,'order'),(15,'order'),(21,'order'),(23,'order'),(29,'order'),(37,'order'),(45,'order'),
(6,'payment'),(14,'payment'),(22,'payment'),(30,'payment'),(38,'payment'),
(7,'shipping'),(17,'shipping'),(25,'shipping'),(31,'shipping'),(39,'shipping'),
(8,'support'),(16,'support'),(24,'support'),(32,'support'),(40,'support'),(48,'support'),
(10,'subscription'),(18,'subscription'),(26,'subscription'),(34,'subscription'),(42,'subscription'),(50,'subscription');
```
```sql
-- View all the customers and their Details
select * from customers;
```
![img alt](https://github.com/nsankareswari-70/Customer-Interaction-Analysis---SQL-Project/blob/bb6c3fc8bc3cc8bae0dc16c0695608b0b1940cc1/cia1.png)

```sql
-- Get the details of the customer 'Ethan Brown'?
```
![img alt](https://github.com/nsankareswari-70/Customer-Interaction-Analysis---SQL-Project/blob/26ec58390257a77ba0b556f5bd1e174e5390e4b7/cia2.png)

```sql
-- Find whose telephone number is 555-222-3333
```
![img alt](https://github.com/nsankareswari-70/Customer-Interaction-Analysis---SQL-Project/blob/12ce4d7713a1b1036195154b363bac2582685358/Cia3.png)

```sql
-- Creating a view to split and store the customer Firstname and the lastname.
create view customer_names as
select 
substring_index(name," ",1) as firstname,
substring_index(name," ",-1) as lastname 
from customers;

select * from customer_names;
```
![img alt](https://github.com/nsankareswari-70/Customer-Interaction-Analysis---SQL-Project/blob/8d30cf5b19cbb22c95e9c2e88ab7f42b11a177c9/cia4.png)

``` sql
From the interactions table, I want to see all the positive reviews
select * from interactions where sentiment='Positive';
```

