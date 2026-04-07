# VTEC Trend Analysis — South African GNSS Stations

MSc-level project analysing Total Electron Content (TEC) trends at three South African GNSS stations using multiple solar and geomagnetic proxies.

---

## Stations
| Code | Location | Lat | Lon |
|------|----------|-----|-----|
| HRAO | Hartebeesthoek | -25.9° | 27.7° |
| SUTH | Sutherland | -32.4° | 20.8° |
| HERM | Hermanus | -34.4° | 19.2° |

---

## Data
- **VTEC**: 30-second interval data from IonolabTEC, filtered to 10:00–14:00 UTC (local noon), 2000–2023
- **F10.7**: Monthly solar radio flux index
- **MgII**: Core-to-wing UV solar proxy
- **Dst / Ap**: Hourly geomagnetic indices, averaged monthly
- **CO₂**: Monthly atmospheric concentration (Mauna Loa)
- Missing VTEC values filled via cubic spline interpolation (order 3)

---

## How to Run

1. Place raw data files in the expected paths (see top of each script)
2. Run scripts in this order:
   - Load and preprocess GNSS station data
   - Load and merge solar/geomagnetic drivers
   - Run OLS regression model (`tec_multiproxy.py`)
   - Run seasonal decomposition
3. Outputs (plots + CSVs) are saved to the working directory

**Dependencies**: `pandas`, `numpy`, `matplotlib`, `statsmodels`, `scikit-learn`, `pymsis`, `seaborn`

---

## Methods (brief)
- Noon-time VTEC averaged monthly and yearly per station
- Predictors standardised (z-score) before regression
- OLS regression fitted separately per station
- Multiplicative seasonal decomposition applied (period = 12 months)
- VIF computed to check multicollinearity

---

## Key Results
- Model captures the solar cycle signal well at both monthly and yearly resolution
- Yearly fit is tighter than monthly — predictors explain inter-annual variance well
- Seasonal multiplier ranges ~0.80–1.16 consistently across all three stations
- Residuals show unexplained structure during 2009–2013 (Solar Cycle 24 ascending phase) — worth investigating further
- Model underestimates peak VTEC at solar maximum, particularly at SUTH

---

## Notes
- Study period limited to 2000–2016 by driver data availability
- Ionospheric shell altitude fixed at 428.8 km (IonolabTEC convention)
- All times in UTC
