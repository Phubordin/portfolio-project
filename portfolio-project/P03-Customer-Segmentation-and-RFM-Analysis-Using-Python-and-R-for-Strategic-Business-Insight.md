# Project 3 : Customer Segmentation and RFM Analysis Using Python and R for Strategic Business Insight

## 📌 Table of Contents
1. [Explore Data and Load Data](#1-explore-data-and-load-data)

   - 1.1 [DownLoad data on PC](#11-download-data-on-pc)
   - 1.2 [Import data on Google Colab](#12-import-data-on-google-colab)
   - 1.3 [Explore Data](#13-explore-data)

2. [Prepare Data](#2-prepare-data)
3. [RFM Analysis Using Python and R](#3-rfm-analysis-using-python-and-r)

     - 3.1 [RFM Analysis Using Python](#31-rfm-analysis-using-python)
     - 3.2 [RFM Analysis Using R](#32-rfm-analysis-using-r)

4. [Exploratory Sales & Customer Analysis (2017–2020)](#4-exploratory-sales--customer-analysis-20172020)

     - 41 [Export Customer Data in California (CSV Format)](#41-export-customer-data-in-california-csv-format)
     - 42 [Export Order Data (CSV): Customers in California and Texas, 2017](#42-export-order-data-csv-customers-in-california-and-texas-2017)
     - 43 [Sales Analysis 2017: Total, Average, and Standard Deviation by Month, Day, and Order](#43-sales-analysis-2017-total-average-and-standard-deviation-by-month-day-and-order)
     - 44 [Highest Profit Segment in 2018](#44-highest-profit-segment-in-2018)
     - 45 [Top 5 States with the Lowest Total Sales (15 April – 31 December 2019)](#45-top-5-states-with-the-lowest-total-sales-15-april--31-december-2019)
     - 46 [Sales Proportion (%) in West and Central Regions, 2019](#46-sales-proportion--in-west-and-central-regions-2019)
     - 47 [Top 10 Products by Order Volume vs. Total Sales (2019–2020)](#47-top-10-products-by-order-volume-vs-total-sales-20192020)
     - 48 [Visual Insights: At Least Two Interesting Plots](#48-visual-insights-at-least-two-interesting-plots)

[Project Summary](#project-summary)

---

   สวัสดีครับ สำหรับ Project นี้ผมมี Mock up Data ของบริษัทแห่งนึง ซึ่งผมจะนำมาวิเคราะห์พฤติกรรมการซื้อ-ขายสินค้า ของลูกค้า โดยการแบ่งกลุ่มลูกค้าออกเป็น 11 กลุ่ม ด้วยวิธี RFM Model

   ซึ่งวิเคราะห์ด้วยภาษา Python บน Google Colab เป็นหลัก และใช้เคราะห์ด้วยภาษษ R บน Rstudio ต่อไปจะเป็นการสำรวจและโหลดข้อมูลเบื้องต้นกันก่อนครับ


## 1 Explore Data and Load Data

ขอขอบคุณ Mock up Data จากพี่ทอย DataRockie สำหรับไฟล์ที่ใช้ในการวิเคราะห์นะครับ

### 11 DownLoad data on PC

ดาวน์โหลดไฟล์ [sample-store.csv](https://drive.google.com/file/d/1-3p1eJCJZjYpfO4rfRh4aMehnUWS2LKY/view?usp=sharing) (Google Drive) ลงบนคอม

📸 Preview :
     
<p align="center">
     <img src="https://github.com/Phubordin/My-Portfolio-Website/blob/main/sample-store.png">
</p>
        
### 12 Import data on Google Colab

Google Colab : [Project 3 : Customer Segmentation and RFM Analysis Using Python and R  for Strategic Business Insight](https://colab.research.google.com/drive/1-zaB6ZUy02SvfJKNKsgmx-6X_3BOsoMh?usp=sharing)

<p align="center">
  <img src="https://github.com/Phubordin/My-Portfolio-Website/blob/main/p3-load-data0.png" alt="load-data-colab">
</p>

```python

import pandas as pd # เรียกใช้ library pandas
import numpy as np  # เรียกใช้ library numpy (โหลดมาเพื่อเตรียมกับสรุปผล Data)
df = pd.read_csv("sample-store.csv") # อ่านข้อมูลในไฟล์ และเก็บไว้ในตัวแปร df

```

1. กดรูปโฟลเดอร์

2. เลือก upload file และ เลือกไฟล์ `sample-store.csv`

3. ไฟล์ถูกอัพโหลดเข้ามา

4. รัน Code สำหรับอ่านไฟล์ที่ปุ่ม Run

📍 ถ้าขาดการเชื่อมต่อกับ Google Colab เป็นเวลานาน หรือรีสตาร์ทเซสชัน (Runtime) ใหม่ ไฟล์ที่อัปโหลดไว้แบบชั่วคราวจะหายไป

ดังนั้น upload ไฟล์ใหม่ขึ้นบน Google Colab อีกครั้งหรือเอาไฟล์ไว้บน Google Drive แล้วเชื่อมต่อกับ Google Colab

หลังจากนั้นกดรัน `df = pd.read_csv("sample-store.csv")` ใหม่อีกรอบเพื่อ assign ตัวแปร

### Explore Data

1. Range Data

   ดูขนาดของตารางว่ามีกี่แถว และกี่คอลัมน์

   ```python
   df.shape # (9994, 21 ex.header) 
   
   ```
Colab

## 2 Prepare Data


## 3 RFM Analysis Using Python and R


## 31 RFM Analysis Using Python
## 32 RFM Analysis Using R
## 4 Exploratory Sales & Customer Analysis (2017–2020)
## 41 Export Customer Data in California (CSV Format)
## 42 Export Order Data (CSV): Customers in California and Texas, 2017
## 43 Sales Analysis 2017: Total, Average, and Standard Deviation by Month, Day, and Order
## 44 Highest Profit Segment in 2018
## 45 Top 5 States with the Lowest Total Sales (15 April – 31 December 2019)
## 46 Sales Proportion (%) in West and Central Regions, 2019
## 47 Top 10 Products by Order Volume vs. Total Sales (2019–2020)
## 48 Visual Insights: At Least Two Interesting Plots
## Project Summary






### 🔍 คลิกดู Interactive Report ด้านล่างนี้:

[เปิดดู RFM Report](https://phubordin.github.io/My-Portfolio-Website/Project_3_Customer_Segmentation_and_RFM_Analysis_Using_Python_and_R_for_Strategic_Business_Insight.html)

![ภาพตัวอย่าง](https://raw.githubusercontent.com/phubordin/My-Portfolio-Website/main/screenshot.png)





