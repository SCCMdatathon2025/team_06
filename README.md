# ICU Cohort Analysis & CLIF Data Format Implementation

This repository contains a comprehensive analysis of adult ICU patients using data converted from MIMIC-IV to the CLIF (Common Longitudinal ICU data Format) standardized format. The analysis creates a rich dataset suitable for federated research across multiple healthcare institutions.

## Overview

### Dataset Summary
- **Total ICU stays analyzed:** 47,048 stays
- **Unique patients:** 33,732 patients  
- **Unique hospitalizations:** 40,391 hospitalizations
- **Study population:** Adult patients (>18 years) with ICU stays ≥48 hours

### Key Features
The analysis pipeline enriches the base ICU cohort with:
- **Laboratory values:** Sodium and creatinine aggregations during ICU stay
- **Medication administration:** 20 medication categories (vasoactives, sedatives, paralytics)
- **Historical diagnoses:** 13 pre-existing conditions from 1-year ICD code lookback
- **Clinical assessments:** RASS and CAM-ICU scores during ICU stay

## CLIF Data Format

### What is CLIF?
CLIF (Common Longitudinal ICU data Format) is a standardized data framework designed to overcome barriers in multicenter critical care research. It was developed by a consortium of nine U.S. academic health systems to enable federated analytics and improve data accessibility.

### Key Benefits for Federated Analysis
- **Standardized structure:** Provides consistent longitudinal data format across institutions
- **Harmonized vocabularies:** Incorporates standardized clinical terminologies
- **Multi-site compatibility:** Enables analysis of patient data across different healthcare systems
- **Reproducible research:** Facilitates collaboration among critical care researchers
- **Language mapping support:** Allows sites with different patient language documentation to participate

### MIMIC-IV to CLIF Conversion
Our dataset represents MIMIC-IV data converted to CLIF format v2.0.0, enabling:
- Standardized patient identification and longitudinal tracking
- Consistent medication categorization and dosing
- Harmonized laboratory value representation
- Unified assessment scoring systems

## Dataset Schema

### Core Tables Used
- **`clif_adt`:** ICU admission/discharge/transfer data
- **`clif_hospitalization`:** Hospital admission details
- **`clif_patient`:** Patient demographics
- **`clif_labs`:** Laboratory results
- **`clif_medication_admin_continuous`:** Continuous medication administration
- **`clif_patient_assessments`:** Clinical assessment scores
- **`diagnoses_icd`:** ICD diagnosis codes (mapped to CLIF format)

### Output Dataset Features (78 columns)

#### Demographics (7 columns)
- Age at admission, sex, race, ethnicity, language
- English speaker indicator for language analysis

#### ICU Characteristics (6 columns)  
- Location type, admission/discharge times, duration
- Unique stay identifier for longitudinal tracking

#### Laboratory Data (10 columns)
- Sodium: mean, median, min, max, count (99.7% coverage)
- Creatinine: mean, median, min, max, count (99.7% coverage)

#### Medication Administration (20 columns)
Boolean indicators for medication categories:
- **Vasoactives:** norepinephrine (26.5%), phenylephrine (25.0%), vasopressin (9.6%)
- **Sedatives:** propofol (40.9%), fentanyl (25.9%), dexmedetomidine (14.7%)
- **Paralytics:** cisatracurium (3.3%), rocuronium (0.6%), vecuronium (0.1%)

#### Historical Conditions (13 columns)
1-year ICD code lookback for:
- **Substance disorders:** alcohol (2.51%), opioid (0.57%), cocaine (0.25%)
- **Neurological:** stroke (2.32%), dementia (0.97%), Alzheimer's (0.15%)
- **Psychiatric:** schizophrenia (0.62%)
- **Sensory impairments:** deafness (0.74%), blindness (0.71%)

#### Clinical Assessments (22 columns)
- **RASS scores:** min, max, mean, median, count (86.7% coverage)
- **CAM-ICU results:** detailed breakdown by assessment components (76.9% coverage)

## Key Findings

### Population Characteristics
- **Age:** 65.4 ± 16.0 years
- **Sex:** 57.2% male, 42.8% female
- **Language:** 89.7% English speakers
- **Duration:** Median 89 hours (IQR: 63-149 hours)

### ICU Distribution
1. Surgical ICU: 27.9% (13,129 stays)
2. Medical ICU: 22.5% (10,568 stays)
3. CVICU: 17.6% (8,284 stays)
4. General ICU: 14.9% (7,030 stays)
5. Cardiac ICU: 12.7% (5,998 stays)
6. Neuro ICU: 4.3% (2,039 stays)

### Clinical Complexity
- **Multiple conditions:** 7.5% have ≥1 historical condition
- **High medication use:** 58.4% received tracked medications
- **Frequent monitoring:** 86.7% have RASS assessments

## Files

### Analysis Notebook
- **`icu_cohort_analysis_complete.ipynb`:** Complete analysis pipeline with data processing, validation, and exploratory analysis

### Output Files
- **`icu_cohort_complete.parquet`:** Final dataset in Parquet format
- **`icu_cohort_complete.csv`:** Final dataset in CSV format

### Source Data (CLIF format)
- `clif_adt.parquet` - ICU location data
- `clif_hospitalization.parquet` - Hospital admission data  
- `clif_patient.parquet` - Patient demographics
- `clif_labs.parquet` - Laboratory results
- `clif_medication_admin_continuous.parquet` - Medication data
- `clif_patient_assessments.parquet` - Clinical assessments
- `diagnoses_icd.csv.gz` - ICD diagnosis codes

## Federated Research Applications

This CLIF-formatted dataset enables:

### Multi-site Studies
- Standardized variable definitions across institutions
- Consistent inclusion/exclusion criteria
- Harmonized outcome measures

### Language-specific Research
- Analysis of care patterns by patient language
- Investigation of communication barriers in critical care
- Development of language-appropriate interventions

### Quality Improvement
- Benchmarking across different ICU types
- Medication usage pattern analysis
- Assessment frequency optimization

### Predictive Modeling
- Development of generalizable risk prediction models
- Validation across diverse patient populations
- Real-time decision support systems

## Technical Implementation

### Processing Pipeline
1. **Cohort Creation:** Adult ICU stays ≥48 hours
2. **Data Enrichment:** Laboratory, medication, and assessment data
3. **Historical Analysis:** 1-year diagnosis lookback
4. **Quality Validation:** Data completeness and consistency checks
5. **Standardization:** CLIF format compliance

### Data Quality Metrics
- **Completeness:** >99% for core clinical variables
- **Consistency:** Standardized coding across all variables
- **Validity:** Range checks and clinical logic validation
- **Uniqueness:** No duplicate stays in final dataset

## Usage

The dataset supports various research questions:
- ICU outcomes by patient characteristics
- Medication effectiveness studies
- Delirium and sedation research
- Health disparities analysis
- Quality of care assessments

## CLIF Resources

For more information about CLIF:
- **Official website:** https://clif-consortium.github.io/website/
- **Current version:** 2.0.0
- **Documentation:** Comprehensive format specifications and implementation guides
- **Research applications:** Published studies and collaborative opportunities

## Dependencies

- Python 3.8+
- pandas, numpy, matplotlib, seaborn
- DuckDB for data processing
- Jupyter notebooks for analysis

---

*This analysis demonstrates the power of standardized data formats like CLIF for enabling sophisticated, multi-institutional critical care research while maintaining data quality and consistency.*
