# Portfolio Assessment 2: Advanced Preprocessing & Model Development

Classifies NASA battery discharge cycles into state-of-health classes (`EOL` < 1.4 Ah, `Degraded` 1.4–1.6 Ah, `Healthy` ≥ 1.6 Ah) with decision trees and SVMs. Every split is by battery: 23 batteries for training and 5-fold grouped CV, 11 unseen batteries for testing.

The notebook lives in `asm_2/` but reads data from the repository root (`../output/`), so set up the environment at the root, then move into `asm_2/`. 

### 1. Clone and enter the repository

```bash
git clone https://github.com/MaiChiLe113/Exploratory-Data-Analysis-NASA-Battery.git
cd Exploratory-Data-Analysis-NASA-Battery
```

### 2. Create the virtual environment (repository root)

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install the packages

```bash
python -m pip install --upgrade pip
python -m pip install jupyterlab ipykernel numpy pandas matplotlib seaborn scipy scikit-learn
python -m ipykernel install --user --name nasa-battery --display-name "Python (nasa-battery)"
```

### 4. Check the input table

Assessment 2 reads `output/nasa_battery_eda_clean.csv` from the repository root:

```bash
ls output/nasa_battery_eda_clean.csv
```

If the file is missing, create it with the Assessment 1 notebook. Set `FORCE_REBUILD = True` in its loading cell, then Restart & Run All:

```bash
cd code
jupyter lab Portfolio_Assessment1_LeMaiChi.ipynb
cd ..
```

### 5. Navigate to `asm_2` and run the notebook

```bash
cd asm_2
jupyter nbconvert --to notebook --execute --inplace Portfolio_Assessment2_LeMaiChi.ipynb
```

Or open it interactively: `jupyter lab Portfolio_Assessment2_LeMaiChi.ipynb`, pick the **Python (nasa-battery)** kernel, then Restart & Run All. In VS Code, select the `.venv` interpreter instead.

The run takes about 2 minutes and uses a fixed seed (42). It rewrites `output/figures/` and `output/tables/` inside `asm_2/`. The stored outputs were last produced with Python 3.13.16 and scikit-learn 1.9.1 on Linux; an earlier run with Python 3.14.5 on macOS gave the same table values.
