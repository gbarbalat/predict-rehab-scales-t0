# predict-rehab-scales-t0
project led by Anaid Perez

In our network of psych rehab centers, nurses collect a whole bunch of data which can be time-consuming.   
8 rehab outcome measures are meant to be routinely collected which can be redundant and cumbersome, frustrate patients and clinicians.  
The aim of this project is to see if it is possible to ease data collection by predicting scores on some of the scales based on background factors and scores on other scales.  
For instance, the STages of Recovery Instrument is a 50-items self-questionaire which may be predicted by shorter scales such as the MARS (medication adherence - 10 items), and the SQoL (quality of life - 18 items). If a model demonstrates good predictive ability for STORI scores based on (some of) these other scales, it could significantly streamline nurses' work, allowing them to allocate time to other important tasks (e.g., research projects or direct patient care). Conversely, if a predictive model shows poor performance, clinicians would be better advised to continue collecting STORI data directly. The decision to use a predictive model versus direct data collection should be based on a careful evaluation of the model's performance, considering both its benefits (time-saving) and potential drawbacks (reduced accuracy).

# Which scales to predict?  
One wishes to predict scales that are time-consuming and cumbersome.  
Other scales would be prone to being predicted rather than actually collected:  
- the STORI (recovery - 50 items)
- the ISMI (self-stigma - 29 items)
- the SERS (self-esteem - 20 items) may be redundant with the SQoL (quality of life - 18 items), which contains a self-esteem dimension
- the WEMWBS (well-being - 14 items) may also be redundant with the SQoL, which contains a physical and psychological well-being dimension

We'll focus on the STORI for this project.

# Which scales to use as predictors?  
In principle, one may wish to predict the STORI using the other scales:  
- the BIS (insight - 8 items)
- the WEMWBS (well-being - 14 items)
- the MARS (medication adherence - 10 items)
- the SQoL (quality of life - 18 items and 8 sub-scores)
- the SERS (self-esteem - 20 items
- the ISMI (self-stigmatisation - 29 items)
- We'll leave out the EAS (only used in France, may not be informative for non-French individuals)
- it may be more accurate to use scores at sub-scales rather than total scores, ie with SQoL sub-dimensions rather than SQoL total score
  
# How to predict?    
- it may be more accuracte to predict score at STORI sub-scale rather than final STORI score (which is a recovery stage)
- for the STORI, this is equivalent to predicting a score at each sub-scale and then "vote for" the recovery stage based on the higher score
- We'll use an ensemble of machine learning algorithms,
- We'll use caret _adaptive_ strategy to find the best set of hyperparameters for each algorithm
- We'll try different models including scales mentioned above (BIS, MARS, SQoL, SERS, ISMI ec ... or none) and leave out one scale at a time to see how the performance changes.
- We'll aim for the minimum number of scales in the predictive model while maintaining a decent predictive performance
- Missing data will be imputed using the R package _mice_ (multiple imputation) so we'll get a range of performances among all the imputed datasets
- We'll add a missingness indicator when using scales as predictors as such missingness might be informative
- We won't impute missingness in outcome
- For each predicted scale (sub-scale of the STORI), we'll try and find which feature values are associated with poor predictions
- If certain feature values are associated with poor predictions, then we might be better off passing the actual scale (STORI) rather than predicting its score
 
# Predictive power of each feature  
The influence of each feature for each participants will be calculated using SHAP value and R packages _fastshap_ and _shapviz_.
