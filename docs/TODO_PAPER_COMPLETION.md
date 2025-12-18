# TODO: Paper Completion Checklist

**Date Created:** December 17, 2025  
**Status:** Active - Review and update needed

---

## 🔴 HIGH PRIORITY - Critical for Publication

### 1. Introduction & Background Alignment with Results

#### 1.1 Abstract Updates
- [ ] **Update Abstract line 14:** Currently says "71-80% test R² (ensemble meta-learner)" - **NEEDS UPDATE** once LightGBM, CatBoost, and Ensemble results are available
  - Current: "achieving 71-80% test R² (ensemble meta-learner)"
  - **Action:** Update with actual ensemble result once script completes
  - **Note:** Keep range if ensemble not yet run, but specify "up to X% with ensemble"

- [ ] **Verify Abstract mentions correct variable count:** Currently says "40+ predictors" - **CHECK** if this should be "26 clean variables" in main text
  - **Current:** "advanced feature engineering (40+ predictors including country as temperature proxy..."
  - **Action:** Consider clarifying: "26 clean variables (excluding circular dependencies) with advanced feature engineering..."
  - **Decision needed:** Should abstract mention both 26 clean (main) and 44 (appendix) or just 26 clean?

#### 1.2 Introduction Section 1.1-1.4
- [ ] **Section 1.4 Significance (line 119):** Currently says "achieving 71-80% test R²" - **UPDATE** with actual results
  - **Action:** Replace with specific results: "achieving 71.63% (Random Forest), 73.71% (XGBoost), 73.22% (Neural Network), and up to X% (Ensemble) test R²"

- [ ] **Section 1.4 (line 120):** Says "40+ predictors" - **CLARIFY** variable set
  - **Action:** Add note: "using 26 clean variables (excluding circular dependencies) in main analysis, with 44-variable results provided in Appendix A for comparison"

- [ ] **Section 1.4 (line 128):** Mentions "Mass-based regulation insights" with "97.5% of explained variance" - **UPDATE** 
  - **Current:** "The finding that vehicle mass dominates energy consumption (97.5% of explained variance)"
  - **Action:** This is from simple linear model (artifact). Update to: "While simple linear models suggest mass dominance (97.5%), advanced models with clean variables reveal more balanced importance, with region, engineered features, and EDS being key predictors. See Section 4.5.4 for discussion of model specification artifacts."
  - **Comment for Markos:** Consider removing or heavily qualifying this statement - it's misleading without context

#### 1.3 Background Section 1.2
- [ ] **Line 42:** Mentions TRB 2025 study with different energy calculation - **VERIFY** this comparison is still accurate
  - **Action:** Check if energy values are correctly compared (22.6 vs 60.3 kWh/100 km)

- [ ] **Line 46:** Mentions Suarez et al. (2025) finding "EDS accounts for 51% of explained variance in CO₂" - **VERIFY** this aligns with our energy findings
  - **Action:** Ensure consistency - we find EDS important for energy, but mass also matters

---

### 2. Methods Section - Equations and Completeness

#### 2.1 Energy Calculation Equations (Section 3.2.1)
- [x] **Equations present:** Lines 317-333 have energy calculation equations - **GOOD**
- [ ] **Add equation numbering:** Equations should be numbered for reference
  - **Action:** Add equation numbers: (1), (2), (3) etc.
  - **Example:** Change `\[E_{tot} = E_{ICE} + E_{el}\]` to `\[E_{tot} = E_{ICE} + E_{el} \quad (1)\]`

#### 2.2 EDS Definition Equation (Section 3.2.2)
- [x] **Equation present:** Line 341 has EDS equation - **GOOD**
- [ ] **Add equation number:** Number this equation

#### 2.3 Statistical Metrics Equations (Section 3.3.3)
- [x] **R² definition:** Line 446 mentions "R² = 1 - (SS_res / SS_tot)" - **GOOD**
- [ ] **Add formal equations for all metrics:**
  - **Action:** Add numbered equations for:
    - R² = 1 - (SS_res / SS_tot) where SS_res = Σ(y_i - ŷ_i)², SS_tot = Σ(y_i - ȳ)²
    - Adjusted R² = 1 - [(1-R²)(n-1)/(n-p-1)] where n=sample size, p=number of predictors
    - RMSE = √[Σ(y_i - ŷ_i)²/n]
    - MAE = Σ|y_i - ŷ_i|/n
    - MAPE = (100/n) × Σ|(y_i - ŷ_i)/y_i|
  - **Location:** Section 3.3.3, after line 450

