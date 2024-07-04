# **Runbook/Prompt for Fitness Goals Tracker Agent**

**Objective:** Automatically update workout metrics in a Google Sheet and send an email summary to the user's doctor using Google Sheets and Gmail actions, while fetching the email template from Google Drive.

## **1\. Update Google Sheet**

**Metrics Tracked:**

- Running Distance (miles)
- Running Duration (hours)
- Walking Distance (miles)
- Walking Duration (hours)
- Core Duration (hours)
- Active Calories Burned across all workouts (calories)
- Average Heart Rate across all workouts (bpm)
- Maximum Heart Rate across all workouts (bpm)

**Steps:**

**1\. Retrieve Workout Metrics:**

- Use the Workout Actions to fetch performance workout metrtics for running, walking, and core exercises.
- Note:
  - For Active calories, Average, Minimum and Maximum Heart Rate, query across all workout types (run, walk, cycle, hike, tennis, core)
  - Convert all workout duration metrics in seconds to hours before updating the Google sheet.

**2\. Update Google Sheet:**

1.  **Get the content** **of the row for each metric**  in the "Fitness Goals Tracker" spreadsheet for the specified month's sheet.
2.  **Update the "Actual Value"column** with the retrieved workout metrics data from step 1.
3.  **Update the "% of Goal Attained" column** using the following calculation: (Actual Value / Goal) \* 100.
4.  **Update the "Goal Outcome" column** to "Achieved" if the value in "Actual Value" is equal to or greater than the value in "Goal" column, otherwise set it to "Not Achieved".

**Example Prompt:**

```
Please update the "Fitness Goals Tracker" spreadsheet as follows:

For the "October 2023", "November 2023" or "December 2023" sheets:
1. Get the row content for each metric in the specified month's sheet.
2. Update  the "Actual Value" column with my workout metrics:
    - Running Distance (miles): [value]
    - Running Duration (hours): [value]
    - Walking Distance (miles): [value]
    - Walking Duration (hours): [value]
    - Core Duration (hours): [value]
    - Active Calories Burned across all workouts (calories): [value]
    - Average Heart Rate across all workouts (bpm): [value]
    - Maximum Heart Rate across all workouts (bpm): [value]
3. Calculate the "% of Goal Attained" for each metric.
4. Update the "Goal Outcome" column to "Achieved" if the value in "Actual Value" is equal to or greater than the value in "Goal" column, otherwise set it to "Not Achieved".
```

## **2\. Fetch Email Template from Google Drive and Send Email Summary with Gmail (Optional)**

**Condition:** Only perform the following steps if the user explicitly requests to email the summary.

**Steps:**

1.  **Fetch Email Template:**
    - Use the "Get File Contents" action from the Google Drive package to fetch the "Workout Performance Summary Template" document.
2.  **Populate the Template:**
    - Replace placeholders with the metrics, goals, actual values, % of goal attained, and goal outcomes for October 2023, November 2023, and December 2023.
    - Replace "\[Doctor's Name\]" with "Dr. Matthews".
    - Replace "\[Your Name\]" with "George".
    - Populate the template with the metrics, goals, actual values, % of goal attained, and goal outcomes.
3.  **Send Email:**
    - Send the email with the populated template
    - Example prompt:

```
Send an email to george@sema4.ai with the subject "Summary of Workout Performance for the Last Three Months" using the populated template.
```

**Email Details:**

- To: `george@sema4.ai`
- Subject: Summary of Workout Performance for the Last Three Months
- Body: \[Insert the summary here\]
