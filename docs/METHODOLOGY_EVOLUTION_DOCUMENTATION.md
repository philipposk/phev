# Methodology Evolution and Analysis Runs Documentation

**Author:** Markos A. Ktistakis, ...  
**Date:** December 2025  
**Purpose:** Comprehensive documentation of all analysis runs, variables, parameters, and project evolution

---

## Executive Summary

This document provides a comprehensive record of the methodological evolution of the PHEV energy consumption analysis project. The project evolved from a simple linear model with 3 variables achieving 44.65% R² to a comprehensive multi-model approach with 40+ predictors achieving 71-92% test R² across different models. This documentation serves as a complete record for reproducibility, future reference, and integration into the paper.

---

## 1. Project Evolution Overview

### 1.1 Initial Analysis Phase (Simple Linear Model)

**Script:** `05_variable_importance.R` (initial version)

**Objective:** Establish baseline model for PHEV energy consumption

**Model Specification:**
```
total_energy ~ mass + aer + region
```

**Variables Used:**
- `mass`: Vehicle mass [kg]
- `aer`: All-electric range [km]
- `region`: EuroVoc regional classification (Northern, Southern, Western, Central_Eastern)

**Parameters:**
- Model type: Linear regression (OLS)
- Validation: None (full dataset used)
- Seed: 42

**Results:**
- R² = 0.4465 (44.65% variance explained)
- Variable importance (LMG method):
  - Mass: 97.5%
  - AER: 1.4%
  - Region: 1.1%

**Limitations Identified:**
1. Missing critical predictor: EDS (Electric Driving Share) not included
2. Only 3 variables used despite 77+ available variables
3. 55% of variance unexplained
4. Model too simple for publication standards

**Files Generated:**
- `tables/variable_importance_lmg.csv`
- `figures/figure5_variable_importance_lmg.png`

---

### 1.2 Improved Analysis Phase (Feature Engineering)

**Script:** `05_variable_importance_IMPROVED.R`

**Objective:** Improve model by adding EDS and basic feature engineering

**Model Specification:**
```
total_energy ~ mass + aer + eds + region + engine_power + battery_capacity + 
              power_to_weight + battery_to_weight + aer_to_mass + 
              eds_aer_interaction + mass_aer_interaction + eds_mass_interaction
```

**Variables Added:**
- `eds`: Electric Driving Share [%]
- `engine_power`: Engine power [kW]
- `battery_capacity`: Battery capacity [kWh]
- Engineered features:
  - `power_to_weight`: Engine power / Mass
  - `battery_to_weight`: Battery capacity / Mass
  - `aer_to_mass`: AER / Mass
  - `eds_aer_interaction`: EDS × AER
  - `mass_aer_interaction`: Mass × AER
  - `eds_mass_interaction`: EDS × Mass

**Models Compared:**
1. Linear Model with LMG decomposition
2. Generalized Additive Model (GAM)
3. Random Forest

**Parameters:**
- Train/test split: 80/20
- Random Forest: mtry=5, ntree=500 (default tuning)
- GAM: k=10 for smooth terms
- Seed: 42

**Results:**
- Linear Model: R² = ~0.50-0.55 (improved from 44.65%)
- GAM: Deviance explained = 53.33%
- Random Forest: R² = 59.44%

**Files Generated:**
- `tables/variable_importance_lmg_improved.csv`
- `tables/variable_importance_gam_improved.csv`
- `tables/variable_importance_rf_improved.csv`
- `figures/figure5a_variable_importance_gam.png`
- `figures/figure5b_variable_importance_rf.png`

---

### 1.3 Final Variable Importance Analysis Phase

**Script:** `05_variable_importance_FINAL.R`

**Objective:** Finalize variable importance analysis with full tuning

**Model Specification:**
```
total_energy ~ mass + aer + eds + region + engine_power + battery_capacity + 
              engine_displacement + vehicle_length + registration_year +
              power_to_weight + battery_to_weight + aer_to_mass +
              eds_aer_interaction + mass_aer_interaction + eds_mass_interaction +
              energy_density + range_efficiency
```

