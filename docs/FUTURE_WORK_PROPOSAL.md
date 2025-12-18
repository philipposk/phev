# Future Work Proposals
**Date:** December 16, 2025  
**Purpose:** Discuss and prioritize future analysis directions

## Current Status

### Completed
- ✅ Comprehensive EDS-focused country-level analysis (10 analysis types)
- ✅ Maps generated (Figures 25-26)
- ✅ Temperature data merging fixed (using MS column)
- ✅ Country-level regression with reduced predictors (to avoid overfitting)

### Current Limitations

1. **Country-Level Regression:**
   - **Issue:** 29 countries with 26 predictors = severe overfitting risk
   - **Solution Implemented:** Reduced to 2-3 key predictors (region, battery, temperature)
   - **Rule of thumb:** Need 10-15 observations per predictor
   - **Current:** Model 1 (region + battery), Model 2 (region + temperature), Model 3 (region + battery + temperature)

2. **Model Re-runs:**
   - Random Forest (91.88% R²) uses 44 variables (includes circular variables)
   - Needs re-run with 26 clean variables for fair comparison
   - Other models (XGBoost, GAM, etc.) also need clean variable versions

## Future Work Proposals

### 1. Individual Vehicle-Level Analysis (High Priority) ⭐

**Rationale:** 
- Current country-level analysis (29 countries) is limited by small sample size
- Individual vehicle-level analysis (265,603 vehicles) provides much more statistical power
- Can use all 26 clean variables without overfitting concerns

**Proposed Analyses:**
- **EDS prediction models:** Predict EDS from vehicle characteristics, country, region
- **Energy consumption models:** Already done, but re-run with clean variables
- **Interaction effects:** Country × vehicle characteristics, Region × battery capacity
- **Hierarchical models:** Country-level random effects on individual vehicle models

**Expected Outcomes:**
- More robust statistical models (large sample size)
- Better understanding of individual vs. country-level effects
- Can validate country-level findings with individual-level data

**Implementation:**
- Use same 26 clean variables as main paper
- Apply best hyperparameters from comprehensive analysis
- Compare individual-level vs. country-level results

---

### 2. Temporal Analysis (Medium Priority)

**Rationale:**
- Current analysis uses cross-sectional data (2021-2023)
- Temporal trends could reveal:
  - Changes in EDS over time (infrastructure improvements)
  - Seasonal effects (temperature, charging behavior)
  - Policy impacts (if policy changes occurred during period)

**Proposed Analyses:**
- **Time series:** EDS trends by country/region over reporting periods
- **Seasonality:** Monthly/quarterly patterns in EDS and energy consumption
- **Policy impacts:** Before/after analysis if policy changes identified
- **Cohort effects:** Compare vehicles registered in different years

**Data Requirements:**
- OBFCM_ReportingPeriod variable (already available)
- Year/date information for vehicles
- Policy change dates (if available)

**Expected Outcomes:**
- Understanding of temporal dynamics
- Policy effectiveness assessment
- Seasonal adjustment factors

---

### 3. Charging Infrastructure Analysis (Medium Priority)

**Rationale:**
- Charging behavior (EnergyIntoBattery_kWh) shows strong correlation with EDS (r=0.47)
- Infrastructure availability likely drives charging behavior
- Temperature data includes charge_points variable

**Proposed Analyses:**
- **Infrastructure effects:** Charge points per country vs. EDS
- **Charging patterns:** Energy into battery patterns by country/region
- **Infrastructure × temperature:** Interaction between infrastructure and climate
- **Infrastructure × vehicle characteristics:** How infrastructure affects different vehicle types

**Data Available:**
- `temperatures 4_MK.xlsx` includes `charge_points` column
- `EnergyIntoBattery_kWh` in OBFCM data
- Country-level aggregation possible

**Expected Outcomes:**
- Quantify infrastructure impact on EDS
- Policy recommendations for infrastructure investment
- Regional infrastructure needs assessment

---

### 4. Vehicle Segment Deep Dive (Low Priority)

**Rationale:**
- Segment analysis shows interesting patterns (lower medium cars have higher EDS)
- Could explore segment-specific models and interactions

**Proposed Analyses:**
- **Segment-specific models:** Separate models for SUV, Sedan, Hatchback, etc.
- **Segment × region interactions:** How segment effects vary by region
- **Segment × battery interactions:** Optimal battery size by segment
- **Segment × charging behavior:** Charging patterns by vehicle type

**Expected Outcomes:**
- Segment-specific insights
- Design recommendations by segment
- Policy implications for different vehicle types

---

### 5. Model Comparison with Clean Variables (High Priority) ⭐

**Rationale:**
- Current Random Forest (91.88% R²) likely includes circular variables
- Need fair comparison across all models with same 26 clean variables
- Parameter transfer approach documented but needs validation

**Proposed Work:**
- **Re-run all models:** RF, XGBoost, LightGBM, CatBoost, GAM, NN, Ensemble
- **Use 26 clean variables:** From `tables/final_selected_variables_CLEAN.csv`
- **Apply parameter transfer:** Use best hyperparameters from 44-variable runs
- **Compare results:** Clean variables vs. 44 variables (in Appendix A)

