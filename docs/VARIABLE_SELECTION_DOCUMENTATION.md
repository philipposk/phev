# Variable Selection Documentation

**Date:** December 16, 2025  
**Script:** `09f_final_variable_selection_CLEAN.R`  
**Status:** ✅ Complete

## Overview

This document describes the final variable selection process that:
1. **Excludes circular/logical dependency variables** (variables derived from the outcome)
2. **Reduces multicollinearity** (VIF-based selection)
3. **Applies to ALL models** (Linear, Random Forest, XGBoost, GAM, Neural Network, Ensemble)

## Step 1: Exclude Circular Variables

### Circular Variables Removed (25 variables)

**Direct energy components (8 variables):**
- `EnTot`, `EnTot100km`, `EnEl`, `EnICE`, `EnEl100km`, `EnICE100km`
- `electric_energy`, `ice_energy`

**Energy-based EDS (1 variable):**
- `EDSen` - Calculated as `EnEl / (EnEl + EnICE) * 100` - CIRCULAR!

**Real-world fuel consumption and CO2 (4 variables):**
- `RW_FC` - Real-world fuel consumption (directly related to energy)
- `RW_CO2` - Real-world CO2 (calculated from fuel consumption)
- `RW_EC` - Real-world energy consumption (THIS IS THE OUTCOME!)
- `RW_OVC` - Real-world OVC

**Gap variables (3 variables):**
- `gap`, `gap%`, `co2_gap` - Derived from RW_CO2 and TA_CO2

**Mileage variables (5 variables):**
- `Mileage_Tot` - Used in calculation: `total_energy = EnTot / Mileage_Tot * 100` - CIRCULAR!
- `Mileage_CD_Eng_Off`, `Mileage_CD_Eng_On`, `Mileage_CI`, `Mileage_CS` - Components of Mileage_Tot

**Fuel consumption (4 variables):**
- `FC_Tot`, `FC_CD`, `FC_CI`, `FC_CS` - Fuel consumption directly related to energy

**Energy into battery (1 variable):**
- `EnergyIntoBattery_kWh` - Component of EnEl calculation

### Variables Kept (Safe to Use)

**Core variables:**
- `mass`, `aer`, `eds` (EDSpel - distance-based, NOT energy-based) ✅

**Type-approval values (OK - not real-world):**
- `TA_CO2`, `TA_FC`, `TA_EC` - Type-approval values, not derived from real-world data

**Vehicle characteristics:**
- Engine power, battery capacity, engine displacement
- Vehicle dimensions (length, width, height)
- Registration year, max passengers, prices

**Categorical variables:**
- Fuel type, region, country, segment, OEM, Make, vehicle body

**Engineered features:**
- Ratios (power-to-weight, battery-to-weight, AER-to-mass)
- Interactions (EDS×AER, mass×AER, etc.)
- Polynomial terms (mass², AER², EDS²)
- Vehicle size metrics (volume, surface area)
- Country/region interactions

## Step 2: Multicollinearity Reduction

**Method:** VIF (Variance Inflation Factor) analysis
- VIF > 10 indicates severe multicollinearity
- VIF > 5 indicates moderate multicollinearity

**Process:**
1. Calculate VIF for all variables (after excluding circular)
2. Iteratively remove variable with highest VIF
3. **Exception:** Always keep core variables (`mass`, `aer`, `eds`) even if high VIF
4. Continue until max VIF ≤ 10 or max iterations reached

## Final Selected Variables (27 variables)

**Core variables (3):**
- `mass`, `aer`, `eds`

**Vehicle characteristics (8):**
- `battery_capacity`, `engine_displacement`
- `vehicle_length`, `vehicle_width`, `vehicle_height`
- `registration_year`, `max_passengers`, `prices`

**Type-approval (1):**
- `ta_ec` (Type-approval energy consumption)

**Categorical numeric (7):**
- `fuel_type_numeric`, `region_numeric`, `segment_numeric`
- `oem_numeric`, `make_numeric`, `vehicle_body_numeric`

**Engineered features (8):**
- `power_to_weight`, `range_efficiency`
- `aer_squared`, `eds_squared`
- `power_aer_interaction`, `power_eds_interaction`
- `country_mass_interaction`, `country_aer_interaction`, `country_eds_interaction`

**VIF Statistics:**
- Max VIF: 42.82 (for `mass` - kept as core variable)
- Mean VIF: 10.35
- Variables with VIF > 10: 8 (mostly core variables and interactions)

## Application to All Models

**These 27 variables should be used for:**
- ✅ Linear Model
- ✅ Random Forest
- ✅ XGBoost/GBM
- ✅ LightGBM
- ✅ CatBoost
- ✅ GAM
- ✅ Neural Network
- ✅ Ensemble Meta-Learner

**Rationale:**
- Tree-based methods (RF, XGBoost) can handle multicollinearity better, but using the same variables ensures fair comparison
- Linear models require low multicollinearity for stable coefficients
- Consistent variable sets enable meaningful model comparison

## Files Generated

- `tables/circular_variables_list.csv` - List of excluded circular variables
- `tables/final_selected_variables_CLEAN.csv` - Final 27 selected variables
- `tables/variable_selection_multicollinearity.csv` - Comparison results

## Usage

**To use these variables in any model script:**
```r
# Load selected variables
selected_vars <- read_csv("tables/final_selected_variables_CLEAN.csv")$Variable

# Filter data to selected variables
model_data <- train_data %>% dplyr::select(total_energy, all_of(selected_vars))
```

## Notes

- **EDS used:** `eds` (EDSpel - distance-based) is OK to use. `EDSen` (energy-based) is excluded as circular.
- **Type-approval values:** TA_CO2, TA_FC, TA_EC are kept as they're not derived from real-world data.
- **Mileage:** All mileage variables excluded as they're used in the energy calculation.
- **Mass:** Kept despite high VIF (42.82) as it's a core variable. Interactions with mass are also included.







