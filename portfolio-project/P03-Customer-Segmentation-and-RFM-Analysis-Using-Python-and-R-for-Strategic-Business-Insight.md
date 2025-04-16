

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

