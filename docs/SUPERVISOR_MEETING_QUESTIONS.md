# Questions for Supervisor Meeting - Paper A Progress Discussion

**Date:** [Meeting Date]  
**Prepared by:** Markos A. Ktistakis  
**Paper:** "The real-world energy use and electric driving share of plug-in hybrid vehicles in Europe"

---

## Overview

This document contains questions organized by category to guide discussion with supervisors about:
- Methodological decisions and interpretations
- Policy implications and messaging
- Paper structure and presentation
- Future work directions
- Publication strategy

**Current Paper Status:**
- ✅ All analysis complete (26 clean variables, 5 models: Linear, RF, XGBoost, Neural Network, GAM, Ensemble)
- ✅ 30+ figures and 16 tables generated
- ✅ All sections written
- ⏳ Final review and publication decisions needed

---

## 1. METHODOLOGICAL QUESTIONS

### 1.1 Variable Selection and Model Specification

**Q1.1:** We identified 25 "circular variables" (e.g., RW_CO2, mileage_tot, gap_pct) that are derived from or directly related to the outcome variable (total_energy). We excluded these and used 26 clean variables for the main analysis, achieving 56-74% test R². The 44-variable model (including circular variables) achieved 91.88% R² but is scientifically problematic. **Should we:**
- **A)** Keep 26 clean variables in main paper (current approach) - more scientifically rigorous but lower R²
- **B)** Present both (26 clean in main, 44 in appendix) - shows impact of variable selection
- **C)** Use a different variable selection approach?

**Q1.2:** We used country as a temperature proxy (country interactions with mass, AER, EDS) because actual temperature data wasn't available. **Is this approach acceptable, or should we:**
- **A)** Try to obtain actual temperature/climate data?
- **B)** Remove country interactions and acknowledge this limitation?
- **C)** Keep current approach but strengthen the justification?

**Q1.3:** The simple linear model (3 variables: mass, AER, region) showed mass dominance (97.5% importance), but advanced models with 26 clean variables show region (73%), engineered features (30-37%), and EDS (28%) as most important. **How should we present this evolution?**
- **A)** Emphasize that simple models are misleading (model specification artifact)
- **B)** Present both as a methodological progression story
- **C)** De-emphasize the simple model results?

### 1.2 Model Comparison and Selection

**Q1.4:** We compared 5 models (Linear, Random Forest, XGBoost, Neural Network, GAM) plus an Ensemble. XGBoost performs best (73.71% test R²), but GAM is more interpretable (64.31% test R²). **For the main paper, should we:**
- **A)** Focus on XGBoost as the best-performing model?
- **B)** Emphasize the Ensemble (73.54% R²) as most robust?
- **C)** Present all models equally and let readers choose?

**Q1.5:** We achieved 26-36% unexplained variance even with advanced models. **Should we:**
- **A)** Acknowledge this as expected (driving patterns, charging behavior not captured)?
- **B)** Try additional feature engineering or data sources?
- **C)** Frame it as a limitation that future work should address?

### 1.3 Statistical Rigor

**Q1.6:** We didn't extract bootstrap confidence intervals for LMG variable importance due to computational constraints. **Is this acceptable, or should we:**
- **A)** Add uncertainty quantification (even if computationally expensive)?
- **B)** Use alternative methods (e.g., permutation importance)?
- **C)** Acknowledge as limitation and proceed?

**Q1.7:** We used 80/20 train/test split with seed=42 for reproducibility. **Should we:**
- **A)** Add cross-validation for more robust estimates?
- **B)** Use different split ratios?
- **C)** Keep current approach (standard and reproducible)?

---

## 2. INTERPRETATION AND MESSAGING QUESTIONS

### 2.1 Key Findings Presentation

