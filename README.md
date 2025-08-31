# Analytical-Codes
1) >>Blueprint : Electric Vehicle Population Trend Analysis 

Key Questions Solved:

 How many total EVs are currently registered? 

Which EV models and makes are most popular? 

What is the trend of EV adoption by year?

 What is the average electric range and MSRP? 

What is the geographical spread of EVs? 

How old are most EVs on the road? 

What type of EVs are most adopted (BEV vs PHEV)? 

What I built: ✅ EV population trend analysis ✅ Model and make popularity ✅ Vehicle age banding & adoption patterns ✅ Price vs range analysis ✅ Geo-mapped EV adoption across cities

Skills Demonstrated: Data modeling | DAX calculated columns & measures mastery | ETL | Regression & interactive analysis | Business Insights | engineering Allied fields Power Query (M) | BI Workspaces | dimensions & metrics | RDBMS | Interactive Visualizations | Advanced filtering | Insight generation | Theory and interactivity | Analytical storytelling for business | Visual branding and presentation

Columns used: VIN (for counting vehicles) Make Model Year EV Type (Battery Electric / Plug-In Hybrid) Electric Range Base MSRP City / Postal Code Data Cleaning & Preparation Steps: Model Year to Numeric: Converted text to whole number. Remove Missing: Filtered out rows with missing or zero VIN, Make, or Model.

 DAX Measures (& Metrics)
Total EVs: Total EVs = COUNTROWS('EV Data')

Average Base MSRP: Avg Base MSRP = AVERAGE('EV Data'[Base MSRP])

Average Electric Range: Avg Electric Range = AVERAGE('EV Data'[Electric Range])

Most Common Model Year : Top Model Year =

CALCULATE(

MAX('EV Data'[Model Year]),

TOPN(1, SUMMARIZE('EV Data', 'EV Data'[Model Year], "Count", COUNTROWS('EV Data')), [Count], DESC)

)

Total Unique Models: Unique Models = DISTINCTCOUNT('EV Data'[Model])

Groupings (DAX Columns)
Vehicle Age Band: Vehicle Age Band =
SWITCH(

TRUE(),

'EV Data'[Vehicle Age] <= 2, "0-2 Years",

'EV Data'[Vehicle Age] <= 5, "3-5 Years",

'EV Data'[Vehicle Age] <= 10, "6-10 Years",

"10+ Years"

)

 Derived Column: 

Vehicle Age : Vehicle Age = YEAR(TODAY()) - 'EV Data'[Model Year] Vehicle Age Band : Vehicle Age Band = SWITCH(TRUE(), 'EV Data'[Vehicle Age]

Relationships:
Only one main flat table is used (EV Data), so relationships were not complex. However, this model is built in a way that it's easy to extend to a star schema (e.g., separate tables for Make, City, Year).

Color Theme:
Background: Neon green automotive theme (high contrast)
Text: White on dark background
Accent: Branded green (matching EV icon), custom fonts/logos applied


Recommended Charts with Full Setup
#TypeVisual Purpose Setup

1️⃣Card (KPI)Show Key Metrics at a glance Fields: • Total EVs (DAX) • Avg Base MSRP (DAX) • Avg Electric Range (DAX) • Top Model Year (DAX)
2️⃣Clustered Column Chart Count of EVs by Model Year-Axis: Model Year Y-Axis: Count of VIN or Total EVs (Measure) Legend: EV Type or Make (optional) Tooltips: Electric Range, Base MSRP
3️⃣Stacked Bar Chart Compare EV distribution by Make Y-Axis: Make X-Axis: Count of VIN Legend: EV Type Tooltips: Avg MSRP, Electric Range
4️⃣Map (Filled or Bubble)Show EV adoption across cities or zip codes Location: City or Postal Code Size: Total EVs Tooltips: Make, Model, Model Year
5️⃣Donut Chart Vehicle Type share Legend: Electric Vehicle Type Values: Count of VIN Tooltips: Make, Model Year, Avg Range
6️⃣Tree map Model Share by Make Group: Make Details: Model Values: Count of VIN Tooltips: Avg Range, Vehicle Age
7️⃣Line Chart (Optional)Trend in EVs over time X-Axis: Model Year Y-Axis: Count of VIN Legend: EV Type or Make
8️⃣Table/Matrix Detailed view by Make + Model + Range Rows: Make, Model Values: Electric Range, Avg Base MSRP, Model Year Conditional Formatting: On Range/MSRP
9️⃣Histogram (Custom visual)Vehicle Age Distribution Axis: Vehicle Age Band Values: Count of VIN

Data Overview: Source: Government datasets 

Main Takeaways
🔋 Data uncovers where EV incentives be working 📍 High-density zones point to infrastructure needs 🧠 Range gaps indicate cost-performance tradeoffs

🔷 Data Limitations
Doesn’t include owner demographics, charging station data, or usage stats
Could be enhanced with weather, fuel cost, or CO2 savings info

2) >>Blueprint: Interactive Heart Disease Risk Analysis  

 Executive Summary:  
This project is directed to transform a raw, clinical dataset on cardiac events into a dynamic and 
insightful Analysis using a Power Tool such as Power BI . The primary objective was to move 
beyond simple data points to uncover the underlying story of heart disease risk. By analyzing 
demographic and clinical factors, we aimed to answer a critical question: Who is most at risk, 
and why? The resulting dashboard serves as a powerful tool for exploratory analysis, capable of 
delivering clear, actionable insights to both technical and non-technical audiences, from 
healthcare analysts to HR recruiters assessing analytical skills. 

2. The Initial Challenge: Finding the Signal in the Noise 
Started with a dataset containing over 1,000 patient records. While rich with potential, the raw 
data presented several problems: 
• Data Redundancy: The dataset was inflated with over 700 duplicate entries, which 
would have severely skewed any analysis and led to inaccurate conclusions. 
• Lack of Clarity: Column names were abbreviated (e.g., cp, trestbps), and key data points 
were purely numerical, making them difficult for a general audience to interpret. 
• Unstructured Insights: The relationships between factors like age, cholesterol, chest 
pain, and heart disease were hidden within the raw numbers, requiring a structured 
approach to uncover and visualize them. 
The mission was to solve these issues by building a robust, user-friendly dashboard that could 
clearly communicate risk factors and patient profiles. 

3. Phase 1: Building a Solid Foundation with Data Cleaning (Power Query) 
Before any analysis, I used Power BI's Power Query Editor to meticulously clean and prepare the 
data. This was the most critical step for ensuring the reliability of our insights. 
• Problem Solved: Data Inaccuracy 
• Action: I performed de-duplication by selecting all columns and using the 
"Remove Duplicates" function. This reduced the dataset from 1,025 to 302 
unique and valid patient records, ensuring our KPIs reflect the true population. 
• Problem Solved: Poor Readability 
• Action:  Executed column formatting by renaming technical headers to be 
descriptive. For example, cp became Chest Pain 
Type and trestbps became Resting Blood Pressure. This made the final dashboard 
intuitive. 
• Problem Solved: Enabling Deeper Analysis 
• Action: Created derived columns to segment the data. Using M language, we 
engineered an Age Group column (Young, Middle, Senior) and a Risk 
Level column (High, Low) based on cholesterol and blood pressure, allowing for 
more granular comparisons. 

