# ADataViewer

Exploring the Alzheimer's Disease Data Landscape

# Artifacts
[![DOI](https://zenodo.org/badge/417242404.svg)](https://zenodo.org/badge/latestdoi/417242404)


## Summary statistics

* The summary statistics were computed [here](/quantiles) (quantiles) and [here](/means) (mean)
    * There are 4 distinct scripts that are used to compute the summary statistics
    * Each script is dedicated to select a subset of participants based on a diagnostic group except one where we take all diagnoses into account. For instance "AD_quantiles_all_datasets-v100.ipynb" is used to compute summary statistics of the selected features for participants that were diagnosed with AD. Note: we restrict the datasets to only baseline visit here.
    * The computed summary statistics are then saved as a CSV file [here](/adata_resources) 

Using the CSV tables we illustrated the following table.

![MicrosoftTeams-image (11)](https://user-images.githubusercontent.com/24376585/126197238-e743415b-f197-4db6-a236-fc2dd75d3f6d.png)


## Ethnicity 

* Using [this](/ethnicity) script, we make a table that would be used to generate pie charts for the ethnicity distribution of any cohort (shown in the figure below)
* The table made by this script is saved [here](/adata_resources)

![Screenshot from 2021-07-19 19-06-50](https://user-images.githubusercontent.com/24376585/126199289-abfc8cc4-edd1-4724-84e1-d30c2fbb09dc.png)


## Modality

* To check for the available modality and plot the ranks, we can use [this script](/Modality_overview)
![Cohorts_data_availability (2)](https://user-images.githubusercontent.com/24376585/126503425-a6ccd1b7-d91b-4580-98bd-c7185083c4cf.png)


## Biomarkers

* To visualize the biomarker distribution, we generated tables that contain measurements of participants for each feature in all datasets
    * The categorical features are Sex, APOE4 and CRD
    * All harmonized numerical features are included
* There are dedicated [scripts](/Tables_Boxplot) for each diagnostic group as well as one script for all diagnoses
* Each script saves the tables where the columns are the "feature + name of cohort" and rows contain the measurements of participants

The tables are then used to generate boxplot for numerical features and stacked barplot for categorical features. Figure below is an example of boxplots.
![Screenshot from 2021-07-20 15-08-29](https://user-images.githubusercontent.com/24376585/126331399-aa4fbc8c-6f85-40c2-8496-88757ef967a6.png)


## Longitudinal assesment

* To investigate the number of visits for each study cohort as well as the number of patients in each diagnosis stage, use [this script](/longitudinal_follow-up.ipynb)
![all_line_long_plot](https://user-images.githubusercontent.com/24376585/126503535-3b8f5406-41b1-4433-ad3c-51e49b5580b2.png)


## Number of conversions from one state to another
 
* We can compute the transition from one diagnostic state to another using [this](/patient_converters)

The following table illustrates the number of patients for each transition

![Screenshot from 2021-07-21 15-52-54](https://user-images.githubusercontent.com/24376585/126500471-ed7d1cd7-a27f-4558-b4d5-bced245be6aa.png)


## StudyPicker, Longitudinal Follow-up, Mappings

To enable a user-friendly tool for assessing cohort studies that could be compatible to use as training and validation datasets, we investigated the feature overlap across our datasets. Additionally, the number of available measurements for each follow-up visit was computed to enable visualization of collected measurements through the study length. [script](/patients_per_modality/number_of_patient_per_modality.ipynb)

Inputs: 
* Harmonized feature scape across the cohorts
* Merged dataset of each cohort

Outputs:
* Table per modality where rows are feature names and columns are the cohorts, the cells contain 1 where the feature was available and 0 where it was not. Note: 0 indicates that the feature was reported in the study but no measurements were collected for any of the participants of that cohort. [here](/patients_per_modality)
* Similar to the point above, one table that contains all the non-existing features in every cohort dataset (we combined the tables into one table). This table can be find [here](/patients_per_modality/feature_availability_in_cohorts), called "nonexistence_features.tsv".
* To investigated whether each feature of a cohort dataset has been collected for all of the participants of that cohort or a subset of the participants, we generated [tables](/patients_per_modality/feature_vs_patient_per_cohort) for all the cohort. For instance, [ADNI.tsv](/patients_per_modality/feature_vs_patient_per_cohort/ADNI.tsv) contains random index for all participants as rows and all the investigated features as columns. For each participant, we look into the original dataset (merged table) and check whether a certain feature was recorded in any visit-point through the study length and if so we store "1" for that participant in the output table.
* the total number of harmonized cohort is saved as a distict tsv file per modality and stored [here](/patients_per_modality/num_mapped_feat_total)
* Lastly, for each harmonized feature, we count the number of patients that have collected measurements for each visit point. The results are stored in separated [tables](/patients_per_modality/number_of_patient_per_visit) for each investigated modality. For instance, [apoe.tsv](/patients_per_modality/number_of_patient_per_visit/apoe.tsv) table contains information about the features related to APOE status. In this table, the cohort names are as rows and harmonized features as columns. Note: there are multiple rows with the same cohort name as the index for longitudinal cohorts and each time point is stored in the same row under the "Months" column. In other words, the "Months" column indicates whether at a certain time-point of the study length the measurements were collected or simply skipped.

All the described outputs are then used for the "StudyPicker" as well as "Longitudinal" (i.e. Biomarker-specific Follow-up) tools on the website. 

The figure below is an exmaple of StudyPicker".
![case1](https://user-images.githubusercontent.com/24376585/126516170-bbf4c1d4-cecf-46e8-b90c-3613cc958912.png)



The figure below is an example of longitudinal plot for a set of features in 4 distinct cohorts.
![study_picker_result](https://user-images.githubusercontent.com/24376585/126516566-13da33e2-965b-4ea2-9759-3919b0573bcf.png)
