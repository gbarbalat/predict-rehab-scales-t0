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

# Which scales to use as predictors?
