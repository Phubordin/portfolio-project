# P2 : Building a Café Restaurant Database Using R and SQL

## 📌 Table of Contents
1. [Create Tables and Perform SQL INSERT with Basic Queries and Aggregation](#1-create-tables-and-perform-sql-insert-with-basic-queries-and-aggregation)
2. [Create Tables and Perform INSERT Using R](#2-create-tables-and-perform-insert-using-r)
3. [Create ER Diagram (DBML Code)](#3-create-er-diagram-dbml-code)

[Project Summary](#project-summary)

---

## 1 Create Tables and Perform SQL INSERT with Basic Queries and Aggregation

```sql
-- สร้าง Table ด้วยด้วย CREATE TABLE ทั้งหมด 5 Table

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
  MenuId INT PRIMARY KEY, -- สร้างคอลัมน์ MenuId เป็น Primary Key
  Name TEXT, -- สร้างคอลัมน์ Name เป็น TEXT
  Categories TEXT CHECK (Categories IN ('Rice,' 'Pasta,' 'Drinks,' 'Dessert')) -- สร้างคอลัมน์ Categories เป็น TEXT และกำหนดให้มีเฉพาะค่า 'Rice,' 'Pasta,' 'Drinks,' 'Dessert' เท่านั้น
);

-- Creating Branch Table
CREATE TABLE Branch (
  BranchId INT PRIMARY KEY, -- สร้างคอลัมน์ BranchId เป็น Primary Key
  Name TEXT, -- สร้างคอลัมน์ Name เป็น TEXT
  Address TEXT -- สร้างคอลัมน์ Address เป็น TEXT
);

-- Creating Customers Table
CREATE TABLE Customers (
  CustomerId INT PRIMARY KEY, -- สร้างคอลัมน์ CustomerId เป็น Primary Key
  Name TEXT, -- สร้างคอลัมน์ Name เป็น TEXT
  Gender TEXT CHECK (Gender IN ('Male', 'Female', 'LGBTQ+')), -- สร้างคอลัมน์ Gender เป็น TEXT และกำหนดให้มีเฉพาะค่า 'Male', 'Female', 'LGBTQ+' เท่านั้น
  Status TEXT CHECK (Status IN ('Member', 'Guest')) -- สร้างคอลัมน์ Status เป็น TEXT และกำหนดให้มีเฉพาะค่า 'Member', 'Guest' เท่านั้น
);

-- Creating Feedback Table
CREATE TABLE Feedback (
  CommentId INT PRIMARY KEY, -- สร้างคอลัมน์ CommentId เป็น Primary Key
  Comment TEXT CHECK (Comment IN ('รสจัดเกิน', 'คุ้มราคา', 'เเพง', 'กลมกล่อม', 'บอกต่อ', 'เค็มเกิน')), -- สร้างคอลัมน์ Comment เป็น TEXT และกำหนดให้มีเฉพาะค่า 'รสจัดเกิน', 'คุ้มราคา', 'เเพง', 'กลมกล่อ
  Emotional TEXT CHECK (Emotional IN ('Positive', 'Negative')) -- สร้างคอลัมน์ Emotional เป็น TEXT และกำหนดให้มีเฉพาะค่า 'Positive', 'Negative' เท่านั้น
);


-- เพื่มข้อมูลแต่ละเเถวเข้าไปใน TABLE ที่สร้างเมื่อสักครู่ ทั้งหมด 5 Table ด้วย INSERT INTO

-- Inserting data into Transactions Table
INSERT INTO Transactions (InvoiceId, BranchId, CustomerId, MenuId, CommentId, InvoiceDate, Quantity, Total_Sales) VALUES
(1,  1, 1, 1, 1, '2023-05-01', 4, 100.00), -- เพิ่มข้อมูลแต่ละคอลัมน์เข้าไปใน Transactions Table ทั้งหมด 10 InvoiceId (1-10 rows)
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
(1, 'Ratchayothin', 'Chatuchak'), -- เพิ่มข้อมูลแต่ละคอลัมน์เข้าไปใน Branch Table ทั้งหมด 3 BranchId (1-3 rows)
(2, 'Rama 7'      , 'BangSue'),
(3, 'ChokChai 4'  , 'Latphrao');

-- Inserting data into Customers Table
INSERT INTO Customers (CustomerId, Name, Gender, Status) VALUES
(1, 'John', 'Male'  , 'Member'), -- เพิ่มข้อมูลแต่ละคอลัมน์เข้าไปใน Customers Table ทั้งหมด 5 CustomerId (1-5 rows)
(2, 'Jane', 'Female', 'Guest'),
(3, 'Alex', 'LGBTQ+', 'Member'),
(4, 'Sara', 'Female', 'Guest'),
(5, 'Tom' , 'Male'  , 'Member');

-- Inserting data into Feedback Table
INSERT INTO Feedback (CommentId, Comment, Emotional) VALUES
(1, 'รสจัดเกิน' , 'Negative'), -- เพิ่มข้อมูลแต่ละคอลัมน์เข้าไปใน Feedback Table ทั้งหมด 6 CommentId (1-6 rows)
(2, 'คุ้มราคา'  , 'Positive'),
(3, 'เเพง'    , 'Negative'),
(4, 'กลมกล่อม' , 'Positive'),
(5, 'บอกต่อ'  , 'Positive'),
(6, 'เค็มเกิน'  , 'Negative');

-- Inserting data into Menus Table
INSERT INTO Menus (MenuId, Name, Categories) VALUES
(1, 'Pad Thai'  , 'Rice'), -- เพิ่มข้อมูลแต่ละคอลัมน์เข้าไปใน Menus Table ทั้งหมด 8 MenuId (1-8 rows)
(2, 'Spaghetti' , 'Pasta'),
(3, 'Coke'      , 'Drinks'),
(4, 'Cake'      , 'Dessert'),
(5, 'Fried Rice', 'Rice'),
(6, 'Lasagna'   , 'Pasta'),
(7, 'Water'     , 'Drinks'),
(8, 'Ice Cream' , 'Dessert');

-------------------- เริ่มเขียน Query ดึงข้อมูลจาก Table ที่เราสร้างไว้ด้านบน --------------------
------------------- โจทย์อยากทราบว่าลูกค้าที่เป็น member มีความคิดเห็นอย่างไรกับร้านอาหารของเรา------------

.mode table ---- ใช้ .mode table เพื่อให้ผลลัพธ์แสดงในรูปแบบตาราง (ตอนแรกผมเขียนบน replit เพื่อให้ users เห็นหน้าตาของผลลัพธ์ จึงใช้ .mode table)
.header on ---- ใช้ .header on เพื่อให้ผลลัพธ์แสดงชื่อคอลัมน์ด้วย (เหตุผลที่ใช้เหมือนกับ .mode table)


WITH OrderDetail AS (	-- สร้าง CTE ชื่อ OrderDetail เพื่อใช้ในการ Join Table ทั้งหมด 5 Table
  SELECT
      * -- เอามาทุกคอลัมน์จากทั้งหมด 5 ตารางที่มา join
  FROM Customers    A -- ตั้งชื่อ Customers เป็น A
  JOIN Transactions B USING(CustomerId) -- Join Table Transactions ด้วย CustomerId
  JOIN Branch       C USING(BranchId) -- Join Table Branch ด้วย BranchId
  JOIN Menus        D	USING(MenuId) -- Join Table Menus ด้วย MenuId
  JOIN Feedback     E	USING(CommentId) -- Join Table Feedback ด้วย CommentId
  WHERE 
    lower(A.Status) = 'member' --ปรับให้ข้อมูลสถานะลูกค้าเป็นตัวเล็กทั้งหมด แล้วค่อยกรองเฉพาะลูกค้าที่เป็น member
) -- เสร็จการใช้ Common Table Expression (CTE) เราจะได้ข้อมูลทั้งหมดเฉพาะลูกค้าที่เป็น member ชื่อตารางว่า OrderDetail
  
SELECT -- เพ่ือการดึงคอลัมน์ และเริ่ม Aggregate ค่า Basic Statistics เพื่อคำนวณหาว่าลูกค้าที่เป็น member มีความคิดเห็นอย่างไรกับร้านอาหารของเรา
  Emotional, -- ดึงคอลัมน์ Emotional เพื่อเค้ามีความคิดเชิง Positive หรือ Negative
  Comment, -- ดึงคอลัมน์ Comment ว่าเค้า feedback อะไรกับร้านเราบ้าง
  max(InvoiceDate) Last_Time, -- เค้าซื้อกับเราครั้งล่าสุดเมื่อไหร่
  sum(Total_Sales) Actual_Sales, -- เค้าตัดสินใจที่จะจ่ายเราจำนวนเงินทั้งหมดเท่าไร
  avg(Total_Sales) Avg_Orders, -- เฉลี่ยต่อ 1 Order เค้าจ่ายเงินเท่าไร
  count(*) N_Bill, -- นับดูว่าบิลล์ที่เค้าซื้อมีทั้งหมดกี่บิล
  count(DISTINCT CustomerId) N_Customers, -- ดูว่ามีลูกค้าที่ feedback แต่ละแบบมากี่คน
  count(DISTINCT BranchId) N_Branches, -- ลูกค้าที่ feedback ลักษณะนี้ เค้าซื้ออาหารกับร้านเราที่สาขาไหนบ้าง
  count(DISTINCT MenuId) N_Menus -- ลูกค้าที่ feedback ลักษณะนี้ เค้าซื้ออาหารกับร้านเราเมนูไหนบ้าง
FROM orderdetail -- ใช้ข้อมูลจากตารางที่เราสร้าง CTE ชื่อ OrderDetail เมื่อสักครู่
GROUP by 2 -- จัดกลุ่มค่า Basic Statistics ตามคอลัมน์ Comment
ORDER by 3 DESC; -- โดยเรียงวันล่าสุดที่ลูกค้าเข้ามาซื้ออาหารกับเรา
```

📌 **RESULT:**

+-----------+-----------+------------+--------------+-----------+--------+-------------+------------+---------+
| Emotional |  Comment  | Last_Time  | Actual_Sales | Avg_Orders| N_Orders| N_Customers | N_Branches | N_Menus|
+-----------+-----------+------------+--------------+-----------+--------+-------------+------------+---------+
| Positive  | คุ้มราคา    | 2023-12-04 | 400.0        | 400.0     | 1      | 1           | 1          | 1       |
| Positive  | บอกต่อ     | 2023-08-03 | 1000.0       | 500.0     | 2      | 2           | 2          | 2       |
| Negative  | รสจัดเกิน   | 2023-05-01 | 100.0        | 100.0     | 1      | 1           | 1          | 1       |
| Negative  | เค็มเกิน    | 2023-03-06 | 600.0        | 600.0     | 1      | 1           | 1          | 1       |
+-----------+-----------+------------+--------------+-----------+--------+-------------+------------+---------+


feedback จากลูกค้าที่ comment มาทั้ง 4 comment

1. คุุ้มราคา

   ส่วนใหญ่พึ่งมาซื้ออาหารกับร้านเราเมื่อวันที่ 04 Dec 2023 ด้วยจำนวนเงินทั้งหมด 400 บาท เฉลี่ยต่อบิลอยู่ที่ 400 เช่นกัน เพราะมี 1 บิลจากลูกค้า 1 คน

   ที่ 1 สาขา ซื้อทั้งหมด 1 เมนู

2. บอกต่อ

   พึ่งเปิดบิลกับร้านเราถัดจากอันแรกคือวันที่ 03 Aug 2023 ด้วยจำนวนเงินทั้งหมด 1000 บาท เฉลี่ยต่อบิลอยู่ที่ 500 โดยที่มี 2 บิลจากลูกค้า 2 คน

   มาจาก 2 สาขา ซื้อทั้งหมด 2 เมนู

3. รสจัดเกิน

   เริ่มหายจากการซื้ออาหารร้านเราค่อนข้างนานพึ่งซื้อเมื่อวันที่ 01 May 2023 ด้วยจำนวนเงินทั้งหมด 100 บาท เฉลี่ยต่อบิลอยู่ที่ 100 เพราะมี 1 บิล

   จากลูกค้า 1 คนที่ 1 สาขา ซื้อทั้งหมด 1 เมนู

4. เค็มเกิน

   ห่างหายจากเราไปนานที่สุดพึ่งซื้อ 06 Mar 2023 ด้วยจำนวนเงินทั้งหมด 600 บาท เฉลี่ยต่อบิลอยู่ที่ 600 เช่นกัน เพราะมี 1 บิลจากลูกค้า 1 คน

   ที่ 1 สาขา ซื้อทั้งหมด 1 เมนู

📌 **สรุปผลลัพธ์:**

สิ่งที่ได้และต้อง Action คือ มีแนวโน้มที่รสชาติหรือปัจจัยเชิงบวกที่ลูกค้าพบเจอได้ดูแก้ไข เพราะที่ผ่านมาลูกค้าที่พึ่งซื้ออาหารจากเราไปเริ่มมี feedback ในเชิงบวก

อย่างไรก็ตาม เราก็ต้องไปดูในส่วนของความคิด Negative ว่า เมนูอะไรส่วนใหญ่ที่ลูกค้าซื้อ โดยจากลูกค้าทุกๆคนมีการ comment เชิงลบ เกิดขึ้นไปยังไง

ถ้าแบ่งได้เป็น 2 กรณี

  - ลูกค้าบอกไม่อร่อย เราก็ต้องไปดูสัดส่วนการใส่วัตถุดิบที่พนักงานปรุง หรือ recipe เกิด tepo ขึ้น เพื่อที่จะได้ action และป้องกันไม่ให้เกิดขึ้นอีก
  
  - ลูกค้าบอกไม่สะอาด ข้อนี้อาจต้องได้รับการแก้ไขมาเป็นอันดับแรกมากที่สุดในบรรดา ทุกปัจจัยเชิงลบ เนื่องจากจะมีความเสียหายวงกว้าง

    อย่างไรก็ตาม ลูกค้า feedback บอกถึงความสะอาด เราต้องดูเลยว่า สาขาไหน ถ้าอยู่ในห้าง ร้านอื่นเป็นไหม หรือพนักงานที่สาขานั้นปิดร้านแล้ว

    ขาดมาตรการการดูแลรักษาตามกฎที่ตั้งไว้ หรือวัตกุดิบหมดอายุ เป็นต้น

ทั้งหมดเหล่านี้เป็นสิ่งที่เราต้อง สงสัย และต้อง Action หากได้ข้อมูลมาแล้ว เพื่อช่วยให้ธุรกิจร้านอาหารของเราเติบโตยั่งยืนได้อย่างมั่นคง ดังนั้น

ทั้งหมดนี้เป็นการสร้าง Database ด้วย SQL และ การดึงคอลัมน์และคำนวณ Basic Statistics เพื่อ Explore ดูว่าลูกค้ามีความคิดเห็นอย่างไรกับร้านอาหาร

ของเรา การ Action อาจจะมากกว่านี้ซึ่งเราก็จะต้องดึงข้อมูลมา และ Monitor เพื่อพัฒนาธุรกิจของเราต่อไป สำหรับตัวอย่างต่อไป

จะเป็นการสร้าง Table ด้วย ภาษา R ที่เป็นภาษาเก่าที่ที่ไว้ใช้ในงาน small data หรือคำนวณ Statistics แบบเน้นๆ โดยเราจะสร้างเหมือน SQL

แต่ใช้ Syntax R อย่างเดียวไม่มีการคำนวณค่า Basic Statistic เพื่อทบทวนความรู้ R

---

## 2 Create Tables and Perform INSERT Using R

```r

# สร้าง 9 คอลัมน์ ใน Transactions Table 
invoiceid <- c(1, 2, 3, 4, 5, 6, 7, 8, 9, 10) # สร้างคอลัมน์นี้เป็น Primary Key ชื่อ invoiceid
branchid1 <- c(1, 2, 3, 1, 2, 3, 1, 2, 3, 1) # สร้างคอลัมน์ brancnhid1 ใส่ 1 เพราะเป็น Foreign Key จาก Branch Table
customerid1 <- c(1, 2, 3, 3, 2, 5, 1, 2, 4, 4) # สร้างคอลัมน์ customerid1 ใส่ 1 เพราะเป็น Foreign Key จาก Customers Table
menuid1 <- c(1, 2, 3, 4, 5, 6, 7, 8, 1, 2) # สร้างคอลัมน์ menuid1 ใส่ 1 เพราะเป็น Foreign Key จาก Menus Table
commentid1 <- c(1, 4, 5, 2, 4, 6, 5, 5, 3, 3) # สร้างคอลัมน์ commentid1 ใส่ 1 เพราะเป็น Foreign Key จาก Feedback Table
invoicedate <- as.Date(c('2023-05-01', '2023-06-02', '2023-08-03', '2023-12-04', '2023-11-05', # สร้างคอลัมน์ invoicedate
                         '2023-03-06', '2023-02-07', '2023-09-08', '2023-05-09', '2023-08-10')) # และปรับเป็น Date Format
quantity <- c(4, 3, 4, 2, 1, 3, 3, 2, 3, 5) # สร้างคอลัมน์ quantity เพื่อดูว่าบิลที่ลูกค้าซื้อมีกี่รายการ
total_sales <- c(100.00, 200.00, 300.00, 400.00, 500.00, 600.00, 700.00, 800.00, 900.00, 1000.00) # สร้าง total_sales ว่ามูลค่าของบิลทั้งหมด


transactions <- data.frame(invoiceid, branchid1, customerid1, menuid1, commentid1, invoicedate, quantity, total_sales) # นำ 9 คอลัมน์
ทั้งหมดมารวมเป็น 1 ตารางด้วยการใช้คำสั่ง data.frame() 

# สร้าง 9 คอลัมน์ ใน Transactions Table Menus Table
menuid2 <- c(1, 2, 3, 4, 5, 6, 7, 8)
name_menu <- c('Pad Thai', 'Spaghetti', 'Coke', 'Cake', 'Fried Rice', 'Lasagna', 'Water', 'Ice Cream')
categories <- c('Rice', 'Pasta', 'Drinks', 'Dessert', 'Rice', 'Pasta', 'Drinks', 'Dessert')

menus <- data.frame(menuid2, name_menu, categories)

# Branch Table
branchid2 <- c(1, 2, 3)
name_branch <- c('Ratchayothin', 'Rama 7', 'ChokChai 4')
address <- c('Chatuchak', 'BangSue', 'Latphrao')
branch <- data.frame(branchid2, name_branch, address)

# Customers Table
customerid2 <- c(1, 2, 3, 4, 5)
name_customer <- c('John', 'Jane', 'Alex', 'Sara', 'Tom')
gender <- c('Male', 'Female', 'LGBTQ+', 'Female', 'Male')
status <- c('Member', 'Guest', 'Member', 'Guest', 'Member')
customers <- data.frame(customerid2, name_customer, gender, status)

# Feedback Table
commentid2 <- c(1, 2, 3, 4, 5, 6)
comment <- c('รสจัดเกิน', 'คุ้มราคา', 'เเพง', 'กลมกล่อม', 'บอกต่อ', 'เค็มเกิน')
emotional <- c('Negative', 'Positive', 'Negative', 'Positive', 'Positive', 'Negative')
feedback <- data.frame(commentid2, comment, emotional)

# Now all 5 data frames are defined and ready to be used.

con <- dbConnect(SQLite(), "HW3-restaurant.db") # create new file

# Writing Tables to SQLite Database using dbWriteTable()
# Assuming `con` is already connected to an SQLite database

dbWriteTable(con, "transactions", transactions)
dbWriteTable(con, "menus", menus)
dbWriteTable(con, "branch", branch)
dbWriteTable(con, "customers", customers)
dbWriteTable(con, "feedback", feedback) 

# Closing connection
dbDisconnect(con)

```



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






