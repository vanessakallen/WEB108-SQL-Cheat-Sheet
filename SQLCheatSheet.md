# WEB-108: SQL Cheat Sheet - Vanessa Allen

## 1. How to login into mysql from terminal
`sudo mysql`

## 3. How to CREATE USERS
`-u root -p`
`CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';` <br>
(username = your username and password = your password)

## 4. How to GRANT PRIVILEGES, Show granted privileges and remove
- **Grant Privileges** <br>
`GRANT ALL PRIVILEGES ON databaseName.* TO 'username'@'localhost';` <br>
(databaseName = the name of your database and localhost = your host)

- **Show Granted Privileges** <br>
`SHOW GRANTS FOR 'username'@'localhost';`

- **Remove Granted Privileges** <br>
`REVOKE PRIVILEGES ON databaseName.* TO 'username'@'localhost';`

## 5. How to SHOW, DELETE & CREATE DATABASES & SELECT DATABASES
- **Show Databases** <br>
`SHOW DATABASES;`

- **Delete Databases** <br>
`DROP DATABASE databaseName;` <br>

- **Select Databases** <br>
`USE databaseName;`

## 6. How to CREATE a TABLE with Columns and their data types
```
CREATE TABLE tableName (
    Column1 datatype,
    Col2 datatype,
    col3 datatype
);
``` 
*No comma on the last datatype.* <br>
**Example:**
```
CREATE TABLE Customers (
    FirstName varchar(255),
    LastName varchar(255) NOT NULL,
    Age INT
);
``` 

## 7. How to SHOW, DELETE & DROP Tables
- **Show Tables** <br>
`SHOW TABLES;` <br>

- **Delete Tables** <br>
`DELETE tableName;` *Usually used to delete specific parts of a table.* <br> 
**Example:** <br>
`DELETE FROM tableName WHERE condition;`

- **Drop Tables** <br>
`DROP TABLE tableName;` *Used to drop entire tables and all data inside.*

## 8. How to Insert ROWS & RECORDS (single and multiple)
- **Single** <br>
`INSERT INTO tableName (Col1) VALUES (Value1);` <br>

- **Multiple** <br>
`INSERT INTO tableName (Col1, Col2, Col3) VALUES ("Value1", "Value2", Value3); `<br>
*Values is where you put the actual data. This can be strings or intergers. Intergers cannot be put in quotations.*

## 9. How to SELECT with the WHERE Clause
```
SELECT columnName
FROM tableName
WHERE condition;
```
**Example:** <br>
`SELECT * FROM Customers WHERE Age > 24;` <br>
*This selects all data from the Customers table and only returns the data where the Age is greater than 24.*

## 10. How to SELECT with the WHERE Clause using a range
```
SELECT Column(s)
FROM tableName
WHERE columnName BETWEEN Value1 AND Value2;
``` 
**Example:** <br>

`SELECT * FROM Customers WHERE Age BETWEEN 50 AND 65;` <br>
*This selects the Age column from the Customers table and returns all the customers with ages between 50 and 65.*

## 11. How to DELETE an individual ROW <br>
`DELETE FROM tableName WHERE condition;` <br>
*Deletes a row whilst keeping the table.*

## 12. How to UPDATE a ROW
```
UPDATE tableName
SET Col1 = Val1, Col2 = Val2 etc...
WHERE condition;
```
**Example:**
```
UPDATE Customers
SET PhoneNumber = '2504548877'
WHERE CustomerID = 487;
```
*Updates a single row by inputing new data into an Existing datatype. In this Example, only the customer with an ID that matches 487 responds to the change.*

## 13. How to add a new column and modify it
- **Add a New Column** <br>
`ALTER TABLE tableName ADD columnName datatype;` <br>
**Example:** <br>
`ALTER TABLE Customers ADD Email varchar(255);` <br>
*This adds a new column to an Existing table.*

