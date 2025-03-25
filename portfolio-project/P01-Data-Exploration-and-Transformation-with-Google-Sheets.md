# P1 : Data Exploration and Transformation with Google Sheets

## 📌 Table of Contents
1. [Filter & Sort Dynamic](#filter-and-sort-dynamic)
2. [Conditional Formatting: Highlight Row](#conditional-formatting-highlight-row)
     - 2.1 [Highlight Data Point เฉพาะ Perfomance ที่ Users กรองข้อมูล](#highlight-data-point-เฉพาะ-perfomance-ที่-users-กรองข้อมูล)
     - 2.2 [Highlight Variable Gender Column แบ่งตามสี](#highlight-variable-gender-column-แบ่งตามสี)
     - 2.3 [Highlight Variable Salary Column ไล่สเกลสูงไปต่ำ](#highlight-variable-salary-column-ไล่สเกลสูงไปต่ำ)
     - 2.4 [Highlight Variable 2 Column ชื่อพนักงานที่มีตัวเลข SNN นำหน้าตามเงื่อนไขที่กำหนด](#highlight-variable-2-column-ชื่อพนักงานที่มีตัวเลข-SNN-นำหน้าตามเงื่อนไขที่กำหนด)
3. [Dynamic Query](#dynamic-query)
4. [Vlookup](#vlookup)
5. [Convert Date](#convert-date)
6. [Regular Expression](#regular-expression)

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

![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-1-6.gif)
![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-1-6.png)


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

📌 **ตัวอย่าง:**

![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter.gif)
![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter.png)

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

📌 **ตัวอย่าง:**

![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter1.gif)
![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter1.png)

---

### Highlight Variable Salary Column ไล่สเกลสูงไปต่ำ

📌 **อธิบายเงื่อนไขการใช้กฎ:**

ก่อนอื่น Set Range ที่ต้องการ HCF เช่นเดิม (`E56:E80`) ตามรูป
จากนั้นเลือก color scale ระบบก็จะทำการ default setting ให้เลยอัตโนมัติ
หรือเราก็อาจจะปรับตามสีที่เราต้องการ เพื่อให้เหมาะสมกับความเข้าใจของ users

📌 **ตัวอย่าง:**

![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter2.gif)
![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter2.png)

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

📌 **ตัวอย่าง:**

![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter3.gif)
![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter3.png)

---

## Dynamic Query
```excel
=QUERY(EMPLOYEE1, 
"select * where " &
IF(B2="All","1=1","N='" & B2 & "'") &
"And " & IF(B3="all","1=1","O = '" & B3 & "'")  &
"And " & IF(B4="All","1=1","L <= date'"& Text(B4,"yyyy-mm-dd") & "'"))
```
📌 **อธิบายสูตร:**

ก่อนอื่นขอผมอธิบายถึง
     - `EMPLOYEE1` แทนด้วยช่วงข้อมูล ตามรูปครับ
     - `B2` แทนด้วย Dropdown List Gender ที่อยู่ในช่วง `EMPLOYEE1`
     - `B3` แทนด้วย Dropdown List Performance ที่อยู่ในช่วง `EMPLOYEE1`
     - `B4` แทนด้วย Dropdown List Hiredate ที่อยู่ในช่วง `EMPLOYEE1`
     
จากนั้นผมขออนุญาตอธิบายโดยแบ่งเป็น 8 ส่วน (โปรดอ่านตามลำดับ) โดยที่ส่วนที่ 2 - 8 คือ `text` สังเกตได้จาก `"`
ดังนั้นตอนท้ายจะถูกนำมาเชื่อมกันด้วย `&` เพื่อให้ชัดเจนยิ่งขึ้นผมขออธิบาย ดังต่อไปนี้

1. `QUERY(EMPLOYEE1, "your query text")`
   - `QUERY()` ใช้คล้ายๆกับภาษา SQL ซึ่งมันไว้ใช้กับการจัดการฐานข้อมูล เช่น select, where, order by, groupby etc.
     โดยที่จะรับค่าพารามิเตอร์อยู่ 2 ตัวหลักๆ ตามตัวอย่างผมจะใช้สูตร `QUERY(EMPLOYEE1, "your query text"` ที่ซึ่งค่าแต่ละค่าแทนด้วย
     `EMPLOYEE1` ช่วงของข้อมูลตามรูป และ `your query text` การเขียน query ของเราเพื่อดึงข้อมูล ซึ่งจะเริ่มเขียนอธิบายตั้งแต่ (ข้อ 2 - ข้อ 8)
     
2. `select * where " &`
   - เลือกทุกคอลัมน์ในช่วง `EMPLOYEE1` โดยที่จะเขียนเงื่อนไขต่อจาก `where` ตั้งแต่ข้อ 3 ถึง 8 เลย
    
3. `IF(B2="All","1=1","N='" & B2 & "'") &`
   สูตร `IF(เงื่อนไข,1,0)` คือ ถ้าเงื่อนไขเป็นจริงจะแสดงผลลัพธ์ 1 ถ้าไม่จริงะแสดงผลลัพธ์ 0 ดังนั้น
     - ถ้า users เลือก Dropdown List เป็น `All` จะแสดงผล 1=1 ซึ่ง 1=1 จะคืนค่าความจริงจะทำให้ คำสั่ง `"select * where 1=1"` แสดงอัติโนมัติ
     - ถ้า users เลือก Dropdown List ไม่เป็น `All` จะแสดงผล `"N='" & B2 & "'"`
          - ถ้าหาก `B2` ถูกเลือกเป็น `male` จะแสดงเป็น `"select * where N = 'male'"` ตามตารางด้านล่าง
            | SSN         | LASTNAME  | FIRST NAME | HIREDATE   | SALARY   | *GENDER* | PERFORMANCE |
            |-------------|-----------|------------|------------|----------|--------|-------------|
            | 109-87-6544 | Foster    | Harold     | 2005-08-14 | $55,000  | Male   | Good        |
            | 222-23-2222 | Marlin    | Bill       | 1977-03-28 | $125,000 | Male   |             |
            | 333-43-4444 | Smith     | Frank      | 1991-01-29 | $65,000  | Male   | Good        |
            | 432-19-8765 | Bronson   | Paul       | 2003-11-20 | $58,000  | Male   | Good        |
            | 444-45-4444 | Frank     | Vernon     | 1985-04-10 | $75,000  | Male   | Good        |
            | 464-64-4466 | Webster   | David      | 1991-01-29 | $58,500  | Male   | Excellent   |
            | 500-50-0505 | Rodriguez | Jose       | 1998-07-16 | $150,000 | Male   | Good        |
            | 555-56-5555 | Charles   | Kenneth    | 1998-06-18 | $40,000  | Male   | Excellent   |
            | 767-74-7373 | Martin    | William    | 2006-08-26 | $23,000  | Male   | Good        |
            | 776-67-6666 | Adamson   | David      | 2002-10-04 | $52,000  | Male   | Excellent   |
            | 925-45-7116 | Whitehead | David      | 1980-07-25 | $175,000 | Male   | Good        |
          
          - ถ้าหาก `B2` ถูกเลือกเป็น `female` จะแสดงเป็น `select * where N = 'female'` ตามตารางด้านล่าง
     
   
5. `"And " &`
6. `IF(B3="all","1=1","O = '" & B3 & "'")  &`
7. `"And " &`
8. `IF(B4="All","1=1","L <= date'"& Text(B4,"yyyy-mm-dd") &`
9. `"'"`

📌 **ตัวอย่าง:**

![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-3-6.gif)
![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-3-6-0.png)
![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-3-6.png)

## Vlookup

📌 **ตัวอย่าง:**

![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-4-6.gif)
![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-4-6.png)

## Convert Date

📌 **ตัวอย่าง:**

![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-5-6.gif)
![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-5-6.png)

## Regular Expression

📌 **ตัวอย่าง:**

![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-6-6.gif)
![Highlight Row](https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-6-6.png)








