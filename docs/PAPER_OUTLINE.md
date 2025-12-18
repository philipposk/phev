# Paper A: Paper Outline and Structure

**Title:** "The real-world energy use and electric driving share of plug-in hybrid vehicles in Europe at vehicle and trip level"

**Authors:** Markos A. Ktistakis, ...

**Target Journal:** Energy, Transportation Research Part D, Applied Energy, or similar

**Status:** Analysis pipeline ready, awaiting data execution

---

## 1. Abstract (250 words)

### Key Points:
- First comprehensive fleet-level energy analysis of PHEVs in Europe (OBFCM 2021-2023)
- Direct EDS measurement from OBFCM (not derived from fuel consumption)
- Multi-scale analysis: fleet → vehicle → trip level
- Statistical rigor: LMG variable importance, uncertainty quantification, representativeness assessment
- Policy-relevant findings on real-world PHEV performance

### Main Results (to be filled after analysis):
- [Total energy consumption distributions]
- [EDS distributions and variability]
- [Key factors influencing energy use]
- [Fleet vs campaign comparison]

---

## 2. Introduction

### 2.1 Background
- PHEV market growth in Europe
- Policy context (CO₂ regulations, Utility Factors)
- Gap between type-approval and real-world performance

### 2.2 Research Gaps
- Limited fleet-level energy analysis (most studies focus on CO₂/FC)
- EDS typically derived from fuel consumption (not direct measurement)
- Lack of multi-scale integration (fleet + vehicle + trip)
- Insufficient statistical rigor in variable importance analysis

### 2.3 Objectives
1. Quantify real-world energy consumption distributions for PHEVs
2. Measure EDS directly from OBFCM data
3. Identify key factors influencing energy use (LMG method)
4. Validate fleet-level findings with detailed campaign data
5. Assess statistical representativeness and uncertainty

### 2.4 Paper Structure
[Standard structure overview]

---

## 3. Literature Review

### 3.1 PHEV Real-World Performance Studies
- ICCT 2022 (8,855 vehicles, EDS analysis)
- Mandev 2024 (32,770 vehicles, country-level differences)
- Plötz & Gnann 2025 (1.4M vehicles, OBFCM 2021-2023, UF analysis)
- Other key studies

### 3.2 Energy vs CO₂ Analysis
- Energy as comprehensive metric
- Well-to-wheel considerations
- Policy relevance

### 3.3 Variable Importance Methods
- LMG method (our contribution)
- Comparison with other methods (GAM, Random Forest)

### 3.4 Research Contributions
- First comprehensive fleet-level energy analysis
- Direct EDS from OBFCM
- LMG variable importance (unique in PHEV literature)
- Multi-scale validation

---

## 4. Data and Methods

### 4.1 Data Sources

#### 4.1.1 OBFCM 2021-2023
- **Source:** European Environment Agency (EEA)
- **Coverage:** 7.7M+ vehicles, 2021-2023
- **PHEVs:** [Number to be filled]
- **Variables:** Energy, EDS, mileage, technical characteristics
- **Data quality:** Pre-processed by EEA, additional cleaning applied

#### 4.1.2 Campaign Data
- **Golf PHEV Campaign:** 18 drivers, 1,127 trips, 27,148 km
- **Prius Campaign:** [Details to be filled]
- **Purpose:** Trip-level validation and detailed analysis

#### 4.1.3 DICE Database
- **Source:** EU CO₂ monitoring database
- **Purpose:** Technical vehicle characteristics (mass, AER, segment)

### 4.2 Energy Calculations

#### 4.2.1 Definitions
- **Total Energy [kWh/100 km]** = Electric Energy + ICE Energy
- **Electric Energy:** Grid energy × charging efficiency (85%)
- **ICE Energy:** Fuel consumption × density × LHV × ICE efficiency
  - Petrol: LHV = 11.53 kWh/L, efficiency = 30.7%
  - Diesel: LHV = 11.86 kWh/L, efficiency = 36.9%

#### 4.2.2 EDS Definition
- **EDS [%]** = (Distance_CD_engine_off / Distance_total) × 100
- Pure electric driving share (charge-depleting, engine off)

### 4.3 Statistical Methods

#### 4.3.1 Variable Importance (LMG Method)
- **Primary Method:** LMG (Lindeman, Merenda, Gold) decomposition
- **Purpose:** Quantify each variable's contribution to R²
- **Implementation:** R package `relaimpo`
- **Bootstrap:** 1000 iterations for confidence intervals

#### 4.3.2 Alternative Methods
- **GAMs:** Generalized Additive Models (mgcv package)
- **Random Forest:** For comparison and validation

#### 4.3.3 Representativeness Assessment
- Comparison with EU fleet statistics
- Propensity score matching (if needed)
- Uncertainty quantification

