# Project 8 : Data-Driven Insights: Sales Performance & Profitability in Looker Studio

[My Portfolio Website (Project 8)](https://phubordin.github.io/My-Portfolio-Website/project_looker_dsb10.html)

## Project Introduction
โปรเจกต์นี้ใช้ชุดข้อมูลจาก [Tableau](https://community.tableau.com/s/question/0D54T00000CWeX8SAL/sample-superstore-sales-excelxls?_gl=1*6jtjnc*_ga*MzUyOTA0ODIyLjE3NTE5NjQxMzE.*_ga_8YLN0SNXVS*czE3NTE5NjQxMjkkbzEkZzEkdDE3NTE5NjQyMDMkajQ2JGwwJGgw*_gcl_au*NTkxNDEyNzk2LjE3NTE5NjQxMzE.)
ซึ่งเคยใช้ไปแล้วใน [Project 3 : RFM Analysis](https://phubordin.github.io/My-Portfolio-Website/project_rfm_py_dsb10.html) 
ซึ่งแน่นอนว่า เป็นข้อมูลการขายสินค้าใน Superstore ในสหรัฐอเมริกา (ไม่ใช่ข้อมูลจริงนะครับ) ข้อมูลนี้ถูกออกแบบขึ้นมาเพื่อใช้ประกอบการฝึกวิเคราะห์ด้วยเครื่องมือเช่น 
Tableau, Power BI, Excel, SQL และ Python โดยมีโครงสร้างและบริบทใกล้เคียงกับข้อมูลจริง

และผ่านการ Clean มาแล้วในระดับนึงจากภายใน [Project 3 : RFM Analysis - 6.4 Clean Data](https://phubordin.github.io/My-Portfolio-Website/project_rfm_py_dsb10.html#64-clean-data) ที่กล่าวไว้ตอนท้ายหัวข้อว่าจะมา Clean ต่อภายในโปรเจกต์นี้โดยการที่..

ผมจะนำมาเพิ่มคอลัมน์เหล่านี้ลงไปด้วย :

- `Price per Unit`
- `Cost per Unit`
- `Profit per Unit`
- `%NPM per Unit`
- `%ROI per Unit`

เพื่อใช้ในการวิเคราะห์สำรวจรวมถึง ***Clean Data : Product ID, Product Name*** เพิ่มด้วยเช่นกันเพราะ..

- 1 Product ID สามารถมีได้หลาย Product Name และ
- 1 Product Name สามารถมีได้หลาย Product ID

(ซึ่งไม่ควรเกิดปัญหานี้มันควรมีความสัมพันธ์แบบ One-to-One) ดังนั้น คอลัมน์ที่เพิ่มขึ้นมาจะช่วยในเรื่อง

1. รู้ %NPM และ %ROI ต่อสินค้า 1 หน่วย เพื่อที่จะได้ make better decision กับรายสินค้าได้ต่อไป
2. ❗️***ไว้พิจารณาการจัดการกับปัญหา Many-to-Many ของคอลัมน์ Product ID, Product Name*** 

## 📊 USA SuperStore Dashboard
Dashboard with Looker Studio : [USA Sales Explorer Dashboard](https://lookerstudio.google.com/reporting/92339059-263d-4e78-85d6-803cdd1c70a4)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-usa-store-ggsheet.gif" alt="Looker Project">
</p>

## 🔢 USA SuperStore - Dataset
USA SuperStore - Google Sheets : [Dataset](https://docs.google.com/spreadsheets/d/1W3uxB51xXKMRELejOsqFhjuyJ1SQRVzw5zptCLszZBs/edit?usp=sharing)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-usa-store-ggsheet.gif" alt="Projecr 8 - ggsheets dataset">
</p>

## Add Columns (Equation)

สมการหาราคาขายต่อชิ้น `Price per Unit`: ⬇︎

$$
\text{Sales} = \text{Price Per Unit} \times \text{Quantity} \times (1 - \text{Discount})
$$

$$
\text{Price Per Unit} = \frac{\text{Sales}}{\text{Quantity} \times (1 - \text{Discount})}
$$

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-price.png" alt="Looker Project">
</p>

---

สมการหาต้นทุนต่อชิ้น `Cost per Unit` : ⬇︎

$$
\text{Profit} = \text{Sales} - (\text{Cost per Unit} \times \text{Quantity})
$$

$$
\text{Cost per Unit} = \frac{\text{Sales} - \text{Profit}}{\text{Quantity}}
$$

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-cost.png" alt="Looker Project">
</p>

---

สมการหากำไรต่อชิ้น `Profit per Unit` : ⬇︎

$$
\text{Profit per Unit} = \text{Price per Unit} - \text{Cost per Unit}
$$

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-profit.png" alt="Looker Project">
</p>

---

สมการหาสัดส่วนกำไรต่อต้นทุน `%NPM per Unit` : ⬇︎

$$
\text{Percent NPM per Unit} = \frac{\text{Profit per Unit}}{\text{Cost per Unit}} \times 100
$$

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-npm.png" alt="Looker Project">
</p>

---

สมการหาสัดส่วนกำไรต่อราคา `%ROI per Unit` : ⬇︎

$$
\text{Percent ROI per Unit} = \frac{\text{Profit per Unit}}{\text{Price per Unit}} \times 100
$$

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-roi.png" alt="Looker Project">
</p>

---

## Add New Product Name
ก่อนที่เราจะสร้างคอลัมน์ `New Product Name` เราจะต้องสร้างตารางความสัมพันธ์แบบ `One-to-One` กับคอลัมน์ `Product Name` และ `Product ID`

เริ่มต้น ผมจะเอา `Product ID` เป็นตัวตั้งต้นในการบอกว่า dataset ชุดนี้มีสินค้าที่ขายออกทั้งหมดกี่แบบ โดยที่

---

**ขั้นตอนที่ 1** : ผมจะสร้างคอลัมน์ `Product ID` โดยใช้สูตร ⬇︎

```{excel}
=UNIQUE(Product ID Range)

```

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-many-product-Ids-1.png" alt="Looker Project">
</p>

จากรูป จะมีจำนวนสินค้าทั้งหมด 1,862 ชิ้น (ไม่รวมหัวตาราง)

📍 เหตุผลที่ยึดหมายเลข `Product ID` เป็นตัวกำหนดหลักว่า `Product Name` ต้องมีชื่อว่าอะไรเพราะ..?

เพราะ จำนวน `UNIQUE(Product ID Range)` > `UNIQUE(Product Name Range)`

(✅ ปล.จริงๆควรไปดูเลยว่า `Product Name` นี้มีเลข Product ID จริงๆอะไรกันแน่ที่ต้นทาง เราอาจจะเดินไปดูที่ โกดังสต๊อคเลยก็ได้ เป็นต้น)

---

**ขั้นตอนที่ 2** : ผมจะสร้างคอลัมน์ `Product Name` โดยใช้สูตร ⬇︎

```{excel}
=XLOOKUP(ที่อิงจาก Product ID ในขั้นตอนที่ 1 ไปหาจากตารางที่อยู่ในชีต USA-SuperStore)

```

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-many-product-Ids-2.png" alt="Looker Project">
</p>

จากรูปเราก็จะได้คอลัมน์ `Product Name` ที่อิงจาก `Product ID` ซึ่งเราจะพบเลยว่ามีค่าซ้ำกัน (จากภาพให้ใช้กำหนด Highlight Conditional Formatting ให้เห็นภาพชัดขึ้น)
ตรงที่เป็น **สีฟ้า** คือ `Product Name` ที่มีหลาย `Product ID` เราจะมาจัดการตรงนี้กัน❗️ 

---

**ขั้นตอนที่ 3** : ผมจะเอาคอลัมน์ `price`, `cost`, `profit`, `npm`, `roi` มาใส่ไว้ในตารางนี้ด้วย โดยใช้สูตร ⬇︎

```{excel}
VLOOKUP(A2:A1863,'USA-SuperStore'!$M$2:$Y$9995,{9, 10, 11, 12, 13},0)

```
<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-many-product-Ids-3.png" alt="Looker Project">
</p>

จากรูปเราจะได้คอลัมน์ทั้งหมด 7 คอลัมน์แล้วคือ

1. `Product ID` ที่ไม่มีค่าซ้ำกันเลย
2. `Product Name` ที่มีค่่าซ้ำกันอยู่ (1 Product Name มีหลาย Product ID)
3. `Price per Unit` Vlookup มาจากตารางหลัก
4. `Cost per Unit` Vlookup มาจากตารางหลัก
5. `Profit per Unit` Vlookup มาจากตารางหลัก
6. `%NPM per Unit` Vlookup มาจากตารางหลัก
7. `%ROI per Unit` Vlookup มาจากตารางหลัก

ขั้นตอนต่อไปเราจะมาพิจาณาว่าจะทำยังไงให้เป็น `One-to-One` สำหรับคอลัมน์ `Product ID` และ `Product Name`

---

⭐️ **ขั้นตอนที่ 4** : จัดการกับ `Product Name` ⬇︎

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-many-product-Ids-4.png" alt="Looker Project">
</p>

จากรูปเราจะเห็นได้ว่ามันจะมี แค่ 3 ส่วนที่เราต้อง Recheck ว่า `Product Name` นี้มี `Product ID` เป็นอะไรกันแน่

เพราะ จากรูป "**เราจะพิจารณาทุกคอลัมน์เลยไม่ให้แถวแต่ละแถวซ้ำกัน**" ปรากฎว่ามันจะมี 3 ส่วนมีซ้ำกัน
เราจะต้องนำ `Product ID` ที่มันซ้ำกันไปดูว่ามันอาจจะมีหลาย `Product Name` ก็ได้ ดูจากรูป ด้านล่าง

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-many-product-Ids-5.png" alt="Looker Project">
</p>

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-many-product-Ids-6.png" alt="Looker Project">
</p>

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-many-product-Ids-7.png" alt="Looker Project">
</p>

ผลปรากรากฎว่า ไม่ซ้ำกันเลยแสดงว่าสิ่งที่เราจะทำคือ 

```
  🔥 เราสามารถที่จะกำหนดชื่อใหม่ได้เลย ทั้งหมดในคอลัมน์ Product Name ตามรูปด้านล่าง
```

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-price-list.gif" alt="Looker Project">
</p>

จะอยู่ในชีต `Price List`

---

🔥🔥**ขั้นตอนที่ 5** (สุดท้าย) : แทนที่ `Product Name` ด้วย `New Product Name` ⬇︎

เพิ่มคอลัมน์ใหม่ชื่อ `New Product Name` จากนั้น `XLOOKUP()` จากตารางที่เราสร้างมาเป็น `One-to-One` แล้วในชีต `Price List` ตามรูปด้านล่าง : ⬇︎

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-price-list.png" alt="Looker Project">
</p>

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-add-new-name-product.png" alt="Looker Project">
</p>

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-drop-old-name-product.png" alt="Looker Project">
</p>

## Congratulation 🎉 Final Dataset

USA SuperStore - [Google Sheets : Dataset](https://docs.google.com/spreadsheets/d/1W3uxB51xXKMRELejOsqFhjuyJ1SQRVzw5zptCLszZBs/edit?usp=sharing)
(ข้อมูลที่พร้อมสร้างแดชบอร์ด)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-usa-store-ggsheet.gif" alt="Looker Project">
</p>

ต่อไป..

เราจะมาเริ่มสร้างพร้อมตั้งคำถาม เพื่อที่จะนำไปสร้าง Dashboard บน Looker Studio กันนะครับ (โดยใช้ Dataset ที่พร้อมใช้งานแล้ว)

สามารถดูได้ที่ : [My Portfolio Website - Project 8 Looker Studio](https://lookerstudio.google.com/reporting/92339059-263d-4e78-85d6-803cdd1c70a4)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-usa-store-ggsheet.gif" alt="Looker Project">
</p>






