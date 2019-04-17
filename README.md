# TelecomChurn-Prediction
Consumer Behavior Analysis for Targeted Retention Initiatives in Telecom sector

## Objectives 
 Analyse customer-level data of a leading telecom firm, build predictive models to identify customers at high risk of churn and identify the main indicators of churn.
     
### Business Understanding
 - If the customer is likely to churn, then firm can increase focus and target marketing towards these customers to avoid business loss.
 
 - The aim is to identify patterns which indicate if a customer is likely to churn, which may be used for taking actions such as providing better offers, resolving services related issues quickly etc

### Data Understanding
 - The dataset contains customer-level information for a span of four consecutive months - June, July, August and September. The months are encoded as 6, 7, 8 and 9 respectively.
 
The business objective is to predict the churn in the last (i.e. the ninth) month using the data (features) from the first three months. To do this task well, understanding the typical customer behaviour during churn will be helpful.

High-value Churn - Approximately 80% of revenue comes from the top 20% customers (called high-value customers). Thus, if we can reduce churn of the high-value customers, we will be able to reduce significant revenue leakage.

In this project, we will predict churn only on high-value customers.

### Analysis

#### 1. Importing and Understanding Data
 - Import the dataset
 - Understand the structure of dataframe

#### 2. Exploratory Data Analysis
 - Derived new columns based on Usage over months June, July and August
 - No missing values and duplicate values in dataset
 - Dropped mobile_number column as it will not be useful in our further analysis
 - Imputed missing values in numerical columns with 0 and categorical columns as Unknown
 - Rescaled the variables by applying normalize function
 - Univariate and Bivariate Analysis by plotting graphs
 
#### 3. Goal-1 : To Predict customers who will churn
 - Applied PCA - Dimensionality Reduction Technique
 - Used SMOTE - Class imbalancing Technique
 - Applied Logistic Regression and SVM
 - Used GridSearchCV for hyperparameter tuning
 
#### 4. Goal-1 Conclusion
                                 Logistic Regression		                       SVM	
	                       Threshold>0.5	Threshold>0.4	           Kernel=Linear	Kernel=RBF
				
               Sensitivity	     0.79	         0.84	                   0.78	          0.78
               Specificity	     0.84	         0.77	                   0.85	          0.86
             ROC_AUC_Score	     0.81	         0.81	                   0.81	          0.82
                  Accuracy	     0.83	         0.78	                   0.84	          0.85
                  
                  
 Since the business is more concerned about not losing the customers, We have to predict the churn customers correctly. A non-churn customer can be predicted as churn but a churn customer should not be predicted as non-churn. Considering this scenario and from the above metrics, we have to choose a model with high sensitivity, good specificity and good ROC_AUC_Score.
 
<font color='green'>We chose Logistic Regression Model with CutOff Threshold as 0.4 as an appropriate model to predict customers who will churn. This model is having high sensitivity, good specificity and good ROC_AUC_score when compared to other models.</font>

#### 5. Goal-2 : Modeling for predictor variables
 - Used SMOTE - Class imbalancing Technique
 - Applied Logistic Regression and used RFE for Feature Selection

#### 6. Goal-2 Conclusion

We have identified two models - Model 8 and Model 9. Lets compare the metrics.
 
                                      Model 8		                              Model 9	
                                Training 	  Test data	                Training	     Test Data
				
               Sensitivity	     0.84	         0.81	                   0.84	          0.81
               Specificity	     0.80	         0.81	                   0.79	          0.80
             ROC_AUC_Score	     0.82	         0.81	                   0.82	          0.81
                  Accuracy	     0.82	         0.81	                   0.82	          0.80
                  
                  
Since the business is more concerned about not losing the customers, We have to predict the churn customers correctly. A non-churn customer can be predicted as churn but a churn customer should not be predicted as non-churn. Considering this scenario and from the above metrics, we have to choose a model with high sensitivity, good specificity and good ROC_AUC_Score for predciting driver variables.
 
<font color='green'>We chose Model 8 as the model gave good results on test data with good sensitivity, specificity and ROC_AUC_Score.</font>
 
 <b>Driver Variables</b>: 
 
 There are total 12 predictor variables that we have arrived at using Model 8.
 
 Following are driver variables impacting the customer churn, so the Telecom Operator can focus mainly on these to identify the High value customer churn in advance to avoid business loss.
<font color='red'> 

 -  av_rech_amt_data_6 : Average recharge amount customer has done for Mobile Internet for the Month 6.
 -  total_ic_mou_8 : Total incoming voice calls for the Month 8
 -  aon : Age on network which refers to the number of days the customer is using the operator T network
 -  last_day_rch_amt_8 : Last day Recharge Amount customer has done for the Month 8
 -  total_ic_mou_6 : Total incoming voice calls for the Month 6
 -  vol_3g_mb_6 : 3G Mobile internet usage in MB  for the Month 6
 -  total_rech_num_7 : Total number of recharges done for the Month 7
 -  offnet_mou_8 : All voice call outside the operator T network for the month 8
 -  vol_3g_mb_8 : 3G Mobile internet usage in MB  for the Month 8
 -  roam_og_mou_8 : Roaming outgoing voice calls for the Month 8
 -  roam_ic_mou_7 : Roaming incoming voice calls for the Month 7
 -  vol_2g_mb_8 : 2G Mobile internet usage in MB  for the Month 8</font>
