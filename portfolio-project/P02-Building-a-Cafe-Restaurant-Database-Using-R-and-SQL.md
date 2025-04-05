# P2 : Building a Café Restaurant Database Using R and SQL

## 📌 Table of Contents
1. [Create Tables and Perform SQL INSERT with Basic Queries and Aggregation](#1-create-tables-and-perform-sql-insert-with-basic-queries-and-aggregation)
2. [Create Tables and Perform INSERT Using R](#2-create-tables-and-perform-insert-using-r)
3. [Create ER Diagram (DBML Code)](#3-create-er-diagram-dbml-code)

[Project Summary](#project-summary)

---

## 1 Create Tables and Perform SQL INSERT with Basic Queries and Aggregation

```sql
CREATE TABLE Transactions (
  InvoiceId INT PRIMARY KEY,
  BranchId INT,
  CustomerId INT,
  MenuId INT,
  CommentId INT, 
  InvoiceDate DATETIME,
  Quantity INT, 
  Total_Sales REAL
);

-- Creating Menus Table
CREATE TABLE Menus (
  MenuId INT PRIMARY KEY,
  Name TEXT,
  Categories TEXT CHECK (Categories IN ('Rice', 'Pasta', 'Drinks', 'Dessert'))
);

-- Creating Branch Table
CREATE TABLE Branch (
  BranchId INT PRIMARY KEY,
  Name TEXT,
  Address TEXT
);

-- Creating Customers Table
CREATE TABLE Customers (
  CustomerId INT PRIMARY KEY,
  Name TEXT,
  Gender TEXT CHECK (Gender IN ('Male', 'Female', 'LGBTQ+')),
  Status TEXT CHECK (Status IN ('Member', 'Guest'))
);

-- Creating Feedback Table
CREATE TABLE Feedback (
  CommentId INT PRIMARY KEY,
  Comment TEXT CHECK (Comment IN ('รสจัดเกิน', 'คุ้มราคา', 'เเพง', 'กลมกล่อม', 'บอกต่อ', 'เค็มเกิน')),
  Emotional TEXT CHECK (Emotional IN ('Positive', 'Negative'))
);

-- Inserting data into Transactions Table
INSERT INTO Transactions (InvoiceId, BranchId, CustomerId, MenuId, CommentId, InvoiceDate, Quantity, Total_Sales) VALUES
(1,  1, 1, 1, 1, '2023-05-01', 4, 100.00),
(2,  2, 2, 2, 4, '2023-06-02', 3, 200.00),
(3,  3, 3, 3, 5, '2023-08-03', 4, 300.00),
(4,  1, 3, 4, 2, '2023-12-04', 2, 400.00),
(5,  2, 2, 5, 4, '2023-11-05', 1, 500.00),
(6,  3, 5, 6, 6, '2023-03-06', 3, 600.00),
(7,  1, 1, 7, 5, '2023-02-07', 3, 700.00),
(8,  2, 2, 8, 5, '2023-09-08', 2, 800.00),
(9,  3, 4, 1, 3, '2023-05-09', 3, 900.00),
(10, 1, 4, 2, 3, '2023-08-10', 5, 1000.00);

-- Inserting data into Branch Table
INSERT INTO Branch (BranchId, Name, Address) VALUES
(1, 'Ratchayothin', 'Chatuchak'),
(2, 'Rama 7'      , 'BangSue'),
(3, 'ChokChai 4'  , 'Latphrao');

-- Inserting data into Customers Table
INSERT INTO Customers (CustomerId, Name, Gender, Status) VALUES
(1, 'John', 'Male'  , 'Member'),
(2, 'Jane', 'Female', 'Guest'),
(3, 'Alex', 'LGBTQ+', 'Member'),
(4, 'Sara', 'Female', 'Guest'),
(5, 'Tom' , 'Male'  , 'Member');

-- Inserting data into Feedback Table
INSERT INTO Feedback (CommentId, Comment, Emotional) VALUES
(1, 'รสจัดเกิน' , 'Negative'),
(2, 'คุ้มราคา'  , 'Positive'),
(3, 'เเพง'    , 'Negative'),
(4, 'กลมกล่อม' , 'Positive'),
(5, 'บอกต่อ'  , 'Positive'),
(6, 'เค็มเกิน'  , 'Negative');

-- Inserting data into Menus Table
INSERT INTO Menus (MenuId, Name, Categories) VALUES
(1, 'Pad Thai'  , 'Rice'),
(2, 'Spaghetti' , 'Pasta'),
(3, 'Coke'      , 'Drinks'),
(4, 'Cake'      , 'Dessert'),
(5, 'Fried Rice', 'Rice'),
(6, 'Lasagna'   , 'Pasta'),
(7, 'Water'     , 'Drinks'),
(8, 'Ice Cream' , 'Dessert');

-------------------- เริ่มเขียน Query ดึงข้อมูลจาก Table ที่เราสร้างไว้ด้านบน --------------------
------------------- โจทย์อยากทราบว่าลูกค้าที่เป็น member มีความคิดเห็นอย่างไรกับร้านอาหารของเรา------------

.mode table
.header on


WITH OrderDetail AS (	
  SELECT
      *
  FROM Customers    A
  JOIN Transactions B USING(CustomerId)
  JOIN Branch       C USING(BranchId)
  JOIN Menus        D	USING(MenuId)
  JOIN Feedback     E	USING(CommentId)
  WHERE 
    lower(A.Status) = 'member'
)
SELECT
  Emotional,
  Comment,
  max(InvoiceDate) Last_Time,
  sum(Total_Sales) Actual_Sales,
  avg(Total_Sales) Avg_Orders,
  count(*) N_Bill,
  count(DISTINCT CustomerId) N_Customers,
  count(DISTINCT BranchId) N_Branches,
  count(DISTINCT MenuId) N_Menus
FROM orderdetail
GROUP by 2
ORDER by 3 DESC;

/* RESULT:

+-----------+-----------+------------+--------------+-----------+--------+-------------+------------+---------+
| Emotional |  Comment  | Last_Time  | Actual_Sales | Avg_Orders| N_Orders| N_Customers | N_Branches | N_Menus |
+-----------+-----------+------------+--------------+-----------+--------+-------------+------------+---------+
| Positive  | คุ้มราคา     | 2023-12-04 | 400.0        | 400.0     | 1      | 1           | 1          | 1       |
| Positive  | บอกต่อ     | 2023-08-03 | 1000.0       | 500.0     | 2      | 2           | 2          | 2       |
| Negative  | รสจัดเกิน    | 2023-05-01 | 100.0        | 100.0     | 1      | 1           | 1          | 1       |
| Negative  | เค็มเกิน     | 2023-03-06 | 600.0        | 600.0     | 1      | 1           | 1          | 1       |
+-----------+-----------+------------+--------------+-----------+--------+-------------+------------+---------+

*/

```

---

## 2 Create Tables and Perform INSERT Using R

---


## 3 Create ER Diagram (DBML Code)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/blob/main/er-diagram.png" alt="ER Diagram">
</p>

```dbml
// Use DBML to define your database structure
// Docs: https://dbml.dbdiagram.io/docs

Table Transactions {
  InvoiceId integer [primary key]
  BranchId integer
  CustomerId integer
  MenuId integer
  CommentId integer 
  InvoiceDate timestamp
  Quantity integer
  Total_Sales real 
  
}

Table Menus {
  MenuId integer [primary key]
  Name varchar
  Categories varchar
}

Table Branch {
  BranchId integer [primary key]
  Name varchar
  Address varchar
}

Table Customers {
  CustomerId integer [primary key]
  Name varchar
  Gendar varchar
  Status varchar
}

Table Feedback {
  CommentId integer [primary key]
  Comment varchar
  Emotional varchar
}

Ref: Customers.CustomerId < Transactions.CustomerId // one-to-many

Ref: Branch.BranchId < Transactions.BranchId

Ref: Menus.MenuId < Transactions.MenuId

Ref: Feedback.CommentId < Transactions.CommentId

```

---

## Project Summary

ก็จบไปแล้วสำหรับ Project 1 : Data Exploration and Transformation with Google Sheets 

โดยมี 6 ตัวอย่าง ไว้ใช้สำหรับ Explore และ Transform ข้อมูล

1. ใช้สูตร filter ข้อมูล และสามารถ Dropdown List เพื่อเลือกเพศและผลการปฎิบัติงานของพนักงาน

2. ใช้ Highlight Conditional Formatting ในการ Hightlight ข้อมูลของพนักงานที่เราต้องการ

3. ใช้สูตร `Query()` ในการ Dropdown List ข้อมูลลูกค้า เพศ, ผลการปฎิบัติงาน, วันเริ่มงานให้มีความ Dynamic

4. `Vlookup()` เครื่องมือยอดฮิตหนึ่งในตระกูล lookup ไว้ใช้หาค่าต่างๆที่มีความสัมพันธ์เชิงข้อมูล

5. แปลงรูปแบบวันที่ไทย เป็นวันที่มาตรฐานสากล ISO ด้วย `SPLIT()`, `DATE()` และ `VLOOKUP()`

6. การ Transform Data ด้วย Regular Expression สูตรที่ใช้หลักๆ `REGEXEXTRACT()` และ `REGEXMATCH()`

เป็นต้น ขอบคุณมากๆครับที่อ่านมาถึงตรงนี้ ฝากผลงาน project อื่นๆด้วยนะครับ ขอบคุณครับ