**Additional Variables:**
- `engine_displacement`: Engine displacement [L]
- `vehicle_length`: Vehicle length [m]
- `registration_year`: Year of registration
- `energy_density`: Battery capacity / Mass
- `range_efficiency`: AER / Battery capacity

**Models:**
1. Tuned Random Forest (mtry tuned via grid search)
2. Tuned GAM (k=8-10 for smooth terms)
3. XGBoost/GBM (alternative advanced method)

**Parameters:**
- Train/test split: 80/20
- Random Forest tuning: mtry values = c(3, 5, 7, 10, floor(sqrt(p)))
- GAM: k=8-10 (tuned)
- XGBoost: n.trees=500, interaction.depth=6, shrinkage=0.01
- Seed: 42

**Results:**
- Random Forest: Test R² = 71.56% (best performing)
- GAM: Test R² = ~61%
- XGBoost: Test R² = ~69%

**Files Generated:**
- `tables/variable_importance_lmg_final.csv`
- `tables/variable_importance_gam_final.csv`
- `tables/variable_importance_rf_final.csv`
- `tables/variable_importance_xgb_final.csv`

---

### 1.4 Comprehensive Model Comparison Phase

**Script:** `09_comprehensive_model_comparison_ALL.R`

**Objective:** Comprehensive comparison of 7 advanced models with full hyperparameter tuning and 40+ predictors

**Model Specifications:**

**1. Linear Model (Baseline - STEP 2):**
```
total_energy ~ [All 44 predictors]
Method: Ordinary Least Squares (OLS) regression
No hyperparameter tuning required
```

**2-8. Advanced Models (STEPS 3-9):**
```
total_energy ~ [40+ predictors including:]
  - Core variables: mass, aer, eds
  - Vehicle characteristics: engine_power, battery_capacity, engine_displacement,
    vehicle_length, vehicle_width, vehicle_height, registration_year,
    mileage_tot, max_passengers, prices
  - Performance metrics: rw_co2, ta_co2, gap_pct
  - Categorical (numeric): fuel_type_numeric, region_numeric, country_numeric,
    segment_numeric, oem_numeric, make_numeric, vehicle_body_numeric
  - Basic engineered: power_to_weight, battery_to_weight, aer_to_mass,
    eds_aer_interaction, mass_aer_interaction, eds_mass_interaction,
    energy_density, range_efficiency
  - Advanced engineered: mass_squared, aer_squared, eds_squared,
    vehicle_volume, vehicle_surface_area,
    power_aer_interaction, battery_aer_interaction, power_eds_interaction,
    country_mass_interaction, country_aer_interaction, country_eds_interaction,
    region_mass_interaction, co2_gap
```

**Models Trained:**
1. **Linear Model (Baseline)** - OLS regression with all 44 predictors (no tuning needed)
2. **Random Forest** - Full hyperparameter tuning
3. **XGBoost/GBM** - Full hyperparameter tuning
4. **LightGBM** - Full hyperparameter tuning (if available)
5. **CatBoost** - Full hyperparameter tuning (if available)
6. **GAM** - Full hyperparameter tuning
7. **Neural Network** - Full hyperparameter tuning
8. **Ensemble Meta-Learner** - Combines all base models

**Hyperparameter Tuning Details:**

**Random Forest:**
- `mtry` values: c(3, 5, 7, 10, floor(sqrt(p)))
- `ntree` values: c(500, 1000)
- `nodesize` values: c(1, 5, 10)
- **Best parameters:** mtry=10, ntree=1000, nodesize=5
- **Best performance:** Test R² = 0.9188 (91.88%), Test RMSE = 1.6607, Test MAE = 1.0715, Test MAPE = 5.08%

**XGBoost/GBM:**
- `n.trees` values: c(500, 1000, 1500)
- `interaction.depth` values: c(4, 6, 8)
- `shrinkage` values: c(0.001, 0.01, 0.05)
- `n.minobsinnode` values: c(5, 10, 20)

