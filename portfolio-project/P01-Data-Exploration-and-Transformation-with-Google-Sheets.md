# P1 : Data Exploration and Transformation with Google Sheets

## 📌 Table of Contents
- [Filter & Sort Dynamic](#filter-&-sort-dynamic)
---

## Filter-&-Sort-Dynamic
```excel
=IFERROR(SORT(FILTER(EMPLOYEE, (GENDER = B2) * (PERFORMANCE = B3)), 5, Not(D2)),"NO DATA")
```
📌 **อธิบายสูตร:**  
- Filter Data จาก EMPLOYEE Range ที่ Gender = Men(`B2`) และ(*) performance = Good(`B3`) -> (`B2, B3` = เป็น dynamic เลือกเพศกับการปฏิบัตืงานได้)
- และ Sort salary(คอลัมน์ที่ `5`) จากมาก-น้อย(`NOT(D2)`) -> (`5` = เป็นการบอกว่าเรียงลำดับคอลัมน์ที่ 5 | `NOT(D2)` = ให้ set ค่า Sort เป็น False เพื่อจะเรียงลำดับจาก มาก-น้อย)
- ถ้า Filter Data ขึ้น Any Error จะให้แสดง `NO DATA`

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