#### 2.4 Model-Specific Equations
- [ ] **GAM equation:** Add general GAM formulation
  - **Action:** Add: g(E[Y]) = β₀ + Σf_j(X_j) where f_j are smooth functions
  - **Location:** Section 3.3.2 or 4.5.2

- [ ] **Random Forest:** Add brief description of ensemble averaging
  - **Action:** Add: ŷ = (1/B)Σŷ_b where B is number of trees
  - **Location:** Section 3.3.2 or 4.5.3

- [ ] **Ensemble meta-learner:** Add equation for weighted combination
  - **Action:** Add: ŷ_ensemble = α₀ + Σα_j × ŷ_j where α_j are learned weights
  - **Location:** Section 4.5.6

---

### 3. Results Section - Update with Actual Results

#### 3.1 Model Performance Results (Section 4.5.6)
- [ ] **Table 5:** Currently shows LightGBM, CatBoost, Ensemble as "[Not available]" or "[Pending]"
  - **Action:** **WAIT FOR SCRIPT TO COMPLETE**, then update with actual results
  - **Priority:** HIGH - This is critical

- [ ] **Update text references:** All mentions of "71-80%" or "75-80%" need actual numbers
  - **Action:** Replace with specific results once available
  - **Locations to check:**
    - Abstract (line 14)
    - Section 1.4 (line 119)
    - Section 4.5.6 (line 1295)
    - Section 6 Conclusions (line 1295)

#### 3.2 Variable Importance Results
- [x] **Random Forest importance:** Section 4.5.3 has detailed importance rankings - **GOOD**
- [ ] **Verify consistency:** Check that importance values match between sections
  - **Action:** Cross-check Section 4.5.3 (lines 682-699) with Section 5.3 (lines 1173-1212)

---

### 4. Discussion Section - Update with Actual Results

#### 4.1 Section 5.2 (Electric Driving Share Policy Implications)
- [ ] **Line 1161:** Says "EDS is the most important factor (209% importance)" - **VERIFY**
  - **Action:** Check if this is from old 44-variable model or clean 26-variable model
  - **Current status:** Section 4.5.3 shows region (73%) as most important with 26 clean vars
  - **Action needed:** Update to reflect clean variable results: "Region (73% importance) and engineered features are most important, with EDS contributing substantially (28% importance)"

#### 4.2 Section 5.3 (Variable Importance: Mass Dominance)
- [ ] **Line 1175:** Says "vehicle mass accounts for 97.5% of explained variance" - **UPDATE**
  - **Current:** This is from simple linear model (artifact)
  - **Action:** Update to: "The simple linear model suggested mass dominance (97.5%), but this was a model specification artifact. Advanced models with clean variables reveal more balanced importance: region (73%), engineered features (30-37%), and EDS (28%) all contribute substantially."
  - **Comment for Markos:** This entire section (5.3) may need revision - it's based on outdated simple model results

#### 4.3 Section 5.4 (Comparison with Literature)
- [ ] **Line 1205:** Mentions "Random Forest model achieves similar performance (72.85% R²)" - **UPDATE**
  - **Action:** Update to "71.63% test R² with 26 clean variables"
  - **Action:** Update "EDS as most important (209% importance)" to reflect clean variable results

- [ ] **Line 1212:** Says "EDS accounts for 209% importance" - **UPDATE**
  - **Action:** Update to reflect clean variable results: "Region (73%), engineered features (30-37%), and EDS (28%) are key predictors"

#### 4.4 Section 5.6 (Implications for PHEV Design)
- [ ] **Line 1234:** Says "EDS dominance in energy consumption (209% importance)" - **UPDATE**
  - **Action:** Update to: "Region (73% importance) and engineered features are most important, with EDS contributing substantially (28% importance)"

- [ ] **Line 1236:** Says "Mass (44% importance)" - **VERIFY**
  - **Action:** Check Section 4.5.3 - shows mass at 31.7% with clean variables
  - **Action:** Update to "Mass (31.7% importance)"

- [ ] **Line 1238:** Says "AER (59% importance)" - **VERIFY**
  - **Action:** Check Section 4.5.3 - shows AER at 36.8% with clean variables
  - **Action:** Update to "AER (36.8% importance)"

- [ ] **Line 1240:** Says "Regional differences (119% importance)" - **VERIFY**
  - **Action:** Check Section 4.5.3 - shows region at 73% with clean variables
  - **Action:** Update to "Regional differences (73% importance)"

---

### 5. Conclusions Section - Update with Actual Results

#### 5.1 Section 6 Conclusions
- [ ] **Line 1295:** Says "test R² values of 71-80%" - **UPDATE** with specific results
  - **Action:** Replace with: "test R² values of 71.63% (Random Forest), 73.71% (XGBoost), 73.22% (Neural Network), 64.31% (GAM), and [X%] (Ensemble) with 26 clean variables"

