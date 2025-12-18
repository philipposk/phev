# Complete Development Log

**Paper:** The real-world energy use and electric driving share of plug-in hybrid vehicles in Europe  
**Date Range:** December 2024 - December 2025  
**Status:** Active

---

## 📋 Overview

This log documents all development activities, corrections, decisions, and milestones in the paper development process. It includes both detailed entries and a summary of important milestones.

---

## 🗓️ Detailed Development Log

### December 2024

**Initial Setup**
- Created initial data loading script (`01_data_loading.R`)
- Created data cleaning script (`02_data_cleaning.R`)
- Created energy calculation script (`03_energy_calculations.R`)
- Established baseline: Simple linear model with 3 variables (mass, AER, region)
- **Result:** 44.65% R²
- **Finding:** Mass accounts for 97.5% of explained variance (model specification artifact)

**Files Created:**
- `01_data_loading.R`
- `02_data_cleaning.R`
- `03_energy_calculations.R`
- `05_variable_importance.R`
- `tables/variable_importance_lmg.csv`
- `figures/figure5_variable_importance_lmg.png`

---

### January 2025

**Feature Engineering Phase**
- Added EDS as critical predictor
- Created basic engineered features (power-to-weight, battery-to-weight, AER-to-mass ratios)
- Added interaction terms (EDS×AER, Mass×AER, EDS×Mass)
- Expanded to 12 variables
- Compared multiple methods: Linear (LMG), GAM, Random Forest

**Results:**
- GAM: 53.33% deviance explained
- Random Forest: 59.44% test R²
- **Improvement:** 14.79 percentage points over baseline

**Files Created:**
- `05_variable_importance_FINAL.R`
- `tables/variable_importance_lmg_improved.csv`
- `tables/variable_importance_gam_improved.csv`
- `figures/figure5a_variable_importance_gam.png`
- `figures/figure5b_variable_importance_rf.png`

---

### February-March 2025

**Systematic Hyperparameter Tuning**
- Expanded feature set to 18 variables
- Added: engine displacement, vehicle length, registration year
- Added: energy density, range efficiency
- Implemented systematic hyperparameter tuning for Random Forest
- **Result:** 71.56% test R² (intermediate phase, ~18 variables)

**Files Created:**
- Updated `05_variable_importance_FINAL.R`
- `tables/variable_importance_rf_tuned.csv`

---

### April-May 2025

**Comprehensive Model Comparison Phase**
- Expanded to 40+ predictors (later 44 variables)
- Added: vehicle dimensions, mileage, prices, CO₂ metrics
- Added: categorical variables (country, segment, OEM, make, vehicle body)
- Added: advanced engineered features (polynomials, vehicle size metrics, country interactions)
- Implemented 7 models: RF, XGBoost, LightGBM, CatBoost, GAM, NN, Ensemble
- Extensive hyperparameter tuning (8+ hours computation)
- **Result:** 91.88% test R² (Random Forest) - **later identified as inflated**

**Files Created:**
- `09_comprehensive_model_comparison_ALL.R`
- `10_create_comprehensive_figures_ALL.R`
- `tables/model_comparison_ALL.csv`
- `figures/figure8-17_*.png` (model comparison figures)

**Issue Identified:** High R² values suspicious - possible circular variables

---

### June 2025

**Circular Variable Identification**
- Created script to identify circular variables: `09d_identify_circular_variables.R`
- **Identified 25 circular variables:**
  - RW_CO2, RW_FC, RW_EC (derived from fuel/energy)
  - Mileage_Tot, Mileage_CD_Eng_Off, etc. (used in energy calculation)
  - gap, gap%, co2_gap (derived from RW values)
  - EDSen (energy-based EDS - calculated from energy components)
  - EnTot, EnEl, EnICE, etc. (direct components of total_energy)

**Decision:** Exclude circular variables for scientific validity

**Files Created:**
- `09d_identify_circular_variables.R`
- `tables/circular_variables_list.csv`
- `VARIABLE_SELECTION_DOCUMENTATION.md`

