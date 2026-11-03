# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
###  Date: 03-11-2026 
### Name : S.Harika
### Reg no: 212224240155
### Dataset: Tesla stock price 
### S/w read : Colab

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

import pandas as pd

# Read just the header to inspect correct column names
temp_df = pd.read_csv("/content/tesla.csv.zip", nrows=1)
columns = list(temp_df.columns)

# Find a column that matches 'date' case-insensitively
date_col = next((col for col in columns if col.lower() == 'date'), None)

if date_col:
    data = pd.read_csv("/content/tesla.csv.zip",
                       parse_dates=[date_col],
                       index_col=date_col)
    print(f"Successfully loaded with date column: '{date_col}'")
    print(data.head())
else:
    print(f"Could not find a date column. Available columns are: {columns}")
    data = pd.read_csv("/content/tesla.csv.zip")
    print(data.head())
```

<img width="820" height="637" alt="image" src="https://github.com/user-attachments/assets/c68f6cc4-7f21-49c7-a7f7-d0f108ca9d65" />

```
close_prices = data['close'].dropna().values

N = len(close_prices)

print("Total data points:", N)
print("Closing Prices:", close_prices[:10])
```

<img width="872" height="72" alt="image" src="https://github.com/user-attachments/assets/25c3607b-638a-42a0-af88-7237ec995f0f" />

```
# Define lags
lags = range(55)

autocorr_values = []

# Calculate mean and variance
mean_data = np.mean(close_prices)
variance_data = np.var(close_prices)

print("Mean:", mean_data)
print("Variance:", variance_data)

# Calculate autocorrelation
for lag in lags:

    if lag == 0:
        autocorr_values.append(1)

    else:
        auto_cov = np.sum(
            (close_prices[:-lag] - mean_data) *
            (close_prices[lag:] - mean_data)
        ) / N

        autocorr_values.append(auto_cov / variance_data)

print("Autocorrelation Values:")
print(autocorr_values)
```

<img width="1746" height="111" alt="image" src="https://github.com/user-attachments/assets/68155519-2022-46ed-ab89-2b42f7f89382" />

```
plt.figure(figsize=(10, 6))

plt.stem(lags, autocorr_values)

plt.title('Autocorrelation of Tesla Close Prices')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')

plt.grid(True)
plt.show()
```

### OUTPUT:

<img width="1057" height="630" alt="image" src="https://github.com/user-attachments/assets/6071652f-a82a-4a43-830e-7362f1efbaa3" />


### RESULT:

Thus we have successfully implemented the auto correlation function in python.
