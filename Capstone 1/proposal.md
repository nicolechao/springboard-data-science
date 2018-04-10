# 1st Capstone Project

## Problem: Airbnb Listing Price prediction
As Airbnb has become one of the most popular hospitality services around the world, it would be interesting & important to predict listing price of Airbnb for both Airbnb itself and traveller. 

## Potential Clients
By predicting listing price, it can be used for better pricing optimization for Airbnb. It can also be used to check if the fare is reasonable for a traveller.

## Data
* The listing data of Seattle Airbnb can be found on Kaggle:
[Seattle Airbnb Open Data](https://www.kaggle.com/airbnb/seattle).
* More data can be found at:
[Inside Airbnb](http://insideairbnb.com/get-the-data.html).

## Approach
1. Use regression for this supervised problem.
2. Predict the listing price using features of listings as predictors.
3. Create normalized-price as followed for better prediction (might change after more exploratory data analysis).
  - price * weather
  - price * # bus station / # light rail in radius
  - price * # bars / # restaurants in radius
  - price * # sightseeing attractions in city

## Deliverables
1. Code
 - data cleaning
 - data exploration analysis
 - machine learning model
2. Presentation Slide Deck
