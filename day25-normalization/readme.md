
# Normalization and Scaling Techniques

In machine learning, **normalization** refers to adjusting the range of data so that different features contribute equally to the learning process. Different scaling techniques normalize data by transforming the values to a common range or distribution.

## 1. Min-Max Scaling:
Min-Max scaling transforms data to a specific range, often between 0 and 1. This is especially useful for algorithms that are sensitive to the scale of features, such as k-Nearest Neighbors (k-NN) or Support Vector Machines (SVM).

The formula for Min-Max scaling is:

![Min-Max Scaling Formula](Min-Max%20Scaling.png)

```
X_scaled = (X - X_min) / (X_max - X_min)
```

- `X` is the original value of the feature.
- `X_min` is the minimum value of the feature.
- `X_max` is the maximum value of the feature.

Min-Max scaling transforms the data so that all values fall within the range `[0,1]`.

## 2. Mean Normalization:
Mean normalization centers the data around zero. This method rescales the feature so the mean is zero and the values are between `-1` and `1`. It’s useful for features with varying ranges.

The formula for Mean Normalization is:

![Min-Max Scaling Formula](Mean%20Normalization.png)

```
X_normalized = (X - mean(X)) / (X_max - X_min)
```

- `mean(X)` is the mean of the feature.
- `X_max` and `X_min` are the maximum and minimum values of the feature.

## 3. MaxAbs Scaling:
MaxAbs scaling scales the data based on the maximum absolute value of each feature. This keeps the sign of the data and is often used when data contains both positive and negative values.

The formula for MaxAbs scaling is:

![Min-Max Scaling Formula](MaxAbs%20Scaling.png)

```
X_scaled = X / |X_max|
```

- `X_max` is the maximum absolute value of the feature.

MaxAbs scaling transforms data to the range `[-1, 1]`.

## 4. Robust Scaling:
Robust scaling is used when the data contains outliers. It scales the data based on the median and the interquartile range (IQR), making it less sensitive to extreme values.

The formula for Robust Scaling is:

![Min-Max Scaling Formula](Robust%20Scaling.png)

```
X_scaled = (X - median(X)) / IQR
```

- `median(X)` is the median of the feature values.
- `IQR` is the interquartile range (difference between the 75th and 25th percentiles).

## 5. Standardization (Z-Score Normalization):
Standardization (also known as Z-score normalization) rescales the data to have a mean of 0 and a standard deviation of 1. This is useful when the model assumes the data is normally distributed, such as in linear regression or logistic regression.

The formula for Standardization is:

![Min-Max Scaling Formula](Standardization.png)

```
X_standardized = (X - μ) / σ
```

- `μ` is the mean of the feature.
- `σ` is the standard deviation of the feature.

Standardization is useful for algorithms that rely on normally distributed data.

## 6. Normalization vs. Standardization:
- **Normalization** rescales the data to a fixed range, usually `[0, 1]`. It is used when you want all features to contribute equally to the model.
- **Standardization** rescales the data to have a mean of 0 and a standard deviation of 1, making it useful for algorithms that assume normally distributed features.
