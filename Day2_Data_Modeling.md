# 📅 Day 2: Data Modeling & Feature Engineering (DAX)

## 🎯 Objective
After cleaning the data on Day 1, the raw numbers were accurate but lacked "Business Context." On Day 2, I focused on **Data Modeling**—creating new categories and dynamic calculations to make the data analysis-ready.

## 🛠️ Tools Used
- **Power BI Desktop** (Data View & Report View)
- **DAX (Data Analysis Expressions)**
- **Calculated Columns** vs. **Measures**

## 📋 Key Features Created

### 1. Segmentation (Calculated Columns)
I created "Smart Columns" to group employees into logical segments. This allows for deeper demographic analysis (e.g., comparing Gen Z vs. Boomers).

**A. Generation Grouping**
*Logic:* Grouped raw ages into standard generational buckets to analyze age-related trends.
dax
Generation = 
SWITCH(
    TRUE(),
    'social_media_vs_productivity'[age] < 25, "Gen Z",
    'social_media_vs_productivity'[age] < 41, "Millennial",
    'social_media_vs_productivity'[age] < 57, "Gen X",
    "Boomer"
)

**B. Social Media Usage Levels **
*Logic:* Segmented users into Low, Moderate, and High usage to test the hypothesis "Does high usage lower productivity?

Code snippet
Social Usage Level = 
IF(
    'social_media_vs_productivity'[daily_social_media_time] < 2, "Low (<2h)",
    IF('social_media_vs_productivity'[daily_social_media_time] < 4, "Moderate (2-4h)", "High (>4h)")
)

**C. Burnout Risk Indicator**
*Logic:* Flagged employees reporting burnout symptoms for more than 20 days/month to identify at-risk departments.

Code snippet
Burnout Risk = IF('social_media_vs_productivity'[days_feeling_burnout_per_month] > 20, "High Risk", "Normal")

### 2. Performance Metrics (DAX Measures)
I created explicit Measures for calculations. Unlike columns, Measures are dynamic and recalculate based on the filters applied by the user (slicers).

**A. Average Productivity Score**
Code snippet
Avg Productivity = AVERAGE('social_media_vs_productivity'[actual_productivity_score])

**B. Average Social Media Time**
Code snippet
Avg Social Time = AVERAGE('social_media_vs_productivity'[daily_social_media_time])

**C. High-Risk Employee Count**
Logic: Counts how many employees are currently flagged as "High Risk" for burnout using the CALCULATE function.
Code snippet
Burnout Count = CALCULATE(COUNTROWS('social_media_vs_productivity'), 'social_media_vs_productivi
