# Ex.No: 1 B                    CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 07/03/2025
# Name : SUDHAKAR K
## AIM:
To perform regular differncing,seasonal adjustment and log transformatio on settle weather data

## ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
   
## PROGRAM:
### Importing the necessary Packages:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller, kpss
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
```

### Loading the dataset:
```
data = pd.read_csv('/content/seattle_weather_1948-2017.csv', parse_dates=['DATE'], index_col='DATE')
```

### Plot the data without Conversion:
```
def test_stationarity(series):
result = adfuller(series.dropna())
print('ADF Statistic:', result[0])
print('p-value:', result[1])
print('Critical Values:', result[4])
print('')
test_stationarity(data['PRCP'])
plt.figure(figsize=(10, 6))
plt.plot(data['PRCP'], label='PRCP')
plt.title('Precipitation Over Time')
plt.xlabel('Date')
plt.ylabel('Precipitation')
plt.legend()
plt.show()

```

### REGULAR DIFFERENCING
```
data['PRCP_diff'] = data['PRCP'] - data['PRCP'].shift(1)
data_diff = data.dropna()
test_stationarity(data_diff['PRCP_diff'])
plt.figure(figsize=(10, 6))
plt.plot(data_diff['PRCP_diff'], label='Differenced PRCP')
plt.title('Differenced Precipitation Over Time')
plt.xlabel('Date')
plt.ylabel('Differenced Precipitation')
plt.legend()
plt.show()
```

### SEASONAL ADJUSTMENT
```
plt.figure(figsize=(12, 6))
plt.subplot(121)
plot_acf(data_diff['PRCP_diff'], ax=plt.gca(), lags=40)
plt.title('ACF of Differenced PRCP')
```

### LOG TRANSFORMATION
```

plt.subplot(122)
plot_pacf(data_diff['PRCP_diff'], ax=plt.gca(), lags=40)
plt.title('PACF of Differenced PRCP')
plt.tight_layout()
plt.show()
```

## OUTPUT:
### WITHOUT CONVERSION:

![image](https://github.com/user-attachments/assets/b1b46bbf-4c81-4fcb-a5cc-5a748c0f6780)



### REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/d801d8b3-242a-4925-81fb-1a675118763e)



### SEASONAL ADJUSTMENT:

![image](https://github.com/user-attachments/assets/52065c38-e4bd-4a00-8fa6-55fe23da3084)



### LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/e08653cf-7425-4895-aefd-720513aee8c3)




### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on settle weather
data.