4. Phase 2: The Engine Room - Data Modeling and DAX 
With clean data, I moved to the modeling phase. Because I consolidated everything into one 
clean table, no complex model relationships were needed. The focus was on writing powerful 
DAX (Data Analysis Expressions) formulas to create the metrics that would drive our visuals. 
DAX Calculated Columns (Creating User-Friendly Labels): 
These columns were added to translate numerical codes into plain English for use in filters and 
legends. 
• Disease Status = IF('heart_disease'[heart_disease] = 1, "Present", "Absent") 
• Gender = IF('heart_disease'[sex] = 1, "Male", "Female") 
• Chest Pain Label = SWITCH(TRUE(), 'heart_disease'[chest_pain_type] = 0, "Typical 
Angina", 'heart_disease'[chest_pain_type] = 1, "Atypical Angina", 
'heart_disease'[chest_pain_type] = 2, "Non-Anginal Pain", "Asymptomatic") 
DAX Measures (The Core KPIs): 
These measures perform the crucial calculations that quantify our insights. 
• Overall Prevalence: Heart Disease Prevalence = 
DIVIDE(CALCULATE(COUNTROWS('heart_disease'), 'heart_disease'[heart_disease]=1), 
COUNTROWS('heart_disease')) 
• Gender-Specific Risk: Male Disease Ratio = CALCULATE([Heart Disease Prevalence], 
'heart_disease'[sex]=1) 
• Age-Related Risk: Avg Age with Disease = CALCULATE(AVERAGE('heart_disease'[age]), 
'heart_disease'[heart_disease]=1) 
• Clinical Indicators: High Cholesterol Rate = 
DIVIDE(CALCULATE(COUNTROWS('heart_disease'), 'heart_disease'[cholesterol] > 240), 
COUNTROWS('heart_disease')) 

5. Phase 3: The Story - Visuals and Insights 
Each visual was carefully chosen to answer a specific question and prove a point. 
• KPI Cards (Top Banner) 
• Reasoning: To provide an immediate, high-level summary of the most critical 
metrics. This gives any viewer an instant understanding of the dataset's key 
f
 igures before they dive deeper. 
• Insights: Showcases the overall disease count, the average age of afflicted 
patients, and the male/female risk ratio immediately. 

• Bar Chart: Age Impact on Heart Disease 
• Visual: Clustered Bar Chart 
• Axis: X-Axis: Age Group, Y-Axis: Count of Patients, Legend: Disease Status 
• Reasoning: This is the best visual for comparing a metric across distinct 
categories. It was deployed to directly address the hypothesis that age is a major 
risk factor. 
• Problem Solved: It visually proves that the prevalence of heart disease increases 
dramatically with age, with the "Senior" group showing the highest proportion of 
cases. 

• Donut Chart: Gender Risk Breakdown 
• Visual: Donut Chart 
• Fields: Legend: Gender, Values: Disease Count 
• Reasoning: A donut or pie chart is perfect for showing the proportional 
breakdown of a single metric. We used it to highlight gender disparity within the 
diseased population. 
• Problem Solved: It instantly communicates that among patients with heart 
disease, males represent a significantly larger portion than females, guiding 
further investigation into gender-specific risks. 

• Scatter Plot: Cholesterol vs. Age 
• Visual: Standard Scatter Chart 
• Axes: X-Axis: age, Y-Axis: cholesterol, Legend: Disease Status 
• Reasoning: A scatter plot is the ultimate tool for visualizing the relationship and 
correlation between two numerical variables. 
• Problem Solved: This chart was the centerpiece for revealing multi-factor risk. It 
clearly shows a cluster of data points in the upper-right quadrant (representing 
older patients with high cholesterol) that are almost exclusively colored for 
"Disease Present," providing powerful, undeniable evidence of combined risk 
factors. 

• Line Chart: BP Spikes by Pain Type 
• Visual: Line Chart 
• Axes: X-Axis: Chest Pain Label, Y-Axis: Average Resting BP 
• Reasoning: A line chart excels at showing trends across an ordered category. 
Here, we use it to see if blood pressure trends differed across types of chest pain. 
• Problem Solved: It helps identify if certain symptoms (pain types) are associated 
with higher clinical indicators like blood pressure, adding another layer to the 
diagnostic picture.

3) >>Blueprint : Breast Cancer Diagnosis Interactive Dashboard (Tableau) 

1. Project Context & Objective 
In the age of data-driven healthcare, early detection is crucial for diseases like breast cancer. 
With a dataset of 569 patients and 32 tumor features (radius, texture, symmetry, etc.), I set out 
to build an interactive Tableau dashboard that transforms complex raw data into clear, 
actionable narratives. The goal: help analysts and healthcare professionals quickly spot risk 
factors, explore diagnostic patterns, and make informed recommendations. 

2. The Challenges Solved 
• Data Clarity: Original column names were cryptic and not user-friendly. 
• Missing Context: No pre-defined groupings for size/risk, which are crucial for segmenting 
cases. 
• Insight Extraction: Relationship between tumor features and malignant/benign diagnosis 
hidden in numbers. 
• Redundancy & Cleanliness: Need to ensure one patient per record, no missing values or 
mis-typed entries. 
• Visual Storytelling: Typical dashboards stagger on basic bar charts—needed advanced, 
more revealing visuals. 

3. Data Preparation Solutions 
(a) Column Formatting & Data Types: 
• Renamed headers (ex: concave points_mean → “Concave Points Mean”) for clinical 
clarity. 
• Corrected types (e.g., forced “id” to String/Dimension, numerical fields as Measure). 
(b) De-duplication & Cleaning: 
• Confirmed unique "id" per patient; verified data integrity (no null/duplicate records). 
(c) Engineered Fields: 
• Tumor Size Group: IF [radius_mean] < 10 THEN "Small" ELSEIF [radius_mean] <= 15 
THEN "Medium" ELSE "Large" END 
• Risk Level: IF [radius_mean] > 15 AND [compactness_mean] > 0.1 THEN "High" ELSE 
"Low" END 
• Diagnosis Label: IF [diagnosis]="M" THEN "Malignant" ELSE "Benign" END 

4. The Analytical Model (Calculated Fields/Measures) 
Key Calculated Fields (by script): 
• Total Patients: COUNTD([id]) 
• Malignant Count: SUM(IF [diagnosis] = "M" THEN 1 ELSE 0 END) 
• Cancer Prevalence Rate: SUM(IF [diagnosis] = "M" THEN 1 ELSE 0 END) / COUNTD([id]) 
• Avg Radius (Malignant): AVG(IF [diagnosis]="M" THEN [radius_mean] ELSE NULL END) 
• High Risk Count: SUM(IF [Risk Level]="High" THEN 1 ELSE 0 END) 
• Diagnosis Ratio (Malignant): SUM(IF [diagnosis]="M" THEN 1 ELSE 0 END) / 
COUNTD([id]) 
No relationships/models needed—single-table data sufficed! 

