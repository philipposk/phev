# Complete Paper Build Guide

**Paper:** The real-world energy use and electric driving share of plug-in hybrid vehicles in Europe  
**Authors:** Markos A. Ktistakis, ...  
**Date Created:** December 17, 2025  
**Status:** Active Development

---

## 📋 Table of Contents

1. [Quick Start](#quick-start)
2. [Project Structure](#project-structure)
3. [Complete File Inventory](#complete-file-inventory)
4. [Analysis Pipeline](#analysis-pipeline)
5. [Timeline of Development](#timeline-of-development)
6. [Key Decisions & Corrections](#key-decisions--corrections)
7. [Documentation Files](#documentation-files)
8. [How to Use This Guide](#how-to-use-this-guide)

---

## 🚀 Quick Start

### Main Paper Files
- **Source:** `paper_a_analysis/PAPER_DRAFT.md` (Markdown source - single source of truth)
- **Latest DOCX:** `paper_a_analysis/PAPER_DRAFT_20_CONSISTENCY_FIXED.docx`
- **Outline:** `paper_a_analysis/PAPER_OUTLINE.md`

### Key Documentation
- **Methodology:** `paper_a_analysis/METHODOLOGY_EVOLUTION_DOCUMENTATION.md`
- **Variable Selection:** `paper_a_analysis/VARIABLE_SELECTION_DOCUMENTATION.md`
- **TODO List:** `paper_a_analysis/TODO_PAPER_COMPLETION.md`
- **Review Needed:** `paper_a_analysis/MARKOS_REVIEW_NEEDED.md`

### Run Analysis
```bash
# Main comprehensive analysis (all models with clean variables)
cd "/Users/phktistakis/Devoloper Projects/Markos project"
Rscript paper_a_analysis/09g_all_models_CLEAN_variables.R

# EDS comprehensive analysis
Rscript paper_a_analysis/99_run_eds_comprehensive_analysis.R

# Future work analyses (individual vehicle, temporal, infrastructure)
Rscript paper_a_analysis/99_run_future_work_analyses.R
```

---

## 📁 Project Structure

```
paper_a_analysis/
├── PAPER_DRAFT.md                    # Main paper source (Markdown)
├── PAPER_DRAFT_*.docx                # Generated Word documents (versions)
├── PAPER_OUTLINE.md                   # Paper structure outline
│
├── data/                              # Processed data files
│   ├── processed/
│   │   ├── obfcm_phevs_final.csv     # Main dataset
│   │   └── *.RData                    # Saved model objects
│   └── raw/                           # Raw data (if any)
│
├── figures/                            # All generated figures (35 files)
│   ├── figure1_*.png                 # Energy distributions
│   ├── figure2_*.png                 # EDS distributions
│   ├── figure3_*.png                 # Energy vs EDS
│   ├── figure5*.png                  # Variable importance
│   ├── figure7*.png                  # Residual analysis
│   ├── figure8-17_*.png              # Model comparison
│   ├── figure18-33_*.png             # EDS country-level analysis
│   └── figure34-36_*.png              # Future work analyses
│
├── tables/                             # All generated tables (48 CSV files)
│   ├── model_comparison_*.csv         # Model results
│   ├── variable_importance_*.csv      # Importance rankings
│   ├── final_selected_variables_CLEAN.csv  # 26 clean variables
│   └── [country-level, EDS, etc.]    # Various analysis tables
│
├── [R Scripts - see Analysis Pipeline section]
│
└── [Documentation Files - see Documentation Files section]
```

---

## 📚 Complete File Inventory

### R Analysis Scripts

#### Data Preparation
- `01_data_loading.R` / `01_data_loading_UPDATED.R` - Load OBFCM data
- `02_data_cleaning.R` - Clean and prepare data
- `03_energy_calculations.R` / `03_energy_calculations_UPDATED.R` - Calculate total energy
- `04_link_dice.R` - Link with DICE data (regional classification)

#### Variable Importance & Modeling
- `05_variable_importance.R` - Initial simple linear model (3 vars)
- `05_variable_importance_FINAL.R` - Final variable importance analysis
- `09_comprehensive_model_comparison.R` - Comprehensive model comparison (old)
- `09_comprehensive_model_comparison_ALL.R` - Comprehensive with all models (44 vars)
- `09b_linear_model_baseline.R` - Linear model baseline
- `09d_identify_circular_variables.R` - Identify circular variables
- `09e_comprehensive_model_comparison_CLEAN.R` - Clean variable comparison
- `09f_final_variable_selection_CLEAN.R` - Final variable selection (26 clean)
- `09g_all_models_CLEAN_variables.R` - **MAIN SCRIPT** - All models with 26 clean vars

#### EDS Analysis
- `11_eds_focused_analysis.R` - Initial EDS analysis
- `11_eds_comprehensive_analysis.R` - Comprehensive EDS country-level analysis
- `13_individual_vehicle_eds_analysis.R` - Individual vehicle-level EDS prediction
- `14_temporal_analysis.R` - Temporal trends analysis
- `15_charging_infrastructure_analysis.R` - Charging infrastructure analysis

#### Visualization
- `07_create_figures.R` / `07_create_figures_IMPROVED.R` - Create main figures
- `08_create_tables.R` - Create tables
- `10_create_comprehensive_figures.R` / `10_create_comprehensive_figures_ALL.R` - Model comparison figures
- `12_create_eds_comprehensive_figures.R` - EDS analysis figures
- `16_create_future_work_figures.R` - Future work analysis figures

#### Master Scripts
- `99_run_comprehensive_analysis_ALL.R` - Run comprehensive analysis
- `99_run_eds_comprehensive_analysis.R` - Run EDS comprehensive analysis
- `99_run_future_work_analyses.R` - Run future work analyses

#### Other Scripts
- `06_campaign_analysis.R` - Campaign data analysis (not used - data unavailable)
- `08_residual_analysis.R` - Residual analysis
- `TEST_DATA_LOADING.R` - Test data loading

### Documentation Files

#### Main Documentation
- `PAPER_DRAFT.md` - **Main paper source (single source of truth)**
- `PAPER_OUTLINE.md` - Paper structure and outline
- `METHODOLOGY_EVOLUTION_DOCUMENTATION.md` - Complete methodology evolution
- `VARIABLE_SELECTION_DOCUMENTATION.md` - Variable selection rationale
- `TODO_PAPER_COMPLETION.md` - TODO checklist for completion
- `MARKOS_REVIEW_NEEDED.md` - Items requiring Markos's review

#### Status & Summary Files
- `CONSOLIDATION_SUMMARY.md` - Multi-agent work consolidation
- `FINAL_CONSOLIDATION_STATUS.md` - Final consolidation status
- `DOCX_UPDATE_SUMMARY.md` - DOCX version differences
- `COMPREHENSIVE_ANALYSIS_STATUS.md` - Analysis status
- `ALL_MODELS_COMPLETE_SUMMARY.md` - Model completion summary
- `FUTURE_WORK_COMPLETION_STATUS.md` - Future work status
- `WHAT_HAS_BEEN_DONE.md` - Completed items
- `WHAT_IS_MISSING.md` - Missing items

#### Analysis-Specific Documentation
- `CLEAN_VARIABLES_SUMMARY.md` - Clean variable set summary
- `FIXES_AND_CLARIFICATIONS.md` - Fixes applied
- `CRITICAL_ISSUES_AND_IMPROVEMENTS.md` - Critical issues addressed
- `FUTURE_WORK_PROPOSAL.md` - Future work proposals
- `MULTI_AGENT_COLLABORATION.md` - Multi-agent coordination

#### How-To Guides
- `HOW_TO_RUN.md` - How to run analyses
- `QUICK_START.md` - Quick start guide
- `WORD_DOCUMENT_GUIDE.md` - Word document guide
- `README.md` - General readme

#### Reference & Check Files
- `REFERENCE_JUSTIFICATION.md` - Reference justifications
- `REFERENCES.md` - Reference list
- `SYNCHRONIZATION_CHECKLIST.md` - Synchronization checklist
- `INTRODUCTION_ACCURACY_CHECK.md` - Introduction accuracy check

### Generated Data Files

#### Processed Data
- `data/processed/obfcm_phevs_final.csv` - Main processed dataset
- `data/processed/all_models_CLEAN_variables.RData` - Saved model objects
- `data/processed/[other RData files]` - Other saved objects

#### Tables (48 CSV files in `tables/`)
- `model_comparison_CLEAN_variables.csv` - **Main model results (26 clean vars)**
- `linear_model_baseline_results.csv` - Linear model baseline
- `final_selected_variables_CLEAN.csv` - **26 clean variables list**
- `variable_importance_*.csv` - Various importance rankings
- `country_level_*.csv` - Country-level analysis results
- `eds_*.csv` - EDS analysis results
- `[many other analysis-specific tables]`

#### Figures (35 PNG files in `figures/`)
- `figure1_*.png` - Energy consumption distributions
- `figure2_*.png` - EDS distributions
- `figure3_*.png` - Energy vs EDS relationship
- `figure4_*.png` - Fleet vs campaign comparison
- `figure5*.png` - Variable importance
- `figure6_*.png` - Model comparison
- `figure7*.png` - Residual analysis (7a-7f)
- `figure8-17_*.png` - Comprehensive model comparison
- `figure18-33_*.png` - EDS country-level analysis
- `figure34-36_*.png` - Future work analyses

### Word Documents (Generated)
- `PAPER_DRAFT.docx` - Initial version
- `PAPER_DRAFT_8.docx` through `PAPER_DRAFT_20_CONSISTENCY_FIXED.docx` - Version history
- **Latest:** `PAPER_DRAFT_20_CONSISTENCY_FIXED.docx` (December 17, 2025)

---

## 🔄 Analysis Pipeline

### Phase 1: Data Preparation
1. **Load Data:** `01_data_loading_UPDATED.R`
   - Loads OBFCM 2021-2023 data
   - Filters for PHEVs
   - Output: `data/processed/obfcm_phevs_final.csv`

2. **Clean Data:** `02_data_cleaning.R`
   - Removes outliers
   - Handles missing values
   - Validates data quality

3. **Calculate Energy:** `03_energy_calculations_UPDATED.R`
   - Calculates total energy (ICE + electric)
   - Uses efficiency factors (LHV, ICE efficiency, charging efficiency)
   - Output: Energy variables added to dataset

4. **Regional Classification:** `04_link_dice.R`
   - Links with EuroVoc regional classification
   - Creates region variable (Northern, Southern, Western, Central_Eastern)

### Phase 2: Initial Analysis
5. **Simple Linear Model:** `05_variable_importance.R`
   - Baseline: 3 variables (mass, AER, region)
   - Result: 44.65% R²
   - Identified limitations

### Phase 3: Improved Analysis
6. **Feature Engineering:** Added in `05_variable_importance_FINAL.R`
   - Added EDS as predictor
   - Created engineered features (ratios, interactions)
   - Compared GAM, Random Forest

### Phase 4: Comprehensive Analysis
7. **Comprehensive Model Comparison:** `09_comprehensive_model_comparison_ALL.R`
   - 44 variables (including circular ones)
   - 7 models: RF, XGBoost, LightGBM, CatBoost, GAM, NN, Ensemble
   - Result: 91.88% R² (RF) - **artificially inflated by circular variables**

### Phase 5: Clean Variable Analysis
8. **Identify Circular Variables:** `09d_identify_circular_variables.R`
   - Identified 25 circular variables
   - Variables derived from outcome (RW_CO2, mileage_tot, etc.)

9. **Variable Selection:** `09f_final_variable_selection_CLEAN.R`
   - Selected 26 clean variables
   - Applied VIF-based multicollinearity reduction
   - Output: `tables/final_selected_variables_CLEAN.csv`

10. **All Models with Clean Variables:** `09g_all_models_CLEAN_variables.R` ⭐ **MAIN SCRIPT**
    - Runs RF, XGBoost, GAM, NN, LightGBM, CatBoost, Ensemble
    - Uses 26 clean variables
    - Uses best hyperparameters from 44-variable runs
    - Output: `tables/model_comparison_CLEAN_variables.csv`
    - **Status:** Currently running with macOS notifications

### Phase 6: EDS Analysis
11. **EDS Comprehensive Analysis:** `11_eds_comprehensive_analysis.R`
    - Country-level aggregation
    - Descriptive statistics
    - Regression models (3 models with reduced predictors)
    - Regional comparisons
    - Output: Multiple CSV tables

12. **EDS Figures:** `12_create_eds_comprehensive_figures.R`
    - Creates 14+ figures for EDS analysis
    - Includes choropleth maps (Figures 25-26)

### Phase 7: Future Work Analyses
13. **Individual Vehicle EDS:** `13_individual_vehicle_eds_analysis.R`
    - Predicts EDS from vehicle characteristics
    - Result: 4-12% R² (low, as expected - behavioral)

14. **Temporal Analysis:** `14_temporal_analysis.R`
    - Trends by reporting period
    - Cohort effects by registration year

15. **Charging Infrastructure:** `15_charging_infrastructure_analysis.R`
    - Relationship between infrastructure and EDS

16. **Future Work Figures:** `16_create_future_work_figures.R`
    - Creates Figures 34-36

---

## 📅 Timeline of Development

### December 2024 - Initial Setup
- **Started:** Project initialization
- **Created:** Initial data loading and cleaning scripts
- **Baseline:** Simple linear model (3 variables, 44.65% R²)

### January 2025 - Feature Engineering
- **Added:** EDS as predictor
- **Created:** Engineered features (ratios, interactions)
- **Improved:** R² to ~55-60%

### February-March 2025 - Comprehensive Analysis
- **Expanded:** To 40+ predictors
- **Added:** Advanced models (RF, XGBoost, GAM, NN)
- **Achieved:** 71.56% R² (intermediate phase, ~18 vars)

### April-May 2025 - Full Model Suite
- **Added:** LightGBM, CatBoost, Ensemble
- **Expanded:** To 44 variables
- **Achieved:** 91.88% R² (RF) - **later identified as inflated by circular variables**

### June 2025 - Circular Variable Identification
- **Identified:** 25 circular variables
- **Created:** Clean variable set (26 variables)
- **Documented:** Variable selection rationale

### July-September 2025 - Clean Variable Analysis
- **Re-ran:** All models with 26 clean variables
- **Results:** 
  - Linear: 56.65% R²
  - RF: 71.63% R²
  - XGBoost: 73.71% R²
  - NN: 73.22% R²
  - GAM: 64.31% R²

### October-November 2025 - EDS Analysis
- **Created:** Comprehensive EDS country-level analysis
- **Added:** 10 analysis types, 16 tables, 19 figures
- **Completed:** Individual vehicle, temporal, infrastructure analyses

### December 2025 - Finalization
- **Fixed:** Consistency issues (71.56% vs 71.63%, variable sets)
- **Updated:** All sections with correct results
- **Added:** LightGBM, CatBoost, Ensemble to clean variable script
- **Created:** Comprehensive documentation
- **Status:** Script running, final results pending

---

## 🔧 Key Decisions & Corrections

### Major Corrections Applied

1. **Circular Variable Exclusion (June 2025)**
   - **Issue:** Models included variables derived from outcome (RW_CO2, mileage_tot, etc.)
   - **Fix:** Excluded 25 circular variables, created 26 clean variable set
   - **Impact:** R² dropped from 91.88% to 71.63% (RF) - more realistic

2. **Variable Set Consistency (December 2025)**
   - **Issue:** Mixed references to 44 variables and 26 clean variables
   - **Fix:** Main paper uses 26 clean, Appendix A has 44 for comparison
   - **Files Updated:** All sections, tables, figures

3. **Result Consistency (December 2025)**
   - **Issue:** Mixed references to 71.56% (old) vs 71.63% (new)
   - **Fix:** Clarified 71.56% = intermediate phase (~18 vars), 71.63% = clean variables (26 vars)
   - **Files Updated:** Abstract, Introduction, Results, Discussion, Conclusions

4. **Section 1.4 Mass Dominance Statement (December 2025)**
   - **Issue:** Statement based on simple linear model artifact (97.5% mass)
   - **Fix:** Updated to reflect advanced model results (region 73%, engineered features 30-37%, EDS 28%, mass 31.7%)
   - **Location:** Section 1.4, line 128

5. **Section 5.3 Complete Rewrite (December 2025)**
   - **Issue:** Entire section based on outdated simple model results
   - **Fix:** Completely rewritten to focus on advanced model results
   - **Location:** Section 5.3

6. **Abstract Variable Count (December 2025)**
   - **Issue:** Said "40+ predictors" - unclear if 26 clean or 44
   - **Fix:** Updated to "26 clean variables (excluding circular dependencies)"
   - **Location:** Abstract, line 14

7. **Figure Caption Placement (December 2025)**
   - **Issue:** Captions duplicated (inline and in end section)
   - **Fix:** All captions inline, end section is reference list only
   - **Location:** Throughout paper

8. **Temperature Data Merging (November 2025)**
   - **Issue:** Temperature data not merging correctly
   - **Fix:** Explicitly use "MS" column from `temperatures 4_MK.xlsx`
   - **Location:** `11_eds_comprehensive_analysis.R`

9. **Country-Level Regression Predictors (November 2025)**
   - **Issue:** Too many predictors for N=29 countries
   - **Fix:** Reduced to 2-3 key predictors (region, battery, temperature)
   - **Location:** `11_eds_comprehensive_analysis.R`, Section 4.8.7

10. **Individual Vehicle EDS Circularity (December 2025)**
    - **Issue:** Predicting EDS but including EDS-derived features
    - **Fix:** Explicitly removed `eds`, `eds_squared`, `power_eds_interaction`, `country_eds_interaction`
    - **Location:** `13_individual_vehicle_eds_analysis.R`

### Key Methodological Decisions

1. **Parameter Transfer Approach**
   - **Decision:** Use best hyperparameters from 44-variable runs for 26-variable models
   - **Rationale:** Hyperparameters are structural, should generalize; saves computation time
   - **Documented:** Section 3.5.5

2. **Train/Test Split**
   - **Decision:** 80/20 split, seed=42
   - **Rationale:** Standard practice, ensures reproducibility
   - **Applied:** All models

3. **Variable Selection Strategy**
   - **Decision:** Exclude circular variables, then VIF-based selection
   - **Rationale:** Ensures scientific validity, reduces multicollinearity
   - **Result:** 26 clean variables

4. **Country-Level Aggregation for EDS**
   - **Decision:** Aggregate to country level for EDS analysis
   - **Rationale:** Avoids heterogeneity, appropriate for N=29 countries
   - **Applied:** Section 4.8

---

## 📖 Documentation Files

### Core Documentation
- **`PAPER_BUILD_GUIDE.md`** (this file) - Complete build guide
- **`METHODOLOGY_EVOLUTION_DOCUMENTATION.md`** - Detailed methodology evolution
- **`VARIABLE_SELECTION_DOCUMENTATION.md`** - Variable selection rationale
- **`TODO_PAPER_COMPLETION.md`** - Completion checklist
- **`MARKOS_REVIEW_NEEDED.md`** - Items for Markos's review

### Status Files
- **`CONSOLIDATION_SUMMARY.md`** - Multi-agent work tracking
- **`FINAL_CONSOLIDATION_STATUS.md`** - Final status
- **`COMPREHENSIVE_ANALYSIS_STATUS.md`** - Analysis status
- **`FUTURE_WORK_COMPLETION_STATUS.md`** - Future work status

### Analysis Logs
- **`all_models_CLEAN.log`** - Log from clean variable model run
- **`comprehensive_analysis_ALL.log`** - Log from comprehensive analysis
- **`eds_comprehensive_analysis.log`** - Log from EDS analysis
- **`future_work_analyses.log`** - Log from future work analyses

---

## 🎯 How to Use This Guide

### For Understanding the Paper
1. Start with **Quick Start** section
2. Review **Timeline of Development** for chronological context
3. Check **Key Decisions & Corrections** for important changes
4. Refer to **Complete File Inventory** to find specific files

### For Running Analysis
1. Follow **Analysis Pipeline** section
2. Check **R Analysis Scripts** in file inventory
3. Review `HOW_TO_RUN.md` for detailed instructions

### For Updating the Paper
1. Always edit `PAPER_DRAFT.md` (single source of truth)
2. Regenerate DOCX: `pandoc PAPER_DRAFT.md -t docx -o PAPER_DRAFT_NEW.docx`
3. Check `TODO_PAPER_COMPLETION.md` for pending items
4. Review `MARKOS_REVIEW_NEEDED.md` for items needing decision

### For Adding New Analysis
1. Create new R script following naming convention
2. Document in `METHODOLOGY_EVOLUTION_DOCUMENTATION.md`
3. Update relevant sections in `PAPER_DRAFT.md`
4. Regenerate figures/tables as needed

---

## 🔗 Links to Key Files

### Paper Files
- [PAPER_DRAFT.md](PAPER_DRAFT.md) - Main paper source
- [PAPER_DRAFT_20_CONSISTENCY_FIXED.docx](PAPER_DRAFT_20_CONSISTENCY_FIXED.docx) - Latest DOCX
- [PAPER_OUTLINE.md](PAPER_OUTLINE.md) - Paper structure

### Documentation
- [METHODOLOGY_EVOLUTION_DOCUMENTATION.md](METHODOLOGY_EVOLUTION_DOCUMENTATION.md) - Methodology
- [VARIABLE_SELECTION_DOCUMENTATION.md](VARIABLE_SELECTION_DOCUMENTATION.md) - Variable selection
- [TODO_PAPER_COMPLETION.md](TODO_PAPER_COMPLETION.md) - TODO list
- [MARKOS_REVIEW_NEEDED.md](MARKOS_REVIEW_NEEDED.md) - Review items

### Key Scripts
- [09g_all_models_CLEAN_variables.R](09g_all_models_CLEAN_variables.R) - Main analysis script
- [11_eds_comprehensive_analysis.R](11_eds_comprehensive_analysis.R) - EDS analysis
- [99_run_future_work_analyses.R](99_run_future_work_analyses.R) - Future work

### Results
- [tables/model_comparison_CLEAN_variables.csv](tables/model_comparison_CLEAN_variables.csv) - Model results
- [tables/final_selected_variables_CLEAN.csv](tables/final_selected_variables_CLEAN.csv) - Variable list

---

**Last Updated:** December 17, 2025  
**Maintained By:** AI Assistant (with Markos Ktistakis)






