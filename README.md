# NASA Battery Exploratory Data Analysis

Data source: [NASA Battery Dataset, CSV distribution by Patrick Fleith](https://www.kaggle.com/datasets/patrickfleith/nasa-battery-dataset).

The [notebook](code/Portfolio_Assessment1_LeMaiChi.ipynb) summarizes discharge experiments and explores **`Capacity` (Ah)**. The dataset contains **7,565 experiments from 34 batteries**: 2,815 charge, 2,794 discharge and 1,956 impedance tests. Detailed findings and engineering discussion belong in the assessment report; see [domain notes](domain/domain.md) for essential terminology and references.

## Project files

 `dataset/metadata.csv`  Experiment index, test conditions and targets; `filename` links to sensor data. <br>
 `dataset/data/*.csv`  One file per experiment, containing sensor samples or impedance measurements. <br>
 `dataset/extra_infos/README_*.txt`  Original field definitions and protocols for the battery IDs in each filename. 
 <br>
 <br>
 `code/Portfolio_Assessment1_LeMaiChi.ipynb`  Data preparation, quality checks, EDA and engineering interpretation. <br>
 `domain/`  Short domain guide. <br>
 <br>
 `output/battery_discharge_features.csv`  Cached discharge features: **2,794 rows × 22 columns**. <br>
 `output/nasa_battery_eda_clean.csv`  Filtered analysis table: **2,750 rows × 23 columns**. <br>
 `output/figures/`  **12 PNG figures (Figures 3–14)**, numbered as in the notebook and report; Figures 1–2 are external diagrams used only in the report. <br>

## Run

From the repository root:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install jupyterlab numpy pandas matplotlib seaborn scipy
cd code
jupyter lab Portfolio_Assessment1_LeMaiChi.ipynb
```

Tested with Python 3.14.5 (macOS, arm64), numpy 2.5.3, pandas 3.0.6, matplotlib 3.11.2, seaborn 0.13.2. The notebook prints these in its environment cell. Set `FORCE_REBUILD = True` in the loading cell to rebuild the feature table from the raw CSVs, then Restart & Run All.

## Workflow and figures

Discharge sensor files → one feature row per experiment → retain non-missing `Capacity > 0` and `n_samples >= 5` → create capacity tertiles → export tables and figures. IQR outliers are flagged and retained.

The notebook displays all **15 selected predictors**, their summary statistics, the **top three signed Pearson correlations** ranked by absolute strength, and multicollinearity checks. Figures are:

| Numbers | Plots, in order |
| --- | --- |
| 3–5 | Missing-values heatmap; numerical-feature boxplots; IQR outlier percentages. |
| 6–9 | Capacity distribution; predictor distributions; correlation matrix; top-three-feature pairplot with `Capacity`. |
| 10–12 | Capacity versus discharge index; per-battery capacity trajectories; capacity by ambient temperature. |
| 13–14 | Samples per discharge experiment; discharge experiments per battery. |

## Essential columns

| Columns | Meaning |
| --- | --- |
| `type`, `start_time` | Operation and start date/time stored as `[year month day hour minute second]`. |
| `battery_id`, `test_id`, `uid`, `filename` | Cell ID, zero-based operation index within a cell, dataset-wide experiment ID and linked CSV filename. |
| `Capacity`, `ambient_temperature` | Discharge capacity (Ah) and test environment temperature (°C). |
| `Voltage_measured`, `Current_measured`, `Temperature_measured`, `Time` | Battery voltage (V), signed current (A), temperature (°C) and elapsed time (s). |
| `Current_charge`, `Voltage_charge`; `Current_load`, `Voltage_load` | Charger readings in charge files; load readings in discharge files (A, V). |
| `Sense_current`, `Battery_current`, `Current_ratio` | Impedance-test branch currents and their ratio. |
| `Battery_impedance`, `Rectified_Impedance`, `Re`, `Rct` | Raw/calibrated impedance and estimated electrolyte/charge-transfer resistance (Ω); unused in this EDA. |
| `n_samples`, `discharge_duration_s` | Sensor-row count and `max(Time) − min(Time)`; diagnostics outside the selected predictor set. |
| `mean_voltage`, `min_voltage`, `max_voltage`, `voltage_std` | Measured voltage summaries (V). |
| `voltage_drop` | First minus last valid voltage in time order (V). |
| `mean_abs_current`, `max_abs_current`, `current_std` | Absolute-current mean/maximum and signed-current standard deviation (A). |
| `mean_temperature`, `max_temperature`, `temperature_rise` | Battery temperature mean/maximum and maximum minus first valid temperature (°C). |
| `mean_abs_load_current`, `mean_load_voltage` | Mean absolute load current (A) and mean load voltage (V). |
| `discharge_index` | One-based discharge order per battery, assigned before filtering. |
| `capacity_class` | `Low`, `Medium`, `High` capacity tertiles; added only to the filtered table, not health thresholds. |