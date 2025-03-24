# P1 : Data Exploration and Transformation with Google Sheets

## 📌 Table of Contents
1. [Filter & Sort Dynamic](#filter-and-sort-dynamic)
2. [Conditional Formatting: Highlight Row](#conditional-formatting-highlight-row)
     - 2.1 [Highlight Data Point เฉพาะ Perfomance ที่ Users กรองข้อมูล](#highlight-data-point-เฉพาะ-perfomance-ที่-users-กรองข้อมูล)
     - 2.2 [Highlight Variable Gender Column แบ่งตามสี](#highlight-variable-gender-column-แบ่งตามสี)
     - 2.3 [Highlight Variable Salary Column ไล่สเกลสูงไปต่ำ](#highlight-variable-salary-column-ไล่สเกลสูงไปต่ำ)
     - 2.4 [Highlight Variable 2 Column ชื่อพนักงานที่มีตัวเลข SNN นำหน้าตามเงื่อนไขที่กำหนด](#highlight-variable-2-column-ชื่อพนักงานที่มีตัวเลข-SNN-นำหน้าตามเงื่อนไขที่กำหนด)

---

## Filter and Sort Dynamic
```excel
=IFERROR(SORT(FILTER(EMPLOYEE, (GENDER = B2) * (PERFORMANCE = B3)), 5, Not(D2)),"NO DATA")
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

## Conditional Formatting: Highlight Row

### Highlight Data Point เฉพาะ Perfomance ที่ Users กรองข้อมูล

```excel
=$G2=$H$1
```
📌 **อธิบายสูตร:**

ก่อนอื่น Set Range ที่ต้องการ HCF ก่อนนะครับ นั่นคือ (`A2:G26`) ตามรูป
`=$G2=$H$1` ใช้เพื่อตรวจสอบว่า ค่าของแต่ละเซลล์ในคอลัมน์ G ตรงกับค่าที่อยู่ในเซลล์ `H1` หรือไม่
(`H1` คือ Dropdown List ของคอลัมน์ G) ถ้าตรงกัน HCF จะทำงานโดยการ Highlight ทั้ง data point(สีเขียว)

เพื่อให้เข้าใจชัดเจนมากยิ่งขึ้น ผมขอแบ่งเป็น 2 ส่วนเพื่อใช้อธิบายสูตร `=$G2=$H$1` ดังนี้
     
1. `$G2` ไล่เช็คคอลัมน์ G เท่านั้น โดยการไล่ไปที่ละแถวเป็น `G1, G2, G3, .., G26` ถ้าแต่ละค่าของ `G1, G2, G3, .., G26`
          matching กับ `$H$1` ตามข้อ 2..
2. `$H$1` ก็คือ Dropdown List ที่ค่าภายในคือค่ามาจากคอลัมน์ G 
          ไล่เช็คทุก cell ที่อยู่ในเฉพาะคอลัมน์ G สำหรับแถวที่อยู่ในช่วง แถวที่ 1 - แถวที่ 26 ในคอลัมน์ ถ้าหากเจอค่าที่ตรงกับค่าเฉพาะใน `$H$1`
          ให้ Highlight เฉพาะ data point นั้นๆ

---

### Highlight Variable Gender Column แบ่งตามสี

```excel
male
```
```excel
female
```

📌 **อธิบายสูตร:**
ก่อนอื่น Set Range ที่ต้องการ HCF เช่นเดิม (`F29:F53`) ตามรูป ผมก็จะแบ่งเป็น 2 เงื่อนไข คือ

1. ถ้าหาก `F29:F53` มีค่า male ก็จะให้เป็นสีครีม
2. ถ้าหาก `F29:F53` มีค่า female ก็เป็นสีแดง

ถ้าเข้าเงื่อนไขใด เงื่อนไขนึงจะแสดงตามรูปตัวอย่าง

---

### Highlight Variable Salary Column ไล่สเกลสูงไปต่ำ

📌 **อธิบายเงื่อนไขการใช้กฎ:**

ก่อนอื่น Set Range ที่ต้องการ HCF เช่นเดิม (`E56:E80`) ตามรูป
จากนั้นเลือก color scale ระบบก็จะทำการ default setting ให้เลยอัตโนมัติ
หรือเราก็อาจจะปรับตามสีที่เราต้องการ เพื่อให้เหมาะสมกับความเข้าใจของ users

---

### Highlight Variable 2 Column ชื่อพนักงานที่มีตัวเลข SNN นำหน้าตามเงื่อนไขที่กำหนด

```excel
=LEFT($A83,1)="0"
```

📌 **อธิบายสูตร:**

ก่อนอื่น Set Range ที่ต้องการ HCF ก่นนะครับ นั่นคือ (`A83:B107`) ตามรูป

`=LEFT($A83,1)="0"` ผมขอแบ่งเป็น 2 ส่วนเพื่ออธิบาย ดังนี้

1. สูตร `=LEFT("Phubordin", 1)` จะคืนค่าผลลัพธ์ตัวที่ `1` นับจากซ้ายไปขวา ผลลัพธ์ของสูตรนี้คือ `P`
2. ถ้าเรา apply กับ `=LEFT($A83,1)="0"` จะเป็นการทดสอบเงื่อนไขว่า ค่าเซลล์ `A83, A84, A85, .., A107` แต่ละค่านั้น
   นับจากทางซ้ายไปขวา โดยเอาตัวอักษรตัวแรกมา แล้วนำไปทดสอบว่าเท่า `0` ไหม?
   - ถ้าเท่ากับ 0 ให้ดำเนินการให้ Highlight Color Scale ที่เรา setting
   - ถ้าไม่ ก็ไม่ต้อง action ใดๆ

---
