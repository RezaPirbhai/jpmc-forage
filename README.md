JPMC - Quantitative Research - Virtual Experience

The project was 4-tasks meant to simulate working in quant research at JPMC.


Task 1:
Given the price of gas at the last day of every month for 4 years, using a model predict the prices for the next year and interpolate the data to approximate price at any given day within those 4 years. 

To do this:
I converted dates into date-time.
Created features - lags, rolling averages and sin and cos functions to represent the seasonality in natural gas prices.
Plotted the time series line plot using seaborn

For the actual model I used:
XGBoost (XGBRegressor) - TimeSeriesSplit and I used 4 folds evaluating the MAE (Mean absolute error) across each fold which showed the model was improving quickly, showing the model was fairly well designed.
We use XGBRegressor here as we were using regression analysis to predict future prices.

Now using the model, I predicted the prices for the next 12 months after the initial end date - plotted this graph which showed the graph was fairly accurate.
Note - I didn’t optimise further, as the dataset was limited and I wanted to prioritize building more complex models."

And finally to make the subprogramme, interpolate for the days we need to estimate and use the precise figures for dates already in the data frame and print error if the date is outside our plausible time range, as the model's prediction would be likely inaccurate.


Task 2: 
This invovled given constraints of when to buy/sell gas and the max injection/withdrawal and storage calculating whether it would be profitable.
As we already had all our models maid this required: 
Iterating through the days to add up the storage costs, and if the day was one where a transaction occured log the transaction and the changes - repeat this process until the end of the date range and voila.


Task 3: 

This took upon a new data set of loans. 
We engineered our features and this type used XGBClassifier instead. 

We used classifier this time as: our problem is 'the probability a borrower defaults' which is a classification problem

We then check our models accuracy using logloss and AUC - this showed 
Log loss - Logarithmic Loss - THe lower the value the closer the model is to 0 the closer it is to perfect. 
AUC - Area under the ROC curve - Which evaluates whether a model is ranking correctly - are risky borrwers default % chance higher than the safe borrowers - where 1 shows a perfect score
Our model after all boosting rounds - stopping at 244 due to our early stopping loss metric output: 0.007 which shows a very accurate model and the AUC was 0.9998 showing again an incredibly accurate model.


Finally our expected loss used a function of the probability of default * 1-recovery rate * loan amt outstanding

Task 4: 

We are finding the best way to split fico scores into buckets
Essentially we are grouping buckets so that default rates vary between buckets and not within - so if we are told someone has a FICO score of X we can estimate their default probability based off what bucket they are in.
Initially I had a problem where my time complexity was O(BN^2) which over our 10,000 data points took too long. 

So we adapted and checked how many borrowers have each fico score and how many defaults each fico score, so we are using aggregated counts rather than individual rows.

We then use the log-likelihood of a Bernoulli variable. 

We then use a DP to find the optimal cuts providing the highest total likelihood so each bucket is statistically consistent. 

We then backtrack to recover the cut points, providing us our buckets.