5. KPI Choices & Rationale 
• Malignant/Benign Counts/Prevalence: Instant sense of dataset baseline and risk 
proportions. 
• Average Size/Texture/Perimeter by Diagnosis: Surfaced key physical differences between 
malignant and benign cases, giving actionable features to clinicians. 
• High Risk Segment Counts: Identified how many patients warrant close 
monitoring/screening. 
• Diagnosis Ratios: Quantitatively track improvement or change over data updates/time. 

6. Visuals Deployed – Every Chart & Why 
Chart 1: Column Chart – Size Impact on Diagnosis 
• Axis: X–Tumor Size Group, Y–Count (SUM([Number of Records])), Color–Diagnosis 
• Why: Clear, vertical orientation highlights which tumor sizes are likeliest to be malignant. 
• Problem Answered: Demonstrates size risk for clinicians; provides urgency to investigate 
"Large" tumors. 

Chart 2: Treemap – Diagnosis Distribution 
• Axis: Rectangle area–Count, Color–Diagnosis 
• Why: Replaces the pie (for variation), instantly communicates relative prevalence, 
making outliers easy to spot. 
• Problem Answered: Visualizes the dominant class, showing that benign tumors are more 
prevalent but malignant cases require focus. 

Chart 3: Scatter Plot – Radius vs. Texture (Colored by Diagnosis) 
• Axis: X–radius_mean, Y–texture_mean, Color–Diagnosis, Size–Count if needed 
• Why: Shows how multiple features interact; clusters reveal which measurements 
coincide with higher malignancy risk. 
• Problem Answered: Exposes high-risk feature zones, aiding both EDA and clinical insight. 

Chart 4: Area Chart – Perimeter by Smoothness 
• Axis: X–Smoothness Binned, Y–AVG(perimeter_mean), Color–Diagnosis 
• Why: Area conveys cumulative perimeter risk over smoothness spectrum. 
• Problem Answered: Answers whether less smooth tumors with higher size indicate 
malignancy. 

Chart 5: Crosstab (Heat Matrix) – Compactness by Size & Diagnosis 
• Axis: Rows–Tumor Size Group, Columns–Diagnosis, Color/Text–AVG(compactness_mean) 
• Why: Pinpoints “hot” cells—where size and feature combos flag highest concern. 
• Problem Answered: Allows targeting of at-risk subgroups for further study. 

Chart 6: Bullet Graph – Overall Malignant Risk 
• Axis: Horizontal Bar–Malignant Prevalence, Reference–50%, Color–benchmark alert 
• Why: Quantifies dataset risk; easy to spot if group exceeds “danger” threshold. 
• Problem Answered: Instantly communicates whether the cohort is high/low risk to non
specialist viewers. 

7. Impact: Problems Solved, Insights Unlocked 
• Translated cryptic, hard-to-read raw data into high-impact visuals and KPIs 
• Surface at-risk patient profiles by size, compactness, and texture—empowering targeted 
investigation 
• Showed clinicians/statisticians which feature intersections to focus on for screening 
• Provided an intuitive, interactive platform for HRs/data scientists to test hypothesis 
• Enabled benchmarking: future data can be compared and updated against this analytical 
baseline 
• Introduced novel visualization types (treemap, heat matrix, bullet graph) to go beyond 
textbook dashboards

4) >>Blueprint  Global Airport Analysis Dashboard 
      Featuring Custom DAX KPIs, Time Zone Mapping, Hemisphere Logic & Country Ranking 
Tools Used: Power BI, Power Query, DAX 
 
      1. Project Context 
In a world that thrives on connectivity, understanding the global spread and characteristics of 
airports is vital for businesses, logistics, travel, and infrastructure planning. This project 
analyzes a dataset of airports from around the world to extract insights based on geography, 
timezone, and frequency of distribution. 
 
       2. Define the Problem / Business Question 
    How are airports distributed globally by country, city, and time zone? 
    Which countries dominate airspace infrastructure? 
    Can we derive custom metrics like time zone regions or hemispheric classification? 
 
      3. Tools Used 
Tool Purpose 
Power BI Data visualization and storytelling 
Power Query Data cleaning, transformation 
DAX Custom KPIs, calculations, ranking logic 
 
          4. Walk Through Process 
     A. Power Query (Data Cleaning Steps) 
• Loaded dataset airports.csv 
• Verified original column names like AirportName, IATA, GeoPointLat, Country_Name, 
etc. 
• Ensured correct data types: 
o Decimal: GeoPointLat, GeoPointLong, UTC_Offset_Hours 
o Text: all others 
• No renaming of columns 
• Removed duplicates using: 
o AirportName, IATA, Country_Name (as composite keys) 
 
        B. Data Modeling 
No additional relationships were required as data was flat. However, calculated columns were 
created for categorization and advanced filtering. 
 
              5. DAX: Custom KPIs & Ranking Logic 
       Measures: 
dax 
CopyEdit 
Total Airports = COUNTROWS(airports) 
 
Total Countries = DISTINCTCOUNT(airports[Country_Name]) 
 
Total Cities = DISTINCTCOUNT(airports[City_Name]) 
 
Avg UTC Offset (Hrs) = AVERAGE(airports[UTC_Offset_Hours]) 
 
Airports per Country = COUNT(airports[AirportName]) 
 
Airports per TimeZone = COUNT(airports[AirportName]) 
 
      Calculated Columns: 
dax 
CopyEdit -- TimeZone Region Bucketing 
TimeZone Region =  
SWITCH( 
    TRUE(), 
    airports[UTC_Offset_Hours] <= -6, "Americas (West)", 
    airports[UTC_Offset_Hours] > -6 && airports[UTC_Offset_Hours] <= 0, 
"Europe/Africa", 
airports[UTC_Offset_Hours] > 0 && airports[UTC_Offset_Hours] <= 6, 
"Asia", 
airports[UTC_Offset_Hours] > 6, "Oceania", 
"Other" 
) 
dax 
CopyEdit -- Hemisphere Classification 
Hemisphere =  
IF(airports[GeoPointLat] >= 0, "Northern Hemisphere", "Southern Hemisphere") 

6. Visualizations Built 
Visual Type 
Description 
KPI Cards Total Airports, Countries, Cities, Avg. UTC 
Bar Chart Top Countries by Airport Count 
Donut Chart Airports by TimeZone Region 
Map Visual Airport locations using Lat/Long 
Table 
Detailed airport list 
Slicers 
Filter by Country, City, Hemisphere, Region 

7. Main Takeaways 
• The majority of airports are clustered in the Northern Hemisphere, especially in 
Americas & Europe/Africa time zones. 
• Some countries like the USA, Canada, Brazil, India, and Australia have higher airport 
densities. 
• Airports span diverse time zones, revealing complexity in global coordination. 

8. Use Visuals to Make My Points 
• Dark theme dashboard to enhance readability 
• Custom KPIs and slicers enabled dynamic filtering 
• Geospatial mapping highlighted global spread intuitively 
• Category columns like “TimeZone Region” gave structure to otherwise numeric offsets 

9. Reflections 
This dashboard proves how even a relatively flat dataset can be turned into rich insights with: 
• Custom DAX logic 
• Smart grouping (TimeZone & Hemisphere) 
• Clean visuals and interactivity 

10. Limitations of Data 
• No elevation data (elevation_ft) 
• No airport types (small_airport, heliport, etc.) 
• No flight volume, passengers, or operational data 

