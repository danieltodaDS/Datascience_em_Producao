## Rossmann Sales Predictions

### Predicting the future sales of Rossmann Drugstore

![image](https://user-images.githubusercontent.com/110186368/206006636-6f17e11b-a0fd-47f6-a5bc-5da45760bc87.png)

*obs: Still the dataset and the company are real, the business problem is ficticious. The dataset was collected from [Kaggle]*

------------------
### Business Problem

  Rossmann is a drugstore chain that operates over 3000 stores in 7 European country. Rossmann's CFO required from the managers a forecast of the sales of each store, because he needs to assure that will have enough budget to make the renovation of them. 
  
  The **Data Science** project is focused on solving the following: 
  
  * Delevop a sales prediction for next 6 weeks for each store to ensure taht budget 
  * Deploy the model of predictions on a Telegram Bot
 
--------------------------
### Business Assumption

--------------------------
### Solution Strategy

**Step 01. Data Description.** The goal is to use statistcs metrics to identify data outside the scope of the business

**Step 02. Feature Engineering.** Derive new attributes based on the original variables to better describe the phenomenon that will be modeled 

**Step 03. Data Filtering.** Filter rows and select columns that do not contain information for modeling or that do not match the scope of the business

**Step 04. Exploratory Data Analysis.** Explore the data to find insights and better understand the impact of variables on model learning 

**Step 05. Data Preparation.** Prepare the data so that the Machine Learning models can learn specific behavior.

**Step 06. Feature Selection.** Selection of the most significant attributes for training the model

**Step 07. Machine Learning Modeling.** Machine Learning model training

**Step 08. Hyperparameter Fine Tuning.** Choose the best values for each of the parameters of the model selected from the previous step 

**Step 09. Convert Model Performance to Business Values.** Convert the performance of the Machine Learning model into a business result

**Step 10. Deploy Model to Production.** Publish the model in a cloud environment so that other people or services can use the results to improve the business decision

--------------------------

### Top 3 business insights 

**1. Closer competition does not implicate reduced sales**

![image](https://user-images.githubusercontent.com/110186368/206879405-1c1f9aaa-9e35-4672-b2cc-7da2a1e0fae8.png)


**2. Older competition has a correlation with a lowering in sales**

![image](https://user-images.githubusercontent.com/110186368/206879580-d3265f2d-1ef3-41f0-8214-3aabcd840fe1.png)


**3. Extended promotions do not implicate greater sales**

![image](https://user-images.githubusercontent.com/110186368/206879870-3abb3201-d92d-46fb-97ee-24fab9573965.png)

--------------------------

### Machine Learning Models Applied

At this project, six models was trained: 

 - Average Model (used as baseline model)
 - Linear Regression
 - Lasso Regression (Regularized Linear Regression)
 - Random Forest Regressor
 - XGBoost Regressor
 
--------------------------

### Machine Learning Models Performance   

After time series cross-validation (except for the average model) it obtained the following results:

| Model                   | MAE               | MAPE          | RMSE |
| :---                    |     ---:          |          ---: | ---:             |
| Linear Regression       | 2094.24+/-301.77  | 0.3+/-0.02	  | 2094.24+/-301.77 |
| Lasso Regression        | 2388.68+/-398.48  | 0.34+/-0.01	  | 2388.68+/-398.48 |
| Random Forest Regressor | 842.21+/-236.42	  | 0.12+/-0.03   | 842.21+/-236.42  |
| XGBoost Regressor       | 1675.93+/-176.76  | 0.23+/-0.01	  | 1675.93+/-176.76 |

Though Random Forest Regressor obtained the lower RMSE, **XGBoost** was the chosen model, because of its time of execution, and an RMSE low enough for the purpose of this project. Its parameter was tuned and the final performance on the test data obtained was:

| Model             | MAE     | MAPE  | RMSE    |
| :---              | ---:    | ---:  | ---:    |
| XGBoost Regressor | 1084.09	| 0.16	| 1575.98 |

#### Metrics definition and interpretation

- MAE: Mean Absolute Error
- MAPE: Mean Absolute Percentage Error
- RMSE: Root Mean Squared Error

RMSE is a metric key to check statistical performance and is used as a standard for measuring performance models.

Both MAE and MAPE, indicate the average error in absolute and relative terms, respectively, and are useful for explaining to the business teams the model's errors

--------------------------

### Business Results

Recapping the business problem, the CFO needs to have 6 six weeks of prediction sales, in order to have the necessary budget to reform the stores. The answer to this question is presented below in an aggregate value (total sum of sales), as well as the best and worst scenarios, calculated from the MAE. 

| Scenario       | Values             | 
| :---           | ---:               | 
| Predictions    |  $ 276,156,800.00  |  
| Worst Scenario |  $ 275,390,761.93  | 
| Best Scenario  |  $ 276,922,824.34  |  

Considering the 1115 stores, it gives a mean of $ 247674/store in the next 6 weeks. The prediction for each store can be seem in the [Telegram BOT](...) 

--------------------------

### Lessons Learned


--------------------------

### Next Steps

--------------------------

### Conclusion 
