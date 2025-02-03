# HR Analytics-Dashboard



## Problem Statement

 

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

  
---
### **5. Dashboard Creation**
###  **Key insights**

### 1. **Total Revenue**
   - **Visual Type:** Card  
   - **Metric:** Total revenue (calculated as the sum of the `sales amount` column).  
   - **Purpose:** Displays the overall revenue across all years and transactions.

     
    
    Revenue = SUM('sales transactions'[sales_amount])

### 2. **Total Sales Quantity**
   - **Visual Type:** Card  
   - **Metric:** Total sales quantity (calculated as the sum of the `sales quantity` column).  
   - **Purpose:** Shows the total number of items sold across all transactions.


    sales Qty = SUM('sales transactions'[sales_qty])

### 3. **Revenue by Customer**
   - **Visual Type:** Horizontal Bar Chart  
   - **Metric:** Revenue by customer (sum of `sales amount`, grouped by `customer name`).  
   - **Purpose:** Highlights revenue contributions from individual customers.

### 4. **Sales Quantity by Customer**
   - **Visual Type:** Horizontal Bar Chart  
   - **Metric:** Sales quantity by customer (sum of `sales quantity`, grouped by `customer name`).  
   - **Purpose:** Displays the quantity of items purchased by individual customers.

### 5. **Sales Revenue by Year** 
   - **Visual Type:** Slicer (Year), Bar Chart  
   - **Metric:** Revenue by year (sum of revenue, grouped by year).  
   - **Purpose:** Tracks sales revenue for each year, allowing comparison of year-over-year performance.

### 6. **Sales by Region** 
   - **Visual Type:** Horizontal Bar Chart  
   - **Metric:** Sales quantity and revenue by region (grouped by market name).  
   - **Purpose:** Displays sales performance by region, helping identify top-performing markets.

### 7. **Top 5 Customers by Revenue** 
   - **Visual Type:** Bar Chart  
   - **Metric:** Revenue by top 5 customers (filtered by revenue, showing the highest revenue customers).  
   - **Purpose:** Highlights the top 5 customers based on revenue, helping to focus on the most profitable clients.

### 8. **Top 5 Products by Revenue** 
   - **Visual Type:** Bar Chart  
   - **Metric:** Revenue by top 5 products (filtered by revenue, showing the highest revenue-generating products).  
   - **Purpose:** Identifies the top-selling products, assisting with inventory and sales strategies.

### 9. **Revenue Trend Over Time** 
   - **Visual Type:** Line Chart  
   - **Metric:** Revenue trend by year/month (sum of revenue, grouped by CY date).  
   - **Purpose:** Displays the trend of revenue over time, helping to assess growth or decline in sales.


    Stakeholder Feedback :Presenting the Power BI Dashboard to stakeholders for feedback.

---
###  **Profit Analysis**

---

**1. Profit Margin Percentage**  
   - **Visual:** Measure for profit margin percentage.  
   - **Metric:** Total profit margin / Revenue.
      
   - **Purpose:** To show the percentage of profit margin for each product.


```bash
   
    Profit margin % = DIVIDE([Total profit Margin],[Revenue],0)
```

---

**2. Profit Margin Contribution**  
   - **Visual:** Measure for profit margin contribution percentage.  
   - **Metric:** Profit margin for a market / Total profit margin.
    
   - **Purpose:** To identify which markets contribute most to profit.

```bash
Profit Mragin Contribution % = DIVIDE([Total profit Margin],CALCULATE([Total profit Margin],ALL('sales products'),ALL('sales markets'),ALL('sales customers')))
```

---

**3. Aggregation Across Dimensions**  
   - **Visual:** Aggregated data across products, customers, and markets.  
   - **Metric:** Profit margin contribution across different dimensions.  
   - **Purpose:** To analyze contributions across multiple levels.

---

**4. Revenue Contribution Percentage**  
   - **Visual:** Measure for revenue contribution percentage.  
   - **Metric:** Revenue for a market / Total revenue.  
   - **Purpose:** To determine which markets contribute most to revenue.

 ```bash
 Revenue contribution % = DIVIDE([Revenue],CALCULATE([Revenue],ALL('sales products'),ALL('sales markets'),ALL('sales customers')))
```

---

**5. Profit vs. Revenue Comparison**  
   - **Visual:** Comparison of profit vs. revenue contribution.  
   - **Metric:** Revenue and profit contribution percentages.  
   - **Purpose:** To identify discrepancies between revenue and profit.

---

**6. Customer-Level Analysis**  
   - **Visual:** Tabular view of customer-level profit margins.  
   - **Metric:** Profit margin for each customer.  
   - **Purpose:** To analyze how individual customers contribute to profit.

---

**7. Unprofitable Customers**  
   - **Visual:** Identifying unprofitable customers.  
   - **Metric:** Negative profit margin for customers.  
   - **Purpose:** To identify and address customers causing losses.

---



---
###  **Performance Insights**

---

1. **Sales Comparison**:
   - **Brick-and-Mortar vs. E-commerce**: Split by sales revenue (79.5% brick-and-mortar, 20% e-commerce).
   - **Visual:** Pie chart showing sales by channel (brick-and-mortar vs e-commerce).

2. **Dynamic Profit Margin Analysis**:
   - **Performance Metrics:** Zones with negative profit margins, marked dynamically.
   - **Visual:** Dynamic coloring of zones where profit margins fall below the target (e.g., below 1% or -5%).
   - **Purpose:** Identify underperforming zones and take action.

3. **Revenue by Zone**:
   - **Visual:** Stacked bar chart
   - **Metric**: Revenue split by geographical zones.
   - **Purpose:** Shows revenue distribution across regions and helps prioritize regions with low performance.

3. **Revenue trends**:
   - **Visual:** Line and clustered column chart.
   -  **Metric:** Primary: Revenue
          Represented by the grey bars (likely "Revenue LY" for   the       previous year) and the pink bars (likely "Revenue" for the current year)
Secondary: Profit Margin %
       Represented by the orange line
   - **Purpose:** To visualize and compare revenue trends over time.The inclusion of the profit margin line adds another layer of analysis, enabling viewers to understand how revenue changes impact profitability.

---








 
 # Report Snapshot (Power BI DESKTOP)
 ![Screenshot 2025-01-15 160233](https://github.com/user-attachments/assets/b672e349-4d30-4c46-b06c-2d92124879e4)


 ![Screenshot 2025-01-15 160301](https://github.com/user-attachments/assets/89853a63-f9e2-4927-a939-f02cdec4cd37)

 
![Screenshot 2025-01-15 160321](https://github.com/user-attachments/assets/3797a445-30a3-455a-9537-15df492ebfcb)

 


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
