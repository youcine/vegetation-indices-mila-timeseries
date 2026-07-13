# Vegetation Indices Time-Series Analysis; Mila Province, Algeria

Monitoring vegetation dynamics in Mila Province, Algeria, using Sentinel-2
imagery (2022–2024): computing NDVI, EVI, and SAVI, building their time
series, quantifying the multi-year trend, and detecting land-use /
vegetation change between 2022 and 2024.

## Data & Tools

- **Imagery:** Sentinel-2 (`COPERNICUS/S2`), scenes with `CLOUDY_PIXEL_PERCENTAGE < 10`
- **Platform:** Google Earth Engine + `geemap`
- **Analysis:** Python — `pandas`, `numpy`, `matplotlib`, `scikit-learn`

## Workflow

1. Load and prepare Sentinel-2 imagery for the study area (Mila Province)
2. Compute NDVI, EVI, and SAVI for every image
3. Extract mean time-series statistics directly from Earth Engine (server-side, no local export)
4. Visualize the combined time series and compute descriptive statistics
5. Fit a simple trend + seasonality regression to quantify long-term change
6. Detect land-use / vegetation change (2022 vs 2024) via a delta-NDVI map
7. Summarize findings in the Conclusions section

## Key Results

- NDVI averaged ~0.13, EVI ~0.17, SAVI ~0.11 over 2022–2024 consistent with
  a semi-arid landscape of sparse/seasonal vegetation over bare soil.
- All three indices show a clear, repeating annual cycle (spring peak,
  summer decline, winter recovery).
- A trend + seasonality regression on NDVI found an estimated trend of
  **-0.00101 per year** (R² = 0.504) statistically negligible relative to
  NDVI's own variability, indicating **no meaningful multi-year greening or
  degradation** over the study period.
- The 2022→2024 delta-NDVI map shows no significant land-use change within
  the province boundary, consistent with the near-zero trend.

## Limitations

- All statistics are a single province-wide spatial average per date; no
  sub-regional breakdown was performed.
- Cloud filtering is scene-level (`CLOUDY_PIXEL_PERCENTAGE`), not per-pixel,
  so some residual cloud/shadow noise remains in the time series;
  per-pixel cloud masking (e.g. s2cloudless) is a natural next step.
- No independent ground-truth or rainfall/temperature data was used to
  validate the vegetation trend.

## How to Run

1. Open `Vegetation_Indices_Time-Series_Analysis.ipynb` in Google Colab or Jupyter.
2. Run the authentication cell (`ee.Authenticate()`) and set your own Earth
   Engine project ID in `ee.Initialize(project="...")`.
3. Run the remaining cells in order.

## Credit

This project's approach was inspired by
[vikas-geotech/Time-series-Analysis-Sentinel-2](https://github.com/vikas-geotech/Time-series-Analysis-Sentinel-2)
(NDVI and EVI time-series analysis using Sentinel-2 data). This repository
extends that idea with a different study area (Mila Province, Algeria), an
added SAVI index, a corrected/validated index computation, a trend +
seasonality regression, and land-use change detection.

## Author

Aya Belaidi
