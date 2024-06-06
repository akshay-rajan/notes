# SQL

Structured Query Language is used to access and manipulate databases.

Relational Database Management System is the basis for SQL. The data in RDBMS is stored in **Tables**. A Table consists of rows (**Tuples**) and Columns (**Attributes**).

SQL keywords are not case sensitive.

## 1. Data Definition Language (DDL):

DDL (Data Definition Language) is a subset of SQL that is used to define and manage the structure of a database. It includes commands such as creating databases, tables, and modifying their structure.


1. **CREATE DATABASE**: Creates a new database.

```sql
CREATE DATABASE databasename;
```

2. **DROP DATABASE**: Delete an existing database.

```sql
DROP DATABASE databasename;
```

3. **CREATE TABLE**: Creates a new table.

```sql
CREATE TABLE table_name (
        column1 datatype,
        column2 datatype,
        column3 datatype,
        ....
);
```

4. **DROP TABLE**: Delete an existing table.

```sql
DROP TABLE tablename;
```

5. **TRUNCATE TABLE**: Delete the data inside the table and not the table itself.

```sql
TRUNCATE TABLE tablename;
```

6. **ALTER TABLE**: Modifies an existing table's structure.

```sql
ALTER TABLE tablename
ADD COLUMN columnname datatype;
```
```sql
ALTER TABLE tablename
DROP COLUMN columnname;
```
```sql
ALTER TABLE tablename
RENAME COLUMN oldname TO newname;
```
```sql
ALTER TABLE tablename
MODIFY COLUMN columnname datatype;
```

7. **CONSTRAINTS**: Rules applied to the data columns.

**On Creation**:

```sql
CREATE TABLE table_name (
        column1 datatype constraint,
        column2 datatype constraint,
        ....
);
```

   **After Creation**:

```sql
ALTER TABLE table_name
ADD CONSTRAINT constr_name constraint (col1,col2,...);
```

i. **NOT NULL**:

```sql
CREATE TABLE Persons (
        ID int NOT NULL,
        LastName varchar(255) NOT NULL,
        FirstName varchar(255) NOT NULL,
        Age int
);

--OR

ALTER TABLE Persons
MODIFY COLUMN Age int NOT NULL;
```

ii. **UNIQUE**:

```sql
CREATE TABLE Persons (
        ID int NOT NULL,
        LastName varchar(255) NOT NULL,
        FirstName varchar(255),
        Age int,
        UNIQUE (ID)
);

--OR

ALTER TABLE Persons
ADD UNIQUE (ID);
```

iii. **PRIMARY KEY**:

```sql
CREATE TABLE Persons (
        ID int NOT NULL,
        LastName varchar(255) NOT NULL,
        FirstName varchar(255),
        Age int,
        PRIMARY KEY (ID)
);

--OR

ALTER TABLE Persons
ADD PRIMARY KEY (ID);
```

iv. **FOREIGN KEY**:

```sql
CREATE TABLE Orders (
        OrderID int NOT NULL,
        OrderNumber int NOT NULL,
        PersonID int,
        PRIMARY KEY (OrderID),
        FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
);

--OR

ALTER TABLE Orders
ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
```

v. **CHECK**:

```sql
CREATE TABLE Persons (
        ID int NOT NULL,
        LastName varchar(255) NOT NULL,
        FirstName varchar(255),
        Age int,
        CHECK (Age>=18)
);

--OR

ALTER TABLE Persons
ADD CHECK (Age>=18);
```

vi. **DEFAULT**:

```sql
CREATE TABLE Orders (
        ID int NOT NULL,
        OrderNumber int NOT NULL,
        OrderDate date DEFAULT GETDATE()
);

--OR

ALTER TABLE Persons
ALTER City SET DEFAULT 'Sandnes';
```

8. **CREATE INDEX**: Creates an index on a table.

```sql
CREATE INDEX idx_lastname 
ON Employees(LastName);
```

9. **AUTOINCREMENT**: Allows a unique number to be generated automatically at a field.

```sql
CREATE TABLE Persons (
        Personid int NOT NULL AUTO_INCREMENT,
        LastName varchar(255) NOT NULL,
        FirstName varchar(255),
        Age int,
        PRIMARY KEY (Personid)
);
```

10. **CREATE VIEW**: Creates a virtual table.

```sql
-- Creation of virtual table
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;

-- Using the virtual table
SELECT * FROM view_name;
```

## 2. Data Manipulation Language (DML):

Used for manipulating the data within the database. It includes commands such as SELECT, INSERT, UPDATE, and DELETE.

1. **SELECT**: Retrieves data from one or more tables.

```sql
SELECT * FROM Employees 
WHERE DepartmentID = 100;
```

2. **INSERT INTO**: Adds new records to a table.
```sql
INSERT INTO Employees (EmployeeID, FirstName, LastName, DepartmentID) 
VALUES (1, 'John', 'Doe', 100);
```

3. **UPDATE**: Modifies existing records in a table.
```sql
UPDATE Employees SET DepartmentID = 200 
WHERE EmployeeID = 1;
```
4. **DELETE**: Removes records from a table.
```sql
DELETE FROM Employees WHERE EmployeeID = 1;
```
5. **JOIN** (**INNER JOIN**): Combines rows from two or more tables based on a related column.
```sql
SELECT Orders.OrderID, Customers.CustomerName FROM Orders
JOIN Customers 
ON Orders.CustomerID = Customers.CustomerID;

-- This is equivalent to the 'comma' syntax
SELECT Orders.OrderID, Customers.CustomerName 
FROM Orders, Customers 
WHERE Orders.CustomerID = Customers.CustomerID;
```
6. **LEFT JOIN**: Returns all records from left table, and matching records from right table (NULL if no match on the right table)

