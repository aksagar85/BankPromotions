# Analyze if customer will subscribe to a product of a Portuguese banking institution
This reports talks about the dataset of direct marketing campaigns of a Portuguese banking institution. The classification goal is to predict if the client will subscribe a term deposit (variable y) or not. We have followed CRISP-DM process model consisting of Business Understanding, Data Understanding, Data Preparation, Modeling, Evaluation, Deployment phases. 

## Dataset Used for this Project 

Data Source :  https://archive.ics.uci.edu/dataset/222/bank+marketing

### Feature Details 

Input variables:

#### bank client data:

1 - age (numeric)

2 - job : type of job (categorical: 'admin.','blue-collar','entrepreneur','housemaid','management','retired','self-employed','services','student','technician','unemployed','unknown')

3 - marital : marital status (categorical: 'divorced','married','single','unknown'; note: 'divorced' means divorced or widowed)

4 - education (categorical: 'basic.4y','basic.6y','basic.9y','high.school','illiterate','professional.course','university.degree','unknown')

5 - default: has credit in default? (categorical: 'no','yes','unknown')

6 - housing: has housing loan? (categorical: 'no','yes','unknown')

7 - loan: has personal loan? (categorical: 'no','yes','unknown')

#### related with the last contact of the current campaign:

8 - contact: contact communication type (categorical: 'cellular','telephone')

9 - month: last contact month of year (categorical: 'jan', 'feb', 'mar', ..., 'nov', 'dec')

10 - day_of_week: last contact day of the week (categorical: 'mon','tue','wed','thu','fri')

11 - duration: last contact duration, in seconds (numeric). Important note: this attribute highly affects the output target (e.g., if duration=0 then y='no'). Yet, the duration is not known before a call is performed. Also, after the end of the call y is obviously known. Thus, this input should only be included for benchmark purposes and should be discarded if the intention is to have a realistic predictive model.

#### other attributes:

12 - campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact)

13 - pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted)

14 - previous: number of contacts performed before this campaign and for this client (numeric)

15 - poutcome: outcome of the previous marketing campaign (categorical: 'failure','nonexistent','success')

#### social and economic context attributes

16 - emp.var.rate: employment variation rate - quarterly indicator (numeric)

17 - cons.price.idx: consumer price index - monthly indicator (numeric)

18 - cons.conf.idx: consumer confidence index - monthly indicator (numeric)

19 - euribor3m: euribor 3 month rate - daily indicator (numeric)

20 - nr.employed: number of employees - quarterly indicator (numeric)

#### Output variable (desired target):

21 - y - has the client subscribed a term deposit? (binary: 'yes','no')


## Business Understanding

### The primary business objective of this project is to make the Portuguese bank's telemarketing campaign successful. We have to develope a prdictive model which can target customers which are more likely to subscribe these products.
### By analysing previous campaigns of the Portuguese bank, we can build and compare different classification models which can accurately find out which clients are more likely to subscribe for the products offered. This prediction can help Portuguese bank to focus it's efforts on specific target audience with greater success rate. 



## Understanding the Data

1. Analyze size of the dataset by using df.shape
2. Check the column information such as names ,data types, value count etc.
3. Check for null and remove null value rows
4. Check for duplicate rows and delete the duplicate rows
5. Understand how many are numeric and how many non-numeric columns
6. Some featues have "unknown" value. We can cleanup these rows as "unkonwn" value is not helpful in creating model
7. We will not use "default" column as all the values are "NO" once we remove "unknown" value rows (Please see visualization for default)
8. Used visualization libraries as well as value_counts to visualize value distribution.

![ValueCount1](https://github.com/aksagar85/BankPromotions/assets/31389612/2388260a-470d-4050-b895-b965b54e30b2)  ![ValueCount2](https://github.com/aksagar85/BankPromotions/assets/31389612/158f1313-c005-48de-9dee-23f4704139bd)

![ValueCount3](https://github.com/aksagar85/BankPromotions/assets/31389612/d6072a6e-2185-4942-9ad6-747ca1cda217) ![ValueCount4](https://github.com/aksagar85/BankPromotions/assets/31389612/8cd810cb-116a-40ba-ae7d-5ad0140f682e)

## Data Preparation

 1. Find if there are any null values and delete or cleanup null values (For this dataset there were no null values present)
 2. Find the duplicates & remove duplicate rows
 3. We are dropping rows which has "unknown" values as those will not help in our model
 4. We are dropping rows which has "unknown" values as those will not help in our model
 5. We are dropping default column because mostly the values are "no"
 6. We will drop poutcome as 85% data is "nonexistent". failure/success is only 15%
 7. We will drop pdays as 96% data is "999". other value percentage is only 4%
 8. We will drop previous as 85% data is "nonexistent". failure/success is only 15%
 9. Age is converted to Ranges instead of using age as number.
 10. Education is converted into numeric values based on education level.
 11. housing and loan are converted from bool to numeric 

## Modeling

We used below 4 classification models on same dataset for comparison
 1. Logistic Regression
 2. KNN (K Nearest neighbour)
 3. Decision Trees
 4. SVM (Support Vector Machine)

Model performance results are in below table : 

![image](https://github.com/aksagar85/BankPromotions/assets/31389612/a22ce554-d93d-487c-92ee-e9a4d2051b17)

We tried using GridSearchCV to find best hyperparameters for above 4 models. Once we used best possible hyperparameters, model performance results changed as below : 

![image](https://github.com/aksagar85/BankPromotions/assets/31389612/10669838-fee1-4124-932a-111842b410f9)


## Results 

### Before the Best Hyperparameters were found :

1. The best performing model is SVM with 0.89687 test accuracy although it was significantly slow with 8.18 seconds Train Time

2. Logistic Regression was lamost as accurate as SVM with 0.89359 test accuracy and it was very fast with 0.15902 seconds of training time.

3. KNN and Decision tree were at number 3 & 4 with respect to accuracy.

### After the Best Hyperparameters were found by using GridSearchCV:

1. The best performing model is "Decision tree" with test accuracy 0.89906 and training time only 0.05621

2. SVMM & Logistic regression are almos as accurate as Decision tree, but SVMM is very slow with training time of 10.14828 seconds of training time

3. KNN is fastest to train with training time of 0.00311 seconds but it is least accurate with test accuracy of 0.88878


## Next Steps :

1. Most of the customers who subscribed have age group 26~35 therefore the Bank Marketing department should target this age group
2. Most customers who subscribed have University Degree so Bank Marketing department can concentrate more on calling people with university degress.
3. Most customers who subscribed have housing loan so Banks can prioritize calling people already owning house and having housing loan than people who are renting
4. Most customers who subscribed have no personal loan so Banks can target people who are not already having personal loan and potentially having funds to invest in Bank Schemes.






