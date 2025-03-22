# P1 : Data Exploration and Transformation with Google Sheets

## 📌 Table of Contents
- [Installation Guide](#overview)
- [Usage](usage.md)
- [Contributing](contributing.md)

---

## 🔢 การคำนวณโบนัสพนักงาน  
```excel
=IFERROR(SORT(FILTER(EMPLOYEE, (GENDER = B2) * (PERFORMANCE = B3)), 5, Not(D2)),"NO DATA")
```
📌 **อธิบายสูตร:**  
- ถ้ายอดขาย (`B2`) มากกว่า `100,000` → ได้โบนัส `10%`  
- ถ้ายอดขาย ≤ `100,000` → ได้โบนัส `5%`  

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


