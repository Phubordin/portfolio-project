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

📌 **ตัวอย่าง:** [แนะนำให้ลองดูใน Sheet: Click](https://docs.google.com/spreadsheets/d/1a3l_9Lgr_G6m5DkfvEdUg4a3fpwKmLog1oEyewA8Zg4/edit?usp=sharing)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-1-6.gif" alt="Highlight Row">
</p>

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-1-6.png" alt="Highlight Row">
</p>

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

📌 **ตัวอย่าง:** [แนะนำให้ลองดูใน Sheet: Click](https://docs.google.com/spreadsheets/d/1a3l_9Lgr_G6m5DkfvEdUg4a3fpwKmLog1oEyewA8Zg4/edit?usp=sharing)


<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter.gif" alt="Highlight Row">
</p>

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter.png" alt="Highlight Row">
</p>

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

📌 **ตัวอย่าง:** [แนะนำให้ลองดูใน Sheet: Click](https://docs.google.com/spreadsheets/d/1a3l_9Lgr_G6m5DkfvEdUg4a3fpwKmLog1oEyewA8Zg4/edit?usp=sharing)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter1.gif" alt="Highlight Row">
</p>

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter1.png" alt="Highlight Row">
</p>

---

### Highlight Variable Salary Column ไล่สเกลสูงไปต่ำ

📌 **อธิบายเงื่อนไขการใช้กฎ:**

ก่อนอื่น Set Range ที่ต้องการ HCF เช่นเดิม (`E56:E80`) ตามรูป
จากนั้นเลือก color scale ระบบก็จะทำการ default setting ให้เลยอัตโนมัติ
หรือเราก็อาจจะปรับตามสีที่เราต้องการ เพื่อให้เหมาะสมกับความเข้าใจของ users

📌 **ตัวอย่าง:** [แนะนำให้ลองดูใน Sheet: Click](https://docs.google.com/spreadsheets/d/1a3l_9Lgr_G6m5DkfvEdUg4a3fpwKmLog1oEyewA8Zg4/edit?usp=sharing)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter2.png" alt="Highlight Row">
</p>

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter2.png" alt="Highlight Row">
</p>

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


<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter3.png" alt="Highlight Row">
</p>

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/hcf-filter3.png" alt="Highlight Row">
</p>

---

## Dynamic Query
```excel
=QUERY(EMPLOYEE1, 
"select * where " &
IF(B2="All","1=1","N='" & B2 & "'") &
"And " & IF(B3="all","1=1","O = '" & B3 & "'")  &
"And " & IF(B4="All","1=1","L <= date'"& Text(B4,"yyyy-mm-dd") & "'"))
```

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-3-6-0.png" alt="Highlight Row">
</p>

📌 **อธิบายสูตร:**
- `EMPLOYEE1` แทนด้วยช่วงข้อมูล ตามรูปครับ
- `B2` แทนด้วย Dropdown List Gender ที่อยู่ในช่วง `EMPLOYEE1`
- `B3` แทนด้วย Dropdown List Performance ที่อยู่ในช่วง `EMPLOYEE1`
- `B4` แทนด้วย Dropdown List Hiredate ที่อยู่ในช่วง `EMPLOYEE1`
     
จากนั้นผมขออนุญาตอธิบายโดยแบ่งเป็น 7 ส่วน (โปรดอ่านตามลำดับ) โดยที่ส่วนที่ 2 - 7 คือ `text` สังเกตได้จาก `"`
ดังนั้นตอนท้ายจะถูกนำมาเชื่อมกันด้วย `&` เพื่อให้ชัดเจนยิ่งขึ้นผมขออธิบาย ดังต่อไปนี้

1. `QUERY(EMPLOYEE1, "your query text")`

   `QUERY()` ใช้คล้ายๆกับภาษา SQL ซึ่งมันไว้ใช้กับการจัดการฐานข้อมูล เช่น select, where, order by, groupby etc.
   โดยที่จะรับค่าพารามิเตอร์อยู่ 2 ตัวหลักๆ ตามตัวอย่างผมจะใช้สูตร `QUERY(EMPLOYEE1, "your query text"` ที่ซึ่งค่าแต่ละค่าแทนด้วย
   `EMPLOYEE1` ช่วงของข้อมูลตามรูป และ `your query text` การเขียน query ของเราเพื่อดึงข้อมูล ซึ่งจะเริ่มเขียนอธิบายตั้งแต่ (ข้อ 2 - ข้อ 7)
     
2. `select * where " &`

   เลือกทุกคอลัมน์ในช่วง `EMPLOYEE1` โดยที่จะเขียนเงื่อนไขต่อจาก `where` ตั้งแต่ข้อ 3 ถึง 7 เลย
    
3. `IF(B2="All","1=1","N='" & B2 & "'") &`

   สูตร `IF(เงื่อนไข,1,0)` คือ ถ้าเงื่อนไขเป็นจริงจะแสดงผลลัพธ์ 1 ถ้าไม่จริงะแสดงผลลัพธ์ 0 ดังนั้น
     - ถ้า users เลือก Dropdown List เป็น `All` จะแสดงผล 1=1 ซึ่ง 1=1 จะคืนค่าความจริงจะทำให้ คำสั่ง `"select * where 1=1"` แสดงอัติโนมัติ
     - ถ้า users เลือก Dropdown List ไม่เป็น `All` จะแสดงผล `"N='" & B2 & "'"`
          - ถ้าหาก `B2` ถูกเลือกเป็น `male` จะแสดงเป็น `"select * where N = 'male'"`
            | SSN         | LASTNAME  | FIRST NAME | HIREDATE   | SALARY   | **GENDER** | PERFORMANCE |
            |-------------|-----------|------------|------------|----------|------------|-------------|
            | 109-87-6544 | Foster    | Harold     | 2005-08-14 | $55,000  | **Male**   | Good        |
            | 222-23-2222 | Marlin    | Bill       | 1977-03-28 | $125,000 | **Male**   |             |
            | 333-43-4444 | Smith     | Frank      | 1991-01-29 | $65,000  | **Male**   | Good        |
            | 432-19-8765 | Bronson   | Paul       | 2003-11-20 | $58,000  | **Male**   | Good        |
            | 444-45-4444 | Frank     | Vernon     | 1985-04-10 | $75,000  | **Male**   | Good        |
            | 464-64-4466 | Webster   | David      | 1991-01-29 | $58,500  | **Male**   | Excellent   |
            | 500-50-0505 | Rodriguez | Jose       | 1998-07-16 | $150,000 | **Male**   | Good        |
            | 555-56-5555 | Charles   | Kenneth    | 1998-06-18 | $40,000  | **Male**   | Excellent   |
            | 767-74-7373 | Martin    | William    | 2006-08-26 | $23,000  | **Male**   | Good        |
            | 776-67-6666 | Adamson   | David      | 2002-10-04 | $52,000  | **Male**   | Excellent   |
            | 925-45-7116 | Whitehead | David      | 1980-07-25 | $175,000 | **Male**   | Good        |
          
          - ถ้าหาก `B2` ถูกเลือกเป็น `female` จะแสดงเป็น `select * where N = 'female'` ตามตารางด้านล่าง
            | SSN         | LASTNAME | FIRST NAME | HIREDATE   | SALARY  | **GENDER** | PERFORMANCE |
            |-------------|----------|------------|------------|---------|------------|-------------|
            | 000-01-0000 | Milgrom  | Patricia   | 2004-10-01 | $57,500 | **Female** | Average     |
            | 000-02-2222 | Adams    | Sandy      | 2001-01-15 | $19,500 | **Female** | Excellent   |
            | 109-87-6543 | Wood     | Emily      | 1997-03-12 | $69,000 | **Female** | Excellent   |
            | 111-12-1111 | Johnson  | James      | 1996-05-03 | $47,500 | **Female** | Good        |
            | 222-52-5555 | Smith    | Mary       | 2006-01-01 | $42,500 | **Female** | Average     |
            | 245-67-8910 | Johanson | Sandy      | 2005-06-02 | $69,000 | **Female** |             |
            | 333-34-3333 | Manin    | Emily      | 2000-12-01 | $49,500 | **Female** | Average     |
            | 333-66-1234 | Brown    | Marietta   | 2001-03-07 | $18,500 | **Female** | Excellent   |
            | 335-55-5533 | Jones    | Holly      | 1986-04-08 | $65,000 | **Female** | Good        |
            | 555-22-3333 | Rubin    | Patricia   | 2003-07-25 | $45,000 | **Female** | Average     |
            | 612-99-1111 | Roberts  | Melissa    | 1984-05-14 | $79,000 | **Female** | Good        |
            | 625-62-6262 | Holmes   | Holly      | 1992-06-15 | $55,000 | **Female** | Average     |
            | 777-78-7777 | Marder   | Kelly      | 1997-09-25 | $38,500 | **Female** | Average     |
              
4. `"And " &`

   เพื่อให้ชัดเจนผมขอยกตัวอย่าง ถ้าหาก users เลือก `B2` เป็น `female` จะเป็น `select * where N = 'female'`
   ถ้าเพิ่ม ข้อ 4 `"And " &` ลงไปจะให้ภาพรวมเป็นแบบนี้ `select * where N = 'female' And` ส่วนที่จะเขียนต่อไป
   จะแสดงข้อถัดไป

5. `IF(B3="all","1=1","O = '" & B3 & "'")  &`

   ในส่วนนี้จะคล้ายข้อ 2 ที่ผ่านมาแค่เปลี่ยนจาก `B2` เป็น `B3` นั่นคือเลือก `Performance` ผมขอข้ามประเด็นเรื่อง `IF()` และ `1=1` ไปสามารถทบทวนข้อ 2 ใหม่ได้
   แต่ถ้า users เลือกอันอื่นที่ไม่ใช่ `All` ซึ่งเป็นไปได้ 3 แบบคือ Good, Average, Excellent
     - `select * where N = 'female' And O = 'Good'`
        | SSN         | LASTNAME  | FIRST NAME | HIREDATE   | SALARY   | GENDER | **PERFORMANCE** |
        |-------------|-----------|------------|------------|----------|--------|-----------------|
        | 109-87-6544 | Foster    | Harold     | 2005-08-14 | $55,000  | Male   | **Good**        |
        | 111-12-1111 | Johnson   | James      | 1996-05-03 | $47,500  | Female | **Good**        |
        | 123-45-6789 | Coulter   | Tracy      | 1993-02-14 | $100,000 |        | **Good**        |
        | 333-43-4444 | Smith     | Frank      | 1991-01-29 | $65,000  | Male   | **Good**        |
        | 335-55-5533 | Jones     | Holly      | 1986-04-08 | $65,000  | Female | **Good**        |
        | 432-19-8765 | Bronson   | Paul       | 2003-11-20 | $58,000  | Male   | **Good**        |
        | 444-45-4444 | Frank     | Vernon     | 1985-04-10 | $75,000  | Male   | **Good**        |
        | 500-50-0505 | Rodriguez | Jose       | 1998-07-16 | $150,000 | Male   | **Good**        |
        | 612-99-1111 | Roberts   | Melissa    | 1984-05-14 | $79,000  | Female | **Good**        |
        | 767-74-7373 | Martin    | William    | 2006-08-26 | $23,000  | Male   | **Good**        |
        | 925-45-7116 | Whitehead | David      | 1980-07-25 | $175,000 | Male   | **Good**        |
       
     - `select * where N = 'female' And O = 'Average'`
       | SSN         | LASTNAME | FIRST NAME | HIREDATE   | SALARY  | GENDER | **PERFORMANCE** |
       |-------------|----------|------------|------------|---------|--------|-----------------|
       | 000-01-0000 | Milgrom  | Patricia   | 2004-10-01 | $57,500 | Female | **Average**     |
       | 222-52-5555 | Smith    | Mary       | 2006-01-01 | $42,500 | Female | **Average**     |
       | 333-34-3333 | Manin    | Emily      | 2000-12-01 | $49,500 | Female | **Average**     |
       | 555-22-3333 | Rubin    | Patricia   | 2003-07-25 | $45,000 | Female | **Average**     |
       | 625-62-6262 | Holmes   | Holly      | 1992-06-15 | $55,000 | Female | **Average**     |
       | 777-78-7777 | Marder   | Kelly      | 1997-09-25 | $38,500 | Female | **Average**     |
     
     - `select * where N = 'female' And O = 'Excellent'`
       | SSN         | LASTNAME | FIRST NAME | HIREDATE   | SALARY  | GENDER | **PERFORMANCE** |
       |-------------|----------|------------|------------|---------|--------|-----------------|
       | 000-02-2222 | Adams    | Sandy      | 2001-01-15 | $19,500 | Female | **Excellent**   |
       | 109-87-6543 | Wood     | Emily      | 1997-03-12 | $69,000 | Female | **Excellent**   |
       | 333-66-1234 | Brown    | Marietta   | 2001-03-07 | $18,500 | Female | **Excellent**   |
       | 464-64-4466 | Webster  | David      | 1991-01-29 | $58,500 | Male   | **Excellent**   |
       | 555-56-5555 | Charles  | Kenneth    | 1998-06-18 | $40,000 | Male   | **Excellent**   |
       | 776-67-6666 | Adamson  | David      | 2002-10-04 | $52,000 | Male   | **Excellent**   |

6. `"And " &`

   เหมือนข้อ 4 เลย ถ้ารวมคำสั่งข้อ 6 ลงไปด้วยจะทำให้สูตรทั้งหมดเป็น `select * where N = 'female' And O = 'Excellent' And`
   
7. `IF(B4="All","1=1","L <= date'"& Text(B4,"yyyy-mm-dd") & "'"`

   เหมือนข้อ 5 และ ข้อ 3 แต่ผลลัพธ์จะสื่อถึงพนักงานคนไหนที่เริ่มทำงานก่อนวันไหน หรือเริ่มทำงานวันที่เท่าไร ซึ่งขึ้นอยู่กับ users กด Dropdown List เลือก
    กล่าวคือให้โฟกัสที่ `L <= date'"& Text(B4,"yyyy-mm-dd")`
        - เราปรับ format วันที่เป็นมาตรฐาน ISO โดยคำสั่ง `Text(B4,"yyyy-mm-dd")`
        - เมื่อปรับ date format ได้แล้ว จะได้ภาพรวมของสูตรดังนี้ `L <= date'yyyy-mm-dd")'`
   กล่าวคือ `L <= date'yyyy-mm-dd")'` จะเลือกข้อมูล วันที่พนักงานเริ่มทำงานหรือก่อนวันนั้นที่ users เลือกใน Dropdone List (`B4`)
   ถ้า users เลือก `B4` เท่ากับ `2004-10-01` และเอาสูตรจากข้อ 6 มาต่อก็จะเป็น `select * where N = 'female' And O = 'Excellent' And L <= date'2004-10-01`

📌 **สรุปผลลัพธ์:**

  เพื่อง่ายต่อการเข้าใจ ขออนุญาตยกตัวอย่างการใช้งาน
       - `B2` เท่ากับ female
       - `B3` เท่ากับ Excellent
       - `B4` เท่ากับ 2004-10-01
  ทำให้ `your query text` เท่ากับ `select * where N = 'female' And O = 'Excellent' And L <= date'2004-10-01`
  ดังนั้น นี่คือสูตรเต็มของ `QUERY()`
  
  ```excel
  =QUERY(EMPLOYEE1,"select * where N = 'female' And O = 'Excellent' And L <= date'2004-10-01")
  ```

  ถ้าหากอยากได้เป็นสูตรทั่วไปโดยไม่กำหนดค่า `B2, B3, B4` เพื่อรอ users ป้อน
  
  ```excel
  =QUERY(EMPLOYEE1, 
  "select * where " &
  IF(B2="All","1=1","N='" & B2 & "'") &
  "And " & IF(B3="all","1=1","O = '" & B3 & "'")  &
  "And " & IF(B4="All","1=1","L <= date'"& Text(B4,"yyyy-mm-dd") & "'"))
  ```
  
📌 **ตัวอย่าง:** [แนะนำให้ลองดูใน Sheet: Click](https://docs.google.com/spreadsheets/d/1a3l_9Lgr_G6m5DkfvEdUg4a3fpwKmLog1oEyewA8Zg4/edit?usp=sharing)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-3-6.gif" alt="Highlight Row">
</p>

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-3-6.png" alt="Highlight Row">
</p>

## Vlookup

```excel
=ArrayFormula(VLOOKUP(I4:I28,A32:F39,{2 ,3 ,4 ,5 ,6},FALSE))
```

```excel
=ArrayFormula(VLOOKUP(H4:H28,A43:E46, {2, 3 ,4, 5},FALSE))
```

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-4-6.png" alt="Highlight Row">
</p>

📌 **อธิบายสูตร:**

สูตร `Vlookup` และการทำเป็น `ArrayFormula` คืออะไร?
- `Vlookup` จะคืนค่าผลลัพธ์จาก cell ที่เรามี ที่เราอ้างอิงจากอีก table (ภายใน table เดียวกันได้)
- `ArrayFormula` จะคืนค่าหลายๆ cell แทนที่จะเป็น cell เดียว

ดังนั้น ผมขออนุญาตแบ่งเป็น 2 สูตรมี สูตรบนกับสูตรล่าง 
- สูตรบน จะแทนด้วย สูตรซ้ายมือ ตามภาพ
- สูตรล่าง จะแทนด้วย สูตรขวามือ ตามภาพ

1. สูตรบน `=ArrayFormula(VLOOKUP(I4:I28,A32:F39,{2 ,3 ,4 ,5 ,6},FALSE))`
   
   ผมขออธิบายส่วนที่ไม่มี `Arrayformula` ก่อน `VLOOKUP(I4:I28,A32:F39,{2 ,3 ,4 ,5 ,6},FALSE))`
   สูตรนี้จะทำงานโดย ค่าในช่วง `I4:I28` มีค่าไหนที่สอดคล้องกับ `A32:A39` ถ้า match กันเจอให้คืนค่าที่จับคู่กันได้จากช่วง `B32:F39` ออกมา
   เพราะว่าเราเลือกที่คอลัมน์ที่ 2, 3, 4, 5, 6 เราเลยใช้ `{2 ,3 ,4 ,5 ,6}` ซึ่งก็คือช่วง `B32:F39` นั่นเอง
   ซึ่งทำให้ผลลัพธ์ที่ได้จะคืนค่าเเค่ cell เดียวที่เขียนสูตร `Vlookup` ลงไป เพื่อให้คืนค่าหลายๆ cell เราจึงเลือกใช้ `ArrayFormula` ซึ่งจะสูตรเต็มคือ
   `=ArrayFormula(VLOOKUP(I4:I28,A32:F39,{2 ,3 ,4 ,5 ,6},FALSE))` ผลลัพธ์จะได้รูปตัวอย่าง
     
2. สูตรล่าง `=ArrayFormula(VLOOKUP(H4:H28,A43:E46, {2, 3 ,4, 5},FALSE))`
   
   คล้ายกับข้อ 1 แค่เปลี่ยน parameter 1 กับ 2 และช่วงที่อยากได้ค่านั้นว่าอยู่ที่คอลัมน์ 2, 3, 4, 5 การทำให้เป็น FALSE หรือ 0 บ่งบอกถึงคืนค่านั้นตรงๆ ไม่ต้องไปเอา
   ค่าที่รองลงมาจากแถว หรือค่าที่ถัดไปจากแถว return กลับมา ต่อไปเราจะลองใช้ `Vlookup` กับการแปลงวันที่ (Convert Date) ในตัวอย่างถัดไป
    
📌 **ตัวอย่าง:** [แนะนำให้ลองดูใน Sheet: Click](https://docs.google.com/spreadsheets/d/1a3l_9Lgr_G6m5DkfvEdUg4a3fpwKmLog1oEyewA8Zg4/edit?usp=sharing)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-4-6.gif" alt="Highlight Row">
</p>

## Convert Date

```excel
=ArrayFormula(SPLIT(A4:A9," "))
```

```excel
=ArrayFormula(DATE(D4:D9-543,VLOOKUP(C4:C9,$A$13:$B$24,2,0),B4:B9))
```

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-5-6.png" alt="Highlight Row">
</p>

จากภาพ จะเป็นการแปลงจากวันที่ภาษาไทย ให้กลายเป็นวันที่มาตฐาณ ISO โดยใช้ 2 สูตรหลักคือ `SPLIT()`, `DATE` และ `VLOOKUP`
ก่อนอื่นผมขออธิบายช่วงต่างๆที่มีในสูตร

- `A4:A9` แทนด้วย ช่วงของวันที่เดิม(วันที่เต็มภาษาไทย วันที่ เดือน ปี พ.ศ.) ซึ่งเราจะเปลี่ยนภายหลัง
- `D4:D9` แทนด้วย ปี พ.ศ. ซึ่งเราจะเปลี่ยนภายหลัง
- `C4:C9` แทนด้วย เดือน ภาษาไทย ซึ่งเราจะใช้ `VLOOKUP` เข้ามา transform โดยอิงจากตารางที่อยู่ในส่วนที่ 1 ของวงกลมสีแดง
- `$A$13:$B$24` แทนด้วย ช่วงอ้างอิงส่วนที่ 1 ของวงกลมสีแดง ที่เราสร้างขึ้นเพื่อจะดุงด่าเหล่านั้นออกมา
- `B4:B9` แทนด้วย เฉพาะวันที่เท่านั้น

เมื่อเรามองดูภาพรวมของช่วงข้อมูลเบื้องต้นแล้ว ผมขออธิบายขั้นตอนต่อไป ซึ่งจะแบ่งออกเป็น 3 ส่วน ดังต่อไปนี้ ตามรูป

1. เราต้องการสร้างตารางเดือน months format ให้สอดคล้องกับที่มีในตารางข้อมูลของเรา โดยเราต้องเรียงลำดับของเดือนดังกล่าวไว้เพ่ืออ้างอิงด้วย

2. `=ArrayFormula(SPLIT(A4:A9," "))`

   ArrayFormula ผมได้อธิบายไว้หัวข้อ `Vlookup` แล้วพูดง่ายๆมันจะคืนค่าหลายๆ cell ออกมาตามช่วงที่เราอ้างอิง
   ส่วน `SPLIT(A4:A9," ")` จะทำการแบ่งข้อความในเซลล์ออกมาเป็นส่วนๆแบ่งจากค่า white space 1 ช่อง
   ซึ่งผลลัพะฺที่ได้จะแสดงแค่ 1 แถว ดังนั้นเราจึงใช้ ArraryFomular เข้ามาช่วยจะได้ว่า
   `=ArrayFormula(SPLIT(A4:A9," "))` สามารถดูได้จากรูปตัวอย่าง

3. `=ArrayFormula(DATE(D4:D9-543,VLOOKUP(C4:C9,$A$13:$B$24,2,0),B4:B9))`

   ข้อนี้จะทำได้ก็ต่อเมื่อทำข้อ 1-2 สำเร็จ ผมขออนุญาตแบ่งออกเป็น 2 ส่วนเพื่ออธิบายดังนี้

   - `VLOOKUP(C4:C9,$A$13:$B$24,2,0),B4:B9)`

     จะเป็นการคืนค่าอ้างอิงจากตารางที่สร้างในข้อ 1 ซึ่งก็คือเดือนที่เป็นตัวเลขที่ตั้งค่าไว้
   
   - `DATE(D4:D9-543,VLOOKUP(C4:C9,$A$13:$B$24,2,0),B4:B9))`
          `DATE(ปี, เดือน, วัน)`

     - `D4:D9-543` ทำให้เป็นปี ค.ศ. โดย(พ.ศ. - 543)
     - ได้จาก `Vlookp` ที่บอกไปเมื่อสักครู่
     - `B4:B9` วันที่ก็เหมือนเดิม (เพราะเป็นเลขที่ถูกแล้วถ้าเป็นเลขไทย อาจจะต้องสร้างตารางอ้างอิงเพิ่ม)

📌 **สรุปผลลัพธ์:**

เราสามารถแปลงค่าวันที่เต็มภาษาไทย เป็นวันที่มาตรฐานสากล ISO ได้ โดยถ้าอิงจากชุดข้อมูลที่เรามี และ Explore เบื้องต้น
จะเห็นได้ว่าสิ่งที่ต้องแก้มีแค่ เดือน, ปี หลังจากที่เราใช้ `SPLIT()` เสร็จ โดยที่

- เดือน เราจะใช้ Vlookup จากตารางอ้างอิงที่สร้างขึ้นในข้อ 1
- ปี พ.ศ. เราแค่ลบ 543 ให้เป็นมี ค.ศ.

จากนั้นเราจะรวม ปี-เดือน-วัน เข้าด้วยกันด้วยคำสั่ง `DATE(ปี, เดือน, วัน)` ก็จะได้วันที่มาตรฐานสากล ISO 

📌 **ตัวอย่าง:** [แนะนำให้ลองดูใน Sheet: Click](https://docs.google.com/spreadsheets/d/1a3l_9Lgr_G6m5DkfvEdUg4a3fpwKmLog1oEyewA8Zg4/edit?usp=sharing)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-5-6.gif" alt="Highlight Row">
</p>

## Regular Expression

```excel
=ArrayFormula(REGEXEXTRACT(B3:B7, "\d-\d{4}-\d{5}-\d{2}-\d"))
```
```excel
=ArrayFormula(REGEXEXTRACT(B3:B7,"M[a-z]+."))
```
```excel
=ArrayFormula(REGEXEXTRACT(B3:B7,".+" & D3:D7 & ".(" & "[A-Z][a-z]+" & ")"))
```
```excel
=ArrayFormula(REGEXEXTRACT(B3:B7,".+" & E3:E7 & ".(" & "[A-Z][a-z]+" & ")"))
```
```excel
=ArrayFormula(REGEXEXTRACT(B3:B7,"Date of Birth (\d{2}.[A-z]+.\d{4})"))
```
```excel
=ArrayFormula(DATEDIF(G3:G7,TODAY(),"Y"))
```
```excel
=ArrayFormula(REGEXEXTRACT(B3:B7,"Address (\d+ [A-z]+ [A-z]+..+ )"))
```
```excel
=ArrayFormula(REGEXEXTRACT(B3:B7," \d{5}"))
```
```excel
=ArrayFormula(REGEXEXTRACT(B3:B7,"Expired Date (\d{2}.[A-z]+.\d{4})"))
```
```excel
=ArrayFormula(REGEXMATCH(K3:K7,"2024"))
```

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-6-6.png" alt="Highlight Row">
</p>

สำหรับตัวอย่างนี้คือการใช้งานสูตรตระกูล Regular Expression ซึ่งในตัวอย่างนี้ผมจะใช้อยู่ 2 สูตร คือ

- `REGEXEXTRACT()` คืนค่าที่ดึงข้อมูลตามต้องการออกมาจาก pattern บางอย่าง หลักๆจะรับอยู่ 2 parameter (cell ที่อยากดึง และ pattern การดึง)
- `REGEXMATCH()` คืนค่า `TRUE` หรือ `FALSE` ตามเงื่อนไขที่กำหนดว่ามีหรือไม่มี 2 parameter (cell ที่อยากตรวจหา และ ค้นหาอะไร)

จากรูปตัวอย่างคอลัมน์ B(วงกลมสีแดงเลข 1 ช่วง `B3:B7`) คุณจะเห็นข้อมูลของลูกค้า ซึ่งเป็นข้อมูลบัตรประชาชนที่ demo ขึ้นมาที่มี pattern การเขียนเหมือนกันทุกแถว คือ

```ID เพศ ชื่อ นามสกุล วันเกิด อายุ ที่อยู่ เลขไปรษณีย์ วันหมดอายุ```

ซึ่งผมจะสกัดหรือดึง ออกมาเป็นแต่ละคอลัมน์ตั้งแต่ C ถึง L ตามรูปโดยใช้สูตร `REGEXEXTRACT()` และ `REGEXMATCH()`
จากนั้นผมจะใช้สูตรจากภาพวงกลมเลข 2 ไปใส่แต่ละคอลัมน์ ที่แสดงในวงกลส่วนของเลข 3 เป็นการทดสอบว่าเงื่อนไขเป็นจริงไหมโดยใช้ `REGEXMATCH()`
ดังนั้นผมขอแบ่งเป็น 10 ส่วน ดังต่อไปนี้ (ผมขอข้ามส่วน `ArrayFomula ไปเลยนะครับ เพราะตัวอย่างที่ผ่านมาๆอธิบายไปแล้ว)

1. `ID` ใช้ `=ArrayFormula(REGEXEXTRACT(B3:B7, "\d-\d{4}-\d{5}-\d{2}-\d"))`

     

2. `Gender` ใช้ `==ArrayFormula(REGEXEXTRACT(B3:B7,"M[a-z]+."))`



3. `FirstName` ใช้ `=ArrayFormula(REGEXEXTRACT(B3:B7,".+" & D3:D7 & ".(" & "[A-Z][a-z]+" & ")"))`



4. `LastName` ใช้ `=ArrayFormula(REGEXEXTRACT(B3:B7,".+" & E3:E7 & ".(" & "[A-Z][a-z]+" & ")"))`



5. `DOB` ใช้ `=ArrayFormula(REGEXEXTRACT(B3:B7,"Date of Birth (\d{2}.[A-z]+.\d{4})"))`



6. `Age` ใช้ `=ArrayFormula(DATEDIF(G3:G7,TODAY(),"Y"))`



7. `Address` ใช้ `=ArrayFormula(REGEXEXTRACT(B3:B7,"Address (\d+ [A-z]+ [A-z]+..+ )"))`



8. `Zipcode` ใช้ `=ArrayFormula(REGEXEXTRACT(B3:B7," \d{5}"))`



9. `Expired Date` ใช้ `=ArrayFormula(REGEXEXTRACT(B3:B7,"Expired Date (\d{2}.[A-z]+.\d{4})"))`



10. `Expired 2024` ใช้ `=ArrayFormula(REGEXMATCH(K3:K7,"2024"))`











📌 **ตัวอย่าง:** [แนะนำให้ลองดูใน Sheet: Click](https://docs.google.com/spreadsheets/d/1a3l_9Lgr_G6m5DkfvEdUg4a3fpwKmLog1oEyewA8Zg4/edit?usp=sharing)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p1-6-6.gif" alt="Highlight Row">
</p>







