# P1 : Data Exploration and Transformation with Google Sheets

## 📌 Table of Contents
- [Filter & Sort Dynamic](#filter-and-sort-dynamic)
---

## Filter and Sort Dynamic
```excel
=IFERROR(SORT(FILTER(EMPLOYEE, (GENDER = B2) * (PERFORMANCE = B3)), 5, Not(D2)),"NO DATA")
```
📌 **อธิบายสูตร:**  ผมขออนุญาตแบ่งเป็น 3 ส่วนดังนี้
1. `FILTER(EMPLOYEE, (GENDER = B2) * (PERFORMANCE = B3))`
   - ผมตั้งชื่อ range ต่างๆที่มีชื่อว่า `EMPLOYEE`(Table), `GENDER`(Column), `PERFORMANCE`(Column) เพื่อง่ายต่อการเลือกช่วง cell มาใช้
     ผมจึงเลือกช่วง `EMPLOYEE` โดยที่เพศ คือ cell `B2` ที่ Dynamic และ`*` ผลการปฏิบัติงาน คือ cell `B3` ที่ Dynamic
     ผลลัพธืจึงถูก Filter ออกมา หลังจากนั้น..
     
2. `SORT(FILTER(..ข้อ 1), 5, Not(D2))`
   - ผมเรียงลำดับ `Salary` จากมากไปน้อย โดยที่ `Salary` อยู่คอลัมน์ที่ `5` และ Default ของการ Sort ที่จะเรียงจากน้อยไปมากได้ก็ต่อเมื่อมีค่า TRUE
     ในอาร์กิวเมนต์ที่ 3 ของ Sort ดังนั้น ผมจึงเลือกคอลัมน์ `Salary` และเรียงลำดับตาม cell `D2` เป็น Checkbox เพื่อให้มีความ Dynamic เมื่อ users
     ติ้ก D2 = True ซึ่งมันจะเรียงจากน้อยไปมาก ดังนั้นผมจึงใช้ `NOT(D2)` เพื่อบังคับให้การติ้กของ users นั้นเรียง `Salary` จากมากไปน้อยโดยอัตโนมัติ
    
4. `IFERROR(..ข้อ 2,"NO DATA")`
   - ถ้าหาก Formula ข้อ 1 หรือ 2 ส่งผลลัพธ์ Error จะให้แสดง `NO DATA` แต่แน่นอนว่าในตาราง `EMPLOYEE` จะต้องมีการ filter ที่ไม่ match กัน
     นั้นหมายความว่าไม่มีค่า filter ที่ต้องการดังนั้นผลลัพธ์จึงแสดง `NO DATA` นั่นเอง !

📌 **ตัวอย่าง:**  

| ssn         | lastname  | firstname | hiredate | salary | gender | performance |
|-------------|-----------|-----------|----------|--------|--------|-------------|
| 925-45-7116 | Whitehead | David     | 29427    | 175000 | Male   | Good        |
| 500-50-0505 | Rodriguez | Jose      | 35992    | 150000 | Male   | Good        |
| 444-45-4444 | Frank     | Vernon    | 31147    | 75000  | Male   | Good        |
| 333-43-4444 | Smith     | Frank     | 33267    | 65000  | Male   | Good        |
| 432-19-8765 | Bronson   | Paul      | 37945    | 58000  | Male   | Good        |
| 109-87-6544 | Foster    | Harold    | 38578    | 55000  | Male   | Good        |
| 767-74-7373 | Martin    | William   | 38955    | 23000  | Male   | Good        |

---

## **2️⃣ ใช้ตารางเพื่อแสดงตัวอย่าง Input และ Output**  
> 📊 **ช่วยให้ Users เข้าใจผลลัพธ์ได้ง่ายขึ้น**  

| ยอดขาย (B2) | โบนัสที่ได้ (สูตร `=IF(B2>100000, B2*10%, B2*5%)`) |
|-------------|-------------------------------------|
| 120,000     | 12,000 (10%) |
| 80,000      | 4,000 (5%) |
| 150,000     | 15,000 (10%) |

=A1 + B1
=sum(A1:C4)