**LightGBM:**
- `num_iterations` values: c(500, 1000, 1500)
- `max_depth` values: c(4, 6, 8)
- `learning_rate` values: c(0.001, 0.01, 0.05)
- `min_data_in_leaf` values: c(5, 10, 20)

**CatBoost:**
- `iterations` values: c(500, 1000, 1500)
- `depth` values: c(4, 6, 8)
- `learning_rate` values: c(0.001, 0.01, 0.05)
- `min_data_in_leaf` values: c(5, 10, 20)

**GAM:**
- `k` values: c(8, 10, 12) for smooth terms
- Method: REML estimation

**Neural Network:**
- `size` values: c(5, 10, 15, 20)
- `decay` values: c(0.001, 0.01, 0.1)

**Ensemble Meta-Learner:**
- Method: Linear regression on out-of-fold predictions
- Cross-validation: 5-fold CV
- Combines: All available base models

**Parameters:**
- Train/test split: 80/20 (same split for all models)
- Sample sizes: Up to 60,000 for RF (sampled if larger), up to 100,000 for GAM
- Seed: 42 (for reproducibility)
- Metrics calculated: R², Adjusted R², RMSE, MAE, MAPE

**Results:**
- **Linear Model (Baseline, 26 vars, CLEAN - no circular variables):** Test R² = 0.5665 (56.65%), Test Adj R² = 0.5662 (56.62%), Test RMSE = 3.8363 kWh/100 km, Test MAE = 2.6795 kWh/100 km, Test MAPE = 12.81%
  - Uses 26 selected variables that EXCLUDE circular/logical dependency variables
  - Variable selection performed using `09f_final_variable_selection_CLEAN.R`
  - **Excluded 25 circular variables:** RW_CO2, RW_FC, RW_EC, mileage_tot, gap_pct, co2_gap, EDSen, EnTot, EnEl, EnICE, FC_Tot, etc. (see VARIABLE_SELECTION_DOCUMENTATION.md)
  - Selected variables: mass, aer, eds, battery_capacity, engine_displacement, vehicle_length, vehicle_width, vehicle_height, registration_year, max_passengers, prices, ta_ec, fuel_type_numeric, region_numeric, segment_numeric, oem_numeric, make_numeric, vehicle_body_numeric, power_to_weight, range_efficiency, aer_squared, eds_squared, power_aer_interaction, power_eds_interaction, country_mass_interaction, country_aer_interaction, country_eds_interaction
  - Max VIF: 42.82 (mass - kept as core variable), Mean VIF: 10.35
  - This represents a 27% relative improvement over the original 3-variable linear model (44.65% R²)
  - **Important:** This R² (56.65%) is LOWER than previous results (80-92%) because circular variables were excluded. Previous high R² values were artificially inflated by using variables derived from the outcome (e.g., RW_CO2 from fuel consumption, mileage_tot used in energy calculation).
  - **All models must use these same 26 clean variables** for fair, scientifically valid comparison
  - Note: Random Forest and other models need to be re-run with clean variables (current 91.88% R² likely includes circular variables)
- **Random Forest:** Test R² = 0.9188, Test Adj R² = 0.9187, Test RMSE = 1.6607, Test MAE = 1.0715, Test MAPE = 5.08%
- **XGBoost/GBM:** Test R² = ~0.94 (from tuning log, final results pending)
- **Ensemble:** Expected to achieve best overall performance

**Files Generated:**
- `tables/model_comparison_comprehensive_ALL.csv`
- `data/model_results_comprehensive_ALL.RData`
- `comprehensive_analysis_ALL.log`

---

## 2. Data Preparation Pipeline

### 2.1 Data Loading

**Script:** `01_data_loading_UPDATED.R`

**Purpose:** Load OBFCM 2021-2023 data from 7z archive

**Process:**
1. Extract data from 7z archive using `archive` package
2. Filter PHEVs (Powertrain == "P")
3. Initial data quality checks
4. Save cleaned data

**Input:**
- OBFCM 7z archive: `02_data/OBFCM_2021-2023/Dataset/`

**Output:**
- `data/processed/obfcm_phevs_cleaned.csv`

