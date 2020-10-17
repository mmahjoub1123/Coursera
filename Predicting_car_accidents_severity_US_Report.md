# Predicting car accidents severity in the US

# 1 Introduction
## 1.1 Background

The high death rate from road accidents is a major concern in today's society. An efficient and valid treatment is therefore of great importance for citizens and societies. Large efforts and studies have addressed the question of road safety. From year 1913 to year 2018 the was a 96% improvement in the death rate. The research is therefore actively participating in reducing mortality rate in roads. In this report we will be studying the car accidents severity in the US between 2016 and 2020.

## 1.2 Problem

The data we are using include date and time of the incidents, category of junction at which collision took place, the weather condition, and other parameters that describes the environment and the situation that led to the accident. This project aims to predict the severity of an accident based on these parameters.

## 1.3 Interest

The analysis will take into account different aspects and factors that can be valuable to car users to avoid and reduce accident risks.

# 2 Data Description

To analyse the problem i used these datas: A Countrywide Traffic Accident Dataset (2016 - 2020) from Kaggle [1]. The Data is collected using streaming reports on important traffic events. This data is captured by a variety of entities, such as the US and state departments of transportation, law enforcement agencies, traffic cameras, and traffic sensors within the road-networks. There are about 3.5 million accident records in this dataset. It includes, among others, detailed description about the incidents, wether conditions, category of junction at which collision took place.


# 3 Methodology
## 3.1 Data cleaning

There were a lot of missing values in many columns. I decided first to drop the columns if their missing values percentage exceed **30** of the total available data, because performing **missing values fill** on the missing data and filling the missing values will be irrelevent for the final use in the model.

There are several problems with the dataset. First, the type of datetime columns wasn’t right. And some other columns contained values for categorical variables written in different **orthographes**. I replaced the different writings for the same value to a normalized **orthographe**. After fixing these problems i checked for outliers in the data. I found there were some extreme outliers, mostly caused by some types of small sample size problem. For example some weather descriptions had only appeared a few times in the dataset, in which the accidents severity was high. I changed the accidents severity for these columns to missing values.

## 3.2 Feature selection

After data cleaning, there were **x** samples and **y** features in the data. Upon examining the meaning of each feature, it was clear that there was some redundancy in the features. For example, there was a feature of the **A**, and another feature of the **B**, with the difference being that **d**. These features are problematic for two reasons: (1) The accident severity was duplicated in two features. (2) The accident’s conditions  was duplicated in multiple features.
In order to fix this, i decided to keep all features that **a**, and dop their cumulative counterparts. There were also other redundancies, such that **a**. For features that can be obtained from the combination of other features, i decided to drop them.

After discarding redundant features, I inspected the correlation of independent variables, and found several pairs that were highly correlated (Pearson correlation coefficient > 0.9). For example, **a**, **b** and **c** were highly correlated. This makes sense, after all, **reason**. From these highly correlated features, only one was kept, others were dropped from the dataset. After all, **nbfeatures** features were selected.

### 3.2.1 Relationship between accident severity and time of the accident
The hypothetis is that at night there is less visibility in the streets.

### 3.2.2 Relationship between accident severity and weather conditions

## 3.3 Predictive modeling

There are two types of models, regression and classification, that can be used to predict accident severity. Regression models can provide additional information on the **thing**, while classification models focus on the level of severity. Therefore, in this study, I carried out classification modeling.


# 4 Results

# 5 Discussion

# 6 Conclusion

# 7 References

[1] [US Accidents](https://www.kaggle.com/sobhanmoosavi/us-accidents/metadata)

