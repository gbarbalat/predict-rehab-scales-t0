# predict-rehab-scales-t0
project led by Anaid Perez

In our network of psych rehab centers, nurses collect a whole bunch of data which can be time-consuming.   
8 rehab outcome measures are meant to be routinely collected which can be redundant and cumbersome, frustrate patients and clinicians.  
The aim of this project is to see if it is possible to ease data collection by predicting scores on some of the scales based on background factors and scores on other scales.  
For instance, the STages of Recovery Instrument is a 50-items self-questionaire which may be predicted by shorter scales such as the WEMWBS (well-being - 14 items), the MARS (medication adherence - 10 items), and the SQoL (quality of life - 18 items). If a model demonstrates good predictive ability for STORI scores based on (some of) these other scales, it could significantly streamline nurses' work, allowing them to allocate time to other important tasks (e.g., research projects or direct patient care). Conversely, if a predictive model shows poor accuracy, clinicians would be better advised to continue collecting STORI data directly. The decision to use a predictive model versus direct data collection should be based on a careful evaluation of the model's performance, considering both its benefits (time-saving) and potential drawbacks (reduced accuracy).

# Which scales to predict?  
One wishes to predict scales that are time-consuming, cumbersome, and hetero-questionnaires.  
Scales that would be prone to being predicted rather than actually collected may be:  
- the STORI (recovery - 50 items)
- the ISMI (self-stigma - 29 items)
- the EAS (which is a hetero-questionnaire evaluating autonomy)
- the SERS (self-esteem - 20 items) may be redundant with the SQoL (quality of life - 18 items), which contains a self-esteem dimension
- the WEMWBS (well-being - 14 items) may also be redundant with the SQoL, which contains a physical and psychological well-being dimension
From discussion with clinicians, we found out that xxxx put here scales that are actually liked and disliked by clinicians.   

# Which scales to use as predictors?  
One wishes to use scales that are quick and acceptable, e.g.  
- the BIS (insight - 8 items)
- the MARS (medication adherence - 10 items)
- the WEMWBS and the SQoL
Of course, one needs to be cautious of the fact that short scales may also be the ones with the least predictive power...
- it may be more accurate to predict with sub-scales rather than total scores
- including sub-scales of the STORI itself to predict other sub-scales

# How to predict?    
- We'll use an ensemble of machine learning algorithms,
- We'll use caret _adaptive_ strategy to find the best set of hyperparameters for each algorithm
- For each predicted scale, we'll find features of patients with poor prediction (if present, these features will lead us to say that this patient might be better off with the score being actually calculated from the scale itself rather than predicted)
- Missing data will be imputed using the R package _mice_ (multiple imputation) so we'll get a range of predictive accuracies among all the imputed datasets

# Two important methodological questions
- which scales/subscale to use as predictors in addition to background factors
- is it better to try and predict the final score or when the scale has multi-dimensions, the score at each subscale. It might be more precise to do the latter
- for the STORI, this is equivalent to predict a score at each sub-scale and then "vote for" the recovery stage based on the higher score
 
# Predictive power of each feature  
The influence of each feature for each participants will be calculated using SHAP value and R packages _fastshap_ and _shapviz_.

# Start with 
- predicting the STORI sub-scores
- with the SQoL and the ISMI but which dimensions?