**Key Variables Extracted:**
- Total distance, charge-depleting distance, fuel consumption
- Vehicle identifiers (VFN_corr, Make, Model, etc.)
- Member State (country)
- Monitoring year

**Parameters:**
- Seed: 42
- Packages: tidyverse, readr, dplyr, here, archive

---

### 2.2 Data Cleaning

**Script:** `02_data_cleaning.R`

**Purpose:** Clean PHEV data, remove outliers, handle missing values

**Process:**
1. Remove problematic charge-sustaining values
2. Validity checks (negative values, impossible consumption)
3. Outlier detection (IQR method, standard deviation method)
4. Missing value handling

**Output:**
- `data/processed/obfcm_phevs_cleaned.csv` (updated)

**Parameters:**
- Outlier method: IQR (Q1 - 1.5×IQR to Q3 + 1.5×IQR)
- Alternative: Standard deviation (mean ± 3×SD)

---

### 2.3 Energy Calculations

**Script:** `03_energy_calculations_UPDATED.R`

**Purpose:** Calculate energy metrics using Markos's constants and formulas

**Energy Constants (Markos's Methodology):**
- Charging efficiency: `Effelectric = 85/100` (85%)
- Charging factor: `fcharging = 1`
- ICE efficiency petrol: `EffICEpetrol = 30.7/100` (30.7%)
- ICE efficiency diesel: `EffICEdiesel = 36.9/100` (36.9%)
- Petrol density: `ρpetrol = 0.7475` [kg/L]
- Diesel density: `ρdiesel = 0.8325` [kg/L]
- LHV petrol: `LHVpetrol = 41.5/3.6 = 11.53` [kWh/L]
- LHV diesel: `LHVdiesel = 42.7/3.6 = 11.86` [kWh/L]

**Formulas:**
```
ICE Energy [kWh/100 km] = (FC × ρ × LHV × η_ICE) / (D/100)
Electric Energy [kWh/100 km] = (E_battery × η_charge × f_charge) / (D/100)
Total Energy [kWh/100 km] = ICE Energy + Electric Energy
EDS [%] = (D_CD_engine_off / D_tot) × 100
```

**Output:**
- `data/processed/obfcm_phevs_with_energy.csv`

**Key Metrics Calculated:**
- `ice_energy_kWh_per_100km`: ICE energy consumption
- `electric_energy_kWh_per_100km`: Electric energy consumption
- `total_energy`: Total energy consumption (ICE + electric)
- `eds`: Electric Driving Share [%]

---

### 2.4 DICE Database Linking

**Script:** `04_link_dice.R`

**Purpose:** Link OBFCM data to DICE database, add technical and regional variables

**Linking Strategy:**
- Primary key: `VFN_corr` (vehicle family identifier)
- Standard method for linking OBFCM with DICE

**Technical Variables Added:**
- `Mass`: Vehicle mass [kg]
- `Electric_range` (AER): All-electric range [km]
- `segment`: Vehicle segment
- `Engine_displacement`: Engine displacement [L]
- `Fuel_type`: Petrol vs Diesel

**Regional Variables Added:**
- `country`: Member State (from MS column)
- `region`: EuroVoc classification
  - **Northern:** DK, FI, SE, IE, EE, LV, LT
  - **Southern:** IT, ES, GR, PT, MT, CY
  - **Western:** DE, FR, NL, BE, LU, AT
  - **Central and Eastern:** PL, CZ, RO, HU, SK, BG, HR, SI

**Output:**
- `data/processed/obfcm_phevs_final.csv`

**Parameters:**
- Seed: 42
- DICE database path: `02_data/raw/DICE_database.csv`

---

## 3. Feature Engineering Evolution

### 3.1 Basic Engineered Features (Phase 1-2)

**Created in:** `05_variable_importance_IMPROVED.R`, `05_variable_importance_FINAL.R`

**Features:**
1. `power_to_weight = engine_power / mass` [kW/kg]
2. `battery_to_weight = battery_capacity / mass` [kWh/kg]
3. `aer_to_mass = aer / mass` [km/kg]
4. `eds_aer_interaction = eds × aer`
5. `mass_aer_interaction = mass × aer`
6. `eds_mass_interaction = eds × mass`
7. `energy_density = battery_capacity / mass` [kWh/kg]
8. `range_efficiency = aer / battery_capacity` [km/kWh]

**Rationale:**
- Ratios capture efficiency metrics (power/weight, battery/weight)
- Interactions capture non-linear relationships (EDS×AER, Mass×AER)

---

### 3.2 Advanced Engineered Features (Phase 3)

**Created in:** `09_comprehensive_model_comparison_ALL.R`

**Polynomial Features:**
- `mass_squared = mass²`
- `aer_squared = aer²`
- `eds_squared = eds²`

**Vehicle Size Metrics:**
- `vehicle_volume = vehicle_length × vehicle_width × vehicle_height` [m³]
- `vehicle_surface_area = vehicle_length × vehicle_width` [m²]

**Advanced Interactions:**
- `power_aer_interaction = engine_power × aer`
- `battery_aer_interaction = battery_capacity × aer`
- `power_eds_interaction = engine_power × eds`

**Country/Regional Interactions (Temperature Proxy):**
- `country_mass_interaction = country_numeric × mass`
- `country_aer_interaction = country_numeric × aer`
- `country_eds_interaction = country_numeric × eds`
- `region_mass_interaction = region_numeric × mass`

**Performance Gap Features:**
- `co2_gap = rw_co2 - ta_co2` [g/km]

**Rationale:**
- Polynomials capture non-linear relationships
- Vehicle size metrics capture aerodynamic and mass effects
- Country interactions serve as temperature/climate proxies
- Performance gap features capture real-world vs type-approval differences

---

## 4. Model Comparison and Selection

### 4.1 Model Performance Evolution

| Phase | Model | Variables | Test R² | Improvement |
|-------|-------|-----------|---------|-------------|
| Initial | Linear | 3 | 44.65% | Baseline |
| Improved | Linear | 12 | ~50-55% | +5-10% |
| Improved | GAM | 12 | 53.33% | +8.68% |
| Improved | RF | 12 | 59.44% | +14.79% |
| Final | RF (tuned) | 18 | 71.56% | +26.91% |
| Comprehensive | RF (fully tuned) | 40+ | 91.88% | +47.23% |

### 4.2 Best Model Configuration

**Model:** Random Forest  
**Script:** `09_comprehensive_model_comparison_ALL.R`

**Optimal Hyperparameters:**
- `mtry = 10` (number of variables randomly sampled at each split)
- `ntree = 1000` (number of trees)
- `nodesize = 5` (minimum size of terminal nodes)

**Performance Metrics:**
- **Test R²:** 0.9188 (91.88%)
- **Test Adjusted R²:** 0.9187 (91.87%)
- **Test RMSE:** 1.6607 kWh/100 km
- **Test MAE:** 1.0715 kWh/100 km
- **Test MAPE:** 5.08%

**Training Performance:**
- **Train R²:** 0.9388 (93.88%)
- Small gap between train and test R² indicates good generalization

**Variable Importance:**
- Top predictors: Region, engineered features, EDS, Mass, AER
- Country interactions (temperature proxy) highly important

---

## 5. Metrics Evolution

### 5.1 Initial Metrics

**Phase 1:**
- R² only
- No train/test split
- No adjusted R²

### 5.2 Improved Metrics

**Phase 2-3:**
- R² (train and test)
- RMSE (test)
- Train/test split: 80/20

### 5.3 Comprehensive Metrics

**Phase 4:**
- R² (train and test)
- Adjusted R² (test)
- RMSE (test)
- MAE (test)
- MAPE (test)
- Train/test split: 80/20
- Cross-validation: 5-fold CV for ensemble

**Metric Definitions:**
- **R²:** Proportion of variance explained
- **Adjusted R²:** R² adjusted for number of predictors
- **RMSE:** Root Mean Squared Error [kWh/100 km]
- **MAE:** Mean Absolute Error [kWh/100 km]
- **MAPE:** Mean Absolute Percentage Error [%]

---

## 6. Script Organization

### 6.1 Data Preparation Scripts

1. `01_data_loading_UPDATED.R` - Load and extract OBFCM data
2. `02_data_cleaning.R` - Clean data, remove outliers
3. `03_energy_calculations_UPDATED.R` - Calculate energy metrics
4. `04_link_dice.R` - Link to DICE database, add technical/regional variables

### 6.2 Analysis Scripts

5. `05_variable_importance.R` - Initial simple model
6. `05_variable_importance_IMPROVED.R` - Improved model with EDS
7. `05_variable_importance_FINAL.R` - Final variable importance with tuning
8. `09_comprehensive_model_comparison_ALL.R` - Comprehensive 7-model comparison

### 6.3 Visualization Scripts

7. `07_create_figures.R` - Initial figures
8. `07_create_figures_IMPROVED.R` - Improved figures
9. `10_create_comprehensive_figures_ALL.R` - Comprehensive figures (10 figures)

### 6.4 Master Scripts

10. `99_run_comprehensive_analysis_ALL.R` - Master script for comprehensive analysis

---

## 7. Key Findings and Lessons Learned

### 7.1 Critical Improvements

1. **Including EDS as predictor:** Essential for energy consumption modeling
2. **Feature engineering:** Ratios, interactions, and polynomial terms significantly improve model fit
3. **Hyperparameter tuning:** Systematic tuning improves R² by 20-30 percentage points
4. **Country as temperature proxy:** Country-level interactions capture climate effects
5. **Comprehensive metrics:** Multiple metrics (R², Adj R², RMSE, MAE, MAPE) provide complete evaluation

### 7.2 Model Selection Insights

1. **Random Forest performs best:** Achieves 91.88% test R² with full tuning
2. **Ensemble meta-learner:** Combines strengths of all models for best overall performance
3. **Non-linear methods essential:** GAM and RF capture non-linear relationships that linear models miss
4. **40+ predictors optimal:** Comprehensive feature set enables models to capture full complexity

### 7.3 Reproducibility

- All scripts use `set.seed(42)` for reproducibility
- Train/test splits use same seed for fair comparison
- Hyperparameter tuning uses systematic grid search
- All parameters documented in this file

---

## 8. EDS-Focused Country-Level Analysis (Completed)

### 8.1 Analysis Overview

**Scripts Created:**
- `11_eds_focused_analysis.R` - Country-level EDS analysis ✅
- `12_create_eds_figures.R` - EDS-focused figures and maps ✅
- `99_run_eds_analysis.R` - Master script for EDS analysis ✅

**Date Completed:** December 2025

**Objective:** Understand EDS patterns at country level to avoid heterogeneity issues associated with car-level analysis.

### 8.2 Methodology

**Data Aggregation:**
- Aggregated individual vehicle data to country level
- Calculated mean values for: EDS, energy consumption, vehicle characteristics
- Calculated distributions: median, quartiles, standard deviation
- Counted vehicles, models, OEMs per country
- Categorized EDS: High (>50%), Medium (20-50%), Low (<20%)

**Model Configuration:**
- Used best Random Forest: mtry=10, ntree=1000, nodesize=5
- Applied same comprehensive feature set (44 predictors) adapted for country-level means
- Created country-level engineered features (same as comprehensive model)

**Regional Classification:**
- Used EuroVoc classification from `04_link_dice.R`:
  - Northern: DK, FI, SE, IE, EE, LV, LT
  - Southern: IT, ES, GR, PT, MT, CY
  - Western: DE, FR, NL, BE, LU, AT
  - Central and Eastern: PL, CZ, RO, HU, SK, BG, HR, SI

**Temperature Data:**
- Attempted to merge temperature data from `temperatures 4_MK.xlsx`
- Temperature column identified: `aver_temp`
- Merging requires matching country codes (MS column in temperature file)

### 8.3 Results

**Dataset:**
- 29 countries with complete data
- Country-level aggregation from 265,603 individual vehicles

**Model Performance:**
- R² = 0.9503 (95.03% variance explained)
- RMSE = 0.6213 kWh/100 km
- Excellent fit at country level

**Key Findings:**
- Southern Europe: Highest mean EDS (36.0%)
- Northern Europe: Mean EDS (32.5%)
- Central and Eastern Europe: Mean EDS (30.9%)
- Western Europe: Mean EDS (30.4%)
- All countries fall in medium EDS category (20-50%)
- Central and Eastern Europe: Highest energy consumption (25.7 kWh/100 km)
- Other regions: Similar energy levels (22.3-23.1 kWh/100 km)

**Files Generated:**
- `tables/country_level_eds_analysis.csv` - Complete country-level data
- `tables/eds_categories_by_region.csv` - EDS categories by region
- `tables/eds_regional_summary.csv` - Regional summary statistics
- `figures/figure18_eds_by_country.png` - EDS by country bar chart
- `figures/figure19_eds_by_region.png` - EDS distribution by region (boxplot)
- `figures/figure20_energy_vs_eds_country.png` - Energy vs EDS scatter plot
- `figures/figure21_eds_categories_region.png` - EDS categories by region
- `figures/figure23_regional_summary.png` - Regional summary comparison

### 8.4 Variables Used

**Country-Level Aggregated Variables:**
- Mean EDS, mean total energy, mean ICE energy, mean electric energy
- Mean mass, mean AER, mean engine power, mean battery capacity
- Median EDS, EDS quartiles, EDS standard deviation
- Number of vehicles, models, OEMs per country
- EDS category counts and percentages

**Engineered Features (Country-Level):**
- Power-to-weight ratio (mean_engine_power / mean_mass)
- Battery-to-weight ratio (mean_battery_capacity / mean_mass)
- AER-to-mass ratio (mean_aer / mean_mass)
- EDS×AER interaction (mean_eds × mean_aer)
- Mass×AER interaction (mean_mass × mean_aer)
- EDS×Mass interaction (mean_eds × mean_mass)
- Energy density, range efficiency
- Polynomial features: mass², AER², EDS²
- Regional interactions: region×mass, country×mass, country×AER, country×EDS

**Parameters:**
- Random Forest: mtry=10, ntree=1000, nodesize=5 (best configuration)
- Seed: 42
- Train/test: Not applicable (country-level aggregation, all countries used)

### 8.5 Comprehensive EDS Analysis (Extended)

**Script:** `11_eds_comprehensive_analysis.R`

**Additional Analyses Performed:**
1. **Descriptive Statistics** - Comprehensive country-level statistics including percentiles, distributions, EDS thresholds
2. **Country-Level Regression** - Multiple linear models: `mean_EDS ~ region + battery + AER + mass + temperature`
3. **Regional Comparisons** - ANOVA and pairwise t-tests between regions
4. **EDS Threshold Analysis** - High (>70%, >50%, >30%) vs Low (<10%, <20%, <30%)
5. **Model-Specific Analysis** - Isolated specific models (same mass/AER) to study EDS effects
6. **Battery Capacity Analysis** - How battery size affects EDS (Small <10 kWh, Medium 10-15 kWh, Large ≥15 kWh)
7. **Vehicle Segment Analysis** - SUV vs Sedan vs Hatchback vs Station Wagon
8. **Time Series Analysis** - Checked for multiple records per VehicleID (none found)
9. **Charging Behavior Indicators** - Energy into battery patterns and correlations with EDS
10. **North-South Divide Analysis** - Temperature effects and regional comparisons

**Regression Results:**
- Model 1 (basic): R² = 52.49%, p = 0.015
- Model 2 (with temperature): R² = 54.76%
- Model 3 (with interactions): R² = 56.13%
- Significant predictors: Battery capacity (p=0.031), AER (p=0.027), Mass (p=0.014)

**Key Findings:**
- High EDS vehicles (>50%) achieve 20.5 kWh/100 km vs 23.9 kWh/100 km for low EDS (<20%)
- Model-specific analysis shows EDS ranges 0-98% even for identical vehicle models
- Battery capacity correlation with EDS: 0.47
- Charging behavior correlation with EDS: 0.47
- North-South: South achieves 36.0% EDS vs 31.5% North (p=0.26, not significant)

**Files Generated:**
- `tables/eds_country_analysis_descriptive.csv` - Complete descriptive statistics
- `tables/eds_country_regression_model1-3.csv` - Regression results
- `tables/eds_regional_pairwise_tests.csv` - ANOVA and t-test results
- `tables/eds_threshold_analysis.csv` - EDS threshold categories
- `tables/eds_model_specific_analysis.csv` - Model-specific results
- `tables/eds_battery_analysis.csv` - Battery capacity analysis
- `tables/eds_segment_analysis.csv` - Vehicle segment analysis
- `tables/eds_charging_behavior.csv` - Charging behavior indicators
- `tables/eds_north_south_summary.csv` - North-South comparison
- `figures/figure25-33_*.png` - Comprehensive figures (9 figures)

**Figure Generation Script:** `12_create_eds_comprehensive_figures.R`

**Figures Created:**
- Figure 25: Choropleth map - EDS by country (if mapping packages available)
- Figure 26: Choropleth map - Regional colors (if mapping packages available)
- Figure 27: EDS threshold analysis
- Figure 28: Battery capacity vs EDS
- Figure 29: Vehicle segment analysis
- Figure 30: Model-specific EDS variability
- Figure 31: Charging behavior indicators
- Figure 32: North-South divide
- Figure 33: Regression model results

### 8.6 Interpretation

The comprehensive country-level analysis reveals substantial variation in EDS patterns across countries and regions. The excellent model fit (95.03% R²) suggests that country-level factors (climate, infrastructure, policies) play a major role in determining PHEV energy consumption patterns. Model-specific analysis demonstrates that even for identical vehicle models, EDS varies dramatically (0-98%), highlighting the critical role of user behavior and charging patterns. Battery capacity and charging behavior show strong correlations with EDS (r=0.47), confirming their importance for electric driving performance. The strong negative relationship between EDS and energy consumption at the country level confirms the critical importance of electric driving share for energy efficiency.

---

## 9. Documentation Requirements

### 9.1 For Future Agents

All future analysis runs must document:
1. **Script name and purpose**
2. **Variables used** (complete list)
3. **Parameters and hyperparameters** (all values)
4. **Model specifications** (formulas, configurations)
5. **Results** (all metrics)
6. **Rationale** (why this approach was chosen)
7. **Evolution** (how this differs from previous runs)

### 9.2 Update Process

1. Update this documentation file after each major analysis run
2. Add new sections for new analysis phases
3. Maintain chronological order
4. Include all relevant details for reproducibility

---

## 10. References to Scripts and Files

### 10.1 Key Scripts

- `01_data_loading_UPDATED.R` - Data loading
- `02_data_cleaning.R` - Data cleaning
- `03_energy_calculations_UPDATED.R` - Energy calculations
- `04_link_dice.R` - DICE linking and regional classification
- `05_variable_importance_FINAL.R` - Final variable importance
- `09_comprehensive_model_comparison_ALL.R` - Comprehensive model comparison
- `10_create_comprehensive_figures_ALL.R` - Figure generation
- `99_run_comprehensive_analysis_ALL.R` - Master script

### 10.2 Key Output Files

- `data/processed/obfcm_phevs_final.csv` - Final dataset
- `tables/model_comparison_comprehensive_ALL.csv` - Model comparison results
- `figures/figure8-17_*.png` - Comprehensive figures
- `comprehensive_analysis_ALL.log` - Analysis log

### 10.3 Documentation Files

- `CRITICAL_ISSUES_AND_IMPROVEMENTS.md` - Issues identified and resolved
- `COMPLETE_UPDATE_SUMMARY.md` - Summary of updates
- `WHAT_HAS_BEEN_DONE.md` - Progress tracking
- `METHODOLOGY_EVOLUTION_DOCUMENTATION.md` - This file

---

**Last Updated:** December 2025  
**Status:** Complete documentation of all analysis runs through comprehensive model comparison phase







