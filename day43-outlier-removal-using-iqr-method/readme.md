Outlier detection and removal using the **Interquartile Range (IQR)** method is a simple and effective technique to identify and remove extreme data points. Here's how it works:

### Steps for Outlier Detection and Removal using the IQR Method:

1. **Calculate Q1 and Q3:**
   - **Q1 (First Quartile)**: This is the 25th percentile of the data, meaning 25% of the data is below this value.
   - **Q3 (Third Quartile)**: This is the 75th percentile of the data, meaning 75% of the data is below this value.

2. **Compute the IQR:**
   - **IQR = Q3 - Q1**

3. **Determine the Outlier Range:**
   - Any data point that lies below **Q1 - 1.5 * IQR** or above **Q3 + 1.5 * IQR** is considered an outlier.
   - These thresholds are called the "lower bound" and "upper bound."

4. **Remove the Outliers:**
   - Filter out any values that fall outside of the lower and upper bounds.

### Python Example

Here's a Python implementation using the `IQR` method for outlier detection:

```python
import numpy as np
import pandas as pd

# Example data
data = [10, 12, 14, 18, 21, 24, 26, 29, 33, 35, 200]

# Convert to DataFrame
df = pd.DataFrame(data, columns=['values'])

# Step 1: Calculate Q1, Q3, and IQR
Q1 = df['values'].quantile(0.25)
Q3 = df['values'].quantile(0.75)
IQR = Q3 - Q1

# Step 2: Define the lower and upper bound for outliers
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

# Step 3: Filter out the outliers
filtered_data = df[(df['values'] >= lower_bound) & (df['values'] <= upper_bound)]

print("Original Data:", df['values'].tolist())
print("Filtered Data (Without Outliers):", filtered_data['values'].tolist())
```

### Breakdown of Code:
1. **Data Creation:** The example uses a small dataset with an obvious outlier (`200`).
2. **Quartiles Calculation:** We calculate the 25th percentile (Q1) and the 75th percentile (Q3).
3. **IQR Calculation:** IQR is simply the difference between Q3 and Q1.
4. **Outlier Boundaries:** Values below the lower bound and above the upper bound are classified as outliers.
5. **Data Filtering:** We filter the dataset by removing the outliers and print the result.

### Output:

```
Original Data: [10, 12, 14, 18, 21, 24, 26, 29, 33, 35, 200]
Filtered Data (Without Outliers): [10, 12, 14, 18, 21, 24, 26, 29, 33, 35]
```

### Notes:
- The `1.5 * IQR` threshold is commonly used, but you can adjust it based on how strict you want the outlier detection to be.
- This method works well for data that is symmetrically distributed and doesn't have too many extreme values.
