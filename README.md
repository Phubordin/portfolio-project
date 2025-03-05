# Portfolio-project
1. P  : Data Exploration and Transformation with Google Sheets
2. P  : Building a Café Restaurant Database Using R and SQL
3. P  : Customer Segmentation and RFM Analysis Using Python and  for Strategic Business Insight
4. P  : Creating a Multi-Round Rock-Paper-Scissors Game in Python and R
5. P  : EDA and Comparison of NYC Flights Data (2013 vs. 2023) with 
6. P  : EDA Visualization of the Diamond Dataset Using  and R Markdown
7. P  : Logistic Regression Analysis on the Titanic Dataset Using 
8. P  : Data-Driven Insights: Sales Performance & Profitability in Looker Studio
9. P  : Chatbot Development for a Pizza Business Using  Programming
10. P : Object-Oriented ATM System: Financial Transactions with Python OOP
11. P mini : Extracting Public API Data with Python: Air Quality Analytics

```python
def hello():
    print("Hello, GitHub!")
```

11. P mini : Extracting Public API Data with Python: Air Quality Analytics
    
| ชื่อ | อายุ | อาชีพ |
|------|----|------|
| Alice | 25 | Developer |
| Bob   | 30 | Designer |
| Charlie | 28 | Data Scientist |

```r
# Intro
library(tidyverse)
library(nycflights13)
library(glue)
library(rnaturalearth)
library(sf)
library(ggplot2)
library(purrr)

?flights # file มีเเถว 336,766 ถ้าเราโหลด nycflights23 เวลารัน
# Flights จะเป็น data 2023 เเล้ว เหมือนมัน update

write.csv(flights, file = "flights.csv") # เขียนไฟล์เพื่อดูขนาดไฟล์
df <- read_csv("flights.csv") # อ่านไฟล์ที่ต้องใชเ _csv เพระาเวลารันมันไม่เป็น tibble ให้

## homework 16.25 - 22.30
## manipulate data (nycflights13)

## นี่คือ table ทั้งหมดที่ file Default (nycflights13)
flights # primary key -> 1 lines = 1 row = 1 เที่ยวบน = 1 การเดินทาง
airlines # primary key -> name_airlines
airports # primary key -> name_air
planes # primary key -> number_planes
weather # primary key ->origin_location_specific_time

## Let's start HOMEWORK--------------------------------------------------------------

### 1. ต้องการอยากทราบว่า คนบินไปรัฐไหนบ้างแตกต่างกันอย่างไร---------------

# 1. โหลดข้อมูลเมืองจาก rnaturalearth
cities <- ne_download(scale = "large", type = "populated_places", returnclass = "sf")

# 2. แปลงตาราง airports ให้เป็น sf object
airport_coords <- airports %>%
  select(faa, name, lat, lon) %>%
  st_as_sf(coords = c("lon", "lat"), crs = 4326, remove = FALSE)

# 3. เชื่อมสนามบินกับเมืองใกล้เคียงที่สุด
matched_cities <- st_join(airport_coords, cities, join = st_nearest_feature)

colnames(matched_cities) <- tolower(colnames(matched_cities))
colnames(matched_cities)[2] <- "name_airport"


# 4. เลือกคอลัมน์ที่ต้องการเพื่อจะนำไป Join 
state <- matched_cities %>%
  select(faa, adm1name, name_airport)

## 5. หาจำนวนเที่ยวบินที่ไปถึงที่สนามบินปลายทาง
n_flight_des <- flights %>%
  filter(if_all(everything(), ~ !is.na(.))) %>%
  select(dest) %>%
  group_by(dest) %>%
  summarise(n_flights = n()) %>%
  arrange(- n_flights)

## ไม่ต้องไปดูตรงอื่นเริ่มตรงนี้ !!!!
## 6. Join table เพื่อดูว่าสนามบินที่ว่าตั้งอยู่เมืองไหน และจัดการค่า NA
prep_n_flights <- n_flight_des %>%
  left_join(state, by = c("dest" = "faa")) %>%
  select(name_airport, dest, adm1name, n_flights) %>%
  # filter(if_any(everything(), is.na)) %>% # ไว้ test ว่าคอลัมน์ไหนมี NA
  mutate(
    adm1name = case_when(
      is.na(adm1name) & dest == "STT" ~ "U.S. Virgin Islands",
      is.na(adm1name) & dest == "BQN" ~ "Puerto Rico",
      is.na(adm1name) & dest == "SJU" ~ "Puerto Rico",
      is.na(adm1name) & dest == "PSE" ~ "Puerto Rico",
      TRUE ~ adm1name
    ), 
    name_airport = case_when(
      is.na(name_airport) & dest == "STT" ~ "Cyril E. King Airport",
      is.na(name_airport) & dest == "BQN" ~ "Rafael Hernandez Airport",
      is.na(name_airport) & dest == "SJU" ~ "Luis Munoz Marin Interenational Airpot",
      is.na(name_airport) & dest == "PSE" ~ "Mercedita Airport",
      TRUE ~ name_airport
    )
  )
# view()

## 7. นับจำนวนเที่ยวบินที่บินไปแต่ละที่ ว่าปี 2013 สนามบินในนิวยอร์กบินไปไหนมากที่สุดเรียงจากน้อยไปมาก

summary_data1 <- prep_n_flights %>% 
  select(adm1name, n_flights) %>%
  group_by(adm1name) %>%
  summarise(n_flights = sum(n_flights)) %>%
  arrange(- n_flights) %>%
  slice_head(n = 5)
#summarise(sum(n_flights))

## แถม
## ลบเเถวที่มี NA ออกให้หมด
## show เเถวที่มี NA ประกอบ
## ลอง make chart คร่าวๆ

flights %>%
  # filter(if_all(everything(), ~ !is.na(.)))
  # filter(if_any(everything(), is.na))
  
  
  summary_data1 %>% 
  ggplot(aes(x = reorder(adm1name,  n_flights), y = n_flights)) + 
  geom_col() + 
  coord_flip()

## ตอบ Florida, California, North Carolina 
## --------------- End 1 ------------------
```

## 🔢 การคำนวณโบนัสพนักงาน  
```excel
=IF(B2>100000, B2*10%, B2*5%)
```
📌 **อธิบายสูตร:**  
- ถ้ายอดขาย (`B2`) มากกว่า `100,000` → ได้โบนัส `10%`  
- ถ้ายอดขาย ≤ `100,000` → ได้โบนัส `5%`  

---

## **2️⃣ ใช้ตารางเพื่อแสดงตัวอย่าง Input และ Output**  
> 📊 **ช่วยให้ Users เข้าใจผลลัพธ์ได้ง่ายขึ้น**  

```md
| ยอดขาย (B2) | โบนัสที่ได้ (สูตร `=IF(B2>100000, B2*10%, B2*5%)`) |
|-------------|-------------------------------------|
| 120,000     | 12,000 (10%) |
| 80,000      | 4,000 (5%) |
| 150,000     | 15,000 (10%) |
```
