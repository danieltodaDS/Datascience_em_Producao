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

#### Data overview 
<details>
  <summary>Click to see the description of the columns</summary>
  
|Feature 	                        |Definition |
| :---                            |     :---          |
|Id 	                            |an Id that represents a (Store, Date) duple within the dataset.|
|Store 	                          |a unique Id for each store.|
|Sales 	                          |the turnover for any given day.|
|DayOfWeek 	                      |day of week on which the sale was made (e.g. DayOfWeek=1 -> monday, DayOfWeek=2 -> tuesday, etc).|
|Date                             |	date on which the sale was made.|
|Customers                        |	the number of customers on a given day.|
|Open                             |	an indicator for whether the store was open: 0 = closed, 1 = open.|
|StateHoliday                     |	indicates a state holiday. Normally all stores, with few exceptions, are closed on state holidays. Note that all schools are closed on public holidays and weekends. a = public holiday, b = Easter holiday, c = Christmas, 0 = None.|
|SchoolHoliday                    |	indicates if the (Store, Date) was affected by the closure of public schools.|
|StoreType                        |	differentiates between 4 different store models: a, b, c, d.|
|Assortment                       |	describes an assortment level: a = basic, b = extra, c = extended.|
|CompetitionDistance              |	distance in meters to the nearest competitor store.|
|CompetitionOpenSince(Month/Year) |	gives the approximate year and month of the time the nearest competitor was opened.|
|Promo 	                          |indicates whether a store is running a promo on that day.|
|Promo2 	                        |Promo2 is a continuing and consecutive promotion for some stores: 0 = store is not participating, 1 = store is participating.|
|Promo2Since(Year/Week)           |	describes the year and calendar week when the store started participating in Promo2.|
|PromoInterval                    |	describes the consecutive intervals Promo2 is started, naming the months the promotion is started anew. E.g. "Feb,May,Aug,Nov" means each round starts in February, May, August, November of any given year for that store.|
  
</details>

#### Assumptions

For missing values in the column "competition_distance" we assume that there is no competitor nearby, and then it was replaced for a greater value than the maximum value of "competition_distance" 

Column "customer", which represents the number of customers, was dropped when training the model since there is no information about this number in the future 

<details>
  <summary>Click to see the new features created</summary>
  
  |New Feature 	                                                                                         | Definition                                     | 
  | :---                                                                                                 |     :---                                       |
  |year/month/day/week_of_year/year_week                                                                 | year/month/day/week_of_year/year_week extraced from the column 'date'                 |
  |day_sin/day_cos/month_sin/month_cos/week_of_year_sin/week_of_year_cos/day_of_week_sin/day_of_week_cos | features derived in sin/cos to capture their ciclycal atribute                      |
  |competition_since                                                                                     | date since the competition was opened          |
  |competiton_time_month                                                                                 | period in months since the competition started |
  |promo_since                                                                                           | concatenation of 'promo2_since_year' and 'promo2_since_week'    
  |promo_time_week                                                                                       | time in weeks from when the promotion was active.                                |
  |state_holiday(christmas/easter_holiday/public_holiday/regular_day)                                    | indicates wheter the sale was made in christmas, easter, public holiday or regular day. |
  |is_promo2                                                                                             | whether the purchase occurred during an active promo2 (1) or not (0)                  |
</details>

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


**2. Older competition has a negative correlation with a lowering in sales**

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

Considering the 1115 stores, it gives a mean of $ 247674/store in the next 6 weeks. 

#### Model Deployment

The prediction for each store for the next 6 weeks can be accessed in a Telegram Bot. The ideia behind this is that the results can be acessed at any time with any device with a proper internet connection. 

To use this bot, you have to inform the id store, after passing a / (e.g. /12, /34, etc). 

Link to chat with Telegram Bot <a href = "https://t.me/sales_predictor_bot" rel="nofollow"> <img src="https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white"> </a>

--------------------------

### Next Steps

- Improve the EDA to find out more insights
- Test other machine learning algorithms
- Forecast of the number of customers, since this feature has a high correlation with sales

--------------------------

### Conclusion 

This project could adreess the requisition of CFO and make predictions of 6 six weeks of sales of each store. Then it will be possible to estimate the budget under disposal to make the renovation of stores and a Telegram Bot to access this information with device connected to internet
