# BlueitCase: Water Risk Forecasting with Remote Sensing and Machine Learning

This project evaluates long-term water risk levels in a selected geographic region (Izmir, Turkey) using satellite-based Earth observation data and machine learning techniques. It is developed as a case study solution for Blueit.

Objectives

Analyze climate and water-related parameters over time (2010-2025)

Estimate missing data using interpolation and random sampling

Label water risk levels (low, medium, high)

Train unsupervised and supervised models for classification

Visualize results to support decision-making

Data Sources

NASA POWER APIMonthly weather data (temperature, precipitation) is fetched using NASA POWER's REST API.

GRACE (Gravity Recovery and Climate Experiment)Groundwater storage estimates from NASA GRACE satellite data via Google Earth Engine (GEE).

SMAP (Soil Moisture Active Passive)Soil moisture data (10km resolution) is extracted from SMAP datasets through GEE.

MODIS (MOD16A2 Evapotranspiration)Monthly evapotranspiration values are simulated (randomly) due to API deprecation warning, but structure is in place for real data integration.

Steps and Methodology

1. Data Collection

Fetch NASA POWER data via REST API

Extract GRACE and SMAP values for a single point using Earth Engine Python API

2. Preprocessing

Merge all datasets on a monthly date index (2010-01 to 2025-07)

Fill missing values using random values within each column's observed min-max range

Resample and align all time series to monthly frequency

3. Unsupervised Risk Clustering (K-Means)

Selected features: soil moisture, evapotranspiration, groundwater, precipitation, temperature

Data is scaled using StandardScaler

KMeans clustering with k=3

Cluster centers are ranked based on domain logic:

Low moisture & groundwater + high evapotranspiration → high risk

Clusters are labeled as low, medium, or high

4. Supervised Classification (Random Forest)

Risk levels are labeled using quantile-based rule set

Random Forest classifier is trained on 80% of data

Classification accuracy is evaluated on the test set (20%)

Confusion matrix and classification report are generated

5. Visualization

Scatter Plot: Water risk level per month (color-coded)

Line Plot: Risk trend over time (with segment coloring)

Confusion Matrix: Evaluating classifier performance

Outputs

All results are saved under the /output folder:

1_nasa_power_data.csv

2_grace_groundwater.csv

3_modis_evapotranspiration.csv

4_smap_soil_moisture.csv

5_combined_climate_data.csv

6_final_with_risk.csv

Trained models and evaluation plots are displayed inline in notebook
To explore the project directly in your browser using Google Colab, use the link below:

🔗 https://colab.research.google.com/drive/1VeJkhrIZWZ--zQFduU-Yf3y84S-evx5S?usp=sharing

I’m sharing the Colab link so that you can view and run the Jupyter Notebook interactively online without any local setup.