11. What Could Have Been Achieved With More Data 
• Runway elevation analysis for aviation safety 
• Airport type breakdown for infrastructure classification 
• Passenger or cargo flow heatmaps 
• Airline-wise airport frequency 
• Temporal patterns with flight schedules

5) >>Blueprint HDFC Bank Stock Analysis Dashboard  

1. Project Context 
HDFC Bank is one of India’s largest private banks and a key component of the stock market. 
The objective of this project was to analyze long-term (daily/monthly)  & short-term (intraday)  
stock data to uncover price patterns, volatility, and trading insights, and to build a Power BI 
dashboard that can be used by analysts, traders, and decision-makers. 

2. Problem Statement 

The client wanted a dashboard to: 
• Track daily, monthly, and intraday stock performance 
• Identify volatility patterns across multiple timeframes (1d, 1m, 5m, 15m datasets) 
• Measure returns, trading volume trends, and intraday behaviors 
• Provide KPIs for quick decision-making 
• Enable visual storytelling with comparisons between daily vs intraday movements 

3. Datasets Used 
• HDFC_1d.csv → Daily OHLC + Volume 
• HDFC_1m.csv → Monthly OHLC + Volume 
• HDFC_5m.csv → 5-minute OHLC + Volume (Intraday) 
• HDFC_15m.csv → 15-minute OHLC + Volume (Intraday) 
Columns included: 
t
 imestamp, Open, High, Low, Close, Volume 

4. Data Cleaning & Preparation (Power Query) 
 
Step-by-step cleaning checklist: 
• Converted timestamp → Date/Time type 
• Derived columns: Year, Month Name, Month Number, Quarter, Day Name, Hour 
• Ensured numeric formatting for Open, High, Low, Close, Volume 
• Removed nulls and duplicates 
• Standardized text fields (if any) 

5. Data Modeling 
• 4 fact tables (HDFC_1d, HDFC_1m, HDFC_5m, HDFC_15m) kept separate 
• Calendar table (if needed) for proper time intelligence 
• Relationships established only where required (mainly by timestamp granularity) 

6. Key KPIs (DAX Measures) 
• Daily KPIs (from HDFC_1d): 
o Average Daily Volatility = AVERAGEX(HDFC_1d, HDFC_1d[High] - HDFC_1d[Low]) 
o Max Daily Close, Min Daily Close, Avg Daily Volume 
• Monthly KPIs (from HDFC_1m): 
o Monthly Return % = DIVIDE((MAX([Close]) - MIN([Open])), MIN([Open]), 0) * 100 
o Average Monthly Return % using AVERAGEX + SUMMARIZE 
o Highest Monthly Close, Lowest Monthly Close 
• 5-Min Intraday KPIs (HDFC_5m): 
o Avg Price Move 5m = AVERAGEX(HDFC_5m, ABS(HDFC_5m[Close] - 
HDFC_5m[Open])) 
o Max/Min Intraday Price (5m), Avg Intraday Volume 
• 15-Min Intraday KPIs (HDFC_15m): 
o Volatility 15m = AVERAGEX(HDFC_15m, HDFC_15m[High] - HDFC_15m[Low]) 
o Volatility % as ratio of Open price 
o Max/Min Intraday Price (15m), Avg Volatility % 

7. Visuals & Titles 
Page 1 — Market Overview (Daily & Monthly) 
• Cards (Top Row): Max Close, Min Close, Avg Volume, Avg Daily Volatility 
• Line Chart: HDFC Daily Closing Price Trend (HDFC_1d, timestamp vs Close) 
• Column Chart: Daily Trading Volume (HDFC_1d, timestamp vs Volume) 
• Area Chart: Daily Price Volatility (High-Low) (HDFC_1d) 
• Column Chart: Average Volume by Day of Week (HDFC_1d, Day Name) 
• Column Chart: Monthly Return % (HDFC_1m, Month Name) 
• Line Chart: Monthly Closing Price Trend (HDFC_1m, Month Name vs Close) 
• Bar Chart: Average Monthly Volume by Quarter (HDFC_1m, Quarter) 
Page 2 — Intraday Analysis (5m & 15m) 
• Cards (Top Row): Max 5m Price, Min 5m Price, Avg Price Move 5m, Avg Volume 15m 
• Line Chart: Intraday Price Movement (5m) (Hour vs Close) 
• Column Chart: Trading Volume by Hour (5m) (Hour vs Volume) 
• Scatter Chart: Price vs Volume (5m) (Close vs Volume) 
• Line Chart: Intraday Price Movement (15m) (Hour vs Close) 
• Column Chart: Trading Volume by Hour (15m) (Hour vs Volume) 
• Area Chart: Volatility per 15-Min Interval (Hour vs Volatility 15m DAX) 

8. Insights & Takeaways 
• HDFC shows clear volatility patterns intraday, with spikes during opening and closing 
market hours. 
• Daily volatility stays within a predictable range, but 5m & 15m intervals capture micro
movements critical for traders.

6) >>Blueprint MySQL Workbench  (Pelican Store Analysis)

     1. Total Revenue (Sales) 
Purpose: Overall sales value—the top-line KPI. 
sql 
SELECT ROUND(SUM(Sales), 2) AS total_revenue 
FROM pelican_store; 
Result: total_revenue'7760.05' 

2. Total Items Sold 
Purpose: Overall basket throughput. 
sql 
SELECT SUM(Items) AS total_items_sold 
FROM pelicanstore; 
Result: total_items_sold 322 

3. Average Order Value (AOV) 
Purpose: Efficiency of each transaction (revenue per order). 
sql 
SELECT ROUND(SUM(Sales) / COUNT(*), 2) AS avg_order_value 
FROM pelican_store; 
Result: avg_order_value 
77.6 

4. Average Items per Order 
Purpose: Basket size trend. 
sql 
SELECT ROUND(AVG(Items), 2) AS avg_items_per_order 
FROM pelican_store; 
Result: avg_items_per_order 
3.22 

5. Average Discount per Order 
Purpose: Promotion intensity and margin pressure. 
sql 
SELECT ROUND(AVG(Discount), 2) AS avg_discount_per_order 
FROM pelican_store; 
Result: avg_discount_per_order 
22.45 

6. Discount Ratio (Discount as % of Sales) 
Purpose: How much discount we give relative to sales; proxy for margin dilution. 
sql 
SELECT ROUND(SUM(Discount) / NULLIF(SUM(Sales),0) * 100, 2) AS discount_pct_of_sales 
FROM pelican_store; 
Result: discount_pct_of_sales 
28.93 

7. Revenue by Payment Method (top driver analysis) 
Purpose: Identify top-performing payment channels. 
sql 
SELECT MethodOfPayment, 
COUNT(*) AS orders, 
SUM(Items) AS items_sold, 
ROUND(SUM(Sales), 2) AS revenue, 
ROUND(SUM(Discount), 2) AS total_discount, 
ROUND(AVG(Sales), 2) AS avg_order_value 
FROM pelican_store 
GROUP BY MethodOfPayment 
ORDER BY revenue DESC; 
Result: orders, items_sold, revenue, total_discount, avg_order_value 
100, 322, 7760.05, 2245.18, 77.6 

