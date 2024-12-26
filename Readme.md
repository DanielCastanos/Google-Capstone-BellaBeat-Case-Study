# Google-Capstone-BellaBeat-Case-Study

**Author:** Daniel Castaños  
**Date:** 12/24/2024 

## Overview  
This project analyzes trends in FitBit user data and provides recommendations to guide Bellabeat’s marketing strategy.  

## Business Task  
Analyze FitBit data to understand user behavior and create actionable marketing insights.  

## Steps in the Analysis:  
1. ❓ **Ask**  
2. 💻 **Prepare**  
3. 🛠 **Process**  
4. 📊 **Analyze**  
5. 📋 **Share**  
6. 🧗‍♀️ **Act**   

## Scenario
As a junior data analyst on Bellabeat's marketing analytics team, my role is to uncover trends in the Smart Device space and provide High-level recommendations for how these trends can inform Bellabeat's marketing team. My analysis will focus on one of Bellabeat's products, exploring how consumers use smart devices. These insights will guide Bellabeat's marketing strategy and be presented to the executive team so they can make Data Driven Decision for future Bellabeats Marketing Campaings.

## 1. Ask
Analyze Smart Devices data to uncover trends and help guide the marketing team on their new marketing campaings.
Stakeholders  
- **Primary Stakeholders:** Urška Sršen and Sando Mur (Bellabeat Executives).  
- **Secondary Stakeholders:** Bellabeat Marketing Analytics Team.

## 2. Prepare 
- **Data Source:** [Fitbit Fitness Tracker Data](https://www.kaggle.com/arashnic/fitbit)
Fitbit Fitness Tracker Data
Source: Publicly available dataset from Kaggle, consisting of personal fitness data from 30 Fitbit users.
Data Description: The dataset includes detailed minute-level data on physical activity, heart rate, and sleep patterns. The specific files used in this analysis are:
heartrate_seconds_merged.csv (minute-by-minute heart rate)
hourlyCalories_merged.csv (hourly calories burned)
minuteCaloriesNarrow_merged.csv (minute-level calories burned)
minuteStepsNarrow_merged.csv (minute-level step data)

**Data Integrity Considerations**
Bias and Representativeness: The dataset is based on self-reported Fitbit data from a small group (30 users). This may introduce bias, as it reflects a specific subset of the population—people who use fitness trackers. Moreover, this small sample size limits the ability to generalize findings to a broader population.
Credibility: While Fitbit data is generally considered reliable, it might not represent all user demographics. Issues like missing data or inconsistencies could exist, but overall, it offers valuable insights into user habits.
Privacy and Licensing
The dataset is shared under a CC0 license, meaning it is free for use, and no personal information is included, ensuring user privacy is protected.

**Data Cleaning and Processing**
To ensure accurate analysis, the following cleaning steps were taken:
Datetime Conversion: Time-based data (e.g., activity timestamps) was converted to a proper datetime format to enable efficient time-series analysis.
Duplicate and Missing Data Checks: The dataset was scanned for duplicate entries and missing values. No significant issues were identified at this stage.
Data Alignment: Timestamps were aligned across different datasets to facilitate merging and cross-referencing of heart rate, steps, and calorie data for each user.

**Data Analysis**
1. Data Aggregation and Merging
Data from different sources (steps, calories, heart rate) was aggregated on both an hourly and daily basis. This approach helps in identifying broader trends in user behavior, such as daily activity peaks and periods of rest. By merging datasets, we were able to observe how physical activity (steps), energy expenditure (calories), and heart rate interact over time.
2. Key Insights from the Data
Calorie Burn and Physical Activity: There is a clear relationship between physical activity (steps) and calories burned. Users who are more physically active tend to burn more calories, especially during peak activity periods, like morning workouts or evening walks.
Heart Rate Trends: Heart rate tends to rise during periods of increased physical activity, indicating a strong link between exercise intensity and cardiovascular response. However, some users showed minimal variation in heart rate, suggesting they might be engaging in less strenuous activities.
Outliers: In some cases, calorie expenditure seemed higher than expected compared to the number of steps taken, suggesting the possibility of non-step-based activities, such as cycling or swimming, contributing to calorie burn.
3. Patterns and Correlations
Correlation between Steps, Heart Rate, and Calories: A positive correlation was observed between the number of steps taken, calories burned, and heart rate. This reinforces the connection between increased physical activity and energy expenditure.
Activity Peaks: Many users exhibited peak activity in the morning or evening, which may reflect common exercise times. Understanding these patterns can help in designing fitness plans or marketing strategies tailored to user habits.
Sedentary Behavior: Users with lower variations in heart rate may benefit from interventions that encourage more movement throughout the day.