**Expected Outcomes:**
- Scientifically valid model comparisons
- Realistic R² values (likely 55-75% range)
- Validation of parameter transfer approach

**Implementation Priority:** ⭐ **HIGH** - Needed for paper completion

---

### 6. Sensitivity Analysis (Low Priority)

**Rationale:**
- Understand robustness of findings
- Test assumptions (train/test split, variable selection, etc.)

**Proposed Analyses:**
- **Different train/test splits:** 70/30, 80/20, 90/10
- **Variable selection sensitivity:** Different VIF thresholds
- **Outlier analysis:** Impact of extreme values
- **Bootstrap confidence intervals:** For key estimates

**Expected Outcomes:**
- Robustness assessment
- Confidence in main findings
- Understanding of sensitivity to assumptions

---

### 7. Policy Simulation (Future Research)

**Rationale:**
- Models can be used for policy scenario analysis
- Predict EDS/energy consumption under different conditions

**Proposed Analyses:**
- **Infrastructure scenarios:** "What if" charge points doubled?
- **Battery size scenarios:** Impact of larger batteries on EDS
- **Regional policy scenarios:** Different policies by region
- **Fleet composition scenarios:** Impact of segment mix changes

**Expected Outcomes:**
- Policy impact predictions
- Cost-benefit analysis support
- Evidence-based policy recommendations

---

## Recommended Priority Order

### Phase 1 (Immediate - Paper Completion)
1. ⭐ **Model Re-runs with Clean Variables** (High Priority)
   - Needed for paper completion
   - Scientifically valid comparisons
   - Estimated time: 8-12 hours computation

2. ⭐ **Individual Vehicle-Level EDS Analysis** (High Priority)
   - Much more statistical power (265K vehicles vs. 29 countries)
   - Can use all 26 clean variables
   - Validates country-level findings
   - Estimated time: 4-6 hours computation + analysis

### Phase 2 (Short-term - Paper Enhancement)
3. **Temporal Analysis** (Medium Priority)
   - Adds dynamic dimension
   - Policy impact assessment
   - Estimated time: 2-4 hours analysis

4. **Charging Infrastructure Analysis** (Medium Priority)
   - Strong correlation already identified (r=0.47)
   - Policy-relevant findings
   - Estimated time: 2-3 hours analysis

### Phase 3 (Long-term - Future Research)
5. **Vehicle Segment Deep Dive** (Low Priority)
6. **Sensitivity Analysis** (Low Priority)
7. **Policy Simulation** (Future Research)

---

## Discussion Points

### 1. Statistical Power Considerations

**Country-Level (29 countries):**
- ✅ Good for descriptive statistics
- ✅ Good for regional comparisons (ANOVA)
- ⚠️ Limited for regression (max 2-3 predictors)
- ⚠️ Cannot use all 26 clean variables

**Individual Vehicle-Level (265,603 vehicles):**
- ✅ Excellent statistical power
- ✅ Can use all 26 clean variables
- ✅ Can model complex interactions
- ✅ Hierarchical models possible (country-level random effects)

**Recommendation:** Focus on individual vehicle-level analysis for modeling, use country-level for descriptive/exploratory analysis.

### 2. Variable Selection for Country-Level Regression

**Current Approach (Fixed):**
- Model 1: Region + Battery (2 predictors + region dummies)
- Model 2: Region + Temperature (if ≥20 countries have temp data)
- Model 3: Region + Battery + Temperature (if ≥20 countries have temp data)

**Rationale:**
- 29 countries / 6 parameters ≈ 4.8 observations per parameter (acceptable minimum)
- Region captures major geographic/climate/infrastructure differences
- Battery is key vehicle characteristic
- Temperature adds climate dimension

**Alternative Approaches:**
- Principal Component Analysis (PCA) to reduce dimensions
- Regularized regression (Ridge/Lasso) to handle many predictors
- Bayesian methods with informative priors

### 3. Parameter Transfer Validation

**Current Approach:**
- Use best hyperparameters from 44-variable runs
- Apply to 26-variable models
- Assumes hyperparameters generalize across variable sets

**Validation Needed:**
- Compare parameter transfer vs. re-tuning on clean variables
- If results differ significantly, may need re-tuning
- Document any differences in paper

---

## Questions for Discussion

1. **Priority:** Which analyses are most important for paper completion vs. future research?

2. **Individual vs. Country-Level:** Should we prioritize individual vehicle-level analysis for modeling, or focus on country-level descriptive analysis?

3. **Model Re-runs:** How urgent is re-running all models with clean variables? (Needed for paper completion)

4. **Temporal Analysis:** Is temporal/seasonal analysis important for this paper, or future work?

5. **Infrastructure Analysis:** Should we include charging infrastructure analysis in this paper, or save for future work?

6. **Parameter Transfer:** Should we validate parameter transfer approach, or assume it's valid?

---

**Next Steps:**
1. Discuss priorities with Markos
2. Implement Phase 1 analyses (model re-runs, individual-level EDS)
3. Update paper with new results
4. Plan Phase 2 analyses based on priorities






