# **Google-Capstone-BellaBeat-Case-Study**

**Author:** Daniel Castaños  
**Date:** 12/24/2024 

---

## **Scenario**
As a junior data analyst on Bellabeat's marketing analytics team, my role is to uncover trends in the smart device space and provide high-level recommendations on how these trends can inform Bellabeat's marketing team. My analysis will focus on one of Bellabeat's products in this case. These insights will guide Bellabeat's marketing strategy and be presented to the executive team so they can make data-driven decisions for future Bellabeat's marketing campaigns.
We chose **Bellabeat's Leaf** (Bellabeat's classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf tracker connects to the Bellabeat's app to track activity, sleep, and stress)

---

## **Business Task**  
Analyze FitBit data to understand user behavior and create actionable marketing insights. 

---
## 1. **Ask**
Taking into consideration that smart device users tend to favor easy-to-read information specially goals. We are looking to uncover ways to gamify health goals and showcase how with **Bellabeat's Leaf** & easy-to-read information, especially goals. We will analyze Smart Devices data to uncover these trends and help guide the marketing team on new marketing campaigns.
### Stakeholders
- **Primary Stakeholders:** Urška Sršen and Sando Mur (Bellabeat's Executives).  
- **Secondary Stakeholders:** Bellabeat's Marketing Analytics Team.

---

## 2. **Prepare**
- **Data Source:** [Fitbit Fitness Tracker Data](https://www.kaggle.com/arashnic/fitbit)

**Source:** Publicly available dataset from Kaggle, consisting of self-reported fitness data. from 30 Fitbit users.
Data Description: The data is stored in CSV files. The dataset includes detailed data on physical activity, heart rate, and sleep patterns. 

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
The dataset is based on self-reported Fitbit data from a small group (30 users). This may create issues with bias, as it represents a specific subset of the population — people who use fitness trackers. Also, it is a small sample size which limits the ability to generalize findings.
2. **Credibility:** 
While Fitbit data is considered reliable, it does not represent all users. Issues like missing data or inconsistencies could pose a problem, but it offers valuable insights into the target market's habits..

### **Privacy and Licensing**
The dataset is under a **CC0 license**, meaning it is free for use, and no personal information is included, ensuring user privacy.

---

## 3. Process
**Data Cleaning and Processing**
We used R for our analysis due to the size of the data
## To ensure accurate analysis, we:
uploaded the CSV files to R and checked for duplicate and missing data. No significant issues were identified. Additionally, we converted `ActivityDate` to the correct format for handling.

```r
# Checking number of unique participants on each data set

n_distinct(daily_activity$Id)

n_distinct(heartrate_seconds$Id)

n_distinct(hourly_calories$Id)

n_distinct(hourly_intensities$Id)

n_distinct(hourly_steps$Id)

n_distinct(minute_calories$Id)

n_distinct(minute_intensities$Id)

n_distinct(minute_mets$Id)

n_distinct(minute_sleep$Id)

n_distinct(minute_steps$Id)

n_distinct(weight_log$Id)

nrow(daily_activity)


# Checking for missing values in each column

colSums(is.na(daily_activity))
colSums(is.na(heartrate_seconds))
colSums(is.na(hourly_calories))
colSums(is.na(hourly_intensities))
colSums(is.na(hourly_steps))
colSums(is.na(minute_calories))
colSums(is.na(minute_intensities))
colSums(is.na(minute_mets))
colSums(is.na(minute_sleep))
colSums(is.na(minute_steps))
colSums(is.na(weight_log))


# Generating summary

summary(daily_activity)


# Ensuring ActivityDate is in Date format

daily_activity$ActivityDate <- as.Date(daily_activity$ActivityDate, format="%m/%d/%Y")
```

## **4. Analyze**
After aggregating the CSV files by ID and transforming the tables to the correct formats, we wanted to understand the difference between Light, Moderate & Intense activity in order to show the relationship between them We first set up a goal of **10k steps** to understand how the different levels of activity perform (according to the [National Institutes of Health](https://www.nih.gov/news-events/nih-research-matters/how-many-steps-better-health). There's some evidence that upping your daily strides can have some surprising benefits, according to a 2022 study published in [JAMA Internal Medicine](https://jamanetwork.com/journals/jamainternalmedicine/fullarticle/2796058). Here are some of them. Improved Mood and Brain Function, Better Mobility, Healthy Weight Loss, Speedier Recovery)

### **Key Findings:**

**Step Goal Achievement:**
Across **457** logged days, users met the 10,000-step goal on **127** days.
This corresponds to **27.79%** of days, showing that users meet the step goal less than **one-third of the time** and showcasing that Health-conscious individuals are not significantly ahead of non-health-conscious ones, raising the question: **What small shifts can help users achieve their health goals?**
```r
# Defining the step goal

step_goal <- 10000


# Adding a column indicating whether the step goal was met

daily_activity <- daily_activity %>%
  mutate(StepGoalMet = ifelse(TotalSteps >= step_goal, 1, 0))


# Calculating percentage of days users met the step goal

step_goal_stats <- daily_activity %>%
  summarise(
    TotalDays = n(),
    GoalMetDays = sum(StepGoalMet),
    PercentGoalMet = (GoalMetDays / TotalDays) * 100
  )

print(step_goal_stats)
```

**Influence of Activity Intensity:**
- **Light Activity:** Users logged an average of **7,657 steps** on days with **light activity**.
- **Moderate Activity:** Users logged an average of **10,269 steps**, surpassing the step goal.
- **Very Active Intensity:** Users logged an average of **10,480 steps**, also exceeding the step goal.
- **Insight:** Higher activity intensities (moderate and very active) are strongly associated with meeting or exceeding the daily step goal but if we see the biggest jump is from light to moderate activity, with the impact of intense activity being almost negligible.
```r
# Summarizing average steps by activity intensity

intensity_analysis <- daily_activity %>%
  summarise(
    AvgSteps_Light = mean(TotalSteps[LightActiveDistance > 0]),
    AvgSteps_Moderate = mean(TotalSteps[ModeratelyActiveDistance > 0]),
    AvgSteps_VeryActive = mean(TotalSteps[VeryActiveDistance > 0])
  )

print(intensity_analysis)
```

We are focusing on the key differences between light and moderate activity, as these provide the most significant shift in average steps taken.
```r
# Calculating average LightActiveDistance and ModeratelyActiveDistance per user

average_activity_difference <- daily_activity %>%
  group_by(Id) %>%
  summarise(
    AvgLightActivity = mean(LightActiveDistance, na.rm = TRUE),
    AvgModerateActivity = mean(ModeratelyActiveDistance, na.rm = TRUE)
  ) %>%
  mutate(Difference = AvgModerateActivity - AvgLightActivity)


# Viewing the calculated differences

print(average_activity_difference)


# Calculating the overall average difference across all users

overall_difference <- mean(average_activity_difference$Difference, na.rm = TRUE)
print(paste("Overall Average Difference:", overall_difference))


# Aggregate data for light activity

light_activity <- daily_activity %>%
  filter(LightActiveDistance > 0, LightlyActiveMinutes > 0) %>%
  summarise(
    AvgLightStepsPerMinute = mean(TotalSteps / LightlyActiveMinutes, na.rm = TRUE),
    AvgLightMinutes = mean(LightlyActiveMinutes, na.rm = TRUE),
    AvgLightSteps = mean(TotalSteps, na.rm = TRUE)
  )


# Aggregate data for moderate activity

moderate_activity <- daily_activity %>%
  filter(ModeratelyActiveDistance > 0, FairlyActiveMinutes > 0) %>%
  summarise(
    AvgModerateStepsPerMinute = mean(TotalSteps / FairlyActiveMinutes, na.rm = TRUE),
    AvgModerateMinutes = mean(FairlyActiveMinutes, na.rm = TRUE),
    AvgModerateSteps = mean(TotalSteps, na.rm = TRUE)
  )


# Combine the results into a single table for easier comparison

activity_aggregate_fixed <- cbind(light_activity, moderate_activity)


# Print the updated aggregated data

print(activity_aggregate_fixed)
```

### **Insights:**
**Overall Average Difference:**

The average difference in distance between light and moderate activity across all users is about 2.4 km. This tells us that users typically engage in significantly fewer moderate activity compared to light activity.

### **Steps Per Minute:**

**Light Activity:** About **40 steps per minute** on average.
**Moderate Activity:** A much higher rate of **856 steps per minute** on average.

### **Time Spent:**

Users spend a lot more time in light activity **(~203 minutes)** than in moderate activity **(~23 minutes)** on average.

### **Total Steps:**

Total steps are higher for moderate activity **(~10,269 steps)** than for light activity **(~7,657 steps)**, even though users spend significantly less time on moderate activity. This highlights the efficiency of moderate activity.

### **Marketing Implications:**

Small Adjustments, Big Results: This data strongly supports the idea that shifting a small portion of light activity to moderate activity can yield much greater results in terms of steps taken and, potentially, calories burned or weight with many more benefits according to the [National Institutes of Health](https://www.nih.gov/news-events/nih-research-matters/how-many-steps-better-health) and the study in 2022 from the [JAMA Internal Medicine](https://jamanetwork.com/journals/jamainternalmedicine/fullarticle/2796058).

Promoting the Bellabeat's Leaf: These findings can be tied to how the Bellabeat's Leaf tracker helps users monitor their activity levels and encourages efficient activity patterns for better results.

Our main idea is to showcase to users how a small shift in their daily activity can have a big impact on their overall goals. We understand how busy lives can be that is why we chose Bellabeat's Leaf for our primary product, as it is easy to wear daily and a simple vibration can remind our users to engage in some sort of moderate activity in order to boost their step count and in turn their health and since it also ties to Bellabeat's app, users will be able to track and see their progress towards their goals live from their phones.

## **Conclusion:**
By analyzing Fitbit data, we realized that moderate activity offers the best return on investment for users trying to meet their health goals. These insights show the potential for Bellabeat's Leaf tracker to push user engagement by promoting moderate activity through reminders and app integration. Next steps include A/B testing campaigns to validate these findings and refine marketing strategies.

