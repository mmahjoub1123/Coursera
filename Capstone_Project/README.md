# Coursera_Capstone
This notebook will be mainly used for the capstone project.


# Useful tools

## Imputation
- Better use SimpleImputer(strategy='constant') to Preprocess for numerical data
- Use SimpleImputer(strategy='most_frequent') for categorical data


## Missing values

- Get columns with missing values( cols_with_missing = [col for col in X_train.columns if X_train[col].isnull().any()] )
- If dropping the columns removes a lot of useful information, so Imputation would perform better.

## To build the model

- the preprocessed DataFrames have the same number of columns,
- the preprocessed DataFrames have no missing values, 
- `X_train` and y_train have the same number of rows, and
- `X_valid` and y_valid have the same number of rows.
- use a method that agrees with how you preprocessed the training and validation data, and set the preprocessed test features to `X_test`.
- use the preprocessed test features and the trained model to generate test predictions.
- Ensure that the preprocessed test DataFrame has no missing values.

## Model Validation
- For small datasets, should run cross-validation.
- For larger datasets, a single validation set is sufficient.


## Remove rows with missing target, separate target from predictors
```
X_full.dropna(axis=0, subset=['SalePrice'], inplace=True)
y = X_full.SalePrice
X_full.drop(['SalePrice'], axis=1, inplace=True)
```
## Break off validation set from training data
X_train_full, X_valid_full, y_train, y_valid = train_test_split(X_full, y, train_size=0.8, test_size=0.2,random_state=0)



## Useful function expressions

scores = {i: f(i, y, y) for i in list_i}
best_i = min(scores, key=scores.get)

## Random Forest models

model = RandomForestRegressor(n_estimators=100, criterion='mae', random_state=0)

## Get names of columns with missing values
cols_with_missing = [col for col in X_train.columns if X_train[col].isnull().any()]

## Drop columns in training and validation data
reduced_X_train = X_train.drop(cols_with_missing, axis=1)

# Imputation
from sklearn.impute import SimpleImputer

## Make copy to avoid changing original data (when imputing)
X_train_plus = X_train.copy()
X_valid_plus = X_valid.copy()

## Imputation
my_imputer = SimpleImputer()
imputed_X_train_plus = pd.DataFrame(my_imputer.fit_transform(X_train_plus))
imputed_X_valid_plus = pd.DataFrame(my_imputer.transform(X_valid_plus))

## Imputation removed column names; put them back
imputed_X_train_plus.columns = X_train_plus.columns
imputed_X_valid_plus.columns = X_valid_plus.columns

# OneHotEncoder

from sklearn.preprocessing import OneHotEncoder

## Apply one-hot encoder to each column with categorical data
OH_encoder = OneHotEncoder(handle_unknown='ignore', sparse=False)
OH_cols_train = pd.DataFrame(OH_encoder.fit_transform(X_train[object_cols]))
OH_cols_valid = pd.DataFrame(OH_encoder.transform(X_valid[object_cols]))

## One-hot encoding removed index; put it back
OH_cols_train.index = X_train.index
OH_cols_valid.index = X_valid.index

## Remove categorical columns (will replace with one-hot encoding)
num_X_train = X_train.drop(object_cols, axis=1)
num_X_valid = X_valid.drop(object_cols, axis=1)

## Add one-hot encoded columns to numerical features
OH_X_train = pd.concat([num_X_train, OH_cols_train], axis=1)
OH_X_valid = pd.concat([num_X_valid, OH_cols_valid], axis=1)

from sklearn.model_selection import cross_val_score


# Cross-validation 
## Multiply by -1 since sklearn calculates *negative* MAE
scores = -1 * cross_val_score(my_pipeline, X, y,
                              cv=5,
                              scoring='neg_mean_absolute_error')
                              
# Results Visualization

import matplotlib.pyplot as plt
%matplotlib inline

plt.plot(results.keys(), results.values())
plt.show()

# GridSearch
from sklearn.model_selection import GridSearchCV
