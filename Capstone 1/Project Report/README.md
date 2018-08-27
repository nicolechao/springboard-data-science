## 1st Capstone Project

# Seattle Airbnb Listing Price Prediction

#### Yueh-Tung (Nicole) Chao


![Home](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/Homepage.png)


![Search](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/Search.png)


## Problem
Airbnb is an American company operating online marketplace and hospitality service for people to lease or rent short-term lodging. The company does not own any real estate. Instead, it is a broker which received percentage service fees in conjunction with every booking.
As from 2008, Airbnb has become one of the most popular hospitality services around the world, which has over 5 million lodging listings in 81,000 cities and 191 countries and has facilitated over 300 million check-ins. 
One challenge that Airbnb hosts & Airbnb itself face is determining the optimal nightly rent price. As hosts, if charing too much, then the renter would select more affordable alternatives. On the other hand, if charging too less, then they lose the potential revenue. As for airbnb, if they can recommend optimal listing price to hosts to maximize their revenue, they can receive more service fees as well.
So in this capstone project, we propose to predict airbnb listing price so that both hosts & AIrbnb can optimize their revenue.


## Client
As mentioned in previous session, by predicting listing price, it can be used for both hosts and airbnb for better pricing optimization & maximize the revenue.


## Data Set
* The listing data of Seattle Airbnb can be found on Kaggle: [Seattle Airbnb Open Data](https://www.kaggle.com/airbnb/seattle).

![Kaggle](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/Kaggle.png)
* To visualize data on map, the shapefile of Seattle neighborhood can be found on Zillow: [Zillow Neighborhood Boundaries](https://www.zillow.com/howto/api/neighborhood-boundaries.htm).

![Zillow](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/SeattleGeo.png)


## Data Wrangling
First, we input data & do data wrangling. We conduct the following steps to clean up data and pick useful features.

1. Select columns that might be useful
 * Visually inspect data & select columns that might be useful.
2. Analyze further & remove unwanted columns
 * Originally there are 51 features/columns in the dataset, we further remove some unwanted columns.
 * For example, we drop city-related columns as we are only predict airbnb listing price for one city now so these columns have same values.
3. Drop duplicates (if applicable)
 * We also removed duplicate samples (rows) & duplicate columns (like neighborhood & neighborhood_cleansed).
4. Fix data types
 * Then we look through all the data & fixed data types. For example, we identify categorical data & use sklearn LabelEncoder to encode then for further usage.
 * We also combing latitude & longitude data using binning techniques.
 * Replace some data with special characters, like ‘$’ or ‘%’ with numerical data.
 * Replace dates with datetime object and transformed them into numerical data by calculating number of dates between the dates and the last-scraped-date, etc.
5. Fix missing values
 * Plot scatter plot for columns with missing values and inspect the trend. Confirmed that most of the features are either linear or random to target. 
 * Fill missing values with mean.
6. Find & fix outliers
 * Remove minimum night outlier by cap it to be 99.5 percentile of the data.
7. Drop unnecessary features as we only have 3818 data points so we might not want to have over 20 features.
 * Plot scatter plot of each feature vs. target, i,e, price and drop some unnecessary columns, i.e., columns that do not seem to affect price.


## Initial Findings
During exploratory data analysis, we ask the following questions:

1. What might be the most important features that affect listing price?
2. Does location/neighborhood affect listing price?
3. If yes, what made these neighborhood special?
and ask follow-up questions if needed.

Initial findings are:

1. As we expected, listing price is correlated to accommodates, bedrooms, bathroom, neighborhood, and property type.
 * Interestingly looks like neighborhoods facing water (either bay or lake) seem to have higher listing prices, like Portage Bay.
![PriceGeo](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/PriceGeo.png)
 - However there might be some exceptions:
    - There might be extremely high listing price although there's only one bedroom, but rarely happened.
    - If the property has a lot more bathrooms, ex. 8, but it's a dorm, the listing price would not increase proportionally.
    -If the property has a lot more bathrooms, ex. 8, but can only accommodate 2 people, the listing price would not increase proportionally, either.
    - If the property is a big house which can accommodate 14 people but its accommodates vs. bedrooms ratio and/or accommodates vs. bathrooms ratio are higher, that means more traveler need to share the bedrooms / bathrooms, the listing price would not increase proportionally, either.
2. Property-type-wise, most of the property type of Seattle listings are house and apartment.
 - Wallingford & First Hill have most number of listings whose property type is house.
 - First Hill & Belltown have most number of listings whose property type is apartment.
 - Over 13% of Seattle Airbnb listings are located in First Hill.
3. In terms of bedrooms and bathrooms, 1 bedroom 1 bathroom Airbnbs which can accommodate 1 ~ 4 people are most common in Seattle.
 - Over 50% of Seattle Airbnb listing are of this type.
 - About 10% of them are located in First Hill.
 - For the rest of Airbnbs, not many of them can accommodate more than 10 people. In fact, only 1.3% of listings can accommodate 10 or more than 10 people, and other than First Hill, most of them are located in some suburban area.


## Modeling
With insights based on exploratory data analysis (EDA), we start to train predictive models.


We check the distribution of our target, which is price & confirmed that taking log can make it distribute more normally & skew is much improved.

![PriceOriVsLog](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/PriceOriVsLog.png
)

We identified five models to try first:

1. K-Nearest Neighbors
	* Predict the label of a data point by
		* Looking at the ‘k’ closest labeled data points
		* Taking a majority vote
2. Linear Regression
	* Predict the label of a data point by a linear function
	* Loss function = Ordinary least squares (OLS), which is sum of squares ofresiduals
3. Ridge Regression (L2 regularization)
	* Same as Linear Regression but penalize large coefficients by L2 regularization: ![Ridge](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/Ridge.gif)
4. Lasso Regression (L1 regularization)
	* Same as Linear Regression but penalize large coefficients by L1 regularization: ![Lasso](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/Lasso.gif)5. Random Forest
	* Predict the label of a data point by ensembling decision trees, which correct for decision trees' habit of overfitting.

And train the above models with three features:

1. Accommodates
2. Bathrooms
3. Bedrooms

Test size of Train-test-split is set to 33%.
We chose Root-Mean-Squared-Error (RMSE) as our scoring metric.

For linear models including Linear Regression, Ridge Regression & Lasso Regression, we also try to take log on price. Here's a brief summary RMSE of each model:

1. K-Nearest Neighbors
 - Best hyperparameter for n_neighbors is 33. RMSE is  63.8775604886.
2. Linear Regression
 - If not taking log on price: RMSE is 65.782884005.
 - If taking log on price: RMSE is 80.6990729468.
3. Ridge Regression
 - If not taking log on price: Best hyperparameter for alpha is 50. RMSE is 65.7372413634.
 - If taking log on price: Best hyperparameter for alpha is 10. RMSE is 80.4074239407.
4. Lasso Regression
 - If not taking log on price: Best hyperparameter for alpha is 0.0001. RMSE is 65.782902475.
 - If taking log on price: Best hyperparameter for alpha is 0.0001. RMSE is 80.6875515723.
5. Random Forest
 - Best hyperparameter for max_depth is 10. Best n_estimators is 30. RMSE is 65.8094760545.

A plot for each model and their corresponding RMSE is like:

![ModelRMSE](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/ModelRMSE.png)

We also include more plots on:

1. Histogram of predicted price
2. Actual price vs. predicted price
3. Residual plot
4. Histogram of residuals

of each model in Appendix.

Based on the above results,

1. KNN has best RMSE.
2. Although taking log on price did make it distribute more normally, RMSE isn't better.
 - We plot influence plot to check if there’s high leverage point: ![PriceGeo](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/InfluencePlot.png)
 - And by removing high leverage points, we trained the model again. However RMSE still isn’t better on linear models.
 - By analyzing further, it looks like there are less data points with price above about 300 and looks like they have a different linear relationship. For this piecewise linear regression is sometimes used.

We then get back to the models. As KNN & Random Forest have best results so far, we analyze outliers of these two models further.

For both models, there are many data with **actual price greater than 600 while predicted price is less than 400**. By looking into them, we found that over half of them are **house** in terms of **property type**, which means it worths to try to add property type into our features.

We then try to add property type into our features:
1. K-Nearest Neighbors
 - Best hyperparameter for n_neighbors is 17. RMSE is  66.2413412525.
2. Random Forest
 - Best hyperparameter for max_depth is 10. Best n_estimators is 80. RMSE is  65.4463938358.

Without property type, KNN has RMSE 65.7802492126, random forest has RMSE 66.1536873354.

After adding property type, KNN gives 66.2413412525, random forest gives 65.4463938358. **Looks like KNN result degraded while Random Forest is improved.**

Also in exploratory data analysis (EDA), we also found that price is also affected by neighborhood. We further added into our features.

1. K-Nearest Neighbors
 - Best hyperparameter for n_neighbors is 4. RMSE is 73.3585695725.
2. Random Forest
 - Best hyperparameter for max_depth is 10. Best n_estimators is 90. RMSE is  63.5181692736.

By adding neighborhood, we can further improve Random Forest results a little bit. RMSE is improved from 65.4463938358 to 63.5181692736.

**However KNN results degrade a lot. By inspecting the KNN models, number of 'n_neighbors' became smaller & smaller when we add more features.**

**Note that KNN depends on similar neighbor data points to get better prediction results. It looks like when we add more features, it increased dementinality. With the curse of dimensionality. Number of similar data points seems becoming less, so RMSE started to get higher.**

**On the other hand, random forest by nature automatically select useful features for splitting so did not have this issue.**

Last but not least, we try the Gradient Boosting model, which predict the label of a data point by

1. Iteratively learning a set of weak models on subsets of the data2. Weighing each weak prediction according to each weak learner'sperformance3. Combine the weighted predictions to obtain a single weightedprediction

Initial trial with hyperparameter tuning only on n_estimators shows that RMSE is 63.749581598.

If we tune more hyperparameters, like learning_rate and max_depth, RMSE is further improved to 63.1581040609, which is the best out of all the models.

In my opinion it proved that with the techniques of gradient boosting, it can indeed improve prediction accuracy.


### Summary
1. We tried 6 different models on Airbnb listing price prediction
 - K-Nearest Neighbors
 - Linear Regression
 - Ridge Regression
 - Lasso Regression
 - Random Forest
 - Gradient Boosting
2. KNN & random forest outperforms linear regression models. After adding more features, random forest performs better than KNN.
 - If looking at KNN results, after adding more features, best parameter for n_neighbors became less. It might be because KNN depends on similar neighbor data points to get better prediction results. When adding more features, it increased dementinality. With the curse of dimensionality. Number of similar data points seems becoming less, so RMSE started to get higher.
 - On the other hand, random forest by nature automatically select useful features when splitting so did not have this issue.
3. Linear regression models did not perform well because here are less data points with price above about 300 and looks like they have a different linear relationship. For this piecewise linear regression is sometimes used.
4. Gradient boosting model gives the BEST RMSE compared to all other models.


## Conclusion
As from 2008, Airbnb has become one of the most popular hospitality services around the world. One challenge that Airbnb hosts & Airbnb itself face is determining the optimal nightly rent price.

In this project, we have done data wrangling to clean up data. We've 

With the model we have developed, now we are able to predict Airbnb listing price given several features, like bedrooms, bathrooms, accommodates, neighborhoods and property type. In addition, we acheived RMSE 63.1581040609 using XGBoost model, which means the square root of the average of squared differences between predicted price and actual price is only about 63. This can be very useful for both Airbnb host and the company itself, as they can now come up with a reasonble price to maximize their revenue.

## Next Steps
While we already tried several models, there are still some interesting future works:

1. Apply natural language processing (NLP) on Airbnb reviews for better listing price prediction.
2. Apply piecewise linear regression model.
3. Apply models on other cities or training model on other cities.


## Other Potential Data Sets
More data can be found at: [Inside Airbnb](http://insideairbnb.com/get-the-data.html).

## Appendix

Plots of each model for the initial modeling trial:

1. K-Nearest Neighbors
![KNNPlot](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/KNN.png)
2. Linear Regression
 - Not taking log on price:
![LinearPlot](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/Linear.png)
 - Taking log on price:
![LinearLogPlot](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/LinearLog.png)
3. Ridge Regression
 - Not taking log on price:
![RidgePlot](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/Ridge.png)
 - Taking log on price:
![RidgeLogPlot](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/RidgeLog.png
)
4. Lasso Regression
 - Not taking log on price:
![LassoLog](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/Lasso.png)
 - Taking log on price:
![LassoLogPlot](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/LassoLog.png)
5. Random Forest
![RandomForestPlot](https://raw.githubusercontent.com/nicolechao/springboard-data-science/master/Capstone%201/Images/RandomForest.png)