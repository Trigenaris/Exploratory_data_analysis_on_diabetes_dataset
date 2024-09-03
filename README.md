<h1> 
  Exploratory Data Analysis on Diabetes Dataset
</h1>

## Business Problem

In this section, we will do an exploratory data analysis for the current diabetes dataset.

## Dataset Story

This dataset is originally from the National Institute of Diabetes and Digestive and Kidney Diseases. The objective of the dataset is to diagnostically predict whether a patient has diabetes, based on certain diagnostic measurements included in the dataset. Several constraints were placed on the selection of these instances from a larger database. In particular, all patients here are females at least 21 years old of Pima Indian heritage.2 From the data set in the (.csv) File We can find several variables, some of them are independent (several medical predictor variables) and only one target dependent variable (Outcome).

## Dataset Features

* **Pregnancies**: To express the Number of pregnancies
* **Glucose**: To express the Glucose level in blood
* **BloodPressure**: To express the Blood pressure measurement
* **SkinThickness**: To express the thickness of the skin
* **Insulin**: To express the Insulin level in the blood
* **BMI**: To express the Body mass index
* **DiabetesPedigreeFunction**: To express the Diabetes percentage
* **Age**: To express the age
* **Outcome**: To express the final result 1 is Yes and 0 is No

## Necessary Libraries

Required libraries and some settings for this section are:

```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

pd.set_option("display.max_columns", None)
pd.set_option("display.max_rows", None)
pd.set_option("display.width", 500)
pd.set_option("display.float_format", lambda x: "%.4f" % x)

```

## Importing the Dataset

First, we import the dataset `diabetes.csv` into the pandas DataFrame.

## General Information About the Dataset

### Checking the Data Frame

As we want to check the data to have a general opinion about it, we create and use a function called `check_df(dataframe, head=5, tail=5)` that prints the referred functions:


    dataframe.head(head)
    
    dataframe.tail(tail)
    
    dataframe.shape
    
    dataframe.dtypes
    
    dataframe.size
    
    dataframe.isnull().sum()
    
    dataframe.describe([0, 0.01, 0.05, 0.10, 0.20, 0.30, 0.40, 0.50, 0.60, 0.70, 0.80, 0.90, 0.95, 0.99, 1]).T

### Defining the Columns

After checking the data frame, we need to define and separate columns as **categorical** and **numerical**. We define a function called `grab_col_names` for separation that benefits from multiple list comprehensions as follows:

    cat_cols = [col for col in dataframe.columns if str(dataframe[col].dtypes) in ['category', 'object', 'bool']]
    num_but_cat = [col for col in dataframe.columns if dataframe[col].nunique() < cat_th and dataframe[col].dtypes in ['uint8', 'int64', 'int32', 'float64']]
    cat_but_car = [col for col in df.columns if df[col].nunique() > car_th and str(df[col].dtypes) in ['object', 'category']]
    cat_cols = cat_cols + num_but_cat
    num_cols = [col for col in dataframe.columns if dataframe[col].dtypes in ['uint8', 'int64', 'float64']]
    num_cols = [col for col in num_cols if col not in cat_cols]

`cat_th` and `car_th` are the threshold parameters to decide the column type.

**Categorical Columns:**

* Outcome

**Numerical Columns:**

* Pregnancies
* Glucose
* Blood Pressure
* Skin Thickness
* Insulin
* BMI
* Diabetes Pedigree Function
* Age

### Summarization and Visualization of the Categorical and Numerical Columns

To summarize and visualize the referred column we create two other functions called `cat_summary` and `num_summary`.

For example, the categorical column **Outcome**:

############### Outcome ###############

Outcome | Outcome Nr | Ratio |
--------|------------|-------|
0       |    500  |  65.1042 |
1       |    268  |  34.8958 |

![__results___12_1](https://github.com/user-attachments/assets/19e5f312-30d1-4f92-b749-80749a624ad6)

Another example is, the numerical column **Pregnancies**:

############### Pregnancies ###############

Process | Result |
--------|--------|
count |  768.0000 |
mean   |   3.8451 |
std    |   3.3696 |
min    |   0.0000 |
1%     |   0.0000 |
5%     |   0.0000 |
10%    |   0.0000 |
20%    |   1.0000 |
30%    |   1.0000 |
40%    |   2.0000 |
50%    |   3.0000 |
60%    |   4.0000 |
70%   |    5.0000 |
80%   |    7.0000 |
90%   |    9.0000 |
95%   |   10.0000 |
99%   |   13.0000 |
max   |   17.0000 |

Name: Pregnancies, dtype: float64

![__results___15_1](https://github.com/user-attachments/assets/dd9185ed-e642-4b06-bc6e-b43f8f09003e)

With the help of a for loop we apply these functions to all columns in the data frame.

We create another plot function called `plot_num_summary(dataframe)` to see the whole summary of numerical columns due to the high quantity of them:

![__results___17_0](https://github.com/user-attachments/assets/882270c6-a38a-4c17-a104-f6a59a22b187)

## Target Analysis

We create another function called `target_summary_with_num(dataframe, target, numerical_col)` to examine the target by numerical features.

For instance *Glucose Feature*

################ Outcome --> Glucose #################

Outcome | Glucose |
--------|---------|
0   |    109.9800 |
1   |    141.2575 |

## Correlation Analysis

To analyze correlations between numerical columns we create a function called `high_correlated_cols(dataframe)`:

![__results___27_1](https://github.com/user-attachments/assets/ec4316aa-c0a7-4f47-b60e-366300c03444)