### 4.4 Data Cleaning
- PHEV identification: Powertrain == "P"
- Removal of problematic CS (charge-sustaining) values
- Outlier detection and removal
- Missing data handling

---

## 5. Results

### 5.1 Dataset Overview
- **Table 1:** Dataset overview (vehicles, years, countries, manufacturers)
- Sample sizes, coverage, representativeness

### 5.2 Energy Consumption Distributions
- **Figure 1:** Total energy distribution (OBFCM)
- **Table 2:** Summary statistics (mean, median, percentiles)
- Stratifications: mass, AER, registration year
- Key findings: [To be filled]

### 5.3 EDS Distributions
- **Figure 2:** EDS distribution (OBFCM)
- Variability and factors influencing EDS
- Comparison with literature (ICCT 2022, etc.)
- Key findings: [To be filled]

### 5.4 Energy vs EDS Relationship
- **Figure 3:** Energy vs EDS scatter plot
- GAM fit for relationship
- Color by AER
- Key findings: [To be filled]

### 5.5 Variable Importance Analysis
- **Figure 5:** LMG variable importance (bar chart with CIs)
- **Table 3:** Variable importance results
- Key factors: Mass, AER, Mileage, Region, etc.
- Comparison with GAM and Random Forest
- Key findings: [To be filled]

### 5.6 Fleet vs Campaign Comparison
- **Figure 4:** Boxplots comparing fleet and campaign data
- **Table 4:** Statistical comparison
- Validation of fleet-level findings
- Key findings: [To be filled]

### 5.7 Seasonality Effects
- **Figure 6:** Monthly energy and EDS trends
- Temperature effects (if data available)
- Key findings: [To be filled]

---

## 6. Discussion

### 6.1 Energy Consumption Patterns
- Comparison with type-approval values
- Factors driving high/low energy consumption
- Policy implications

### 6.2 EDS Variability
- Range of EDS values and drivers
- Comparison with regulatory Utility Factors
- Policy relevance

### 6.3 Variable Importance Insights
- Most important factors (from LMG analysis)
- Unexpected findings
- Methodological contributions

### 6.4 Multi-Scale Validation
- Agreement between fleet and campaign data
- Strengths and limitations of each approach
- Recommendations for future studies

### 6.5 Limitations
- Data representativeness
- Missing variables
- Methodological assumptions
- Temporal coverage (2021-2023)

### 6.6 Policy Implications
- Real-world vs type-approval gaps
- Utility Factor recommendations
- Energy policy considerations

---

## 7. Conclusions

### 7.1 Main Findings
1. [Key finding 1 - energy distributions]
2. [Key finding 2 - EDS patterns]
3. [Key finding 3 - variable importance]
4. [Key finding 4 - policy implications]

### 7.2 Contributions
- First comprehensive fleet-level energy analysis
- Direct EDS measurement methodology
- LMG variable importance application
- Multi-scale validation framework

### 7.3 Future Work
- OBFCM 2024 data (when available)
- Extended campaign analysis
- Well-to-wheel analysis
- Policy scenario modeling

---

## 8. Acknowledgments

- EEA for OBFCM data
- Co-authors and collaborators
- Funding sources

---

## 9. References

[To be compiled from literature review]

---

## Figures (6 must-have)

1. **Figure 1:** Total Energy Distribution (OBFCM) - Histogram with stratifications
2. **Figure 2:** EDS Distribution (OBFCM) - Histogram with stratifications
3. **Figure 3:** Energy vs EDS Relationship - Scatter plot with GAM fit, colored by AER
4. **Figure 4:** Fleet vs Campaign Comparison - Boxplots for energy and EDS
5. **Figure 5:** Variable Importance (LMG) - Bar chart with confidence intervals
6. **Figure 6:** Seasonality Effects - Monthly trends for energy and EDS

---

## Tables (4 must-have)

1. **Table 1:** Dataset Overview - Sample sizes, years, countries, manufacturers
2. **Table 2:** Summary Statistics - Mean, median, percentiles for key variables
3. **Table 3:** Variable Importance (LMG) - Contributions with confidence intervals
4. **Table 4:** Fleet vs Campaign Comparison - Statistical comparison

---

## Word Count Target

- Abstract: 250 words
- Introduction: 800-1000 words
- Literature Review: 1500-2000 words
- Methods: 1200-1500 words
- Results: 2000-2500 words
- Discussion: 1500-2000 words
- Conclusions: 400-500 words
- **Total: ~8000-10000 words** (typical for energy/transportation journals)

---

## Next Steps

1. ✅ Analysis pipeline created
2. ⏳ Extract and load OBFCM data
3. ⏳ Run complete analysis pipeline
4. ⏳ Generate all figures and tables
5. ⏳ Fill in results sections with actual findings
6. ⏳ Write full paper draft
7. ⏳ Review and revise
8. ⏳ Submit to target journal

---

**Last Updated:** December 2025  
**Status:** Ready for data execution and paper writing




