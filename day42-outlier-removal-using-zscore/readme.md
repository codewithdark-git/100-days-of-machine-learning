Outlier detection and removal using the **Z-score** method is another widely-used technique, especially effective for data that is normally distributed. The Z-score measures how many standard deviations a data point is from the mean.

### Steps for Outlier Detection and Removal using the Z-Score Method:

1. **Calculate the Mean and Standard Deviation:**
   - Compute the **mean (μ)** and **standard deviation (σ)** of the data.

2. **Calculate the Z-score for Each Data Point:**
   - For each data point `x`, the Z-score is calculated as:
     \[
     Z = \frac{x - \mu}{\sigma}
     \]
   - A Z-score tells us how many standard deviations a point is away from the mean.

3. **Define a Threshold:**
   - A common threshold is **Z > 3** or **Z < -3**, meaning any data point with a Z-score greater than 3 or less than -3 is considered an outlier.
   - You can adjust the threshold based on your data.

4. **Remove the Outliers:**
   - Filter out any data points with Z-scores that exceed the threshold.

### Python Example

Here's a Python implementation using the Z-score method for outlier detection:

```python
import numpy as np
import pandas as pd
from scipy import stats

# Example data
data = [10, 12, 14, 18, 21, 24, 26, 29, 33, 35, 200]

# Convert to DataFrame
df = pd.DataFrame(data, columns=['values'])

# Step 1: Calculate the Z-scores
df['z_score'] = stats.zscore(df['values'])

# Step 2: Define a threshold for outliers (commonly Z > 3 or Z < -3)
threshold = 3

# Step 3: Filter out the outliers
filtered_data = df[np.abs(df['z_score']) < threshold]

print("Original Data:", df['values'].tolist())
print("Filtered Data (Without Outliers):", filtered_data['values'].tolist())
```

### Breakdown of Code:
1. **Data Creation:** A small dataset with an outlier (`200`).
2. **Z-score Calculation:** Using `scipy.stats.zscore()` to compute Z-scores for each value in the dataset.
3. **Threshold Definition:** We define `Z > 3` or `Z < -3` as outliers.
4. **Data Filtering:** Data points with a Z-score within the threshold are kept, and others (outliers) are removed.

### Output:

```
Original Data: [10, 12, 14, 18, 21, 24, 26, 29, 33, 35, 200]
Filtered Data (Without Outliers): [10, 12, 14, 18, 21, 24, 26, 29, 33, 35]
```

### Notes:
- **Z-score Interpretation:** A Z-score of 0 means the data point is exactly at the mean. A Z-score of 1 means it's one standard deviation away from the mean, and so on.
- **Threshold Adjustment:** The threshold of 3 standard deviations is common, but for more lenient outlier detection, you can lower it (e.g., Z > 2 or Z > 2.5).
- **Assumptions:** The Z-score method works best when your data is approximately normally distributed. If your data has a skewed distribution, this method might not be as effective.

This method is particularly useful when you want a statistical-based approach to detect outliers.