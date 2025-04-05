# P2 : Building a Café Restaurant Database Using R and SQL

## 📌 Table of Contents
1. [Create Tables and Perform SQL INSERT with Basic Queries and Aggregation](#1-create-tables-and-perform-sql-insert-with-basic-queries-and-aggregation)
2. [Create Tables and Perform INSERT Using R](#2-create-tables-and-perform-insert-using-r)
3. [Create ER Diagram (DBML Code)](#3-create-er-diagram-dbml-code)

[Project Summary](#project-summary)

---

## 1 Create Tables and Perform SQL INSERT with Basic Queries and Aggregation

```sql

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






