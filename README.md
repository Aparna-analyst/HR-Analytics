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
 ![Screenshot 2025-01-15 160233](https://github.com/user-attachments/assets/b672e349-4d30-4c46-b06c-2d92124879e4)

# Insights

Following inferences can be drawn from the dashboard;


### 1. **Key Insights**:
   -  Delhi leads in revenue generation across all markets with 519.51 Million, with brick-and-mortar stores(482.84 M) contributing significantly more than e-commerce channels(36.68 M).

 -  While Delhi also leads in sales quantity(988K), the gap between revenue and sales quantity suggests higher average pricing or premium products are contributing to revenue
   -  Revenue shows seasonal peaks around mid-year, with a declining trend in the most recent period (2020).
 -  "Electricalsara Stores" is the largest customer, contributing significantly to revenue(413.33 M), particularly in the brick-and-mortar segment.
   - A significant portion of revenue(468.96M) is from a single product category marked as "(Blank)," followed by other key products like Prod040.

     - **Action**: Investigate and resolve the "(Blank)" category to ensure better data integrity, and optimize inventory and marketing for top-performing products.
## 2. **Profit Analysis**:
 - Bhubaneswar contributes the highest profit percentage (10.5%), while Lucknow has a negative profit contribution (-2.7%).

 - Mumbai leads in profit contribution (23.9%), followed closely by Delhi (22.1%), showing strong profitability in these two markets.

 - Delhi dominates revenue contribution with 54.7%, followed by Mumbai (14.2%) and Ahmedabad (12.7%).

- Electricalsara Stores remains the top contributor with 46.2% of total revenue but has a low profit margin percentage (0.4%).
- Surge Stores contributes only 2.8% of revenue but has one of the highest profit margins (6.2%), suggesting efficient operations.

## 2. **Performance Insights**:
 - Bhubaneswar South leads revenue contribution (10.5%), indicating it is a top-performing zone.
- Lucknow North has a negative revenue contribution (-2.7%), indicating possible losses or inefficiencies in that zone.
- Revenue peaked in February 2020, followed by a decline starting in March. The most significant dip occurred in June 2020 with a sharp drop in both revenue and profit margin.
- The  revenue in the current year (2020) is high compared to the last year (2019) for most months, except for June 2020, where revenue fell significantly below the previous year's performance. 
- Electricalsara Stores is the top customer, contributing 46.2% of the total revenue, while other top customers like Excel Stores and Premium Stores have a significantly smaller share.

# References
   https://codebasics.io
