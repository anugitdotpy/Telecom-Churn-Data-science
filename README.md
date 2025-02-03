# Telecom-Churn-Data-science


## Business Problem Overview

In the telecom industry, customers are able to choose from multiple service providers and actively switch from one operator to another. In this highly competitive market, the telecommunications industry experiences an average of 15-25% annual churn rate. Given the fact that it costs 5-10 times more to acquire a new customer than to retain an existing one, customer retention has now become even more important than customer acquisition.

For many incumbent operators, retaining high profitable customers is the number one business goal.

To reduce customer churn, telecom companies need to predict which customers are at high risk of churn.

In this project, we will analyse customer-level data of a leading telecom firm, build predictive models to identify customers at high risk of churn and identify the main indicators of churn.

## Understanding and Defining Churn

**1.Telecom Payment Models**:
- Postpaid: Customers pay after using services (monthly/annually).
- Prepaid: Customers recharge in advance before using services.
 
**2.Churn in Postpaid**: Customers inform the operator before switching, making churn identification straightforward.

**3.Churn in Prepaid**: Customers may stop using services without notice, making churn detection challenging.

**4.Importance of Churn Prediction**: Critical for prepaid customers, especially in India & Southeast Asia, where prepaid is the dominant model.


## Definitions of Churn 

There are various ways to define churn, such as:

**Revenue-based churn:** Customers who have not utilised any revenue-generating facilities such as mobile internet, outgoing calls, SMS etc. over a given period of time. One could also use aggregate metrics such as ‘customers who have generated less than INR 4 per month in total/average/median revenue’.

The main shortcoming of this definition is that there are customers who only receive calls/SMSes from their wage-earning counterparts, i.e. they don’t generate revenue but use the services. For example, many users in rural areas only receive calls from their wage-earning siblings in urban areas.

**Usage-based churn:** Customers who have not done any usage, either incoming or outgoing - in terms of calls, internet etc. over a period of time.

A potential shortcoming of this definition is that when the customer has stopped using the services for a while, it may be too late to take any corrective actions to retain them. For e.g., if we define churn based on a ‘two-months zero usage’ period, predicting churn could be useless since by that time the customer would have already switched to another operator.

In this project, we will use the **usage-based** definition to define churn.

## High-value Churn

In the Indian and the southeast Asian market, approximately 80% of revenue comes from the top 20% customers (called high-value customers). Thus, if we can reduce churn of the high-value customers, we will be able to reduce significant revenue leakage.

In this project, we will define high-value customers based on a certain metric (mentioned later below) and predict churn only on high-value customers.

## Understanding the Business Objective and the Data

The dataset contains customer-level information for a span of four consecutive months - June, July, August and September. The months are encoded as 6, 7, 8 and 9, respectively. 
The business objective is to predict the churn in the last (i.e. the ninth) month using the data (features) from the first three months. 

## Customer Behavior During Churn

- Good Phase: The customer is satisfied with the service and shows normal usage behavior.

- Action Phase: Customer experiences issues (e.g., unfair charges, competitor offers) and exhibits changes in behavior, signaling potential churn risk.

- Churn Phase: The customer stops using the service, and their data is used to tag churn but is not available for prediction.

- Prediction Focus: The key is identifying customers in the action phase to take corrective actions and prevent churn.

## Data Preparation

The following data preparation steps are crucial for this problem:

1. **Derive new features**
This is one of the most important parts of data preparation since good features are often the differentiators between good and bad models. We will use our business understanding to derive features that we think could be important indicators of churn.

2. **Filter high-value customers**
As mentioned above, we need to predict churn only for the high-value customers. Define high-value customers as follows: Those who have recharged with an amount more than or equal to X, where X is the 70th percentile of the average recharge amount in the first two months (the good phase).

3. **Tag churners and remove attributes of the churn phase**
Now tag the churned customers (churn=1, else 0) based on the fourth month as follows: Those who have not made any calls (either incoming or outgoing) AND have not used mobile internet even once in the churn phase. The attributes we need to use to tag churners are:

- total_ic_mou_9
- total_og_mou_9
- vol_2g_mb_9
- vol_3g_mb_9

After tagging churners, we need to remove all the attributes corresponding to the churn phase (all attributes having ‘ _9’, etc. in their names).

## Modelling

Modelling for Churn Prediction

**1.Purpose of the Model**:
- Predict if a high-value customer will churn in the near future.
- Identify key factors that influence customer churn.
  
**2.Actionable Insights**:
- The company can offer special plans, discounts, or better services to retain customers.
  
**3.Handling Class Imbalance**:
- Since churn is low (5-10%), use techniques like oversampling (SMOTE) or undersampling to balance the dataset.
  
**4.Building a Logistic Regression Model**:
- Helps identify important predictors of churn.
- Handle multicollinearity to ensure accurate feature selection.
  
**5.Feature Importance Visualization**:
- Use plots, summary tables, and bar charts to display key churn indicators.
