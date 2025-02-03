# HR Analytics-Dashboard



## Problem Statement
   ATliQ Hardware faces challenges in tracking employee attendance, understanding work preferences, and gaining insights into absenteeism trends due to reliance on Excel sheets. This lack of structured data makes it difficult for HR and management to optimize resources, plan capacity, and address employee well-being. A Power BI-based data analytics solution is proposed to provide real-time insights into attendance, absenteeism, and operational efficiency, supporting strategic planning, resource allocation, and employee engagement.

 

1. **Data Management Challenges:**  
   - Heavy reliance on Excel sheets for tracking employee attendance and work preferences.  
   - Inconsistent and unstructured data, making insights extraction difficult.  

2. **Attendance and Work Trends:**  
   - Difficulty in analyzing work-from-home vs. work-from-office patterns.  
   - Understanding preferences for work-from-home days (e.g., Mondays or Fridays).  

3. **Absenteeism Analysis:**  
   - Lack of insights into reasons for sick leaves.  
   - Identifying patterns of mass absenteeism, which could indicate health issues or seasonal factors.  

4. **Operational Efficiency:**  
   - Limited ability to plan team-building activities based on workforce availability.  
   - Challenges in capacity planning for hybrid work models and infrastructure optimization.  

5. **Strategic Planning:**  
   - Need for better insights to align HR strategies and operational decisions.  

6. **Proposed Solution:**  
   - Implementation of a Power BI dashboard to provide real-time insights into attendance, absenteeism trends, and operational efficiency.  






### Steps followed 




---


### **1. Data Connection**
- Connected Power BI to an Excel workbook containing multiple sheets (e.g., April, May, June).
- Imported data from these sheets into the Power BI environment.

---

### **2. Data Modeling**
- Accessed the **Model View** in Power BI to establish relationships between the sheets (e.g., employee code, date).
- Verified that data relationships were correctly defined based on the common columns across the sheets (e.g., `employee_code`, `attendance_date`).
- Ensured that the model structure is appropriate for analysis (fact table: attendance data, dimension tables: employee, dates).

---

### **3. Data Transformation in Power Query**

#### **Step 1: Filter Unnecessary Data**
- **Attendance Data**:
  - Removed rows with missing or invalid employee codes (e.g., `-1`, `0` values).
  - Ensured that only relevant data, like specific months, was retained after filtering.

#### **Step 2: Standardize Data for Consistency**
- Created a new column to standardize dates for analysis (e.g., consolidating multiple date columns into one).
- Used Power Query's **Unpivot** feature to transform columns into rows, ensuring that each record had one date associated with the employee.

#### **Step 3: Handling Missing or Duplicate Data**
- Identified missing attendance data (e.g., missing 1st May data) and flagged as necessary.
- Removed duplicates or inconsistent records (e.g., newline characters in columns).

#### **Step 4: Apply Transformations**
- Applied transformations to clean and standardize the data.
- Applied **Unpivot Other Columns** to ensure date data is in a single column.

---

### **4. Post-Transformation Validation**
- Verified transformed data:
  - Ensured that no irrelevant data remained, such as incorrect or invalid employee codes.
  - Confirmed that the date data was correctly formatted and consolidated into a single column.
  - Conducted a random check to validate the accuracy of the transformed data (e.g., checked for correct employee attendance dates).

---

### **5. Loading Data to Power BI**
- After transformations, clicked **Close & Apply** to load the cleaned data into Power BI for analysis and visualization.
- Disabled the load for intermediate steps to optimize the final dataset.



  
---

# Attendance Metrics - Power BI DAX Measures

This project analyzes employee attendance data using custom DAX measures in Power BI. Below is a detailed summary of the key metrics and their DAX implementations.

### 1. **Total Working Days**  
This measure calculates the total number of working days by excluding non-working days (WO for weekends and HO for holidays).  

**DAX:**  
```DAX
VAR totaldays = COUNT('Final data'[value])
VAR nonworkdays = CALCULATE(COUNT('Final data'[value]), 'Final data'[value] IN {"WO", "HO"})
RETURN totaldays - nonworkdays
```

---

### 2. **WFH Count (Work From Home Days)**  
Calculates the total number of work-from-home days.

**DAX:**  
```DAX
SUM('Final data'[WFH Count])
```

---

### 3. **SL Count (Sick Leave Days)**  
Calculates the total number of sick leave days.

**DAX:**  
```DAX
SUM('Final data'[SL Count])
```

---

### 4. **Present Days**  
Calculates the number of present days, including work-from-home days.  

**DAX:**  
```DAX
VAR presentdays = CALCULATE(COUNT('Final data'[value]), 'Final data'[value] = "P")
RETURN presentdays + [WFH Count]
```

---

### 5. **Presence Percentage**  
Determines the percentage of presence based on total working days.

**DAX:**  
```DAX
DIVIDE('Measure Table'[Present Days], 'Measure Table'[Total working days], 0)
```

---

### 6. **SL Percentage (Sick Leave)**  
Calculates the percentage of sick leave days out of the total working days.

**DAX:**  
```DAX
DIVIDE('Measure Table'[SL Count], 'Measure Table'[Total working days], 0)
```

---

### 7. **WFH Percentage**  
Calculates the percentage of work-from-home days out of the present days.

**DAX:**  
```DAX
DIVIDE('Measure Table'[WFH Count], 'Measure Table'[Present Days], 0)
```

