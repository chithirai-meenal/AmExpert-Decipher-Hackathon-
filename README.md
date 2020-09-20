# AmExpert-Decipher-Hackathon-

Explained my approach to solve a Hackathon conducted by AnalyticsVidhya that helped me stand in the 8th position in Private Leaderboard.

**Link to Competition: https://datahack.analyticsvidhya.com/contest/amexpert-decipher-women-machine-learning-hackathon/  **

**Leaderboard Rank - 8**: My Username in the competition - anonymousC683HQ

https://datahack.analyticsvidhya.com/contest/amexpert-decipher-women-machine-learning-hackathon/pvt_lb



**Objective**

To predict the credit card spend of customers for next three months using the past three months customer usage and demographic data. 

**Evaluation Criteria**

Accuracy of the predictive model is evaluated using Root Mean Squared Logarithmic Error (RMSLE). 
                          
**Data**

Customer credit/ debit usage and demographic information for three months – Apr, May, Jun – is shared for training. 
* Rows – 32,820
* Columns - 44

A new set of customers’ data is shared for testing the model performance. Evaluation is based on the accuracy achieved by testing the model on test dataset.
* Rows – 14,067
* Columns – 43 (Except the target variable)


**Approach**

1)  Data Ingestion and Cleaning

* Replaced all numeric rows containing NA with 0. Reason for imputing with 0 is that it made sense to retain 0 rather than imputing with mean/ median for most variables. Ex: Credit/ Debit card spend/ count may be 0 in real world scenarios.
*  Target variable ‘cc_cons’ is found to be extremely skewed to the right. That is, very few customers had spent extremely high compared to others. 
    * However, model finds it really difficult to predict for low spend customers rather than high spend customers. 
    * This is found after implementing the model and analyzing the error terms. 
    * Model predicted higher values for extremely low spenders that increased the final RMSLE.
    * Hence, replaced those ‘cc_cons’ values that fall under 1% percentile with median value to help the model predict lesser values for such cases and it helped to boost the accuracy.
* Created an exhaustive list of 157 derived variables to capture the interaction among independent variables.
* Label encoded categorical variables to help for modeling exercise.

2) Modeling:

* Used LightGBM for predicting credit card spend after trying out multiple other algorithms like XGBoost and CatBoost.
* Fine-tuned the parameters of LightGBM using Grid Search and Random Search to find out the best parameters for fitting.
* Performed 10 folds cross-validation to remove any bias and avoid over-fitting.



