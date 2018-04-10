# JSON-Based Data Exercises


## Problem
Using data in file 'data/world_bank_projects.json' and data wrangling skills to:

1. Find the 10 countries with most projects.
2. Find the top 10 major project themes (using column 'mjtheme_namecode').
3. In 2. some entries have only the code and the name is missing. Create a dataframe with the missing names filled in.

## Approach
1. Use pandas, json, json_normalize from pandas.io.json package to load / analyze data.
2. Use groupby / value_counts functions to find top countries / themes.
3. Extract names from data where name exists and then fill them to missing ones.
4. Plot bar chart to visualize data after cleaning up the data.


## Deliverables
1. Data wrangling code in Python notebook.
