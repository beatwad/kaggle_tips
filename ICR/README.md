# ICR Kaggle Competition
Each version of model must be tagged with v.A.B.C.D system version: A - feature ver., B - model ver,. C - validation ver, D - inference ver.

## TODO list
* ✅ Run and train ***TabPFN*** model **-->** *Increased* LB position and *decreased* log_loss in during training
* ✅ Nested CV
* ✅ Balance class samples (undersampling, post-processing, SMOTE)
* ✅ Data leakage exploit
* ✅ Filter original features (gain importance + permutation importance + BORUTA SHAP)
* ✅ Analyze time features
* ✅ Should we delete objects with the outliers? Or cap the outliers values? (Use IsolationForest to detect outliers)
* ✅ Ensemble 5-10 optimised with Optuna LGBM, CatBoost and XGBoost models, train all of them on 10-20 Fold data
* ✅ Analyze features with high correlation, should we drop some of them?
* ✅ Encode Epsilon as ordinal, encode test as max(Epsilon) + 1 - doesn't work, LB score gets significantly worse
* ✅ Try RandomUnderSampling - doesn't work, makes only worse
* ✅ Feature engineering (log, square, sqrt, plus, minus) - doesn't work
* ✅ Delete objects on which models make mistakes - CV improves significantly, LB - decreases
* ✅ Try to drop DA - CV improves, LB slightly decreases
* ✅ Train each model on individual KFold split
* ✅ Ensemble TabPFNs with different number of ensembles in settings - doesn't work
* ⏺ Real class balance on the LB seems to be 1:3, use it in your model
* ⏺ Try to do different RandomUnderSample for every model
* ⏺ Try to find out LB feature distribution
* ⏺ Try different number of folds; 11 folds - LB slightly decreases, 15 folds - LB increases
* ⏺ Try different number of models
* ⏺ Try RandomOverSampling from the same imblearn library
* ⏺ TabPFN, as all transformers, may be sensitive to uninformative features. And this dataset has a lot of them. Try to drop features one-by-one and check if TabPFN performance increases
* 🟦 Delete outliers using AdjustedScaler from adjdatatools
* 🟦 Make submission without clipping outliers
* 🟦 Try to set different class weights on inference, and check if score is changed. If it is - we can fit our models to this class distribution
* 🟦 Try KNN-imputing. Or don't use imputation at all?
* 🟦 Ensemble TabPFN with LGBM, CatBoost, XGBoost, KNN, LinReg and AutoGluon
* 🟦 Add DNN, optimize it's architechture
* 🟦 Add TabNet
* 🟦 Try multi-label classification
* 🟦 Try regularization for LogReg
* 🟦 Group by first and last letter of feature name, try to find dependensies between group name/mean/mode/median/min/max/std/nunique/count and target
* 🟦 Add post-processing based on additional target data (look into Ideas)
* ❌ Try DART optimization for XGBoost (too slow)


✅ - Done <br>
🟦 - Planning <br>
⏺ - In progress <br>
⏸ - Put on hold <br>
❌ - Canceled <br>
⚠️ - Check it out <br>

## Ideas
* 🟦 Yo Daug I've heard you like boosting, so let's predict with TabPFN/KNN and boost it's errors with boosting
* ❌⏺ Denoising:
      for f in features:
         train_df[f] = np.floor(train_df[f]*100)/100 # if noise confuses model, this trick helps to delete it, doesn't work for LGBM
      Slightly improves CV for LGBM with ratio 1000
* ❌⏺ Log:
      for f in features:
         train_df[f] = np.sign(train_df[f]) * np.log1p(np.abs(train_df[f])) # doesn't work for GB, maybe will work for NNs
* 🟦 Can try to deanonimise feachers with this: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5938178/
* 🟦 Post-processing: DO NOT use code like test[test['class_0'] < 0.13] = 0 or test[test['class_0'] > 0.87] = 1. 
     One false classified object gives an error = -log(1e-15) = 34.53 => log-loss increases dramtically! So if use
     post-processing, use test[test['class_0'] < 0.13] = 0.1/0.01 or test[test['class_0'] > 0.87] = 0.9/0.99


## Experiments
* Simple *LGBM* with no fine-tuning: **LB 0.44**
* Fine-tuned *LGBM* by AutoML: **LB 0.31**
* *TabPFN*: **LB: 0.26** 
* Fine-tuned *LGBM* + Nested CV: **CV/LB: 0.2/0.17** 
* Fine-tuned with Optuna 20 *LGBM* + *XGBoost* + *CatBoost* + Stacking (10 Folds): **CV/LB: 0.158/0.17** 
* Fine-tuned *LGBM* 20 models avg + Feature selection: **CV/LB: 0.166/0.17** 
* Fine-tuned *LGBM* 20 models avg + Feature selection (also drop DA): **CV/LB: 0.163/0.18** 

## Resources:
* https://arxiv.org/abs/2207.01848
* https://arxiv.org/abs/2211.02941
* https://github.com/automl/TabPFN
* https://www.kaggle.com/code/beatwad/dealing-with-very-small-datasets/edit
* https://sebastianraschka.com/blog/2022/deep-learning-for-tabular-data.html


