# Anomaly Detection Project

This project focuses on detecting anomalies in a dataset using multiple techniques, including **Moving Average**, **Z-score**, **Isolation Forest**, and **Local Outlier Factor (LOF)**. These methods are applied to identify outliers in different variables, with the goal of understanding how each technique behaves with different data characteristics and thresholds.

## Description

Anomaly detection is a critical task in identifying unusual patterns or behaviors in data. In this project, several techniques were implemented to detect anomalies in a time-series dataset. The methods vary in their sensitivity and ability to detect both global and local anomalies, making them useful for different scenarios.

### Techniques Used

- **Moving Average**: Smooths the data to detect short-term and long-term trends and fluctuations.
- **Z-score**: A statistical method used to detect outliers based on the number of standard deviations a point is from the mean.
- **Isolation Forest**: A machine learning model that isolates observations by randomly selecting a feature and splitting the data based on values.
- **Local Outlier Factor (LOF)**: A density-based method that detects anomalies by comparing the density of a point with the density of its neighbors.

### Key Findings

- **Moving Average**:
  - **7-day and 30-day Moving Averages** detected a large number of anomalies (803 and 688 respectively). These windows are more sensitive to short and medium-term fluctuations, detecting more anomalies with dynamically adjusted thresholds.
  - **90-day Moving Average**, however, detected fewer anomalies (369 in total), indicating that a longer period smooths out smaller fluctuations and focuses more on long-term trends.
  - In summary, 7-day and 30-day moving averages are suitable for detecting rapid changes but may generate more false positives, while the 90-day moving average is more stable and suitable for long-term analysis but may miss finer fluctuations.

- **Z-score**:
  - The Z-score method with a threshold of 3 standard deviations detected relatively few anomalies (39-111 across columns), indicating a stricter approach.
  - Voltage columns (VL1, VL2, VL3) showed moderate anomaly detection, suggesting some fluctuations are present but within an acceptable range.
  - While the Z-score is effective at identifying extreme outliers, it may not detect smaller, potentially relevant fluctuations in the data.

- **Isolation Forest**:
  - With a contamination rate of 0.5, Isolation Forest detected 882 anomalies across columns, suggesting that the model is very sensitive and tends to classify many points as anomalies.
  - With a contamination rate of 0.1, the number of detected anomalies dropped significantly (177), indicating more rigorous classification.
  - Isolation Forest's sensitivity to contamination was evident, with higher contamination rates leading to more anomalies detected. This method is useful for highlighting extreme points but depends on the contamination parameter.

- **Local Outlier Factor (LOF)**:
  - LOF detected 170 anomalies globally, which is moderate and similar to the Z-score method.
  - LOF's performance varied by column, with current (IL1, IL2, IL3) columns showing significantly more anomalies (1284-1950). This indicates that LOF identifies more outliers in columns with higher variability.
  - LOF excels in detecting local anomalies by comparing the density of a point to that of its neighbors, making it suitable for identifying outliers in denser distributions.

### Comparative Analysis

- **Sensitivity**:
  - Techniques like **7-day and 30-day Moving Averages** and **LOF** tend to detect more anomalies, particularly in the current columns, making them useful for detecting quick events or spikes but prone to false positives.
  - **Z-score** and **Isolation Forest** are more conservative, detecting anomalies only when there is a significant deviation, which makes them better suited for identifying exceptional anomalies but may miss smaller, relevant changes.

- **Local vs Global Detection**:
  - **LOF** is particularly sensitive to local anomalies and detects a high number of outliers in current columns. However, it may lead to an overload of detections for some datasets.
  - **Isolation Forest** and **Z-score** are more global and conservative, focusing on larger deviations and exceptions.

### General Conclusions

- **Moving Average** and **LOF** are more sensitive to short-term fluctuations and may generate more false positives, but are effective for detecting rapid changes and immediate anomalies.
- **Z-score** and **Isolation Forest** are stricter and filter out minor deviations, making them suitable for identifying exceptional anomalies but less sensitive to smaller fluctuations.
- The number of anomalies detected is highly dependent on parameters like the threshold in the Z-score or the contamination level in Isolation Forest. As these parameters change, the sensitivity of each technique increases or decreases, impacting the quantity and type of anomalies detected.

### Libraries Used

- **Pandas**: For data manipulation and analysis.
- **Matplotlib** and **Seaborn**: For visualization of anomalies and trends.
- **Scikit-learn**: For implementing machine learning models like Isolation Forest, LOF, and other preprocessing tasks.
- **NumPy**: For numerical computations and array handling.