**Q2.1:** Our main finding is that real-world EDS (30.5% mean) is substantially lower than regulatory Utility Factors (50-70%). **How strongly should we emphasize this policy critique?**
- **A)** Strong critique: "Utility Factors are systematically overestimated"
- **B)** Moderate: "Real-world EDS is lower than assumed, suggesting Utility Factors may need revision"
- **C)** Neutral: "We observe lower EDS than regulatory assumptions"

**Q2.2:** Variable importance shows region (73%) is most important, followed by engineered features (30-37%) and EDS (28%). **What is the policy message?**
- **A)** Regional policies (charging infrastructure, climate) are critical
- **B)** Vehicle design (engineered features) matters but context (region) matters more
- **C)** Multiple factors interact - no single silver bullet

**Q2.3:** Energy consumption (22.6 kWh/100 km) is higher than type-approval values. **Should we:**
- **A)** Calculate and present explicit "energy gaps" (like fuel consumption gaps)?
- **B)** Focus on absolute values and distributions?
- **C)** Compare to other powertrain technologies (BEV, HEV, ICE)?

### 2.2 Comparison with Literature

**Q2.4:** Our co-authored study (Suarez et al., 2025) found EDS accounts for 51% of CO₂ variance, while we find EDS accounts for 28% of energy variance. **How should we explain this difference?**
- **A)** Energy includes both ICE and electric, so EDS has less direct impact
- **B)** Different variable sets and methods
- **C)** Both - acknowledge methodological differences

**Q2.5:** Plötz & Gnann (2025) analyzed 1.4M PHEVs focusing on Utility Factors and fuel consumption. We analyze 265K PHEVs focusing on energy and EDS. **How should we position our contribution?**
- **A)** Complementary: different focus (energy vs fuel, EDS vs Utility Factors)
- **B)** Extension: we add energy analysis and variable importance
- **C)** Independent: different research questions

---

## 3. POLICY IMPLICATIONS QUESTIONS

### 3.1 Utility Factors and Regulations

**Q3.1:** Our findings suggest Utility Factors overestimate real-world EDS. **Should we:**
- **A)** Make explicit recommendations for revising Utility Factors?
- **B)** Present evidence and let policymakers decide?
- **C)** Focus on scientific findings without policy prescriptions?

**Q3.2:** We find region is the most important predictor (73% importance). **What are the policy implications?**
- **A)** Country-specific regulations or Utility Factors
- **B)** Infrastructure investment priorities
- **C)** Regional policy coordination needed

### 3.2 Consumer Information and Transparency

**Q3.3:** We show high variability in EDS (0-99.5%) and energy consumption. **Should we recommend:**
- **A)** Consumer information campaigns about real-world performance?
- **B)** Labeling requirements showing real-world ranges?
- **C)** Just present findings without recommendations?

---

## 4. PAPER STRUCTURE AND PRESENTATION QUESTIONS

### 4.1 Abstract and Introduction

**Q4.1:** The abstract mentions "26 clean variables" but also references "40+ predictors" in some places. **Should we:**
- **A)** Standardize to "26 clean variables" throughout?
- **B)** Mention both (26 clean in main, 44 in appendix)?
- **C)** Use "26 clean variables with advanced feature engineering"?

**Q4.2:** We have extensive EDS analysis (country-level, model-specific, battery capacity, etc.) - 10 analysis types, 16 tables, 19 figures. **Should we:**
- **A)** Keep all in main paper (comprehensive but long)?
- **B)** Move some to appendix or supplementary material?
- **C)** Focus on most policy-relevant findings in main paper?

### 4.2 Results Presentation

**Q4.3:** We have 30+ figures. **What's the right balance?**
- **A)** Keep all (comprehensive visualization)
- **B)** Reduce to essential figures (~15-20), move rest to appendix
- **C)** Focus on 6-8 key figures in main paper

**Q4.4:** Variable importance is presented using multiple methods (LMG, GAM, Random Forest). **Should we:**
- **A)** Present all methods equally?
- **B)** Focus on one primary method (LMG) with others as validation?
- **C)** Use ensemble/average of methods?

### 4.3 Discussion and Limitations

