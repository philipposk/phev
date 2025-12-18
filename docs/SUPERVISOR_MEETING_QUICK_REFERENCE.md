# Quick Reference: Supervisor Meeting Questions

**One-page summary of critical questions for Markos's supervisor meeting**

---

## 🔴 CRITICAL DECISIONS NEEDED

### 1. Variable Selection (Q1.1)
**Issue:** 26 clean variables (56-74% R²) vs 44 variables including circular ones (91.88% R²)
**Question:** Use 26 clean (scientifically rigorous) or present both?
**Impact:** Core scientific validity of paper

### 2. Policy Messaging (Q2.1)
**Issue:** Real-world EDS (30.5%) much lower than Utility Factors (50-70%)
**Question:** How strongly to critique Utility Factors? Strong/moderate/neutral?
**Impact:** Paper's policy impact and tone

### 3. Simple Model Presentation (Q4.6)
**Issue:** Simple model shows mass dominance (97.5%), contradicts advanced models (region 73%, EDS 28%)
**Question:** Remove/qualify simple model or use as methodological evolution story?
**Impact:** Paper consistency and credibility

### 4. Target Journal (Q5.4)
**Question:** Transportation Research Part D / Applied Energy / Science of the Total Environment / Other?
**Impact:** Submission strategy, word count, figure limits

### 5. Co-Authorship (Q7.1)
**Question:** Who should be co-authors? (Suarez et al. collaborators, DICE providers, etc.)
**Impact:** Ethics, collaboration, paper positioning

### 6. Variable Importance Interpretation (Q8.1)
**Issue:** RF importance sums to >100% (region 73% + features 30-37% + EDS 28% = 131-138%)
**Question:** How to interpret and present this?
**Impact:** Correctness of results presentation

---

## 🟡 IMPORTANT CLARIFICATIONS

### Methodology
- **Country as temperature proxy:** Acceptable or need actual temperature data?
- **Bootstrap CIs for LMG:** Add uncertainty quantification or acknowledge limitation?
- **Unexplained variance (26-36%):** Expected limitation or try to reduce?

### Interpretation
- **Energy gaps:** Calculate explicit gaps (like fuel gaps) or focus on absolute values?
- **Comparison with Suarez et al. (2025):** How to explain EDS importance difference (51% CO₂ vs 28% energy)?
- **Model selection:** Focus on XGBoost (best, 73.71% R²) or Ensemble (robust, 73.54% R²)?

### Paper Structure
- **30+ figures:** Keep all, reduce to essentials, or move some to appendix?
- **EDS analysis scope:** Right balance or too much EDS focus for energy paper?
- **Abstract wording:** "26 clean variables" vs "40+ predictors" - standardize?

### Future Work
- **2023 data:** Wait and update, or submit current version?
- **Campaign data:** Priority for future work or try to obtain now?
- **Extensions:** Well-to-wheel, seasonality, driving patterns - priorities?

---

## 📊 KEY NUMBERS TO DISCUSS

- **Sample:** 265,603 PHEVs, 29 countries, 2021-2022
- **Energy:** 22.6 kWh/100 km mean (ICE: 16.5, Electric: 6.1)
- **EDS:** 30.5% mean (vs 50-70% Utility Factors)
- **Model Performance:** 56-74% test R² (26 clean variables)
- **Variable Importance:** Region 73%, Engineered features 30-37%, EDS 28%, Mass 31.7%
- **Data Cleaning:** 31,964 vehicles removed (11.22%)

---

## ✅ DECISIONS ALREADY MADE (Confirm with Supervisors)

- ✅ Using 26 clean variables for main analysis (excludes circular dependencies)
- ✅ 80/20 train/test split with seed=42 for reproducibility
- ✅ Multiple models compared (Linear, RF, XGBoost, Neural Network, GAM, Ensemble)
- ✅ Energy calculation using Markos's constants (LHV, ICE efficiencies)
- ✅ Comprehensive EDS analysis included (country-level, model-specific, etc.)

---

## 📝 MEETING PREPARATION CHECKLIST

- [ ] Read full questions document: `SUPERVISOR_MEETING_QUESTIONS.md`
- [ ] Print key figures (energy distribution, EDS distribution, variable importance)
- [ ] Prepare 1-2 page summary of main findings
- [ ] Bring paper draft (digital or printed)
- [ ] Note specific sections needing supervisor input
- [ ] Prepare to take notes on all decisions

---

## 🎯 MEETING OUTCOMES TO ACHIEVE

1. **Clarity on variable selection approach** (26 vs 44 variables)
2. **Agreement on policy messaging tone** (Utility Factor critique strength)
3. **Decision on simple model presentation** (remove/qualify/keep)
4. **Target journal identified** (for submission strategy)
5. **Co-authorship confirmed** (who, order)
6. **Timeline established** (submission date, revision schedule)
7. **Action items documented** (what to do next, by when)

---

**Full detailed questions:** See `SUPERVISOR_MEETING_QUESTIONS.md`
