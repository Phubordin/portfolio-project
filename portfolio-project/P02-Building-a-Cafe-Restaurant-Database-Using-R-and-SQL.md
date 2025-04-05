# P2 : Building a Café Restaurant Database Using R and SQL

## 📌 Table of Contents
1. [Create ER Diagram](#1-create-er-diagram)
2. [Create Tables and Perform SQL INSERT with Basic Queries and Aggregation](#2-create-tables-and-perform-sql-insert-with-basic-queries-and-aggregation)
3. [Create Tables and Perform INSERT Using R](#3-create-tables-and-perform-insert-using-r)

[Project Summary](#project-summary)

---

## 1 Create ER Diagram
## 2 Create Tables and Perform SQL INSERT with Basic Queries and Aggregation
## 3 Create Tables and Perform INSERT Using R

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
📌 **อธิบายสูตร:**

ผมขออนุญาตแบ่งเป็น 3 ส่วนดังนี้

1. `FILTER(EMPLOYEE, (GENDER = B2) * (PERFORMANCE = B3))`

   - ผมตั้งชื่อ range ต่างๆที่มีชื่อว่า `EMPLOYEE`(Table), `GENDER`(Column), `PERFORMANCE`(Column) เพื่อง่ายต่อการเลือกช่วง cell มาใช้

     ผมจึงเลือกช่วง `EMPLOYEE` โดยที่เพศ คือ cell `B2` ที่ Dynamic และ`*` ผลการปฏิบัติงาน คือ cell `B3` ที่ Dynamic

     ผลลัพธืจึงถูก Filter ออกมา หลังจากนั้น..
     
2. `SORT(FILTER(..ข้อ 1), 5, Not(D2))`

   - ผมเรียงลำดับ `Salary` จากมากไปน้อย โดยที่ `Salary` อยู่คอลัมน์ที่ `5` และ Default ของการ Sort ที่จะเรียงจากน้อยไปมากได้ก็ต่อเมื่อมีค่า TRUE

     ในอาร์กิวเมนต์ที่ 3 ของ Sort ดังนั้น ผมจึงเลือกคอลัมน์ `Salary` และเรียงลำดับตาม cell `D2` เป็น Checkbox เพื่อให้มีความ Dynamic เมื่อ users

     ติ้ก D2 = True ซึ่งมันจะเรียงจากน้อยไปมาก ดังนั้นผมจึงใช้ `NOT(D2)` เพื่อบังคับให้การติ้กของ users นั้นเรียง `Salary` จากมากไปน้อยโดยอัตโนมัติ
    
3. `IFERROR(..ข้อ 2,"NO DATA")`

   - ถ้าหาก Formula ข้อ 1 หรือ 2 ส่งผลลัพธ์ Error จะให้แสดง `NO DATA` แต่แน่นอนว่าในตาราง `EMPLOYEE` จะต้องมีการ filter ที่ไม่ match กัน

     นั้นหมายความว่าไม่มีค่า filter ที่ต้องการดังนั้นผลลัพธ์จึงแสดง `NO DATA` นั่นเอง !

📌 **ตัวอย่าง:** [แนะนำให้ลองดูใน Sheet: Click](https://docs.google.com/spreadsheets/d/1a3l_9Lgr_G6m5DkfvEdUg4a3fpwKmLog1oEyewA8Zg4/edit?usp=sharing)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-1-6.gif" alt="Highlight Row">
</p>

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-1-6.png" alt="Highlight Row">
</p>

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