8. Conversion proxy by Payment Method (Avg Items and Avg Discount) 
Purpose: Examine behavior differences across payment rails. 
sql 
SELECT MethodOfPayment, 
ROUND(AVG(Items), 2) AS avg_items, 
ROUND(AVG(Discount), 2) AS avg_discount 
FROM pelican_store 
GROUP BY MethodOfPayment 
ORDER BY avg_items DESC; 
Result: Gender, orders, revenue, avg_order_value, total_discount 
Female, 93, 7364.65, 79.19, 2154.58 
Male, 7, 395.4, 56.49, 90.6 

9. Revenue and AOV by Gender 
Purpose: Segment performance by gender. 
sql 
SELECT Gender, 
COUNT(*) AS orders, 
ROUND(SUM(Sales), 2) AS revenue, 
ROUND(AVG(Sales), 2) AS avg_order_value, 
ROUND(SUM(Discount), 2) AS total_discount 
FROM pelican_store 
GROUP BY Gender 
ORDER BY revenue DESC; 
Result: age_band, orders, items_sold, revenue, avg_order_value, avg_discount 
45-54, 28, 99, 2508.68, 89.6, 24.05 
35-44, 29, 92, 2150.61, 74.16, 20.38 
25-34, 24, 85, 1887.33, 78.64, 29.05 
65+, 6, 16, 477.77, 79.63, 15 
55-64, 8, 22, 417.56, 52.2, 16.56 
<25, 5, 8, 318.1, 63.62, 12.18 

10. Revenue by Marital Status 
Purpose: Understand household effect. 
sql 
SELECT MaritalStatus, 
COUNT(*) AS orders, 
ROUND(SUM(Sales), 2) AS revenue, 
ROUND(AVG(Sales), 2) AS avg_order_value 
FROM pelican_store 
GROUP BY MaritalStatus 
ORDER BY revenue DESC; 
Result: Customer, orders, items_sold, revenue, total_discount 
98, 1, 10, 287.59, 18 
23, 1, 7, 266, 66.5 
97, 1, 9, 253, 82.75 
94, 1, 17, 229.5, 33 
41, 1, 13, 198.8, 62.7 
28, 1, 5, 192.8, 48.2 
51, 1, 6, 176.62, 58.88 
13, 1, 9, 160.4, 103.6 
93, 1, 5, 159.75, 0 
71, 1, 5, 155.32, 57.18 

11. Age Cohort performance 
Purpose: Identify sweet-spot age bands. 
sql 
WITH cohorts AS ( 
SELECT CASE 
WHEN Age < 25 THEN '<25' 
WHEN Age BETWEEN 25 AND 34 THEN '25-34' 
WHEN Age BETWEEN 35 AND 44 THEN '35-44' 
WHEN Age BETWEEN 45 AND 54 THEN '45-54' 
WHEN Age BETWEEN 55 AND 64 THEN '55-64' 
ELSE '65+' 
END AS age_band, 
Sales, Items, Discount 
FROM pelican_store 
) 
SELECT age_band, 
COUNT(*) AS orders, 
SUM(Items) AS items_sold, 
ROUND(SUM(Sales),2) AS revenue, 
ROUND(AVG(Sales),2) AS avg_order_value, 
ROUND(AVG(Discount),2) AS avg_discount 
FROM cohorts 
GROUP BY age_band 
ORDER BY revenue DESC; 
Result: Customer, total_discount, revenue, discount_pct_of_sales 
39, 25.02, 13.23, 189.12 
91, 158.3, 95.2, 166.28 
62, 91.48, 59.91, 152.7 
45, 35.2, 23.8, 147.9 
4, 121.1, 100.4, 120.62 
42, 16.5, 19.5, 84.62 
90, 46.4, 57.6, 80.56 
20, 32.2, 44.8, 71.88 
63, 37.4, 53.6, 69.78 
99, 31.4, 47.6, 65.97 

12. Top 10 High-Value Customers 
Purpose: Target for retention/loyalty. 
sql 
SELECT Customer, 
       COUNT(*) AS orders, 
       SUM(Items) AS items_sold, 
       ROUND(SUM(Sales),2) AS revenue, 
       ROUND(SUM(Discount),2) AS total_discount 
FROM pelican_store 
GROUP BY Customer 
ORDER BY revenue DESC 
LIMIT 10; 
Result: Leaderboard of highest-revenue customers. 

13. Heavy Discount users (Top 10 by discount share) 
Purpose: Margin risk monitoring. 
sql 
SELECT Customer, 
       ROUND(SUM(Discount),2) AS total_discount, 
       ROUND(SUM(Sales),2) AS revenue, 
       ROUND(SUM(Discount) / NULLIF(SUM(Sales),0) * 100, 2) AS discount_pct_of_sales 
FROM pelican_store 
GROUP BY Customer 
HAVING SUM(Sales) > 0 
ORDER BY discount_pct_of_sales DESC, total_discount DESC 
LIMIT 10; 
Result: Customers who get the largest discount share relative to their spend. 

14. Basket Mix: Items vs. Sales correlation proxy 
Purpose: Check whether bigger baskets translate to higher spend consistently. 
sql 
SELECT ROUND(AVG(Items),2) AS avg_items, 
       ROUND(AVG(Sales),2) AS avg_sales, 
       ROUND(AVG(Sales) / NULLIF(AVG(Items),0), 2) AS avg_sales_per_item 
FROM pelican_store; 
Result: High-level efficiency metric (revenue per item). 

15. Payment Method efficiency (Sales per Item) 
Purpose: Identify channels with the best monetization per item. 
sql 
SELECT MethodOfPayment, 
       ROUND(SUM(Sales) / NULLIF(SUM(Items),0), 2) AS sales_per_item, 
       ROUND(SUM(Sales),2) AS revenue, 
       SUM(Items) AS items 
FROM pelican_store 
GROUP BY MethodOfPayment 
ORDER BY sales_per_item DESC; 
Result: Rank payment methods by revenue-per-item efficiency. 

16. Gender × Marital cross-segmentation 
Purpose: Pinpoint strongest demographic segment. 
sql 
SELECT Gender, 
       MaritalStatus, 
       COUNT(*) AS orders, 
       ROUND(SUM(Sales),2) AS revenue, 
       ROUND(AVG(Sales),2) AS avg_order_value 
FROM pelican_store 
GROUP BY Gender, MaritalStatus 
ORDER BY revenue DESC; 
Result: Which demographic combination spends the most. 

17. Price-sensitivity: Average Discount by Age Band 
Purpose: Spot groups most responsive to discounts. 
sql 
WITH cohorts AS ( 
  SELECT CASE 
           WHEN Age < 25 THEN '<25' 
           WHEN Age BETWEEN 25 AND 34 THEN '25-34' 
           WHEN Age BETWEEN 35 AND 44 THEN '35-44' 
           WHEN Age BETWEEN 45 AND 54 THEN '45-54' 
           WHEN Age BETWEEN 55 AND 64 THEN '55-64' 
           ELSE '65+' 
         END AS age_band, 
         Discount 
  FROM pelican_store 
) 
SELECT age_band, 
       ROUND(AVG(Discount),2) AS avg_discount_per_order 