- **Modify a Column** <br>
`ALTER TABLE tableName ALTER COLUMN columnName datatype;` <br>
**Example:** <br>
`ALTER TABLE Customers ALTER COLUMN Age varchar(255);` <br>
*This would modify the Age column to be a varchar instead of an interger.*

## 14. How to Order by and use Distinct
- **Order By**
```
SELECT Col(s)
FROM tableName
ORDER BY Col(s) ASC or DESC;
```
**Example:** <br>
`SELECT * FROM Customers ORDER BY Age ASC;` <br>
*This orders all customers from youngest to oldest.* <br>

To select multiple columns: <br>
`SELECT * FROM Customers ORDER BY Age ASC, Name DESC;`

- **Distinct** <br>
`SELECT DISTINCT Col(s) FROM tableName;`<br>
**Example:** <br>
`SELECT DISTINCT Age FROM Customers;` <br>
*Distinct returns distinct/different values. It is useful in tables where there are many duplicates and you only want to list the different values.*

## 15. How to Concatenate Columns <br>
`SELECT CONCAT(Col1, " ", Col2, " ", etc...) FROM tableName AS colName;` <br>
**Example:** <br>
`SELECT CONCAT(Address, " ", PostalCode, " ", City etc...) FROM Customers AS Address;` <br>
*This allows for three columns to be put into one "Address" column.*

## 16. How to Select Distinct Rows <br>
`SELECT DISTINCT Col(s) FROM tableName;` <br>
**Example:** <br>
`SELECT DISTINCT Age FROM Customers;` <br>
*This selects only the different values from Age in the Customers table.*

## 17. How to use LIKE to Search
```
SELECT Col(s)
FROM tableName
WHERE columnName LIKE pattern;
```
**Example:** <br>
`SELECT * FROM Customers WHERE Address LIKE 'C%';` <br>
*This returns all addresses that begin with the letter C. You can switch the place of the % sign to get address that **end** in C.*

## 18. How Select using IN
*IN allows you to specify multiple values in the WHERE line.*
```
SELECT Col(s)
FROM tableName
WHERE ColName IN (Value(s));
```
**Example:** <br>
`SELECT * FROM Customers WHERE Age IN (19, 24, 65);` <br>
*This selects all columns from Customers table and returns the Customers who are of the ages of 19, 24, and 65.*

## 19. How to Create & Remove Index <br>
`CREATE INDEX indexName ON tableName (Col(s));` <br>
**Example:** <br>
`CREATE INDEX NameIndex ON Customers (LastName, FirstName);` <br>
*This creates an index named NameIndex on the columns LastName and FirstName in the Customers table.*

## 20. Create Two Tables demonstrating a one to many relationship that shows a PK & FK
```
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FirstName VARCHAR(255) NOT NULL,
    LastName VARCHAR(255) NOT NULL,
    Age INT,
    Email VARCHAR(255) NOT NULL
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE NOT NULL,
    AmountTotal DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```
*Here, the Customers table has a primary key of CustomerID, the Orders table has a primary key of OrderID and a foreign key of CustomerID, which references the primary key in the Customers table. This creates a one to many relationship between customers and orders, because one customer can have multiple orders.*

## 21. How to use Inner Join
*Inner Join is used to combine rows from two or more tables. It is based on related columns between these to tables.* <br>
```
SELECT Customers.Name, Orders.OrderDate
FROM Customers
INNER JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```
*This returns all rows where the CustomerID column in the Customers table matches the CustomerID column in the Orders table. The result will include columns named Name and OrderDate from both tables.*

## 22. How to JOIN Multiple Tables
```
SELECT Col(s)
FROM Table1
INNER JOIN Table2
ON Table1.relatedColumn = Table2.relatedColumn;
```
**Example:** 
```
SELECT * FROM Orders 
JOIN Customers 
ON Orders.CustomerID = Customers.ID;
```
*This is joining the Orders table with the Customers table on the CustomerID column in the Orders table and the ID column in the Customers table. This results in a new table that includes all the columns from both the Orders and Customers tables, where the rows with matching CustomerID and ID values are combined (joined).*