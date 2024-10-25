Outlier detection using the **Percentile Method** and **Winsorization** is a robust technique to deal with extreme values by capping or adjusting them, rather than removing them. This approach is particularly useful when we want to maintain the overall data structure but limit the influence of outliers.

### 1. **Percentile Method:**
   This method works by defining outliers as values outside a specific percentile range, typically the 1st and 99th percentiles, or the 5th and 95th percentiles, depending on how extreme the outliers are.

### Steps for Outlier Detection using the Percentile Method:
1. **Set the Percentile Range:**
   - Decide on the percentile cutoffs (e.g., 1st and 99th, 5th and 95th).
   
2. **Calculate the Lower and Upper Bound:**
   - Use the chosen percentiles to define the lower and upper bounds.
   - Any data point below the lower percentile or above the upper percentile is considered an outlier.

3. **Optionally Remove the Outliers:**
   - You can either remove the outliers or cap them (Winsorization) to the boundary values.

### Python Example for the Percentile Method:

```python
import numpy as np
import pandas as pd

# Example data
data = [10, 12, 14, 18, 21, 24, 26, 29, 33, 35, 200]

# Convert to DataFrame
df = pd.DataFrame(data, columns=['values'])

# Step 1: Define the percentile range (e.g., 5th and 95th percentile)
lower_percentile = df['values'].quantile(0.05)
upper_percentile = df['values'].quantile(0.95)

# Step 2: Filter out the outliers
filtered_data = df[(df['values'] >= lower_percentile) & (df['values'] <= upper_percentile)]

print("Original Data:", df['values'].tolist())
print("Filtered Data (Without Outliers):", filtered_data['values'].tolist())
```

### Breakdown:
- **Percentile Calculation:** We compute the 5th and 95th percentiles.
- **Data Filtering:** We filter the data to remove values that fall outside these bounds.

### Output:

```
Original Data: [10, 12, 14, 18, 21, 24, 26, 29, 33, 35, 200]
Filtered Data (Without Outliers): [12, 14, 18, 21, 24, 26, 29, 33]
```

---

### 2. **Winsorization Technique:**
Winsorization is a technique where extreme values (outliers) are **replaced**, rather than removed, by the nearest non-outlier values based on chosen percentiles.

### Steps for Winsorization:
1. **Set the Percentile Range:**
   - Choose percentiles (e.g., 1st and 99th, 5th and 95th) to define the bounds for capping.

2. **Calculate the Lower and Upper Bound:**
   - Calculate the lower and upper bounds based on the chosen percentiles.

3. **Cap the Outliers:**
   - Replace values below the lower bound with the lower bound.
   - Replace values above the upper bound with the upper bound.

### Python Example for Winsorization:

```python
import numpy as np
import pandas as pd

# Example data
data = [10, 12, 14, 18, 21, 24, 26, 29, 33, 35, 200]

# Convert to DataFrame
df = pd.DataFrame(data, columns=['values'])

# Step 1: Define the percentile range (e.g., 5th and 95th percentile)
lower_percentile = df['values'].quantile(0.05)
upper_percentile = df['values'].quantile(0.95)

# Step 2: Winsorize the data by capping outliers to the percentile boundaries
df['winsorized_values'] = np.where(df['values'] < lower_percentile, lower_percentile, 
                                   np.where(df['values'] > upper_percentile, upper_percentile, df['values']))

print("Original Data:", df['values'].tolist())
print("Winsorized Data:", df['winsorized_values'].tolist())
```

### Breakdown:
- **Percentile Calculation:** The 5th and 95th percentiles are used as boundaries for capping.
- **Winsorization:** Any values below the 5th percentile are replaced with the 5th percentile value, and values above the 95th percentile are replaced with the 95th percentile value.

### Output:

```
Original Data: [10, 12, 14, 18, 21, 24, 26, 29, 33, 35, 200]
Winsorized Data: [12, 12, 14, 18, 21, 24, 26, 29, 33, 35, 35]
```

### Notes:
- **Percentile Method:** This method is more focused on identifying and removing extreme values.
- **Winsorization:** This is preferred when you want to limit the impact of outliers without removing data points, particularly in small datasets.
- **Choice of Percentiles:** The choice of percentiles (e.g., 1st and 99th, 5th and 95th) should depend on how many extreme values you expect in the data.