**Q4.5:** We acknowledge several limitations (no campaign data, no 2023 data, no seasonality, 26-36% unexplained variance). **Should we:**
- **A)** Strengthen limitations section with more detail?
- **B)** Add mitigation strategies for each limitation?
- **C)** Keep current level of detail?

**Q4.6:** The simple linear model (mass dominance, 97.5%) appears in early sections but contradicts advanced model results. **Should we:**
- **A)** Remove or heavily qualify simple model results?
- **B)** Use it as a "straw man" to show why advanced methods are needed?
- **C)** Present as methodological evolution story?

---

## 5. FUTURE WORK AND EXTENSIONS QUESTIONS

### 5.1 Immediate Extensions

**Q5.1:** We have 2021-2022 data but 2023 data may be available. **Should we:**
- **A)** Wait for 2023 data and update analysis?
- **B)** Submit current version and note 2023 data in future work?
- **C)** Do both: submit now, update later?

**Q5.2:** Campaign data (trip-level) were not available. **Should we:**
- **A)** Make obtaining campaign data a priority for future work?
- **B)** Acknowledge limitation and proceed?
- **C)** Try to obtain campaign data before submission?

### 5.2 Methodological Extensions

**Q5.3:** We could add:
- Well-to-wheel analysis (country-specific electricity mixes)
- Seasonality analysis (if date data becomes available)
- Driving pattern variables (speed, acceleration - if available)
- Charging infrastructure data

**Which should be priorities for:**
- **A)** This paper (if feasible)?
- **B)** Future work?
- **C)** Not necessary?

### 5.3 Publication Strategy

**Q5.4:** **What is the target journal/conference?**
- **A)** Transportation Research Part D (transport/environment)
- **B)** Applied Energy (energy focus)
- **C)** Science of the Total Environment (environmental focus)
- **D)** Other: _______________

**Q5.5:** **Timeline expectations:**
- **A)** Submit within 1-2 months?
- **B)** Take more time for additional analysis?
- **C)** Flexible timeline?

---

## 6. DATA AND TECHNICAL QUESTIONS

### 6.1 Data Quality and Representativeness

**Q6.1:** We removed 31,964 vehicles (11.22%) during cleaning, with systematic issues in some models (e.g., Porsche zero RW_EC reporting, JEEP COMPASS CS mode issues). **Should we:**
- **A)** Investigate these systematic issues further?
- **B)** Acknowledge in limitations and proceed?
- **C)** Contact manufacturers about data quality?

**Q6.2:** Step 5 (VFN validation filtering) was skipped because the validation file wasn't found. This step would have removed ~38,733 vehicles in the original analysis. **Should we:**
- **A)** Try to obtain the VFN validation file?
- **B)** Proceed without it (current approach)?
- **C)** Use alternative validation methods?

### 6.2 Energy Calculation Methodology

**Q6.3:** We use Markos's energy calculation constants (LHV: 11.53/11.86 kWh/L, ICE efficiencies: 30.7%/36.9%). **Are these:**
- **A)** Standard/accepted values?
- **B)** Should be justified more in the paper?
- **C)** Subject to sensitivity analysis?

**Q6.4:** Our energy values (22.6 kWh/100 km mean) differ from TRB 2025 study (60.3 kWh/100 km) due to different calculation methods. **Should we:**
- **A)** Add detailed comparison explaining differences?
- **B)** Just acknowledge different methods?
- **C)** Consider harmonizing methods?

---

## 7. CO-AUTHORSHIP AND COLLABORATION QUESTIONS

### 7.1 Co-Authorship

**Q7.1:** **Who should be co-authors?**
- Suarez et al. (2025) co-authors?
- DICE database providers?
- Campaign data contributors (if available)?
- Others: _______________

**Q7.2:** **What is the authorship order?**
- Markos as first author?
- Order based on contribution?
- Other arrangement?

### 7.2 Related Work Coordination