---

### July 2025

**Clean Variable Selection**
- Created variable selection script: `09f_final_variable_selection_CLEAN.R`
- Applied VIF-based multicollinearity reduction
- **Selected 26 clean variables**
- Excluded all 25 circular variables
- **Result:** More realistic R² values

**Files Created:**
- `09f_final_variable_selection_CLEAN.R`
- `tables/final_selected_variables_CLEAN.csv`
- `CLEAN_VARIABLES_SUMMARY.md`

---

### August-September 2025

**Clean Variable Model Re-runs**
- Created script: `09g_all_models_CLEAN_variables.R`
- Re-ran all models with 26 clean variables
- Used best hyperparameters from 44-variable runs (parameter transfer approach)
- **Results:**
  - Linear Model: 56.65% test R²
  - Random Forest: 71.63% test R²
  - XGBoost: 73.71% test R²
  - Neural Network: 73.22% test R²
  - GAM: 64.31% test R²

**Files Created:**
- `09g_all_models_CLEAN_variables.R`
- `tables/model_comparison_CLEAN_variables.csv`
- `data/processed/all_models_CLEAN_variables.RData`

**Documentation:**
- Updated `METHODOLOGY_EVOLUTION_DOCUMENTATION.md`
- Created `COMPREHENSIVE_ANALYSIS_STATUS.md`

---

### October 2025

**EDS Comprehensive Analysis**
- Created: `11_eds_comprehensive_analysis.R`
- Country-level aggregation approach
- Descriptive statistics, regression, regional comparisons
- **Issue:** Temperature data merging failed initially
- **Fix:** Explicitly use "MS" column from `temperatures 4_MK.xlsx`
- **Result:** Temperature data merged for all 29 countries

**Files Created:**
- `11_eds_comprehensive_analysis.R`
- `12_create_eds_comprehensive_figures.R`
- `99_run_eds_comprehensive_analysis.R`
- Multiple CSV tables (16 tables)
- Multiple figures (19 figures including choropleth maps)

**Documentation:**
- `FIXES_AND_CLARIFICATIONS.md` - Documented temperature merge fix

---

### November 2025

**Country-Level Regression Fix**
- **Issue:** Too many predictors for N=29 countries (risk of overfitting)
- **Fix:** Reduced to 2-3 key predictors:
  - Model 1: region + battery
  - Model 2: region + temperature
  - Model 3: region + battery + temperature
- **Result:** More parsimonious models (R² = 40-49%)

**Future Work Analyses**
- Created: `13_individual_vehicle_eds_analysis.R`
- Created: `14_temporal_analysis.R`
- Created: `15_charging_infrastructure_analysis.R`
- Created: `16_create_future_work_figures.R`
- Created: `99_run_future_work_analyses.R`

**Issue:** Individual vehicle EDS prediction had circularity
- **Fix:** Explicitly removed `eds`, `eds_squared`, `power_eds_interaction`, `country_eds_interaction`
- **Result:** Realistic R² values (4-12%)

**Files Created:**
- Future work analysis scripts
- `tables/individual_vehicle_eds_results.csv`
- `tables/temporal_analysis_results.csv`
- `tables/charging_infrastructure_results.csv`
- `figures/figure34-36_*.png`

---

### December 2025

**Consistency Fixes**
- **Issue:** Mixed references to 71.56% (old) vs 71.63% (new)
- **Fix:** Clarified throughout paper
  - 71.56% = intermediate phase (~18 vars)
  - 71.63% = clean variables (26 vars)
  - 91.88% = 44 vars (including circular) - Appendix A only

- **Issue:** Mixed references to variable counts (26 clean vs 44)
- **Fix:** Main paper uses 26 clean, Appendix A has 44 for comparison

- **Issue:** Section 1.4 mass dominance statement misleading
- **Fix:** Updated to reflect advanced model results (region 73%, not mass 97.5%)

