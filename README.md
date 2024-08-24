### Name: KARTHIKEYAN R
### Register Number: 212222240046
### Date:
# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on Gold Price Data.
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
%matplotlib inline

train = pd.read_csv("/content/Gold Price.csv")


train['Date'] = pd.to_datetime(train['Date'], format='%Y-%m-%d')  
train.set_index('Date', inplace=True)  
train.head()

train['Price'].plot(title='Gold Price') 

def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)

adf_test(train['Price'])
```
### REGULAR DIFFERENCING:
```
train['Price_diff'] = train['Price'] - train['Price'].shift(1)
train['Price_diff'].dropna().plot(title='Differenced Gold Price')
```


### SEASONAL ADJUSTMENT:
```
n = 7 
train['Price_seasonal_diff'] = train['Price'] - train['Price'].shift(n) 
train['Price_seasonal_diff'].dropna().plot(title='Seasonally Differenced Gold Price')
```

### LOG TRANSFORMATION:
```
train['Price_log'] = np.log(train['Price'])


train['Price_log_diff'] = train['Price_log'] - train['Price_log'].shift(1)

train['Price_log_diff'].dropna().plot(title='Log Differenced Gold Price')
```
### OUTPUT:
![Untitled](https://github.com/user-attachments/assets/79a8bf69-c399-471e-b05a-cb5382759485)

### REGULAR DIFFERENCING:
![Untitled](https://github.com/user-attachments/assets/5066e3ae-471c-4e9b-a6a5-4deea0c96d93)


### SEASONAL ADJUSTMENT:
![Untitled](https://github.com/user-attachments/assets/3216bba1-03a4-4821-ac6d-6bc87d14f4ae)


### LOG TRANSFORMATION:

![Untitled](https://github.com/user-attachments/assets/36758b67-66f2-4f82-9441-991480ac6702)


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on Gold price.
