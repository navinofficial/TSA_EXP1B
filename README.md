# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 16/5/2026

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
### Name : Navinkumar V
### Reg no : 212223230141
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv("gold_rate_history.csv")
data.head()

if data.index.name == 'Date':
    data = data.reset_index()
data['Date'] = pd.to_datetime(data['Date'], format='mixed', dayfirst=False)
data.drop_duplicates(subset=['Date'], keep='first', inplace=True)
data.set_index('Date',inplace=True)

data['rate_diff'] = data['rate'] - data['rate'].shift(1)

result = seasonal_decompose(data['rate'], model='additive', period=12)
data['rate_sea_diff'] = result.resid

data['rate_log'] = np.log(data['rate'])
data['rate_log_diff'] = data['rate_log'] - data['rate_log'].shift(1)

result = seasonal_decompose(data['rate_log_diff'].dropna(),model='additive',period=12)
data['rate_log_seasonal_diff'] = result.resid

plt.figure(figsize=(16,16))
plt.subplot(6,1,1)
plt.plot(data['rate'],label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Date')
plt.ylabel('rate')

plt.subplot(6,1,2)
plt.plot(data['rate_diff'],label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Differenced Price')

plt.subplot(6,1,3)
plt.plot(data['rate_sea_diff'],label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Seasonally djusted Price')

plt.subplot(6,1,4)
plt.plot(data['rate_log'],label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transfermation')
plt.xlabel('Date')
plt.ylabel('Log(Price)')

plt.subplot(6,1,5)
plt.plot(data['rate_log_diff'],label='Log Transformation and Regular Differencing')
plt.title('Log Transfermation and Regular Differencing')
plt.xlabel('Date')
plt.ylabel('RDiff(Log(Price))')

plt.subplot(6,1,6)
plt.plot(data['rate_log_seasonal_diff'],label='Log Transformation and Regular Differencing and Seasonal Differencing')

plt.title('Log Transfermation and Regular Differencing and Seasonal Differencing')
plt.xlabel('Date')
plt.ylabel('SDiff(RDiff(Log(Price)))')

plt.tight_layout()
plt.show()
data.plot(kind='line')

```

### OUTPUT:
<img width="330" height="178" alt="image" src="https://github.com/user-attachments/assets/41e24cef-4c50-475c-8e2a-68485939be73" />
<img width="1104" height="231" alt="image" src="https://github.com/user-attachments/assets/25c1245f-f690-4e39-9e41-aa1a7b12340d" />

### REGULAR DIFFERENCING:
<img width="497" height="136" alt="image" src="https://github.com/user-attachments/assets/ddb091fb-62ed-48f1-bf0e-068b66f4c5a6" />


### SEASONAL ADJUSTMENT:
<img width="497" height="139" alt="image" src="https://github.com/user-attachments/assets/14f9219a-084f-4643-a919-e2ceea60def2" />


### LOG TRANSFORMATION:
<img width="461" height="130" alt="image" src="https://github.com/user-attachments/assets/4ec60f22-9d65-42ee-b586-796f0dd1f08c" />


<img width="481" height="118" alt="image" src="https://github.com/user-attachments/assets/b20b73af-2689-4617-8f08-1b27e192cb8d" />


<img width="519" height="118" alt="image" src="https://github.com/user-attachments/assets/41e953c1-80a0-4c44-9150-e0d1b8b6c694" />


<img width="461" height="326" alt="image" src="https://github.com/user-attachments/assets/5c6c7aa2-94a4-445b-9551-387ed4495e89" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
