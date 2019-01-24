# Take Home Challenge Exercise


## Problem: Rider Retention Prediction

### Part 1 ‑ Exploratory data analysisThe attached logins.json file contains (simulated) timestamps of user logins in a particular geographic location. Aggregate these login counts based on 15minute time intervals, and visualize and describe the resulting time series of login counts in ways that best characterize the underlying patterns of the demand. Please report/illustrate important features of the demand, such as daily cycles. If there are data quality issues, please report them.### Part 2 ‑ Experiment and metrics designThe neighboring cities of Gotham and Metropolis have complementary circadian rhythms: on weekdays, Ultimate Gotham is most active at night, and Ultimate Metropolis is most active during the day. On weekends, there is reasonable activity in both cities. However, a toll bridge, with a two way toll, between the two cities causes driver partners to tend to be exclusive to each city. The Ultimate managers of city operations for the two cities have proposed an experiment to encourage driver partners to be available in both cities, byreimbursing all toll costs.1. What would you choose as the key measure of success of this experiment inencouraging driver partners to serve both cities, and why would you choose this metric?2. Describe a practical experiment you would design to compare the effectiveness of theproposed change in relation to the key measure of success. Please provide details on:  * how you will implement the experiment  * what statistical test(s) you will conduct to verify the significance of the observation  * how you would interpret the results and provide recommendations to the city operations team along with any caveats.### Part 3 ‑ Predictive modelingUltimate is interested in predicting rider retention. To help explore this question, we have provided a sample dataset of a cohort of users who signed up for an Ultimate account in January 2014. The data was pulled several months later; we consider a user retained if they were “active” (i.e. took a trip) in the preceding 30 days.We would like you to use this data set to help understand what factors are the best predictors for retention, and offer suggestions to operationalize those insights to help Ultimate.The data is in the attached file ultimate_data_challenge.json. See below for a detailed description of the dataset. Please include any code you wrote for the analysis and delete the dataset when you have finished with the challenge.1. Perform any cleaning, exploratory analysis, and/or visualizations to use the provided data for this analysis (a few sentences/plots describing your approach will suffice). What fraction of the observed users were retained?2. Build a predictive model to help Ultimate determine whether or not a user will be active in their 6th month on the system. Discuss why you chose your approach, what alternatives you considered, and any concerns you have. How valid is your model? Include any key indicators of model performance.3. Briefly discuss how Ultimate might leverage the insights gained from the model to improve its longterm rider retention (again, a few sentences will suffice).

## Data
1. A login timestamp table ( "Data/logins.json" ) that has timestamps of user logins in a particular geographic location.
2. A rider table ( "Data/ultimate\_data\_challenge.json" ) with the following columns:
  * city: city this user signed up in  * phone: primary device for this user  * signup_date: date of account registration; in the form ‘YYYY MM DD’  * last_trip_date: the last time this user completed a trip; in the form ‘YYYY MM DD’  * avg_dist: the average distance in miles per trip taken in the first 30 days after signup  * avg_rating_by_driver: the rider’s average rating over all of their trips  * avg_rating_of_driver: the rider’s average rating of their drivers over all of their trips  * surge_pct: the percent of trips taken with surge multiplier > 1  * avg_surge: The average surge multiplier over all of this user’s trips  * trips_in_first_30_days: the number of trips this user took in the first 30 days after signing up  * ultimate_black_user: TRUE if the user took an Ultimate Black in their first 30 days; FALSE otherwise  * weekday_pct: the percent of the user’s trips occurring during a weekday


## Approach

### Part 1 ‑ Exploratory data analysis
* Apply time series resmapling method to identify underlying pattern.

### Part 2 ‑ Experiment and metrics design
* Apply hypothesis testing to measure success of this experiment.

### Part 3
1. Apply data wrangling to fix data types and fill missing values and fix outliers if applicable.
2. Define retained rider using time series analysis techniques.
3. Apply exploratory data analysis to find potential correlation between features and target, i.e., whether rider is retained.
4. Apply machine learning with 4 different models:
  * K-Nearest Neighbors
  * Logistic Regression
  * Random Forest
  * Gradient Boosting
5. Analyze models and find predictive features.


## Conclusion
With the exploratory data analysis and predictive model, avg\_rating\_by\_driver, surge\_pct, weekday\_pct and city are key features for predicting rider retention. The models can also be used to maintain / improve the rider retention.

For example, Ultimate can focus more on riders whose sign up city is Astapor since their retention seem not good. Ultimate should also focus more on improving Android application user experience since their retention is not good.

## Deliverables
1. Data wrangling, exploratory data analysis & modeling code in Python notebook.