- [ ] **Line 1295:** Says "ensemble meta-learner... typically achieves the highest performance (75-80% test R²)" - **UPDATE**
  - **Action:** Replace with actual ensemble result once available
  - **If not available:** Change to "ensemble meta-learner is expected to achieve the highest performance by combining diverse base models"

- [ ] **Line 1301:** Says "region is the most important predictor (73% importance)" - **VERIFY**
  - **Action:** This matches Section 4.5.3 - **GOOD**, but verify it's from clean variable model

---

## 🟡 MEDIUM PRIORITY - Important for Scientific Completeness

### 6. Methods Section - Additional Scientific Rigor

#### 6.1 Train/Test Split Details
- [ ] **Add train/test split details:** Currently mentioned but not detailed
  - **Action:** Add: "Data were split into training (80%) and test (20%) sets using stratified random sampling (seed=42) to ensure representative distribution of vehicle characteristics across splits"
  - **Location:** Section 3.3.3 or 4.5.6

#### 6.2 Cross-Validation Details
- [ ] **Add cross-validation details:** Mentioned for ensemble but not detailed
  - **Action:** Add: "For ensemble meta-learner, we used 5-fold cross-validation to generate out-of-fold predictions, preventing overfitting in the meta-learner"
  - **Location:** Section 4.5.6

#### 6.3 Hyperparameter Tuning Details
- [ ] **Add hyperparameter search space:** Currently mentions "systematic tuning" but not ranges
  - **Action:** Add table or text describing:
    - Random Forest: mtry ∈ {3,5,7,10,√p}, ntree ∈ {500,1000}, nodesize ∈ {1,5,10}
    - XGBoost: n.trees ∈ {500,1000,1500}, depth ∈ {4,6,8}, shrinkage ∈ {0.001,0.01,0.05}, minobs ∈ {5,10,20}
    - GAM: k ∈ {8,10,12} for smooth terms
    - Neural Network: size ∈ {10,20,30}, decay ∈ {0.001,0.01,0.1}
  - **Location:** Section 3.5.4 or 4.5.6

#### 6.4 Variable Selection Methodology
- [ ] **Add VIF threshold details:** Currently mentions "VIF-based selection" but not thresholds
  - **Action:** Add: "Variables with VIF > 10 were considered for removal, with mean VIF = 10.35 and max VIF = 42.82 (mass) in final 26-variable set"
  - **Location:** Section 3.5.5

#### 6.5 Circular Variable Exclusion Rationale
- [x] **Present:** Section 3.5.5 describes circular variable exclusion - **GOOD**
- [ ] **Add to Methods section:** Consider adding brief summary in Section 3.3.1
  - **Action:** Add note: "Circular variables (derived from outcome) were excluded - see Section 3.5.5 for complete list"

---

### 7. Results Section - Additional Details

#### 7.1 Confidence Intervals
- [ ] **Add uncertainty quantification:** Currently missing for most results
  - **Action:** Add 95% confidence intervals for:
    - Mean energy consumption (22.6 ± X kWh/100 km)
    - Mean EDS (30.5 ± X %)
    - Model R² values (if possible through bootstrap)
  - **Location:** Section 4.2, 4.3, 4.5.6

#### 7.2 Model Comparison Statistical Tests
- [ ] **Add model comparison tests:** Currently just reports R² differences
  - **Action:** Consider adding:
    - Paired t-tests for model predictions
    - Diebold-Mariano tests for forecast accuracy
    - Or note: "Model comparison based on test set performance metrics"
  - **Location:** Section 4.5.6

#### 7.3 Residual Analysis Details
- [x] **Present:** Section 4.5.5 has residual analysis - **GOOD**
- [ ] **Add statistical tests:** Consider adding:
  - Shapiro-Wilk test for normality
  - Breusch-Pagan test for heteroscedasticity
  - Or note: "Visual inspection suggests approximate normality and homoscedasticity"
  - **Location:** Section 4.5.5

---

### 8. Discussion Section - Additional Scientific Context

#### 8.1 Model Interpretation
- [ ] **Add discussion of model limitations:** Currently in Section 5.5 but could be expanded
  - **Action:** Add discussion of:
    - Why 28% variance remains unexplained
    - What factors might explain remaining variance
    - Limitations of fleet-level vs trip-level data
  - **Location:** Section 5.5 (expand existing)

#### 8.2 Comparison with Type-Approval
- [ ] **Add quantitative gap analysis:** Currently mentions gap but doesn't quantify
  - **Action:** Add: "Real-world energy consumption (22.6 kWh/100 km) exceeds type-approval values by approximately X% (type-approval typically 15-20 kWh/100 km)"
  - **Location:** Section 5.1 or 4.2.1

