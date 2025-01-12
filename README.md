# SQL-Server

SQL Server scripts are typically written in Transact-SQL (T-SQL), Microsoft's proprietary extension to SQL. They are used to interact with SQL Server databases for tasks such as querying data, managing database objects, and automating processes.

Here’s an overview of common SQL Server script types and examples:

---

### **1. Querying Data**
Retrieve data using `SELECT` statements with filters, sorting, and grouping.

```sql
SELECT FirstName, LastName, Email
FROM Employees
WHERE Department = 'Sales'
ORDER BY LastName ASC;
```

---

### **2. Creating Database Objects**
Define structures like tables, views, stored procedures, and indexes.

#### Create Table
```sql
CREATE TABLE Products (
    ProductID INT IDENTITY(1,1) PRIMARY KEY,
    ProductName NVARCHAR(100) NOT NULL,
    Price DECIMAL(10, 2),
    Quantity INT DEFAULT 0,
    CreatedDate DATETIME DEFAULT GETDATE()
);
```

#### Create View
```sql
CREATE VIEW ActiveProducts AS
SELECT ProductID, ProductName, Price
FROM Products
WHERE Quantity > 0;
```

---

### **3. Modifying Data**
Insert, update, or delete records in tables.

#### Insert
```sql
INSERT INTO Products (ProductName, Price, Quantity)
VALUES ('Laptop', 799.99, 10);
```

#### Update
```sql
UPDATE Products
SET Price = 749.99
WHERE ProductName = 'Laptop';
```

#### Delete
```sql
DELETE FROM Products
WHERE Quantity = 0;
```

---

### **4. Writing Stored Procedures**
Encapsulate reusable logic in a procedure.

```sql
CREATE PROCEDURE GetProductsByPriceRange
    @MinPrice DECIMAL(10, 2),
    @MaxPrice DECIMAL(10, 2)
AS
BEGIN
    SELECT ProductID, ProductName, Price
    FROM Products
    WHERE Price BETWEEN @MinPrice AND @MaxPrice;
END;
```

---

### **5. Writing Functions**
Create scalar or table-valued functions.

#### Scalar Function
```sql
CREATE FUNCTION dbo.GetFullName(@FirstName NVARCHAR(50), @LastName NVARCHAR(50))
RETURNS NVARCHAR(101)
AS
BEGIN
    RETURN @FirstName + ' ' + @LastName;
END;
```

#### Table-Valued Function
```sql
CREATE FUNCTION dbo.GetActiveProducts()
RETURNS TABLE
AS
RETURN (
    SELECT ProductID, ProductName, Price
    FROM Products
    WHERE Quantity > 0
);
```

---

### **6. Managing Transactions**
Control transactional integrity using `BEGIN TRANSACTION`, `COMMIT`, and `ROLLBACK`.

```sql
BEGIN TRANSACTION;

UPDATE Products
SET Quantity = Quantity - 1
WHERE ProductID = 1;

IF @@ERROR <> 0
    ROLLBACK TRANSACTION;
ELSE
    COMMIT TRANSACTION;
```

---

### **7. Index Management**
Create and manage indexes for performance optimization.

#### Create Index
```sql
CREATE INDEX IX_Products_ProductName
ON Products (ProductName);
```

#### Drop Index
```sql
DROP INDEX IX_Products_ProductName ON Products;
```

---

### **8. Scheduling Jobs**
Automate tasks using SQL Server Agent jobs. You can script these using T-SQL and the `sp_add_job` system stored procedures.

---

Do you need help with a specific SQL Server script or use case? Let me know!
