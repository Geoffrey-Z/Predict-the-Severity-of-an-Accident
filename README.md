# Predict-the-Severity-of-an-Accident

# 1. Introduction

Traffic accidents are a significant source of deaths, injuries, property damage, and a major concern for public health and traffic safety. Accidents are also a major cause of 
traffic congestion and delay. Effective management of accident is crucial to mitigating accident impacts and improving traffic safety and transportation system efficiency. 
Accurate predictions of severity can provide crucial information for emergency responders to evaluate the severity level of accidents, estimate the potential impacts, and implement efficient accident management procedures. By recognizing the key factors that influence accident severity, the solution may be of great utility to various Government Departments/Authorities like DOT and Police. The results of analysis and modeling can be used by these Departments to take appropriate measures; such as early warning system to drivers; to reduce accident impact and thereby improve traffic safety. It is also useful to the Insurers in terms of reduced claims and better underwriting as well as rate making.
Introduction where you discuss the business problem and who would be interested in this project.

# 2. Data Understanding
The dataset come from City of Seattle Open Data Portal that contains all types of collisions from 2004 to Present. This raw dataset consists of 221,266 cases and 40 attributes. The description of each columns can be found in this link 

https://s3.us.cloud-object-storage.appdomain.cloud/cf-courses-data/CognitiveClass/DP0701EN/version-2/Metadata.pdf

SEVERITYCODE feature is the target variable to predict the severity of car accidents. It is a categorical feature that is defined as 1, 2 to indicate the accident was of 
Prop Damage only, Injury.

# 3. Data Preparation
# 3.1 Data Clean Up
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(2).png)

The plot above tells us that there is a extreme imbalance for the target variable.

I remove features in dataset that may:
- have high percentage of missing data over 85%.
- irrelevant to accident severity such as ReportNo, Status.
- be derived from others features such as SEVERITYDESC, SEGLANEKEY. These derived features don’t add value to dataset. It also create unnecessary correlation between features.
- be provided after the accidents has been reported and processed such as count of Fatality victims based on its severity. Post accidents features create strong bias into our model.


## Percent of missing values in each column
|column|missing percent|
|---|---|
|PEDROWNOTGRNT|	97.602646|
|EXCEPTRSNDESC|	97.103861|
|SPEEDING|	95.205807|
|INATTENTIONIND|	84.689710|
|INTKEY|	66.574718|
|EXCEPTRSNCODE|	56.434123|
|SDOTCOLNUM|	40.959455|
|JUNCTIONTYPE|	3.251093|
|X|	2.739979|
|Y|	2.739979|
|LIGHTCOND|	2.655736|
|WEATHER|	2.610018|
|ROADCOND|	2.574574|
|ST_COLDESC|	2.519096|
|COLLISIONTYPE|	2.519096|
|UNDERINFL|	2.508822|
|LOCATION|	1.375126|
|ADDRTYPE|	0.989351|
|ST_COLCODE|	0.009246|
|SDOT_COLDESC|	0.000000|
|SEGLANEKEY|	0.000000|
|CROSSWALKKEY|	0.000000|
|SEVERITYCODE|	0.000000|
|VEHCOUNT|	0.000000|
|SDOT_COLCODE|	0.000000|
|INCDTTM|	0.000000|
|INCDATE|	0.000000|
|PEDCYLCOUNT|	0.000000|
|PEDCOUNT|	0.000000|
|PERSONCOUNT|	0.000000|
|SEVERITYDESC|	0.000000|
|SEVERITYCODE.1|	0.000000|
|STATUS|	0.000000|
|REPORTNO|	0.000000|
|COLDETKEY|	0.000000|
|INCKEY|	0.000000|
|OBJECTID|	0.000000|
|HITPARKEDCAR|	0.000000|

Each features are examined thoroughly for its consistency for every classes. Some features clearly stand out as a differentiator for a class but indistinguishable on other classes.

![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(9).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(10).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(11).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(12).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(13).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(14).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(15).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(16).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(17).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(18).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(19).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(20).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(21).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(22).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(23).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(24).png)

# 3.2 Feature Engineering
The time and date of when the accident happens maybe contain some information. For example, Friday evening road traffic gets heavier increasing the probability of road accident. I extract MONTH, DAY, HOUR features from accident date and time. We can see that these three new features somewhat related to accident severity. For example, be in a traffic in Friday night December increases the chance of fatality accident.

![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(4).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(3).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(6).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(5).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(8).png)
![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(7).png)

Latitude and longitude feature are converted to Cartesian coordinate assuming the earth is sphere. From the scatter plot below we can see property damages accident is everywhere but fatality accidents are at certain location.

After data clean up, feature engineering and hot encode categorical data, the clean dataset has 75 predictors with 184,146 samples.

# 4. Methodology

Logistic Regression and Random Forest models are used to solve the problem which is to predict the accident severity. I use the following techniques to handle the imbalance in the dataset:

- Feed the models with resampled train data after train_test_split process. I use SMOTE algorithm from imblearn-learn package for oversampling.

![image](https://github.com/Geoffrey-Z/Predict-the-Severity-of-an-Accident/blob/master/IMG/download%20(25).png)
