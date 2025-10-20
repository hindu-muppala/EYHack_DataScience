
# EYHack Urban Heat Island (UHI) Data Science Model

This notebook demonstrates how to analyze and model the Urban Heat Island (UHI) effect using geospatial and remote sensing data, combining Landsat and Sentinel data sources, and advanced regression techniques.

## Overview

- **Goal**: Predict UHI index using remote sensing bands, geospatial indices, and environmental data for New York.
- **Process**: Data cleaning, feature engineering, geospatial data extraction, regression modeling, and visualization.

## 1. Data Preparation

- **Input**: `train_df2.csv` containing:
  - `Longitude, Latitude, datetime, UHI Index, NVDI_Index, Band_11`
- Removes duplicates for clean processing.

## 2. Feature Engineering

- Calculates environmental indices:
  - **LST**: Land Surface Temperature (Band 10)
  - **NDVI**: (Band 5 - Band 4)/(Band 5 + Band 4)
  - **NDBI, BUI, UI**: Various indices from band combinations

## 3. Geospatial Data Extraction

- Uses Xarray, rioxarray, rasterio, stackstac, pystac_client, and Microsoft Planetary Computer for:
  - Extracting and matching geospatial band values (`swir16`, `swir22`, `coastal`, `drad`, `emis`, `emsd`, `trad`) for each point.
- **Mapping**: High-res plotting of UHI index on spatial map

## 4. Weather Data Integration

- Loads additional weather features from `NY_Mesonet_Weather.xlsx` .

## 5. Model Training and Testing

- **Train/Test Split**: 70:30 random split
- Trains **XGBoost regressor** to predict UHI Index. Evaluates with RMSE and R².
- Example metrics: RMSE ≈ 0.006, R² ≈ 0.85

## 6. Reproducibility

- Random sampling for visualizations is used for reproducibility (`numpy.random.choice`).

## 7. Visualization

- Plots UHI index against coordinates using matplotlib.
- Visualizes remote sensing band data for inspection and quality check.

## 8. Utilities

- Scripts add band values to dataset by geospatial matching.
- Includes routines for handling duplicates and missing values.

## Requirements

- Python (>=3.7)
- pandas, numpy, matplotlib, seaborn
- scikit-learn, xgboost
- rioxarray, rasterio, stackstac, pystac_client, planetary_computer, osmnx, netCDF4
- Jupyter Notebook or Colab

Install major dependencies using:
```bash
pip install -r requirements.txt
# or, as seen in the notebook:
pip install rioxarray stackstac pystac_client planetary_computer pyodc osmnx odc-stac netCDF4
```

## How to Run

1. Prepare input files: `train_df2.csv`, relevant `.tiff` or NetCDF band files, and (optionally) `NY_Mesonet_Weather.xlsx`.
2. Open the notebook in Jupyter or Google Colab.
3. Execute cells sequentially.
4. Inspect the model evaluation metrics and plots.

## Notes

- Remote sensing features depend on having data access via specified coordinate bounds and API.
- Adjust file paths for your environment if not using Colab.

***

**References**
- Microsoft Planetary Computer API
- scikit-learn, XGBoost documentation

***
