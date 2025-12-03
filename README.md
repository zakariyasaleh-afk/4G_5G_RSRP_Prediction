# 4G_5G_RSRP_Prediction
Predicting 4G and 5G signal strength (RSRP) using device and network measurements with a Random Forest model.

## Project Overview
This project predicts *4G and 5G signal strength (RSRP)* at a device using a combination of device measurements and network parameters. A *Random Forest Regressor* is trained on the dataset to model the relationship between location, network metrics, and signal level.

## Dataset
- *Source:* https://data.mendeley.com/datasets/dx5xyyfz2y/1
- This dataset contains 30,925 labelled and cleaned records collected from a dense 2 km² urban area surrounding Sunway University, Selangor, Malaysia and captures radio signal quality      metrics (RSRP, RSRQ, SNR, etc.)
- *Features:* Device location, speed, altitude, network type, signal quality metrics, neighboring cell information, uplink/downlink throughput, bandwidth indicators.
- *Label:* Level (RSRP in dBm)
- *Size:* 30925 labelled and cleaned records

### Data Preprocessing
- Categorical features (Operatorname, NetworkTech) are one-hot encoded.
- Dataset is split into training (80%) and testing (20%) sets.
- Features considered include:

Longitude, Latitude, Altitude, Speed, Operatorname, NetworkTech, Qual, SNR, CQI, DL_bitrate, UL_bitrate, BANDWIDTH, SecondCell_RSRP, SecondCell_SNR, NRxLev1, NQual1, LAC

### Model Training
- *Random Forest Regressor* with:
  - n_estimators=100
  - random_state=42
- Trains on all device and network features to predict RSRP.
- Handles non-linear relationships and interactions between features.

### Evaluation
- Metrics:
  - *Mean Squared Error (MSE)*
  - *Coefficient of Determination (R²)*
- Visualizations:
  - Scatter plot of actual vs predicted RSRP:
    
     <img width="583" height="450" alt="Screenshot 2025-12-01 013243" src="https://github.com/user-attachments/assets/a89551e1-ee75-45fc-b657-5b230e3372f8" />

  - Prediction error histogram
  - Feature importance bar chart

### Results
- MSE: 12.246
- R²: 0.899
- Mean prediction error: 0.023
- Standard deviation of errors: 3.499

### Feature Importance Table

| Feature               | Description                                          | Importance Score|
|-----------------------|------------------------------------------------------|-----------------|
| NRxLev1               | Signal strength received from the neighboring cell   | 0.327           |
| SNR                   | Signal-to-noise ratio of the connection              | 0.144           |
| Qual                  | Signal quality metric reported by the device         | 0.119           |
| Latitude              | Device latitude coordinate                           | 0.096           |
| Longitude             | Device longitude coordinate                          | 0.088           |
| SecondCell_RSRP       | Signal strength received from a secondary cell       | 0.061           |
| Altitude              | Device altitude above ground                         | 0.030           |
| Speed                 | Device movement speed                                | 0.022           |
| NetworkTech_4G        | Indicates if the device is connected to a 4G network | 0.021           |
| NetworkTech_5G        | Indicates if the device is connected to a 5G network | 0.020           |
| NQual1                | Quality metric of the neighboring cell               | 0.017           |
| SecondCell_SNR        | Signal-to-noise ratio from the second cell           | 0.016           |
| CQI                   | Channel Quality Indicator reported by the device     | 0.013           |
| UL_bitrate            | Uplink throughput in the connection                  | 0.006           |
| DL_bitrate            | Downlink throughput in the connection                | 0.006           |


Note: Importance scores are derived from the trained Random Forest model.

## Insights
-NRxLev1, SNR, and Qual dominate the feature importance, meaning neighbor cell signal strength and signal quality metrics are most critical for predicting RSRP.
-Location features (Latitude, Longitude, Altitude) also contribute, showing spatial influence on signal levels.
-Network technology indicators (4G/5G) have moderate importance, reflecting differences in signal characteristics across technologies.
-UL/DL bitrate are less important, showing that throughput alone is not a strong predictor of RSRP.

## Dependencies
- Python 3.x
- pandas
- numpy
- matplotlib
- scikit-learn