FROM cohorts 
GROUP BY age_band 
ORDER BY avg_discount_per_order DESC; 
Result: Age cohorts ranked by discount taken. 

18. High vs Low Discount impact on AOV 
Purpose: Understand discount thresholds on order value. 
sql 
WITH bands AS ( 
  SELECT CASE 
           WHEN Discount >= 50 THEN '50+' 
           WHEN Discount BETWEEN 20 AND 49.99 THEN '20-49.99' 
           WHEN Discount BETWEEN 1 AND 19.99 THEN '1-19.99' 
           ELSE '0' 
         END AS discount_band, 
         Sales 
  FROM pelican_store 
) 
SELECT discount_band, 
       COUNT(*) AS orders, 
       ROUND(AVG(Sales),2) AS avg_order_value 
FROM bands 
GROUP BY discount_band 
ORDER BY FIELD(discount_band,'0','1-19.99','20-49.99','50+'); 
Result: How AOV changes with discount band. 

19. Outlier detection: Highest single-order Sales 
Purpose: Audit and campaign insights. 
sql 
SELECT * 
FROM pelican_store 
ORDER BY Sales DESC 
LIMIT 5; 
Result: Top 5 largest orders for QA/strategies. 

20. Quality checks: Negative or inconsistent values 
Purpose: Data integrity. 
sql 
SELECT * 
FROM pelican_store 
WHERE Sales < 0 OR Items <= 0 OR Discount < 0 OR Age <= 0; 
Result: Returns any suspicious records (should be zero rows)   

7) >> MYsql Workbench Worldcup Analysis

SCENARIO 1: Scoring Trends 
• Goals per match evolution by year 
• Decade-wise scoring patterns 
• Highest scoring matches 
• Top scoring teams by tournament 

SCENARIO 2: Team Performance 
• Most successful teams across all World Cups 
• Performance by tournament stage 
• Home advantage analysis 
• Winners and runners-up tracking 

SCENARIO 3: Attendance Patterns 
• Attendance trends over time 
• Stadium capacity utilization 
• Match Importance vs attendance 
• Host country impact on crowds 

SCENARIO 4: Geographic Analysis 
• Matches by host country 
• Most-used stadiums 
• Continental distribution 
• Venue efficiency metrics 

SCENARIO 5: Referee Patterns 
• Most active referees 
• Referee nationality analysis 
• High-scoring matches by referee 
• Performance in crucial matches 

SCENARIO 6: Tournament Evolution 
• Tournament size growth 
• Format changes over time 
• Duration analysis 
• Penalty shootout trends 

SCENARIO 7: Advanced KPIs 
• Tournament competitiveness index 
• Stadium ROI analysis 
• Team consistency metrics 
• Overall tournament quality scores 

CODES-Snippets 

SCENARIO 1: SCORING TRENDS ANALYSIS 
1.1 Goals per match by tournament year 
sql 
SELECT  
year, 
COUNT(DISTINCT game_id) as total_matches, 
SUM(goals) as total_goals, 
ROUND(SUM(goals) / COUNT(DISTINCT game_id), 2) as avg_goals_per_match, 
MAX(goals) as highest_goals_in_match, 
MIN(goals) as lowest_goals_in_match 
FROM world_cup_data  
GROUP BY year  
ORDER BY year; 

1.2 Top scoring teams by tournament 
sql 
SELECT  
year, 
team, 
SUM(goals) as total_goals, 
COUNT(*) as matches_played, 
ROUND(AVG(goals), 2) as avg_goals_per_match 
FROM world_cup_data  
GROUP BY year, team 
HAVING matches_played >= 3 
ORDER BY year, total_goals DESC; 

1.3 Highest scoring individual matches 
sql 
SELECT  
year, 
date, 
stadium, 
MAX(CASE WHEN team_num = 1 THEN team END) as team1, 
MAX(CASE WHEN team_num = 1 THEN goals END) as team1_goals, 
MAX(CASE WHEN team_num = 2 THEN team END) as team2, 
MAX(CASE WHEN team_num = 2 THEN goals END) as team2_goals, 
(MAX(CASE WHEN team_num = 1 THEN goals END) +  
MAX(CASE WHEN team_num = 2 THEN goals END)) as total_goals 
FROM world_cup_data 
GROUP BY year, date, stadium, game_id 
ORDER BY total_goals DESC 
LIMIT 20; 

1.4 Tournament scoring evolution (decade-wise) 
sql 
SELECT  
CASE  
WHEN year BETWEEN 1930 AND 1939 THEN '1930s' 
WHEN year BETWEEN 1940 AND 1949 THEN '1940s' 
WHEN year BETWEEN 1950 AND 1959 THEN '1950s' 
WHEN year BETWEEN 1960 AND 1969 THEN '1960s' 
WHEN year BETWEEN 1970 AND 1979 THEN '1970s' 
WHEN year BETWEEN 1980 AND 1989 THEN '1980s' 
WHEN year BETWEEN 1990 AND 1999 THEN '1990s' 
WHEN year BETWEEN 2000 AND 2009 THEN '2000s' 
WHEN year BETWEEN 2010 AND 2019 THEN '2010s' 
ELSE '2020s' 
END as decade, 
COUNT(DISTINCT year) as tournaments, 
COUNT(DISTINCT game_id) as total_matches, 
SUM(goals) as total_goals, 
ROUND(AVG(goals), 2) as avg_goals_per_team_per_match 
FROM world_cup_data 
GROUP BY decade 
ORDER BY decade; 

SCENARIO 2: TEAM PERFORMANCE ANALYSIS 
2.1 Most successful teams across all World Cups 
sql 
SELECT  
team, 
COUNT(DISTINCT year) as tournaments_played, 
COUNT(*) as total_matches, 
SUM(goals) as total_goals_scored, 
ROUND(AVG(goals), 2) as avg_goals_per_match, 
COUNT(CASE WHEN stage = 'FINAL ROUND' THEN 1 END) as final_appearances, 
COUNT(CASE WHEN stage = '1/2 FINAL' THEN 1 END) as semifinal_appearances 
FROM world_cup_data 
GROUP BY team 
HAVING tournaments_played >= 5 
ORDER BY tournaments_played DESC, total_goals_scored DESC; 

2.2 Team performance by tournament stage 
sql 
SELECT  
stage, 
COUNT(DISTINCT game_id) as matches, 
COUNT(DISTINCT team) as teams_involved, 
SUM(goals) as total_goals, 
ROUND(AVG(goals), 2) as avg_goals_per_team, 
MAX(goals) as highest_individual_score 
FROM world_cup_data 
WHERE stage IS NOT NULL 
GROUP BY stage 
ORDER BY avg_goals_per_team DESC; 

2.3 Home advantage analysis 
sql 
SELECT  
CASE  
WHEN team = home THEN 'Home Team' 
ELSE 'Away Team' 
END as team_status, 
COUNT(*) as matches, 
SUM(goals) as total_goals, 
ROUND(AVG(goals), 2) as avg_goals_per_match, 
COUNT(CASE WHEN goals >= 2 THEN 1 END) as high_scoring_matches 
FROM world_cup_data 
WHERE home IS NOT NULL 
GROUP BY team_status; 

