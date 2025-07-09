# Project 8 : Data-Driven Insights: Sales Performance & Profitability in Looker Studio

## Project Introduction
โปรเจกต์นี้ใช้ชุดข้อมูลจาก [Tableau](https://community.tableau.com/s/question/0D54T00000CWeX8SAL/sample-superstore-sales-excelxls?_gl=1*6jtjnc*_ga*MzUyOTA0ODIyLjE3NTE5NjQxMzE.*_ga_8YLN0SNXVS*czE3NTE5NjQxMjkkbzEkZzEkdDE3NTE5NjQyMDMkajQ2JGwwJGgw*_gcl_au*NTkxNDEyNzk2LjE3NTE5NjQxMzE.)
ซึ่งเคยใช้ไปแล้วใน [Project 3 : RFM Analysis](https://phubordin.github.io/My-Portfolio-Website/project_rfm_py_dsb10.html#65-export-clean-data) 
แน่นอนว่า เป็นข้อมูลการขายสินค้าใน Superstore ในสหรัฐอเมริกา (ไม่ใช่ข้อมูลจริงนะครับ) ข้อมูลนี้ถูกออกแบบขึ้นมาเพื่อใช้ประกอบการฝึกวิเคราะห์ด้วยเครื่องมือเช่น 
Tableau, Power BI, Excel, SQL และ Python โดยมีโครงสร้างและบริบทใกล้เคียงกับข้อมูลจริง

แต่เราจะนำมา เพิ่มคอลัมน์เหล่านี้ลงไปด้วย :

- `Price per Unit`
- `Cost per Unit`
- `Profit per Unit`
- `%NPM per Unit`
- `%ROI per Unit`

เพื่อใช้ในการวิเคราะห์สำรวจรวมถึง ***Clean Data : Product ID, Product Name*** ด้วยเนื่องจาก
1 Product ID สามารถมีได้หลาย Product Name และ
1 Product Name สามารถมีได้หลาย Product ID

(ซึ่งไม่ควรเกิดปัญหานี้มันควรมีความสัมพันธ์แบบ One-to-One) ดังนั้น คอลัมน์ที่เพิ่มขึ้นมาจะช่วยในเรื่อง

1. รู้ %NPM และ %ROI ต่อสินค้า 1 หน่วย เพื่อที่จะได้ make better decision กับรายสินค้าได้ต่อไป
2. ❗️***ไว้พิจารณาการจัดการกับปัญหา Many-to-Many ของคอลัมน์ Product ID, Product Name*** 

## USA Sales Explorer Dashboard
Dashboard with Looker Studio : [USA Sales Explorer Dashboard](https://lookerstudio.google.com/reporting/92339059-263d-4e78-85d6-803cdd1c70a4)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-usa-store-ggsheet.gif" alt="Titanic Project">
</p>

## USA Store Dataset
USA Store - Google Sheets : [Dataset](https://docs.google.com/spreadsheets/d/1W3uxB51xXKMRELejOsqFhjuyJ1SQRVzw5zptCLszZBs/edit?usp=sharing)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-usa-store-ggsheet.gif" alt="Projecr 8 - ggsheets dataset">
</p>

## Add Columns (Equation)

สมการหาราคาขายต่อชิ้น `Price per Unit`:

$$
\text{Sales} = \text{Price Per Unit} \times \text{Quantity} \times (1 - \text{Discount})
$$

$$
\text{Price Per Unit} = \frac{\text{Sales}}{\text{Quantity} \times (1 - \text{Discount})}
$$

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-price.png" alt="Titanic Project">
</p>

สมการหาต้นทุนต่อชิ้น `Cost per Unit` :

$$
\text{Profit} = \text{Sales} - (\text{Cost per Unit} \times \text{Quantity})
$$

$$
\text{Cost per Unit} = \frac{\text{Sales} - \text{Profit}}{\text{Quantity}}
$$

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-cost.png" alt="Titanic Project">
</p>

สมการหากำไรต่อชิ้น `Profit per Unit` :

$$
\text{Profit per Unit} = \text{Price per Unit} - \text{Cost per Unit}
$$

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-profit.png" alt="Titanic Project">
</p>

สมการหาสัดส่วนกำไรต่อต้นทุน `%NPM per Unit` :

$$
\text{\%NPM per Unit} = \frac{\text{Profit per Unit}}{\text{Cost per Unit}} \times 100
$$

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-npm.png" alt="Titanic Project">
</p>

สมการหาสัดส่วนกำไรต่อราคา `%ROI per Unit` :

$$
\text{\%ROI per Unit} = \frac{\text{Profit per Unit}}{\text{Price per Unit}} \times 100
$$

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/raw/main/p8-roi.png" alt="Titanic Project">
</p>
