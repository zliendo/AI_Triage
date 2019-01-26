# Interpretable Deep Attention Neural Networks for assisting Triage

**May 2018**

This repository contains the code I implemented for [IDANN Triage](https://www.ischool.berkeley.edu/projects/2018/idann-triage), which was the capstone project for my Masters on Data Science 
at UC Berkeley. This project was implemented on May 2018.

IDANN Triage helps emergency departments to identify and prioritize patients significantly ill by predicting critical outcomes; it utilizes deep neural networks with an attention layer for model interpretability. IDANN captured 37.4% more critical outcomes.   

Product web page: [IDANN Triage site](https://zliendo.github.io/idann_home.html)   
IDANN github repositories:   
* [Original capstone](https://github.com/r-hopper/MIDS-Capstone-EHR-ED-Care) (private), 
* [Code after refactorization](https://github.com/idanntriage/idann_triage) (public). The code was re-factored for easy reading and replication, keeping model's architecture and performance levels (we are creating other project to evolve the initial model).

I implemented code for data pre-preprocessing, deep learning models with an interpretation layer, visualizations and javascript API.   

## Pre-Processing and Exploratory Data Analysis (EDA)

|N. | Type | Task and its Notebook|  files|  
|---|---|---|---| 
| 1a | Pre-Processing | Transforms CDC fixed format files to CSV format. </br> Notebook:   [transform_fixed_to_csv.ipynb](notebooks/data_pre_processing/transform_fixed_to_csv.ipynb) | **Input:** data/raw/ED[year], </br> data/external/format[year].txt  </br> **Output:**  data/interim/ED[year].csv | 
| 1b | Pre-Processing | Consolidates files from different years into one and applies exclusion criteria. </br> Notebook: [consolidating_files.ipynb](notebooks/data_pre_processing/consolidating_files.ipynb)   |  **Input:** data/interim/ED[year].csv </br> **Output:** data/processed/ED_TOTAL_2009_2009.csv , </br> data/processed/ED_TOTAL_2009_2015.csv | 
| 2 | EDA | Exploratory Data Analysis of CDC data from 2009 to 2015. </br> Notebook: [CDC_eda_ESI_CO.ipynb](notebooks/eda/CDC_eda_ESI_CO.ipynb)|**Input:**  data/processed/ ED_TOTAL_2009_2015.csv | |

## Training Models   
|N. | Type | Task and its Notebook|  files|  
|---|---|---|---| 
| 3| **LR_BAS**:  Baseline Model | Logistic Regression replication Model that predicts critical outcomes. </br> Notebook: [CDC_LR_2009_baseline.ipynb](notebooks/modeling/CDC_LR_2009_baseline.ipynb) |  **Input:** data/processed/ ED_TOTAL_2009_2009.csv   | 
| 4a| **LR_RMH**: Improving LR Model|  Logistic Regression with additional features like: Reason for Visit (RFV) codes as vectors to capture its hierarchical semantic. </br> Notebook: [CDC_LR_2009_more_features.ipyn](notebooks/modeling/CDC_LR_2009_more_features.ipynb)    | **Input:**  data/processed/ ED_TOTAL_2009_2009.csv   |
| 4b|  **RF**: Random Forest|  We also implemented a Random forest (RF) model which provides a list of feature importance, relevant for model interpretation. However its performance was lower than the LR model. </br> Notebook: [CDC_RF_2009.ipynb](notebooks/modeling/CDC_RF_2009.ipynb)   |  **Input:** data/processed/ ED_TOTAL_2009_2009.csv   |
| 4c| **FNN**:Forward Neural Newtwork  |  FNN with the same features than RF and LR_RMH. </br> Notebook: [CDC_NN_2009_modeling.ipynb](notebooks/modeling/CDC_NN_2009_modeling.ipynb)    |  **Input:** data/processed/ ED_TOTAL_2009_2009.csv   |
| 4d| **FNN_TE**: FNN and Embeddings|  Forward Neural Newtwork (FNN) with embedding for the Reason for Visit (RFV) codes. </br>  Notebook:[CDC_NN_Embedding_2009_modeling.ipynb](notebooks/modeling/CDC_NN_Embedding_2009_modeling.ipynb)    | **Input:**  data/processed/  ED_TOTAL_2009_2009.csv   |
|5| **FNN_TE_ATT**: FNN Attention  for Critical Outcomes| FNN_TE with Attention Layer, predicts critical outcomes, with the attention layer. </br> Notebooks: [CDC_ATT_NN_2009_Text_Emb.ipynb](notebooks/modeling/CDC_ATT_NN_2009_Text_Emb.ipynb)    | **Input:** data/processed/ ED_TOTAL_2009_2009.csv   | 
|6| **FNN_TEA_RS**: FNN Attention for Resource estimation|  FNN_TE with Attention Layer, with multiclass outcome for resource utilization, Notebook: [CDC_ATT_RSS_NN_2009_Text_Emb.ipynb](notebooks/modeling/CDC_ATT_RSS_NN_2009_Text_Emb.ipynb)     |  **Input:** data/processed/ ED_TOTAL_2009_2009.csv   | 

## Prediction and pulling attention relative weights

|N. | Type | Task and its Notebook|  files|  
|---|---|---|---| 
|10|Prediction | Example of predicting for one record and pulling attention relative weights from the model that had just done the prediction </br> Notebook: [CO_ATT_prediction_interpretability_sample.ipynb](notebooks/prediction/CO_ATT_prediction_interpretability_sample.ipynb)    | **Input:** data/processed/ ED_TOTAL_2010_2010.csv </br> **Output:**  |
|11|Prediction | Example of how to predict for one record (it includes call to py method that is used in the cloud api-service) </br> Notebook: [ATTNN_predict_for_one_record.ipynb](notebooks/prediction/ATTNN_predict_for_one_record.ipynb)    | **Input:** data/processed/ ED_TOTAL_2010_2010.csv </br> **Output:**  |

