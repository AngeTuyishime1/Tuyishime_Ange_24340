# Tuyishime_Ange_24340
summary of the Problem Statement for "Tech Haven"
Background:
"Tech Haven," an electronic devices store, faces challenges with inventory management, customer experience, and sales tracking, affecting its overall performance.

Current Issues:

Inventory Management:
Manual tracking leads to discrepancies and stockouts.
Ineffective communication about new products and promotions.
Customer Experience:
Long wait times at checkout.
Limited product information available.
Inadequate feedback mechanisms.
Sales Tracking:
Lack of a comprehensive sales system.
Inconsistent management of promotions.
---------------------------------------------------------------------------
-- Create Customers table
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100),
    ContactInfo VARCHAR(100)
);

-- Create Products table
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    Name VARCHAR(100),
    Description VARCHAR(255),
    Price DECIMAL(10, 2)
);

-- Create Sales table (foreign keys to Customers and Products)
CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    CustomerID INT,
    ProductID INT,
    SaleDate DATE,
    Amount DECIMAL(10, 2),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);

-- Create Inventory table (one-to-one relationship with Products)
CREATE TABLE Inventory (
    InventoryID INT PRIMARY KEY,
    ProductID INT,
    QuantityAvailable INT,
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
---------------------------------------------------
-- Insert Customers
INSERT INTO Customers (CustomerID, Name, ContactInfo) 
VALUES (1, 'mugisha', 'mugisha@gmail.com');

INSERT INTO Customers (CustomerID, Name, ContactInfo) 
VALUES (2, ' kanyana', 'kanyana@gmail.com');

-- Insert Products
INSERT INTO Products (ProductID, Name, Description, Price) 
VALUES (101, 'Laptop', 'High-performance laptop', 1200.00);

INSERT INTO Products (ProductID, Name, Description, Price) 
VALUES (102, 'Smartphone', 'Latest model smartphone', 800.00);

-- Insert Sales
INSERT INTO Sales (SaleID, CustomerID, ProductID, SaleDate, Amount) 
VALUES (1001, 1, 101, TO_DATE('2024-10-01', 'YYYY-MM-DD'), 1200.00);

INSERT INTO Sales (SaleID, CustomerID, ProductID, SaleDate, Amount) 
VALUES (1002, 2, 102, TO_DATE('2024-10-02', 'YYYY-MM-DD'), 800.00);

-- Insert Inventory
INSERT INTO Inventory (InventoryID, ProductID, QuantityAvailable) 
VALUES (1, 101, 10);

INSERT INTO Inventory (InventoryID, ProductID, QuantityAvailable) 
VALUES (2, 102, 15);
-----------------------------------------------------
Update Data
sql
Copy code
-- Update product price
UPDATE Products
SET Price = 1300.00
WHERE ProductID = 101;

-- Update inventory quantity
UPDATE Inventory
SET QuantityAvailable = 9
WHERE ProductID = 101;
Delete Data
sql
Copy code
-- Delete a sale record
DELETE FROM Sales
WHERE SaleID = 1002;
-- Delete a product
DELETE FROM Products
WHERE ProductID = 102;

-----------------------------------------------------
-- Retrieve all sales with customer and product information
SELECT Customers.Name AS CustomerName, Products.Name AS ProductName, Sales.SaleDate, Sales.Amount
FROM Sales
JOIN Customers ON Sales.CustomerID = Customers.CustomerID
JOIN Products ON Sales.ProductID = Products.ProductID;
Subquery to Check Stock Before a Sale
sql

-- Check if a product is in stock before processing a sale
SELECT ProductID, QuantityAvailable
FROM Inventory
WHERE ProductID = (SELECT ProductID FROM Products WHERE Name = 'Laptop');
