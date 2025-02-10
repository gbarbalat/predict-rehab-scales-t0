# predict-rehab-scales-t0
project led by Anaid Perez

In our network of psych rehab centers, nurses collect a whole bunch of data which can be time-consuming.   
8 measures are collected which can be redundant and cumbersome, frustrate patients and clinicians.  
The aim of this project is to see if it is possible to ease data collection by predicting scores on some of the scales based on background factors and scores on other scales.  
For instance, the STages of Recovery Instrument is a 50-items self-questionaire which may be predicted by shorter scales such as the WEMWBS (well-being - 14 items), the MARS (medication adherence - 10 items), and the SQoL (quality of life - 18 items). If a model has a good predictive ability to predict scores at the STORI based on (some of) these scales, then this would ease the nurses' work, and give them some time to work on other things (e.g. other research projects). Conversely, a predictive model may not have good predictive accuracy and therefore clinicians may be better off collecting this scale directly.

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

# How to predict?    
- We'll use an ensemble of machine learning algorithms, e.g. SuperLearner of  
SL.library <- list("SL.mean",
                   c("SL.caret.xgboost", "All", "screen.mixed", "screen.randomForest"),
                   c("SL.caret.ranger", "All","screen.mixed",  "screen.randomForest"),
                   #c("SL.rpart", "All","screen.mixed",   "screen.randomForest"),#bratMachine not working with caret, rpart with very low predictive accucary
                   #c("SL.caret.ksvm", "All","screen.mixed",  "screen.randomForest"),#pbs with predictions in caret
                   c("SL.caret.naive_bayes", "All", "screen.mixed", "screen.randomForest"),
                   #c("SL.caret.earth", "All", "screen.mixed", "screen.randomForest"),#if continuous predictors
                   c("SL.caret.glm", "All", "screen.mixed", "screen.randomForest"),
                   c("SL.caret.step.interaction", "screen.mixed", "screen.randomForest"),#,
                   c("SL.caret.glmnet", "All", "screen.mixed",  "screen.randomForest"))
  - We'll use caret _adaptive_ strategy to find the best set of hyperparameters for each algorithm
  - For each predicted scale, we'll find features of patients with poor prediction
  - Missing data will be imputed using the R package _mice_ (multiple imputation) so we'll get a range of predictive accuracies among all the imputed datasets
  - One important methodological question will be whether we'll try and predict the final score or when the scale has multi-dimensions, the score at each subscale. It might be more precise to do the latter. This needs to be investigated further.
 
# Predictive power of each feature  
The influence of each feature for each participants will be calculated using SHAP value and R packages _fastshap_ and _shapviz_.