**Q7.3:** We reference Suarez et al. (2025) which is co-authored. **Should we:**
- **A)** Coordinate messaging to avoid contradictions?
- **B)** Ensure complementary rather than overlapping content?
- **C)** Independent papers are fine?

---

## 8. SPECIFIC AMBIGUITIES TO CLARIFY

### 8.1 Variable Importance Interpretation

**Q8.1:** Random Forest variable importance sums to >100% (e.g., region 73%, engineered features 30-37%, EDS 28% = 131-138%). **How should we interpret this?**
- **A)** These are relative importances, not percentages of variance
- **B)** Interactions cause overlap, so sums can exceed 100%
- **C)** Need to normalize or present differently

**Q8.2:** LMG method gives variance decomposition (sums to 100%), but GAM and RF give different metrics. **Should we:**
- **A)** Focus on LMG as primary (sums to 100%, interpretable)?
- **B)** Present all methods but note different metrics?
- **C)** Convert all to same scale for comparison?

### 8.2 Model Performance Interpretation

**Q8.3:** Our best model (XGBoost) achieves 73.71% test R². **Is this:**
- **A)** Excellent for this type of analysis?
- **B)** Good but room for improvement?
- **C)** Should be higher?

**Q8.4:** The gap between train and test R² is small (e.g., RF: 93.88% train vs 71.63% test). **Does this indicate:**
- **A)** Good generalization (small gap)?
- **B)** Overfitting (large absolute difference)?
- **C)** Both - need to interpret carefully?

### 8.3 EDS Analysis Scope

**Q8.5:** We have extensive EDS analysis (country-level, individual vehicle prediction, etc.). **Is this:**
- **A)** Appropriate scope for an energy consumption paper?
- **B)** Too much EDS focus (should be more energy-focused)?
- **C)** Right balance (EDS is key driver of energy)?

---

## 9. PUBLICATION-SPECIFIC QUESTIONS

### 9.1 Journal Requirements

**Q9.1:** **What are the target journal requirements?**
- Word count limits?
- Figure/table limits?
- Supplementary material policies?
- Data availability requirements?

**Q9.2:** **Should we prepare:**
- **A)** Supplementary material with all 30+ figures?
- **B)** Data/code repository (GitHub, Zenodo)?
- **C)** Both?

### 9.2 Review and Revision Strategy

**Q9.3:** **What is the review process?**
- **A)** Internal review first (supervisors, colleagues)?
- **B)** Direct submission?
- **C)** Preprint first (arXiv, ResearchGate)?

**Q9.4:** **Timeline for revisions:**
- **A)** Address all supervisor feedback before submission?
- **B)** Submit and revise based on reviewer feedback?
- **C)** Iterative: submit draft, get feedback, revise, then submit?

---

## 10. PRIORITY QUESTIONS (Must Ask)

**If time is limited, focus on these critical questions:**

1. **Q1.1** - Variable selection (26 clean vs 44 variables) - **CRITICAL for scientific validity**
2. **Q2.1** - Policy messaging strength (Utility Factor critique) - **CRITICAL for paper impact**
3. **Q4.6** - Simple model presentation (mass dominance) - **CRITICAL for consistency**
4. **Q5.4** - Target journal - **CRITICAL for submission strategy**
5. **Q7.1** - Co-authorship - **CRITICAL for ethics and collaboration**
6. **Q8.1** - Variable importance interpretation (>100% sums) - **CRITICAL for correct presentation**

---

## NOTES FOR MEETING

**Bring to meeting:**
- [ ] Paper draft (current version)
- [ ] Key figures (print or digital)
- [ ] Summary of main findings (1-2 pages)
- [ ] List of specific decisions needed (this document)

**After meeting:**
- [ ] Document all decisions made
- [ ] Update paper based on feedback
- [ ] Create action items with deadlines
- [ ] Schedule follow-up if needed

---

**Last Updated:** [Date]  
**Status:** Ready for supervisor meeting
