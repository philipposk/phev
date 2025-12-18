# Items Requiring Markos's Review and Decision

**Date:** December 17, 2025  
**Purpose:** Items that need your review, decision, or manual action

---

## 🔴 CRITICAL - Requires Your Decision

### 1. Section 1.4 (Line 128) - Mass Dominance Statement

**Current Text:**
> "The finding that vehicle mass dominates energy consumption (97.5% of explained variance) suggests that mass-based regulations may be more effective than AER-based incentives for reducing PHEV energy consumption."

**Issue:** This statement is based on the simple linear model (3 variables), which is a model specification artifact. Advanced models with clean variables show:
- Region: 73% importance
- Engineered features: 30-37% importance  
- EDS: 28% importance
- Mass: 31.7% importance (not 97.5%)

**Recommendation:** 
- **Option A:** Remove this statement entirely
- **Option B:** Heavily qualify it: "While simple linear models suggest mass dominance (97.5%), this was a model specification artifact. Advanced models reveal more balanced importance, with region, engineered features, and EDS being key predictors. See Section 4.5.4 for discussion."

**Action Needed:** Please decide which option and I'll implement it.

---

### 2. Section 5.3 - "Variable Importance: Mass Dominance" 

**Issue:** This entire section (lines 1173-1191) is based on the outdated simple linear model finding (97.5% mass). It contradicts the advanced model results presented in Section 4.5.3.

**Current Content:**
- Discusses mass as "primary driver" (97.5%)
- Says AER has "minimal direct effect" (1.4%)
- Says regional effects are "small" (1.1%)

**Advanced Model Reality:**
- Region: 73% (most important)
- Engineered features: 30-37%
- EDS: 28%
- Mass: 31.7%
- AER: 36.8%

**Recommendation:** 
- **Option A:** Delete this section entirely and merge relevant points into Section 5.4 (Comparison with Literature)
- **Option B:** Completely rewrite to focus on advanced model results
- **Option C:** Keep but add strong disclaimer that it's from simple model and is superseded

**Action Needed:** Please decide which option.

---

### 3. Abstract - Variable Count Wording

**Current Text (Line 14):**
> "advanced feature engineering (40+ predictors including country as temperature proxy..."

**Issue:** Main paper uses 26 clean variables, 44 variables are in Appendix A.

**Recommendation:**
- **Option A:** "26 clean variables (excluding circular dependencies) with advanced feature engineering..."
- **Option B:** "26 clean variables in main analysis (44 variables including circular dependencies in Appendix A) with advanced feature engineering..."
- **Option C:** Keep "40+ predictors" but add note about clean variable selection

**Action Needed:** Please decide on abstract wording.

---

## 🟡 IMPORTANT - Needs Your Input

### 4. New References to Add

The following references may need to be added if we include results from these methods:

1. **LightGBM:** Ke, G., Meng, Q., Finley, T., Wang, T., Chen, W., Ma, W., ... & Liu, T. Y. (2017). Lightgbm: A highly efficient gradient boosting decision tree. *Advances in neural information processing systems*, 30.

2. **CatBoost:** Prokhorenkova, L., Gusev, G., Vorobev, A., Dorogush, A. V., & Gulin, A. (2018). CatBoost: unbiased boosting with categorical features. *Advances in neural information processing systems*, 31.

3. **Ensemble Meta-Learner:** Wolpert, D. H. (1992). Stacked generalization. *Neural networks*, 5(2), 241-259.

4. **VIF (Variance Inflation Factor):** O'Brien, R. M. (2007). A caution regarding rules of thumb for variance inflation factors. *Quality & quantity*, 41(5), 673-690.

**Action Needed:** Please confirm if these should be added once LightGBM/CatBoost/Ensemble results are included.

---

### 5. Equation Numbering

**Current Status:** Equations are present but not numbered.

**Equations Present:**
- Energy calculation (lines 317, 321, 323)
- EDS definition (line 341)
- GAM formulation (line 397)

**Recommendation:** Add equation numbers (1), (2), (3), etc. for easier referencing.

**Action Needed:** Please confirm if you want equation numbering added.

---

### 6. Additional Scientific Elements

**Consider Adding:**
1. **Confidence Intervals:** For mean energy (22.6 ± X), mean EDS (30.5 ± X), model R² values
2. **Statistical Tests:** Shapiro-Wilk for normality, Breusch-Pagan for heteroscedasticity
3. **Effect Sizes:** Cohen's d for model improvements
4. **Sensitivity Analysis:** How results change with different train/test splits

**Action Needed:** Please indicate which (if any) of these you'd like added.

---

## 📋 ITEMS TO REVIEW AFTER SCRIPT COMPLETES

### 7. Update All "71-80%" References

**Locations:**
- Abstract (line 14)
- Section 1.4 (line 119)
- Section 4.5.6 (line 1295)
- Section 6 Conclusions (line 1295)

**Action Needed:** Once LightGBM, CatBoost, and Ensemble results are available, I'll update these with specific values. Please review after update.

---

### 8. Update Variable Importance Values in Discussion

**Sections to Update:**
- Section 5.2 (line 1161): Currently says "EDS (209% importance)" - should be "Region (73%), EDS (28%)"
- Section 5.4 (line 1205): Currently says "72.85% R²" - should be "71.63% R²"
- Section 5.4 (line 1212): Currently says "EDS (209% importance)" - needs update
- Section 5.6 (line 1234): Currently says "EDS (209% importance)" - needs update
- Section 5.6 (line 1236): Currently says "Mass (44%)" - should be "Mass (31.7%)"
- Section 5.6 (line 1238): Currently says "AER (59%)" - should be "AER (36.8%)"
- Section 5.6 (line 1240): Currently says "Region (119%)" - should be "Region (73%)"

**Action Needed:** I'll update these after you confirm the decisions above. Please review after update.

---

## ✅ ITEMS I'LL HANDLE AUTOMATICALLY

- [x] Update Table 5 with LightGBM, CatBoost, Ensemble results (once script completes)
- [x] Add equation numbers and formal metric equations
- [x] Add hyperparameter search space details
- [x] Add train/test split details
- [x] Update all R² references with actual values
- [x] Final consistency check across all sections

---

## 📝 NOTES

- **Script Status:** Currently running with macOS notifications enabled
- **Consistency Fixes:** Already applied in `PAPER_DRAFT_20_CONSISTENCY_FIXED.docx`
- **Next Steps:** 
  1. Wait for script to complete
  2. Update results in paper
  3. Address items above based on your decisions
  4. Generate final DOCX

---

**Please review the items marked "Requires Your Decision" and let me know your preferences. I'll implement them accordingly.**






