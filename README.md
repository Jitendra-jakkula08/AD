Here's a step-by-step guide for setting up your database, creating tables, and inserting sample data for your Vehicle Inventory app:

---

### **README for Database Setup**

#### **1. Create the Database**
First, create the database using the following SQL command:
```sql
CREATE DATABASE vehicle_inventory_db;
```
Switch to the newly created database:
```sql
USE vehicle_inventory_db;
```

---

### **2. Create the `users` Table**
Create the table for storing user information:
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    aadharnumber VARCHAR(12),
    pannumber VARCHAR(10)
);
```

---

### **3. Create the `admins` Table**
Create the table for storing admin information:
```sql
CREATE TABLE admins (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL
);
```

---

### **4. Create the `vehicles` Table**
Create the table for storing vehicle information:
```sql
CREATE TABLE vehicles (
    id INT AUTO_INCREMENT PRIMARY KEY,
    make VARCHAR(255),
    model VARCHAR(255),
    year INT,
    price DECIMAL(10,2),
    status VARCHAR(20) DEFAULT 'available',
    description TEXT,
    image_url VARCHAR(255),
    isAvailableForRent BOOLEAN,
    isAvailableForSale BOOLEAN,
    type VARCHAR(50)
);
```

---

### **5. Create the `rent_requests` Table**
Create the table for managing rental requests:
```sql
CREATE TABLE rent_requests (
    request_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    vehicle_id INT,
    request_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(20) DEFAULT 'Pending',
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (vehicle_id) REFERENCES vehicles(id)
);
```

---

### **6. Create the `buy_requests` Table**
Create the table for managing purchase requests:
```sql
CREATE TABLE buy_requests (
    request_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    vehicle_id INT,
    request_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(20) DEFAULT 'Pending',
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (vehicle_id) REFERENCES vehicles(id)
);
```

---

### **7. Create the `sale_requests` Table**
Create the table for managing vehicle sale requests:
```sql
CREATE TABLE sale_requests (
    request_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    vehicle_description TEXT,
    image_url VARCHAR(255),
    status VARCHAR(20) DEFAULT 'Pending',
    request_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    make VARCHAR(255),
    model VARCHAR(255),
    year INT,
    price DECIMAL(10,2),
    type VARCHAR(50),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

---

### **8. Create the `rental_details` Table**
Create the table for storing rental details:
```sql
CREATE TABLE rental_details (
    detail_id INT AUTO_INCREMENT PRIMARY KEY,
    request_id INT,
    username VARCHAR(255),
    rental_duration INT,
    additional_notes TEXT,
    rent_start_date DATE,
    rent_end_date DATE,
    FOREIGN KEY (request_id) REFERENCES rent_requests(request_id)
);
```

---

### **9. Insert Sample Data into `users` Table**
```sql
INSERT INTO users (username, password, email, aadharnumber, pannumber, created_at) VALUES
    ('Jitu', 'password123', 'jitu@gmail.com', '123412341234', 'ABCDE1234F', CURRENT_TIMESTAMP),
    ('Navya', 'password123', 'navya@gmail.com', '234523452345', 'FGHIJ5678K', CURRENT_TIMESTAMP),
    ('Manisha', 'password123', 'manisha@gmail.com', '345634563456', 'KLMNO9012P', CURRENT_TIMESTAMP),
    ('Mrudul', 'password123', 'mrudhul@gmail.com', '456745674567', 'QRSTU3456V', CURRENT_TIMESTAMP);
```

---

### **10. Insert Sample Data into `vehicles` Table**
```sql
INSERT INTO vehicles (make, model, year, price, status, description, image_url, isAvailableForRent, isAvailableForSale, type) VALUES
    ('Toyota', 'Corolla', 2018, 15000.00, 'available', 'A reliable pre-owned sedan.', '/images/toyota_corolla.jpg', 1, 1, 'Sedan'),
    ('Honda', 'Civic', 2020, 18000.00, 'available', 'Compact car with great fuel economy.', '/images/honda_civic.jpg', 0, 1, 'Compact'),
    ('Ford', 'Explorer', 2019, 25000.00, 'available', 'Spacious SUV, perfect for families.', '/images/ford_explorer.jpg', 1, 1, 'SUV');
```

---

### **11. Insert Sample Data into `rent_requests` Table**
```sql
INSERT INTO rent_requests (user_id, vehicle_id, request_date, status) VALUES
    (1, 1, NOW(), 'Pending'),
    (2, 2, NOW(), 'Approved'),
    (3, 3, NOW(), 'Pending');
```

---

### **12. Insert Sample Data into `buy_requests` Table**
```sql
INSERT INTO buy_requests (user_id, vehicle_id, request_date, status) VALUES
    (1, 1, NOW(), 'pending'),
    (2, 2, NOW(), 'approved'),
    (3, 3, NOW(), 'pending');
```

---

### **13. Insert Sample Data into `sale_requests` Table**
```sql
INSERT INTO sale_requests (user_id, vehicle_description, image_url, status, make, model, year, price, type) VALUES
    (2, 'Selling my KTM Duke 390, in excellent condition.', 'url/to/image12.jpg', 'pending', 'KTM', 'Duke 390', 2022, 7000.00, 'bike'),
    (3, 'Selling my Royal Enfield Classic 350, a classic bike.', 'url/to/image15.jpg', 'approved', 'Royal Enfield', 'Classic 350', 2021, 4000.00, 'bike');
```

---

### **14. Insert Sample Data into `rental_details` Table**
```sql
INSERT INTO rental_details (request_id, username, rental_duration, additional_notes, rent_start_date, rent_end_date) VALUES
    (1, 'Jitu', 12, 'This is a rental request.', '2024-11-01', '2024-11-13');
```

---

### **15. Verify the Tables and Data**
Run these commands to check your data:
```sql
SELECT * FROM users;
SELECT * FROM admins;
SELECT * FROM vehicles;
SELECT * FROM rent_requests;
SELECT * FROM buy_requests;
SELECT * FROM sale_requests;
SELECT * FROM rental_details;
```

This setup will give you a structured and functional database for your Vehicle Inventory app. Let me know if you need any adjustments or further assistance!
