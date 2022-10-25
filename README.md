# School District Analysis
## Project Overview
I have been tasked with assisting a city school district in analyzing student standardized test score data.  I will present data based on school size, school type, and school budget to allow the district to make funding and resource decisions.

## Resources
Data Source: new_full_student_data.csv
Software: Anaconda Navigator, Jupyter Notebook, Python 3.7.6, Pandas

## Process
- Collect the student data from the CSV file into a DataFrame for use with Pandas
- Prepare a cleaned version of the DataFrame by accounting for missing, incomplete, erroneous, and duplicated data and 
- Summarize key pieces of data with statistical analysis
- Use more specific analysis to drill down and analyze subsets of data
- Use grouping and aggregation to compare and contrast data
## Summary
Based on the data we were given, we have been able to provide information to the school district that may help with funding or resource decisions.  Some questions to consider:  

1. Does student population size impact test scores?  Based on the data, it seems that question depends on whether or not the school is Public or Charter.  However, when looking at student grade data, Public school 12th graders are performing well, while Charter school 11th graders are outperforming their Public school counterparts.  What is happening between 10th grade and 12th grade that can account for this?

2. Does school budget impact test scores?  At first glance, it seems that Charter schools are performing equally well with fewer dollars.  There also seems to be a discrepancy in Public school funding as evidenced by the budget of the largest Public school, Wagner High School. Based on Reading scores and budget allocations, it worth investigating either what Wagner is doing or how more resources can be allocated to Wagner, or how other Public schools can maximize the use of their budgets.

3. What can be learned?  It seems there are extra questions that need to be asked at each school.  How is there such a discrepancy between Math scores and Reading scores?  What are Charter schools doing with Math? What are Public schools doing with Reading?

What must remembered after all this provided data, the most important data cannot be stored in a CSV file: each student's story.  Education is about each student's journey through life and learning.  It is important to remember how narrow our picture of education is when we are attempting to measure it with test scores.