---



 # Report Snapshot (Power BI DESKTOP)
 ![Image](https://github.com/user-attachments/assets/d12036ab-080f-4725-9854-443c13159d8c)

# Insights

Here are insights and observations based on the provided dashboard:

### **High-Level Observations**
1. **Presence Insights:**
   - The overall **Presence % is 91.83%**, indicating strong attendance.
   - **WFH (Work from Home) percentage is 10%**, showing a reasonable proportion of remote work.
   - **SL (Sick Leave) percentage is only 1.10%**, suggesting minimal health-related absenteeism.

2. **Trend Analysis (by Date Charts):**
   - **Presence % Trend:**  
     The presence trend shows fluctuations but maintains consistency above 80% in most months.
   - **WFH % Trend:**  
     WFH days see noticeable spikes in certain periods, suggesting planned remote work schedules or special scenarios.
   - **SL % Trend:**  
     Sick leave percentages remain low but have sporadic spikes, possibly indicating health incidents during specific periods.

3. **Day of the Week Insights:**  
   - **Highest Presence:** Monday (93.21%) and Wednesday (92.11%) have the highest attendance rates.
   - **WFH Preference:** Friday (13.01%) shows the highest WFH percentage, indicating a possible end-of-week remote work policy or employee preference.
   - **SL Occurrence:** Monday (1.62%) has the highest sick leave percentage, which could suggest post-weekend health issues.

---
# **Presence Insights Report: April – June 2022**

## **1. Overall Trend Analysis**
| Metric       | April 2022  | May 2022  | June 2022  | Trend |
|-------------|------------|------------|------------|---------|
| **Presence %** | **94.05%** | **89.75%**  | **91.82%**  | **Decreased in May, recovered in June**  |
| **WFH %** | **9.08%** | **11.23%**  | **9.44%**  | **Increased in May, then decreased** |
| **SL %** | **0.43%** | **1.68%**  | **1.18%**  | **Spike in May, slight recovery in June** |

- **Presence was highest in April (94.05%) but dropped in May (89.75%) due to increased WFH and SL%.**  
- **WFH peaked in May (11.23%) but started decreasing in June (9.44%).**  
- **Sick Leave (SL) was lowest in April (0.43%) but peaked in May (1.68%) before slightly improving in June (1.18%).**  

## **2. Employee-Specific Trends**
- **Highest Presence:**  
  - April: **Adriel Pace & Adyson Moyer (100%)**  
  - May: **Caylee Meadows (100%)**  
  - June: **Aditya Walls, Adriel Pace & Adyson Moyer (100%)**  

- **Lowest Presence:**  
  - April: **Goerge carr (52.38%)**  
  - May: **Kaylah Schultz (27.27%)**  
  - June: **Avanna Atkins (0%) - On extended sick leave**  

- **Highest WFH %:**  
  - April: **George Carr (100%)**  
  - May: **Gustavo Ritter (100%)**  
  - June: **Alexander Davenport (100%)**  

- **Highest SL %:**  
  - April: **mckayla Parker (9.52%)**  
  - May: **Ayanna Atkins (22.73%)**  
  - June: **Emma Freeman (19.23%)**  


## **3. Day-of-Week Trends**
| Metric       | Best Presence Day | Lowest Presence Day | Most WFH Day | Highest Sick Leave Day |
|-------------|------------------|------------------|-------------|-----------------|
| **April** | **Monday (96.46%)** | **Thursday (90.42%)** | **Friday (12.15%)** | **Thursday (1.30%)** |
| **May** | **Monday (90.74%)** | **Friday (86.54%)** | **Friday (15.93%)** | **Monday (2.41%)** |
| **June** | **Tuesday (95.54%)** | **Friday (89.15%)** | **Monday (10.96%)** | **Monday (2.55%)** |

 **Key Insights:**  
- **Monday remains the highest sick leave day across  months**, suggesting employees may be extending weekends.  
- **Friday consistently has the highest WFH percentage, peaking in May (15.93%).**  
- **Presence is generally lower on Fridays, likely due to WFH preferences.**  

## **4. Actionable Recommendations**
### **A. Improve Presence & Reduce SL%**
- Implement **wellness initiatives** to reduce sick leave, especially on **Mondays** when SL is highest.  
- Monitor employees with consistently low presence (e.g., Avanna Atkins in June).  

### **B. Optimize Work From Home Policy**
- Since **Friday has the highest WFH% every month**, consider **formalizing a hybrid work policy** (e.g., designated remote days).  
- Employees with **high WFH percentages** (e.g., **Alexander Davenport in June**) should be provided with collaboration tools for efficiency.  

### **C. Address Friday Absenteeism**
- Since **Friday has the lowest presence across all three months**, explore **engagement strategies** like flexible hours, team activities, or early log-off options.  

## **5. Conclusion**
- **April had the highest presence (94.05%), but May saw a dip (89.75%) due to increased WFH and SL%.**  
- **June showed signs of recovery (91.82%) as WFH and SL percentages dropped.**  
- **Monday is the most affected day for SL, while Friday consistently has the highest WFH.**  
- **A strategic hybrid work model and employee wellness programs can further stabilize presence and reduce absenteeism.**  

 **Final Recommendation:**  
Organizations should **continue monitoring trends** and **adjust policies** based on employee attendance patterns for better workforce productivity. 

---

# References
   https://codebasics.io
