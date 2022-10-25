# School District Analysis
## Project Overview
I have been tasked with assisting a city school district in analyzing student standardized test score data.  I will present data based on school size, school type, and school budget to allow the district to make funding and resource decisions.

## Resources
**Data Source:** new_full_student_data.csv

**Software:** Anaconda Navigator, Jupyter Notebook, Python 3.7.6, Pandas

## Process
### 1. Collect the student data from the CSV file into a DataFrame for use with Pandas
I used the code to import dependencies, link to the data source, and read the file.  
```
import pandas as pd
import os
```
```
full_student_data = os.path.join('../Resources/new_full_student_data.csv')
student_df = pd.read_csv(full_student_data)
```

I checked for proper reading with `student_df.header()`

![Step1image](https://github.com/jakatz87/School_District_Analysis/blob/main/Resources/Step1image.png)

### 2. Prepare a cleaned version of the DataFrame by accounting for missing, incomplete, erroneous, and duplicated data
I checked for any missing data with `student_df.isna().sum()`, and found there were few enough missing entries that removing them would not impact the validity of the results (around 0.5%).  

I removed the entries with missing data using `student_df=student_df.dropna()`.

I repeated the process with duplicate data using `student_df.duplicated().sum()` and `student_df=student_df.drop_duplicates()`.

### 3. Summarize key pieces of data with statistical analysis
I ensured each column had proper formatting and data type and found only one column, Grades, needed altering.  

I used `student_df['grade']=student_df['grade'].str.replace('th', '')` and `student_df['grade']=student_df['grade'].astype(int)` to make sure I could work with the data appropriately.

I used `student_df.describe()` to get a general sense of the data:

![Step3image](https://github.com/jakatz87/School_District_Analysis/blob/main/Resources/Step3image.png)

I noticed the data was slightly skewed to the left.

### 4. Use more specific analysis with grouping and aggregation to drill down and analyze subsets of data
The first analysis compared the average budget between Public and Charter schools:
```
budget_mean=student_df.groupby(["school_type"]).mean()
budget_mean.loc[:, "school_budget"]
```

![Step4imagea](https://github.com/jakatz87/School_District_Analysis/blob/main/Resources/Step4imagea.png)

The next analysis grouped schools by student population:
```
student_df.rename(columns={"student_id":"student_count"}, inplace=True)
student_count=student_df.groupby("school_name").count().sort_values("student_count", ascending=False)
student_count.loc[:,"student_count"]
```

![Step4image1](https://github.com/jakatz87/School_District_Analysis/blob/main/Resources/Step4image.png)

The next analysis looked at both Math and Reading scores by grade and school type:
```
avg_math_score=student_df.groupby(["school_type", "grade"]).mean().round(0)
avg_math_score.loc[:, ["math_score"]]
```
![imagemathscore](https://github.com/jakatz87/School_District_Analysis/blob/main/Resources/Step4image2.png)

```
avg_reading_score=student_df.groupby(["school_type", "grade"]).mean().round(0)
avg_reading_score.loc[:, ["reading_score"]]
```

![imagereadingscore](https://github.com/jakatz87/School_District_Analysis/blob/main/Resources/Step4image2b.png)

The final analysis compared schools by type and ranked them by average Math score or by average Reading score:
```
student_count=student_df.groupby(["school_name", "school_type"]).mean().sort_values("reading_score", ascending=False)
student_count[["reading_score", "math_score", "school_budget"]]
```
This is ranked by average Reading score:

![finalimage](https://github.com/jakatz87/School_District_Analysis/blob/main/Resources/Step4image3.png)

## Summary
Based on the data we were given, we have been able to provide information to the school district that may help with funding or resource decisions.  Some questions to consider:  

1. Does student population size impact test scores?  Based on the data, it seems that question depends on whether or not the school is Public or Charter.  However, when looking at student grade data, Public school 12th graders are performing well, while Charter school 11th graders are outperforming their Public school counterparts.  What is happening between 10th grade and 12th grade that can account for this?

2. Does school budget impact test scores?  At first glance, it seems that Charter schools are performing equally well with fewer dollars.  There also seems to be a discrepancy in Public school funding as evidenced by the budget of the largest Public school, Wagner High School. Based on Reading scores and budget allocations, it is worth investigating either what Wagner is doing or how more resources can be allocated to Wagner, or how other Public schools can maximize the use of their budgets.

3. What can be learned?  It seems there are extra questions that need to be asked at each school.  How is there such a discrepancy between Math scores and Reading scores?  What are Charter schools doing with Math? What are Public schools doing with Reading? What other factors, like student attendance or access to free and reduced meal plans, may be at play?

What must be remembered after all this provided data, the most important data cannot be stored in a CSV file: each student's story.  Education is about each student's journey through life and learning.  It is important to remember how narrow our picture of education is when we are attempting to measure it with test scores.

