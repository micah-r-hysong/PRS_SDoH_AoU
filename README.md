# PRS and Social Determinants of Health in All of Us

## Summary

This project explores two main questions 1) Does the association between PRS and disease vary by social environment? 2) Does jointly modeling genetic and social risk improve disease prediction? This question was assessed using diseases and PRSs selected by eMERGE https://doi.org/10.1038/s41591-024-02796-z. You can find the disease algorithms implemented in All of Us (AoU) here: https://github.com/micah-r-hysong/PRS_SDoH_analysis/tree/main 

Prior to this analysis, we conducted an extensive exploration of the Social Determinant of Health (SDoH) data available in AoU. Please see and cite: 

Hysong, M.R., Manning, A.K., Green, M.D. et al. Practical considerations for social determinant-based disease prediction in the All of Us research program. Commun. Health 1, 17 (2026). https://doi.org/10.1038/s44528-026-00018-1 

This repo details the curation of the SDoH variables used in this analysis, PRS calculation and PC mean and variance adjustment, evaluation of PRS-disease associations across SDoH, and the construction and external validation of a Polysocial Risk Score (PsRS). 

### Cohort Building
0000_demographics_WGS.ipynb loads in the demographic data table; cleans up the race and ethnicity variables; makes a more inclusive SexGender column that considers both sex assigned at birth and gender; makes an age_at_last_event (in the EHR) variable; adds genetically infered ancestry groups and genetic PCs; adds richer demographic data such as disability status, LGBTQIA+ identitiy status, income, education, military status, birthplace, and healthcare coverage. This notebook also filters participants to those with at least three entries over three years in the EHR to reduce data availability bias. In Version 8 (V8), this leads to a sample size of 135,611 with sufficient EHR data and WGS. 

### SDoH data curation 
Creation of individual-level semi-continuous 5-level education variable and percentage of the poverty threshold variables. The percentage of the poverty threshold variable was created by dividing the reported annual household income by the corresponding poverty threshold based on location (contiguous state vs Alaska vs Hawaii), size of household, and date of survey completion. This value was then multiplied by 100 and coded such that higher values indicate lower income and higher risk, resulting in the 'individual_poverty' variable. ACS data was also loaded in to get three digit zip code area-level measures. Read more about SDoH data curation at https://doi.org/10.1038/s44528-026-00018-1 

### PRS calculation and PC mean and variance adjustment
See https://github.com/micah-r-hysong/AoU_PRS_calc for workbench 2.0 version 

### Evaluation of PRS-disease associations across SDoH
Notebooks 014 through 025. 

### PsRS construction
030_out_of_fold_PsRS_joint_modeling_AUC.ipynb Disease-specific polysocial risk scores (PsRS) were constructed using an elastic net–regularized logistic regression model on individual poverty, individual education, and the seven area-level SDoH measures. An 80/20 training testing split was used with five-fold cross-validation. Out-of-fold predictions were pooled across all five folds, resulting in one independent out-of-sample prediction per individual for each model. This code performs a paired bootstrap comparison of out-of-fold (OOF) AUCs for the genetic and joint models. ORs for PsRS were also obtained. 

### PsRS external validation
A PsRS was also constructed using a full-data refit in 045_generate_PsRS_external_validation.ipynb. These weights were used for external validation as evaluated in 050_external_validation_analysis.ipynb. 






