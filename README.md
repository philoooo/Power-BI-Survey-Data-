## Power BI Dashboard: Breaking Down the Data Professional Survey Results
---
  I uploaded my .xlsx file into Power BI and transformed the query titled "Data Professional Survey" using Power Query to prepare it for visualization.

## Data Cleaning
1. I deleted the columns ‘Browser’, ‘OS’, ‘City’, ‘Country’, and ‘Referrer’ because they contained mostly blank rows and weren’t necessary.

2. For ‘Q1: Which Title Best Fits Your Current Role’, there were many repetitive or overly detailed entries. I split this column using a custom delimiter '(', set to split at the left-most occurrence. This created two parts: the first (.1) held cleaned-up job titles with only seven distinct values, which was much easier to work with. I removed the second part (.2) since it was no longer needed.

3. I repeated the same cleaning method for ‘Q5: Favorite Programming Language’, which had too many "Other" responses due to it being a free-text field. I used a colon : as the delimiter to simplify and separate the data into manageable values.

4. To make ‘Q3: Current Yearly Salary (in USD)’ usable for numeric calculations, I duplicated the column and split it by digit-to-non-digit transitions, which created three columns.

    .1 had the first number in the range,

    .2 included the second number (but with “k” or “-”),

    .3 just had “k” and was removed.
5. I then used Replace Values to remove “k” and “-” from .2, converted both .1 and .2 to whole numbers, and created a custom column called ‘Average Salary’ using the formula:
= ([Q3 Copy.1] + [Q3 Copy.2]) / 2.
6. I changed the data type of the new column to a decimal number.

7. I also cleaned the ‘Q11: What country do you want to live in’ and ‘Q4: What industry do you work in’ columns using the same left-most parenthesis split method. After splitting, I removed the extra .2 columns and kept the simplified values.

8. Finally, I clicked Close & Apply to finish the data preparation.

![FinishedColumns](https://github.com/philoooo/Power-BI-Survey-Data-/blob/main/prof2.PNG)

## Building the Dashboard
1. I started by adding a title to the dashboard: "Breaking Down the Data Professional Survey Results."

2. I created a card visualization showing the count of unique IDs and renamed the field to “Total Survey Respondents.” I added another card that calculates the average of the Current Age column and renamed it “Average Age of Survey Respondents.”

3. I built a stacked bar chart using ‘Q1: Which Title Best Fits Your Current Role’ for both the y-axis and the legend, and used the average of the Average Salary column as the value. This helped sort salaries by job title. I titled the chart “Average Salary by Job Title.”

4. For the programming language breakdown, I created a stacked column chart with ‘Q5: Favorite Programming Language’ on the x-axis and count of unique IDs on the y-axis. I added a legend showing job titles, then renamed the chart to “Favorite Programming Languages.”

5. I added a Tree Map using ‘Q11: Which Country Do You Live In’ as the category and the distinct count of IDs as the value. This allows users to interact with the dashboard and filter by country, showing more precise salary data for specific regions. Since all salary values are in USD, this helps provide context when comparing countries—someone appearing to "make less" might not actually earn less in local terms.

6. I inserted a gauge chart that uses Q6 (Work-Life Balance Happiness). The value shows the average, and I used the minimum and maximum values in that column to set the range. I repeated the same steps to create another gauge chart, this time using Salary Happiness as the data source.

7. I finished the dashboard by inserting a donut chart showing responses to the question about how difficult it was to break into the data field. I used the count of each response and titled the chart “Difficulty Breaking Into Role.”

8. To bring everything together visually, I applied the Highrise theme to give the dashboard a modern, consistent color scheme that makes the visuals stand out and feel cohesive.

![Dashboard](https://github.com/philoooo/Power-BI-Survey-Data-/blob/main/prof1.PNG)
   
## Findings:
This Power BI dashboard provides a clean and interactive breakdown of real survey responses from professionals in the data industry. It highlights patterns in job titles, salaries, favorite programming languages, regional trends, and perceptions of work-life balance and job satisfaction. It also visualizes how difficult people found it to break into the field, offering insights that can help newcomers and professionals alike.
