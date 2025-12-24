# PBAcourse-Sick_leave-and-Job_Satisfaction-Fall-2025
Final project for my course Programming for Business Analytics in the fall 2025 that looks at the effect of a sick leave law enacted in Vermont on 01 january 2017 on job satisfaction.

Other participants ; 方喻萱(Yu-Hsuan Fang) and 吳睿芸 (Jui-Yun Wu).




**Data** : dataverse_files (1).zip
originally found at https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/UDMSIR 


**copie comforme of the ReadMe found on dataverse**



# County–Month Job-Satisfaction Dataset (`JS_wide.csv`)

This repository contains the file **`JS_wide.csv`**, a monthly U.S. county-level panel dataset used in the *jobsat* paper.  
The dataset integrates:

- a tweet-based job-satisfaction indicator derived from geolocated Twitter data classified using a fine-tuned large language model,
- labor-market indicators from the Bureau of Labor Statistics (BLS) LAUS program,
- income data from the American Community Survey (ACS) 5-year estimates, and
- rurality classifications from the USDA Rural–Urban Continuum Codes.

The dataset spans **January 2013 – December 2023** and contains **282,079 county–month observations**.

---

## 1. File Description

**File:** `JS_wide.csv`  
**Format:** Comma-separated values (UTF-8)  
**Unit of observation:** county–month  
**Key identifier:** `StateCounty` (county FIPS code, stored as integer)

---

## 2. Variable Dictionary

Below is the complete description of all columns in the CSV, following the exact column order:

| Column name | Type | Description |
|-------------|------|-------------|
| **StateCounty** | int | Five-digit county FIPS code (state FIPS + county FIPS). Stored as integer without leading zeros (e.g., “01001” → `1001`). Reconstruct using `sprintf("%05d", StateCounty)`. |
| **year** | int | Calendar year of the observation. |
| **month** | int | Calendar month (1–12). |
| **employed** | num | Number of employed individuals (BLS LAUS). |
| **labor_force** | num | Labor force size (employed + unemployed). |
| **unemployed** | int | Number of unemployed individuals. |
| **unemployment_rate** | num | Monthly unemployment rate in percent: `100 * unemployed / labor_force`. |
| **rural** | int | USDA Rural–Urban Continuum Code (1–9); 1–3 = metro, 4–9 = non-metro. |
| **population** | int | County population (ACS 5-year estimates). |
| **jobsat** | num | Tweet-based job-satisfaction index in [-1, 1], computed as the mean of recoded tweet-level sentiment scores. Higher values indicate more positive sentiment. |
| **stat_se_jobsat** | num | Standard deviation of tweet-level job-satisfaction scores within the county–month. |
| **ntweets_jobsat** | int | Total number of tweets processed for job-satisfaction classification. |
| **validtweets_jobsat** | int | Tweets with valid sentiment labels (used to compute `jobsat`). |
| **natweets_jobsat** | int | Tweets with missing or unusable sentiment labels. |
| **acs5** | int | Median household income (ACS 5-year estimates, in USD). |
| **State** | int | Two-digit state FIPS code. |
| **date** | string | First day of the corresponding month (e.g., “2013-01-01”). |

---

## 3. Relation to the HFGI Project and Original Data Sources

The job-satisfaction indicator (`jobsat`) is part of the broader project:

**The Human Flourishing Geographic Index (HFGI)**, see: Iacus, Jain,  Nasuto,  Porro,  Carammia, and  Vezzulli (2025) “[Human Flourishing Geographic Index (USA, 2013-2023)](https://doi.org/10.7910/DVN/T39JBY).” 

The HFGI is conceptually inspired by the flourishing framework 
of the Harvard Human Flourishing Program (VanderWeele, 2017) and 
includes monthly and yearly county/state-level indicators across 
several well-being dimensions.  
The dataset is constructed from 
approximately **2.6 billion georeferenced tweets** from 
the **Harvard CGA Geotweet Archive** [Lewis et al., 2016](https://doi.org/10.7910/DVN/3NCMB6).

The `jobsat` indicator:

- is aggregated at the county–month level,
- takes values in [-1, 1],
- reflects expressed satisfaction or dissatisfaction with job conditions,
- includes tweet-volume measures (`ntweets_jobsat`, `validtweets_jobsat`, `natweets_jobsat`).

### Additional Data Sources

- **Rurality**: USDA Economic Research Service, *Rural–Urban Continuum Codes (2023)*.  
- **Income**: U.S. Census Bureau, *American Community Survey (ACS) 5-Year Estimates*.  
- **Labor-market indicators**: U.S. Bureau of Labor Statistics (BLS), *Local Area Unemployment Statistics (LAUS)*, accessed through the public BLS API.