2.4 Tournament winners and runners-up analysis 
sql 
SELECT  
year, 
MAX(CASE WHEN stage = 'FINAL ROUND' AND team_num = 1 THEN team END) as team1, 
MAX(CASE WHEN stage = 'FINAL ROUND' AND team_num = 1 THEN goals END) as team1_goals, 
MAX(CASE WHEN stage = 'FINAL ROUND' AND team_num = 2 THEN team END) as team2, 
MAX(CASE WHEN stage = 'FINAL ROUND' AND team_num = 2 THEN goals END) as team2_goals, 
CASE  
WHEN MAX(CASE WHEN stage = 'FINAL ROUND' AND team_num = 1 THEN goals END) >  
MAX(CASE WHEN stage = 'FINAL ROUND' AND team_num = 2 THEN goals END) 
THEN MAX(CASE WHEN stage = 'FINAL ROUND' AND team_num = 1 THEN team END) 
ELSE MAX(CASE WHEN stage = 'FINAL ROUND' AND team_num = 2 THEN team END) 
END as winner, 
stadium as final_venue 
FROM world_cup_data 
WHERE stage = 'FINAL ROUND' 
GROUP BY year, stadium 
ORDER BY year; 

SCENARIO 3: ATTENDANCE PATTERNS ANALYSIS 
3.1 Attendance trends by year 
sql 
SELECT  
year, 
COUNT(DISTINCT game_id) as total_matches, 
SUM(attendance) / COUNT(DISTINCT game_id) as avg_attendance_per_match, 
MAX(attendance) as highest_attendance, 
MIN(attendance) as lowest_attendance, 
STDDEV(attendance) as attendance_std_dev 
FROM world_cup_data 
GROUP BY year 
ORDER BY year; 

3.2 Stadium capacity utilization analysis 
sql 
SELECT  
stadium, 
COUNT(DISTINCT game_id) as matches_hosted, 
AVG(attendance) as avg_attendance, 
MAX(attendance) as max_attendance, 
MIN(attendance) as min_attendance, 
year 
FROM world_cup_data 
GROUP BY stadium, year 
HAVING matches_hosted >= 3 
ORDER BY avg_attendance DESC 
LIMIT 20; 

3.3 Attendance by tournament stage 
sql 
SELECT  
stage, 
COUNT(DISTINCT game_id) as matches, 
ROUND(AVG(attendance), 0) as avg_attendance, 
MAX(attendance) as peak_attendance, 
MIN(attendance) as min_attendance 
FROM world_cup_data 
WHERE stage IS NOT NULL 
GROUP BY stage 
ORDER BY avg_attendance DESC; 

3.4 Host country attendance impact 
sql 
SELECT  
year, 
home as host_country, 
COUNT(DISTINCT game_id) as total_matches, 
ROUND(AVG(attendance), 0) as avg_attendance, 
SUM(attendance) as total_attendance, 
MAX(attendance) as peak_single_match 
FROM world_cup_data 
GROUP BY year, home 
ORDER BY year; 

3.5 Attendance patterns by match importance 
sql 
SELECT  
CASE  
WHEN stage LIKE '%FINAL%' THEN 'Finals' 
WHEN stage LIKE '%1/2%' THEN 'Semi-Finals' 
WHEN stage LIKE '%1/4%' THEN 'Quarter-Finals' 
WHEN stage LIKE '%1/8%' THEN 'Round of 16' 
WHEN stage LIKE '%GROUP%' THEN 'Group Stage' 
ELSE 'Other' 
END as match_importance, 
COUNT(DISTINCT game_id) as matches, 
ROUND(AVG(attendance), 0) as avg_attendance, 
MAX(attendance) as highest_attendance 
FROM world_cup_data 
GROUP BY match_importance 
ORDER BY avg_attendance DESC; 

SCENARIO 4: GEOGRAPHIC DISTRIBUTION ANALYSIS 
4.1 Matches by host country/region 
sql 
SELECT  
home as host_country, 
year, 
COUNT(DISTINCT game_id) as matches_hosted, 
COUNT(DISTINCT stadium) as venues_used, 
ROUND(AVG(attendance), 0) as avg_attendance, 
SUM(goals) as total_goals_in_country 
FROM world_cup_data 
GROUP BY home, year 
ORDER BY year, matches_hosted DESC; 

4.2 Most used stadiums across all World Cups 
sql 
SELECT  
stadium, 
home as country, 
COUNT(DISTINCT year) as different_tournaments, 
COUNT(DISTINCT game_id) as total_matches, 
ROUND(AVG(attendance), 0) as avg_attendance, 
SUM(goals) as total_goals_witnessed 
FROM world_cup_data 
GROUP BY stadium, home 
HAVING total_matches >= 5 
ORDER BY total_matches DESC; 

4.3 Geographic distribution by continent 
sql 
SELECT  
CASE  
WHEN home IN ('Brazil', 'Argentina', 'Chile', 'Uruguay', 'Mexico', 'USA') THEN 'Americas' 
WHEN home IN ('Italy', 'France', 'Germany', 'England', 'Spain', 'Sweden', 'Switzerland') THEN 'Europe' 
WHEN home IN ('Japan', 'South Korea') THEN 'Asia' 
ELSE 'Other' 
END as continent, 
COUNT(DISTINCT year) as tournaments_hosted, 
COUNT(DISTINCT game_id) as total_matches, 
ROUND(AVG(attendance), 0) as avg_attendance 
FROM world_cup_data 
GROUP BY continent 
ORDER BY tournaments_hosted DESC; 

4.4 Venue efficiency analysis (goals per attendance) 
sql 
SELECT  
stadium, 
home as country, 
year, 
COUNT(DISTINCT game_id) as matches, 
SUM(goals) as total_goals, 
SUM(attendance) as total_attendance, 
ROUND(SUM(goals) / SUM(attendance) * 1000, 3) as goals_per_1000_spectators 
FROM world_cup_data 
GROUP BY stadium, home, year 
HAVING matches >= 3 
ORDER BY goals_per_1000_spectators DESC 
LIMIT 20; 

SCENARIO 5: REFEREE PATTERNS ANALYSIS 
5.1 Most active referees across tournaments 
sql 
SELECT  
referee, 
COUNT(DISTINCT year) as tournaments_officiated, 
COUNT(DISTINCT game_id) as matches_officiated, 
ROUND(AVG(goals), 2) as avg_goals_per_match, 
SUM(goals) as total_goals_in_matches, 
COUNT(CASE WHEN booked IS NOT NULL THEN 1 END) as matches_with_bookings 
FROM world_cup_data 
WHERE referee IS NOT NULL AND referee != '' 
GROUP BY referee 
HAVING matches_officiated >= 5 
ORDER BY matches_officiated DESC; 

5.2 Referee nationality patterns 
sql 
SELECT  
SUBSTRING_INDEX(referee, '(', -1) as referee_country, 
COUNT(DISTINCT referee) as number_of_referees, 
COUNT(DISTINCT game_id) as matches_officiated, 
ROUND(AVG(goals), 2) as avg_goals_per_match 
FROM world_cup_data 
WHERE referee IS NOT NULL  
AND referee != ''  
AND referee LIKE '%(%' 
GROUP BY referee_country 
HAVING matches_officiated >= 10 
ORDER BY matches_officiated DESC; 

