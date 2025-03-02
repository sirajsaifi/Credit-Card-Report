# **Credit Card Dashboard**

![](https://github.com/sirajsaifi/Credit-Card-Report/blob/main/Sheet1.png)

![](https://github.com/sirajsaifi/Credit-Card-Report/blob/main/Sheet2.png)

## **Project Objective**
Developed a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends, enabling stakeholders to monitor and analyze credit card operations effectively.

## **DAX Queries**

### **Create AgeGroup Column**
```dax
AgeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[customer_age] < 30, "20-30",
    'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
    'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
    'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
    'public cust_detail'[customer_age] >= 60, "60+",
    "unknown"
)
```

### **Create IncomeGroup Column**
```dax
IncomeGroup = SWITCH(
    TRUE(), 
    'public cust_detail'[income] < 35000, "Low",
    'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Med",
    'public cust_detail'[income] >= 70000, "High",
    "unknown"
)
```

### **Calculate Revenue**
```dax
Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
```

### **Calculate Week Number**
```dax
week_num2 = WEEKNUM('public cc_detail'[week_start_date])
```

### **Current Week Revenue**
```dax
Current_week_Revenue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
    )
)
```

### **Previous Week Revenue**
```dax
Previous_week_Revenue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1
    )
)
```

## **Project Insights**

### **Transaction and Revenue**
- Revenue and Transaction peaked during Quarter 3
- Businessmen category from Job Profession generated the maximum revenue
- Most of the Interest was generated from Married people
- Total interest is 7.84M
- Total Revenue is 55M

### **Customer**
- Personal Loans were mostly taken by Married people
- 50 - 60 years Age group witnessed the highest Median Income which is 48K
- 40 - 50 years Age group owns the highest number cars as compared to other age groups
- The highest number of houses were owned by 40 - 50 years Age group
- The Lowsest number of houses were owned by 60+ years Age group
