# **Google-Capstone-BellaBeat-Case-Study**

**Author:** Daniel Castaños  
**Date:** 12/24/2024 

---

## **Overview** 
This project analyzes trends in FitBit user data and provides recommendations to guide Bellabeat’s marketing strategy.  

---

## **Business Task**  
Analyze FitBit data to understand user behavior and create actionable marketing insights. 

---

## **Scenario**
As a junior data analyst on Bellabeat's marketing analytics team, my role is to uncover trends in the Smart Device space and provide High-level recommendations for how these trends can inform Bellabeat's marketing team. My analysis will focus on one of Bellabeat's products in these case. These insights will guide Bellabeat's marketing strategy and be presented to the executive team so they can make Data Driven Decision for future Bellabeats Marketing Campaings.
we choose **Bellabeats Leaf** (Bellabeat’s classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf tracker connects to the Bellabeat app to track activity, sleep, and stress)

---

## 1. **Ask**
Analyze Smart Devices data to uncover trends and help guide the marketing team on their new marketing campaings.
### Stakeholders
- **Primary Stakeholders:** Urška Sršen and Sando Mur (Bellabeat Executives).  
- **Secondary Stakeholders:** Bellabeat Marketing Analytics Team.

---

## 2. **Prepare**
- **Data Source:** [Fitbit Fitness Tracker Data](https://www.kaggle.com/arashnic/fitbit)

**Source:** Publicly available dataset from Kaggle, consisting of self reported fitness data from 30 Fitbit users.
Data Description: 10 CSV Files, The dataset includes detailed data on physical activity, heart rate, and sleep patterns. 

**Files used in this analysis are:**

- `dailyActivity_merged.csv`
- `heartrate_seconds_merged.csv`
- `hourlyCalories_merged.csv`
- `hourlyIntensities_merged.csv`
- `hourlySteps_merged.csv`
- `minuteCaloriesNarrow_merged.csv`
- `minuteIntensitiesNarrow_merged.csv`
- `minuteMETsNarrow_merged.csv`
- `minuteSleep_merged.csv`
- `minuteStepsNarrow_merged.csv`
- `weightLogInfo_merged.csv`

### **Data Integrity Considerations**
1. **Bias and Representativeness:** 
The dataset is based on self-reported Fitbit data from a small group (30 users). This may introduce bias, as it reflects a specific subset of the population—people who use fitness trackers. Moreover, this small sample size limits the ability to generalize findings to a broader population.
2. **Credibility:** 
While Fitbit data is generally considered reliable, it might not represent all user demographics. Issues like missing data or inconsistencies could exist, but overall, it offers valuable insights into user habits.

### **Privacy and Licensing**
The dataset is shared under a **CC0 license**, meaning it is free for use, and no personal information is included, ensuring user privacy is protected.

---

## 3. Process
**Data Cleaning and Processing**
We went with R for our Analizys given the size of the data
## To ensure accurate analysis we:
### Converted Datetime: 
Uploaded CSV to R converted ActivityDate to correct format for handeling.
Checked for Duplicate and Missing Data: The dataset was scanned for duplicate entries and missing values. No significant issues were identified.
******************** R Code *******************

## **4. Analyze**
We first set up a Goal of 10k steps to understand the difference between Light, Moderate & Intense activity to understand the relationship between them

### **Key Findings:**

**Step Goal Achievement:**
Across 457 logged days, users met the 10,000-step goal on 127 days.
This corresponds to 27.79% of days, showing that users meet the step goal less than one-third of the time.
********************************* R code ****************************************
**Influence of Activity Intensity:**
Light Activity: Users logged an average of 7,657 steps on days with light activity.
Moderate Activity: Users logged an average of 10,269 steps, surpassing the step goal.
Very Active Intensity: Users logged an average of 10,480 steps, also exceeding the step goal.
Insight: Higher activity intensities (moderate and very active) are strongly associated with meeting or exceeding the daily step goal.
******************************** R Code *****************************************
We are looking for the key differences from light activity to moderate since is the one that gives the biggest shift in average steps taken
************************************ R Code *************************************
### **Insights:**
**Overall Average Difference:**

The average difference in distance covered between light and moderate activity across users is approximately -2.4 km. This indicates that users typically engage in significantly less moderate activity compared to light activity.

### **Steps Per Minute:**

**Light Activity:** About 40 steps per minute on average.
**Moderate Activity:** A much higher rate of 856 steps per minute on average.

### **Time Spent:**

Users spend a lot more time in light activity (~203 minutes) than in moderate activity (~23 minutes) on average.

### **Total Steps:**

Total steps are higher for moderate activity (~10,269 steps) than for light activity (~7,657 steps), even though users spend significantly less time on moderate activity. This highlights the efficiency of moderate activity.

### **Marketing Implications:**

Small Adjustments, Big Results: This data strongly supports the idea that shifting a small portion of light activity to moderate activity can yield much greater results in terms of steps taken and, potentially, calories burned or weight lost.

Promoting the Bellabeat Leaf: These findings can be tied to how the Bellabeat Leaf tracker helps users monitor their activity levels and encourages efficient activity patterns for better results.

Our main idea is to showcase to users how a small shift in their daily activity can have a big impact in their overall goals.