---

## 🟢 LOW PRIORITY - Nice to Have

### 9. Additional Scientific Elements

#### 9.1 Supplementary Materials
- [ ] **Consider adding:**
  - Full variable importance tables for all models
  - Hyperparameter tuning results
  - Residual plots for all models
  - Sensitivity analysis (how results change with different train/test splits)
  - **Action:** Note in "Future Work" or create supplementary materials section

#### 9.2 Reproducibility
- [ ] **Add reproducibility statement:**
  - **Action:** Add: "All analysis code, data processing scripts, and model configurations are available at [repository URL] or upon request"
  - **Location:** Section 3 or Acknowledgments

#### 9.3 Data Availability
- [ ] **Add data availability statement:**
  - **Action:** Add: "OBFCM data are available from the European Environment Agency (EEA) upon request. Processed datasets and analysis results are available from the authors."
  - **Location:** Section 3.1 or Acknowledgments

---

## 📋 COMMENTS FOR MARKOS - Things to Review/Decide

### Items That May Need Removal or Major Revision

1. **Section 1.4 (line 128) - Mass-based regulation insights:**
   - **Current:** "The finding that vehicle mass dominates energy consumption (97.5% of explained variance)"
   - **Issue:** This is from simple linear model (artifact), not representative of true relationships
   - **Recommendation:** Either remove entirely or heavily qualify with explanation of model specification artifact
   - **Action needed:** Markos to decide if this should be removed or revised

2. **Section 5.3 - Variable Importance: Mass Dominance:**
   - **Current:** Entire section based on simple linear model finding (97.5% mass)
   - **Issue:** This is outdated and contradicts advanced model results
   - **Recommendation:** Revise to focus on advanced model results (region, engineered features, EDS)
   - **Action needed:** Markos to review and revise this section

3. **Abstract mentions "40+ predictors":**
   - **Issue:** Main paper uses 26 clean variables, 44 variables are in Appendix
   - **Recommendation:** Clarify in abstract: "26 clean variables (excluding circular dependencies) with advanced feature engineering"
   - **Action needed:** Markos to decide on abstract wording

### New References That May Be Needed

1. **LightGBM method:**
   - **Action:** Add reference if LightGBM results are included
   - **Potential:** Ke et al. (2017) "LightGBM: A Highly Efficient Gradient Boosting Decision Tree"

2. **CatBoost method:**
   - **Action:** Add reference if CatBoost results are included
   - **Potential:** Prokhorenkova et al. (2018) "CatBoost: unbiased boosting with categorical features"

3. **Ensemble methods:**
   - **Action:** Add reference for ensemble meta-learner approach
   - **Potential:** Wolpert (1992) "Stacked Generalization" or more recent ensemble review

4. **VIF (Variance Inflation Factor):**
   - **Action:** Add reference for VIF-based variable selection
   - **Potential:** O'Brien (2007) "A Caution Regarding Rules of Thumb for VIF"

5. **Adjusted R²:**
   - **Action:** Add reference if not already cited
   - **Potential:** Already standard, but could cite original work

### Other Scientific Completeness Items

1. **Effect sizes:**
   - **Consider adding:** Cohen's d or similar for comparing model improvements
   - **Location:** Section 4.5.6

2. **Model diagnostics:**
   - **Consider adding:** AIC/BIC for model comparison (if applicable)
   - **Location:** Section 4.5.6

3. **Sensitivity analysis:**
   - **Consider adding:** How results change with different train/test splits or random seeds
   - **Location:** Section 5.5 (Limitations) or Future Work

4. **Cross-validation results:**
   - **Consider adding:** K-fold CV results in addition to train/test split
   - **Location:** Section 4.5.6

---

## ✅ COMPLETED ITEMS

- [x] Energy calculation equations present (Section 3.2.1)
- [x] EDS definition equation present (Section 3.2.2)
- [x] Basic metric definitions present (Section 3.3.3)
- [x] Circular variable exclusion documented (Section 3.5.5)
- [x] Residual analysis present (Section 4.5.5)
- [x] Variable importance results documented (Section 4.5.3)
- [x] Model comparison table structure in place (Table 5)

---

## 📝 NOTES

- **Script Status:** LightGBM, CatBoost, and Ensemble models are currently running. Once complete, update Table 5 and all text references.
- **Consistency Check:** After all updates, perform final consistency check to ensure:
  - All R² values match between sections
  - All variable importance values match
  - All variable counts are correct (26 clean vs 44)
  - All model names and methods are consistent

---

**Last Updated:** December 17, 2025  
**Next Review:** After script completion and results update