- **Issue:** Section 5.3 based on outdated simple model
- **Fix:** Completely rewritten to focus on advanced model results

- **Issue:** Abstract variable count unclear
- **Fix:** Updated to "26 clean variables (excluding circular dependencies)"

**Figure Caption Placement**
- **Issue:** Captions duplicated (inline and end section)
- **Fix:** All captions inline, end section is reference list only
- **Files Updated:** `PAPER_DRAFT.md`, generated new DOCX

**Script Updates**
- Added LightGBM, CatBoost, Ensemble to `09g_all_models_CLEAN_variables.R`
- Added macOS notifications for each model completion
- **Status:** Script currently running

**Documentation Created**
- `PAPER_BUILD_GUIDE.md` - Complete build guide
- `DEVELOPMENT_LOG_COMPLETE.md` - This file
- `DEVELOPMENT_LOG_SUMMARY.md` - Summary version
- `TODO_PAPER_COMPLETION.md` - Completion checklist
- `MARKOS_REVIEW_NEEDED.md` - Review items

**Files Created:**
- `PAPER_DRAFT_20_CONSISTENCY_FIXED.docx` - Latest version
- Multiple documentation files

---

## 🎯 Important Milestones Summary

### Key Achievements

1. **Baseline Established (Dec 2024)**
   - Simple linear model: 44.65% R²
   - Identified limitations

2. **Feature Engineering (Jan 2025)**
   - Added EDS and engineered features
   - Improved to 59.44% R² (RF)

3. **Hyperparameter Tuning (Feb-Mar 2025)**
   - Systematic tuning
   - Improved to 71.56% R² (RF, intermediate)

4. **Comprehensive Analysis (Apr-May 2025)**
   - 7 models, 44 variables
   - 91.88% R² (RF) - later identified as inflated

5. **Circular Variable Exclusion (Jun 2025)**
   - Identified 25 circular variables
   - Created 26 clean variable set

6. **Clean Variable Analysis (Aug-Sep 2025)**
   - Re-ran all models with clean variables
   - Realistic results: 71.63% R² (RF), 73.71% (XGBoost)

7. **EDS Comprehensive Analysis (Oct 2025)**
   - Country-level analysis
   - 10 analysis types, 16 tables, 19 figures

8. **Future Work Analyses (Nov 2025)**
   - Individual vehicle, temporal, infrastructure
   - 3 new analysis types, 3 figures

9. **Finalization (Dec 2025)**
   - Consistency fixes
   - Documentation complete
   - Script running for final models

---

## 🔧 All Corrections Applied

1. **Circular Variable Exclusion** (June 2025)
2. **Temperature Data Merging Fix** (October 2025)
3. **Country-Level Regression Predictor Reduction** (November 2025)
4. **Individual Vehicle EDS Circularity Fix** (November 2025)
5. **Result Consistency (71.56% vs 71.63%)** (December 2025)
6. **Variable Set Consistency (26 vs 44)** (December 2025)
7. **Section 1.4 Mass Dominance Update** (December 2025)
8. **Section 5.3 Complete Rewrite** (December 2025)
9. **Abstract Variable Count Clarification** (December 2025)
10. **Figure Caption Placement** (December 2025)
11. **LightGBM/CatBoost/Ensemble Added to Script** (December 2025)

---

## 📊 Current Status

**Completed:**
- ✅ Data preparation pipeline
- ✅ Variable selection (26 clean variables)
- ✅ All main models re-run with clean variables (RF, XGBoost, GAM, NN)
- ✅ EDS comprehensive analysis
- ✅ Future work analyses
- ✅ Consistency fixes
- ✅ Documentation

**In Progress:**
- ⏳ LightGBM, CatBoost, Ensemble models (script running)

**Pending:**
- ⏸️ Update Table 5 with final model results
- ⏸️ Final paper review
- ⏸️ Figure insertion into DOCX
- ⏸️ Author information
- ⏸️ Reference completion

---

**Last Updated:** December 17, 2025






