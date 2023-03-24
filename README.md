# Predicting Recipe Time Preparation
A regression and prediction project concerning recipes and ratings on food.com, for DSC 80 at UC San Diego.

By: Charlie Gillet (cgillet@ucsd.edu)

## Introduction

My prediction problem is to predict the number of minutes to prepare recipes, and this is a regression problem since number of minutes is a continuous variable. The relevant information that is known at the time of prediction are the date at which the recipe was submitted, the nutrition facts, and the average rating of the recipe.

## Baseline Model

My modeling process will involve feature engineering, fitting the model with a loss function, and evaluating the model using RMSE. The features I will be using in my model are the date at which the recipe was submitted (year and month), the nutrition facts, and the average rating of the recipe. The recipe’s submission date is a categorical ordinal variable since it follows a time sequential order. To make this variable functional for prediction I will use ordinal encoding to make the first year-month combination (January 2008) marked as a 1, and the last year-month combination (December 2018) marked as 132 (There are 132 different year-month combinations). The nutrition facts are all quantitative continuous data, so no feature engineering is necessary for them. The average rating of the recipe is also a quantitative continuous variable, so no feature engineering is necessary. Lastly, I had to make changes to the ‘minutes’ column of the dataset because there were some extreme outliers. 

Upon checking the recipes website, these extremely high preparation time values were due to recipes that involve leaving a food item to sit for weeks or months, or they were joke recipes. I chose to cap this at 1 week or 10080 minutes. This resulted in about 200 entires being removed from the dataset, which is negligible since the dataset has over 200000 rows. Additionally, the average rating column had about 3000 null values, which I removed from the dataset for simplicity, which is relatively negligible.

The performance of my model was not ideal, since I just used the raw values from the dataset without any modification.

## Final Model

To improve upon my baseline model, I came up with some ideas on which columns to modify so that I could experiment with either changing these columns or leaving them as-is. I planned to modify the ‘date_ordinal’ column and the nutritional columns by standardizing them, and to modify the average rating column with quantile transformation. After experimentation, I found the best result to be to quantile transforming the average rating column and standardizing all of the nutritional columns, and leaving the submission date column as-is. I believe these changes improved my model because the average rating column primarily consists of duplicate values, like 4, 4.5, or 5. This makes it so that the distribution of average ratings is not normal, since values are clustered around these duplicate values. Using quantile transformer with normal distribution makes the rating values less clustered, so it is easier to find a trend with them. This led to a decrease in RMSE compared to the baseline model, which is a sign of improvement. Standardizing the nutritional columns made less of a difference than using the quantile transformer on the average rating column, but it still led to a decrease in RMSE.