5.3 High-scoring matches by referee 
sql 
SELECT  
referee, 
year, 
date, 
stadium, 
MAX(CASE WHEN team_num = 1 THEN team END) as team1, 
MAX(CASE WHEN team_num = 1 THEN goals END) as goals1, 
MAX(CASE WHEN team_num = 2 THEN team END) as team2, 
MAX(CASE WHEN team_num = 2 THEN goals END) as goals2, 
(MAX(CASE WHEN team_num = 1 THEN goals END) +  
MAX(CASE WHEN team_num = 2 THEN goals END)) as total_goals 
FROM world_cup_data 
WHERE referee IS NOT NULL 
GROUP BY referee, year, date, stadium, game_id 
HAVING total_goals >= 5 
ORDER BY total_goals DESC; 

5.4 Referee performance in high-stakes matches 
sql 
SELECT  
referee, 
stage, 
COUNT(DISTINCT game_id) as matches, 
ROUND(AVG(goals), 2) as avg_goals, 
COUNT(CASE WHEN booked IS NOT NULL THEN 1 END) as matches_with_cards 
FROM world_cup_data 
WHERE referee IS NOT NULL  
AND stage IN ('FINAL ROUND', '1/2 FINAL', '1/4 FINAL') 
GROUP BY referee, stage 
ORDER BY stage, matches DESC; 

SCENARIO 6: TOURNAMENT FORMAT EVOLUTION 
6.1 Tournament size evolution 
sql 
SELECT  
year, 
COUNT(DISTINCT team) as participating_teams, 
COUNT(DISTINCT game_id) as total_matches, 
COUNT(DISTINCT stage) as tournament_stages, 
ROUND(COUNT(DISTINCT game_id) / COUNT(DISTINCT team), 2) as matches_per_team_avg 
FROM world_cup_data 
GROUP BY year 
ORDER BY year; 

6.2 Stage distribution by tournament 
sql 
SELECT  
year, 
stage, 
COUNT(DISTINCT game_id) as matches_in_stage, 
COUNT(DISTINCT team) as teams_in_stage 
FROM world_cup_data 
WHERE stage IS NOT NULL 
GROUP BY year, stage 
ORDER BY year, matches_in_stage DESC; 

6.3 Tournament duration analysis 
sql 
SELECT  
year, 
MIN(STR_TO_DATE(SUBSTRING(date, 1, 10), '%d-%m-%Y')) as tournament_start, 
MAX(STR_TO_DATE(SUBSTRING(date, 1, 10), '%d-%m-%Y')) as tournament_end, 
DATEDIFF( 
MAX(STR_TO_DATE(SUBSTRING(date, 1, 10), '%d-%m-%Y')), 
MIN(STR_TO_DATE(SUBSTRING(date, 1, 10), '%d-%m-%Y')) 
) as tournament_duration_days, 
COUNT(DISTINCT game_id) as total_matches 
FROM world_cup_data 
GROUP BY year 
ORDER BY year; 

6.4 Penalty shootout evolution 
sql 
SELECT  
year, 
COUNT(CASE WHEN pk != 'False' AND pk IS NOT NULL THEN 1 END) as penalty_shootouts, 
COUNT(DISTINCT game_id) as total_matches, 
ROUND( 
COUNT(CASE WHEN pk != 'False' AND pk IS NOT NULL THEN 1 END) /  
COUNT(DISTINCT game_id) * 100, 2 
) as penalty_shootout_percentage 
FROM world_cup_data 
GROUP BY year 
HAVING penalty_shootouts > 0 
ORDER BY year; 

SCENARIO 7: ADVANCED KPIs AND BUSINESS METRICS 
7.1 Tournament Competitiveness Index 
sql 
SELECT  
year, 
COUNT(DISTINCT team) as teams, 
ROUND(STDDEV(goals), 3) as goal_variance, 
ROUND(AVG(goals), 2) as avg_goals, 
COUNT(CASE WHEN goals = 0 THEN 1 END) as shutouts, 
ROUND( 
COUNT(CASE WHEN goals = 0 THEN 1 END) / COUNT(*) * 100, 2 
) as shutout_percentage, -- Competitiveness score (lower variance = more competitive) 
ROUND(STDDEV(goals) / AVG(goals), 3) as competitiveness_ratio 
FROM world_cup_data 
GROUP BY year 
ORDER BY year; 

7.2 Stadium ROI Analysis 
sql 
SELECT  
stadium, 
year, 
COUNT(DISTINCT game_id) as matches_hosted, 
SUM(attendance) as total_spectators, 
SUM(goals) as total_goals, 
ROUND(SUM(goals) / COUNT(DISTINCT game_id), 2) as goals_per_match, 
ROUND(SUM(attendance) / COUNT(DISTINCT game_id), 0) as avg_attendance, -- Entertainment value index 
ROUND( 
(SUM(goals) * 1000) / SUM(attendance), 3 
) as entertainment_per_1000_fans 
FROM world_cup_data 
GROUP BY stadium, year 
HAVING matches_hosted >= 3 
ORDER BY entertainment_per_1000_fans DESC; 

7.3 Team Consistency Analysis 
sql 
SELECT  
team, 
COUNT(DISTINCT year) as tournaments, 
COUNT(*) as total_matches, 
ROUND(AVG(goals), 2) as avg_goals, 
ROUND(STDDEV(goals), 3) as goal_consistency, 
MAX(goals) - MIN(goals) as goal_range, -- Consistency score (lower is more consistent) 
ROUND(STDDEV(goals) / AVG(goals), 3) as consistency_index 
FROM world_cup_data 
GROUP BY team 
HAVING tournaments >= 3 AND total_matches >= 10 
ORDER BY consistency_index ASC; 

7.4 Tournament Quality Metrics 
sql 
SELECT  
year, 
home as host_country, 
COUNT(DISTINCT game_id) as total_matches, 
ROUND(AVG(attendance), 0) as avg_attendance, 
SUM(goals) as total_goals, 
COUNT(CASE WHEN goals >= 3 THEN 1 END) as high_scoring_performances, -- Quality indicators 
ROUND(AVG(goals), 2) as goals_per_team_match, 
ROUND( 
COUNT(CASE WHEN goals >= 3 THEN 1 END) / COUNT(*) * 100, 2 
) as high_scoring_percentage, -- Overall tournament quality score 
ROUND( 
(AVG(goals) * 0.4) +  
(AVG(attendance) / 1000 * 0.3) +  
(COUNT(CASE WHEN goals >= 3 THEN 1 END) / COUNT(*) * 100 * 0.3), 2 
) as quality_score 
FROM world_cup_data 
GROUP BY year, home 
ORDER BY quality_score DESC; 

Immediate Insights 
• Historical scoring trends showing which eras were most/least offensive 
• Team dynasty analysis identifying the most successful national teams 
• Stadium economics - which venues provide best fan experience 
• Geographic patterns - how hosting affects attendance and performance 
• Referee impact - do certain officials influence match outcomes 
• Tournament evolution - how formats changed to increase excitement 
• Competitiveness metrics - which tournaments were most balanced 
