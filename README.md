# 4G_5G_RSRP_Prediction
Predicting 4G and 5G signal strength (RSRP) using device and network measurements with a Random Forest model.

## Project Overview
This project predicts *4G and 5G signal strength (RSRP)* at a device using a combination of device measurements and network parameters. A *Random Forest Regressor* is trained on the dataset to model the relationship between location, network metrics, and signal level.

## Dataset
- *Source:* https://data.mendeley.com/datasets/dx5xyyfz2y/1
- *Features:* Device location, speed, altitude, network type, signal quality metrics, neighboring cell information, uplink/downlink throughput, bandwidth indicators.
- *Label:* Level (RSRP in dBm)
- *Size:* 30926
- *Missing values:* None

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
  - Scatter plot of actual vs predicted RSRP
  - Prediction error histogram
  - Feature importance bar chart

### Results
- MSE: your_value_here
- R²: your_value_here
- Mean prediction error: your_value_here
- Standard deviation of errors: your_value_here

### Feature Importance Table

| Feature            | Importance Score | Description                               |
|--------------------|------------------|-------------------------------------------|
| NRxLev1            | 0.327            | Neighbor cell signal strength             |
| SNR                | 0.144            | Signal-to-noise ratio                     |
| Qual               | 0.119            | Signal quality                             |
| Latitude           | 0.096            | Device latitude                            |
| Longitude          | 0.088            | Device longitude                           |
| SecondCell_RSRP    | 0.061            | Signal strength from second cell          |
| Altitude           | 0.030            | Device altitude                            |
| Speed              | 0.022            | Device speed                               |
| NetworkTech_4G     | 0.021            | Binary indicator for 4G network           |
| NetworkTech_5G     | 0.020            | Binary indicator for 5G network           |
| NQual1             | 0.017            | Neighbor cell quality metric               |
| SecondCell_SNR     | 0.016            | Signal-to-noise ratio from second cell    |
| CQI                | 0.013            | Channel quality indicator                  |
| UL_bitrate         | 0.006            | Uplink throughput                           |
| DL_bitrate         | 0.006            | Downlink throughput                         |

Note: Importance scores are derived from the trained Random Forest model.

## Insights
- Location (latitude & longitude) and neighboring cell signals strongly influence predicted RSRP.
- Network type (4G vs 5G) affects signal patterns and is captured by binary indicators.
- Device conditions like speed and altitude impact signal fluctuations.
- Channel quality (CQI) and SNR are critical for accurate signal prediction.

## Dependencies
- Python 3.x
- pandas
- numpy
- matplotlib
- scikit-learn
- tensorflow 