7. **RIGHT JOIN**: Returns all records from right table, and matching records from left table (NULL if no match on the left table)

8. **UNION**: Combine the result set of two or more `SELECT` statements.
```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

### where

The `WHERE` clause in SQL is used to filter records. It's used to extract only those records that fulfill a specified condition.

```sql
SELECT * FROM Employees WHERE Salary > 50000;
```

The `WHERE` clause can be combined with logical operators like `AND`, `OR`, and `NOT`, as well as comparison operators like `=`, `<>`, `<`, `>`, `<=`, `>=`.

`LIKE` is a simple pattern matching operator that allows us to use the wildcards:
- `%` - Matches any sequence of characters
- `_` - Matches any single character

```sql
SELECT * FROM employees WHERE last_name LIKE 'S%';
```
 `IN` is used to mention all possible values as an array.

```sql
SELECT * FROM employees WHERE last_name IN ('Ron', 'Harry');
```

`BETWEEN` is used to provide a range of values as an array, which satisfies the condition.

```sql
SELECT * FROM employees WHERE YEAR(hire_date) BETWEEN 1999 AND 2001;
```

## 3. DCL (Data Control Language):

Used for controlling the access to data within the database. It includes commands such as `GRANT` and `REVOKE`.

## 4. TCL (Transaction Control Language): 

Used for managing transactions within a database. It includes commands such as `COMMIT`, `ROLLBACK`, and `SAVEPOINT`.


# PL/SQL

PL/SQL (Procedural Language/Structured Query Language) is a programming language used for developing applications within Oracle databases. 
It extends SQL (Structured Query Language) by adding procedural capabilities, allowing developers to write procedural code such as loops, conditional statements, and error handling directly within SQL blocks. PL/SQL is commonly used to create stored procedures, functions, triggers, and packages, which enhance the functionality and performance of Oracle database applications.

### 1. Declare a Variable

```sql
DECLARE my_variable VARCHAR(50);
```

### 2. Create a Simple Loop

```sql
DECLARE counter INT DEFAULT 1;
WHILE counter <= 5 DO
        SELECT counter;
        SET counter = counter + 1;
END WHILE;
```

### 3. Create a Conditional Statement

```sql
IF x > 5 THEN
        SELECT 'x is greater than 5';
ELSE
        SELECT 'x is not greater than 5';
END IF;
```

### 4. Create a Function

```sql
CREATE FUNCTION calculate_area(length FLOAT, width FLOAT)
RETURNS FLOAT
BEGIN
        DECLARE area FLOAT;
        SET area = length * width;
        RETURN area;
END;
```

### 5. Create a Procedure

Procedures (PL/SQL Blocks) have no return values. These are used for operations to be performed multiple times.

```sql
CREATE PROCEDURE display_message(IN message VARCHAR(255))
BEGIN
        SELECT message;
END;
```

The `IN` indicates that a parameter is an `INPUT` parameter. We provide a value for this parameter when the procedure is called. Also `IN` is the default mode of a parameter, and hence can be avoided.
Other keywords are `OUT` (representing an output parameter) and `INOUT` (a parameter that can be both read and modified).

# MySQL

MySQL is an open-source relational database management system (RDBMS) that uses Structured Query Language (SQL) for adding, accessing, and managing content in a database.
It's known for its speed, reliability, and flexibility.

MySQL provides a rich set of built-in functions that you can use in SQL statements.

1. **String Functions**: Manipulate and process string data.
   - `CONCAT(str1, str2, ...)`: Returns a string that results from concatenating the arguments.
   - `LENGTH(str)`: Returns the length of a string in bytes.
   - `SUBSTRING(str, pos, len)`: Returns a substring from a string starting at a specified position.

2. **Numeric Functions**: Perform operations on numeric data.
   - `ABS(X)`: Returns the absolute value of X.
   - `CEIL(X) or CEILING(X)`: Returns the smallest integer value not less than X.
   - `FLOOR(X)`: Returns the largest integer value not greater than X.

3. **Date and Time Functions**: Process date and time data.
   - `NOW()`: Returns the current date and time.
   - `CURDATE()`: Returns the current date.
   - `DATEDIFF(expr1, expr2)`: Returns the difference in days between two date expressions.

4. **Control Flow Functions**: Implement conditional logic.
   - `IF(expr1, expr2, expr3)`: If expr1 is TRUE, IF() returns expr2; otherwise, it returns expr3.
   - `CASE`: Implements a complex conditional construct.

5. **Aggregate Functions**: Perform a calculation on a set of values and return a single value.
   - `AVG(expr)`: Returns the average value of expr.
   - `SUM(expr)`: Returns the sum of expr.
   - `COUNT(expr)`: Returns a count of the number of non-NULL values of expr.

6. **Comparison Functions**: Compare values and return a logical value.
   - `COALESCE(value,...)`: Returns the first non-NULL value in the list.
   - `GREATEST(value1,value2,...)`: Returns the greatest value in the list of arguments.
   - `LEAST(value1,value2,...)`: Returns the smallest value in the list of arguments.

7. **Conversion Functions**: Convert a value from one data type to another.
   - `CAST(expr AS type)`: Converts a value to a specified type.
   - `CONVERT(expr,type)`: Converts a value to a specified type.

8. **Information Functions**: Provide information about databases, tables, and server settings.
   - `DATABASE()`: Returns the default (current) database name.
   - `USER()`: Returns the current MySQL user name and host name.

[MySQL Functions Reference](https://dev.mysql.com/doc/refman/8.3/en/built-in-function-reference.html).
[MySQL Data Types Reference](https://dev.mysql.com/doc/refman/8.3/en/data-types.html)
