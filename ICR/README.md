# ICR Kaggle Competition

## TODO list
* ✅ Run and train ***TabPFN*** model **-->** *Increased* LB position and *decreased* log_loss in during training
* ✅ Nested CV
* ✅ Filter original features (gain importance + permutation importance + BORUTA SHAP)
* ✅ Analyze time features
* 🟦 Try KNN-imputing. Or don't use imputation at all?
* 🟦 Encode Epsilon as ordinal, encode test as max(Epsilon) + 1
* ✅ Should we delete objects with the outliers? Or cap the outliers values? (Use IsolationForest to detect outliers)
* ✅ Check RandomUnderSampling
* 🟦 Delete objects on which models make mistakes
* ✅ Analyze features with high correlation, should we drop some of them?
* ⏺ Cosine class distance works, need to make submission with it
* ⏺ Clip features with the outliers, need to make submission with them and without them
* ⏺ Ensemble 5-10 optimised with Optuna LGBM, CatBoost and XGBoost models, train all of them on 10-20 Fold data
* 🟦 Try to set different class weights (one with less ratio, another one with bigger) for any GBM model, and check if score is changed. If it is - we can fit our models to this class distribution. 
* 🟦 Group by first and last letter of feature name, try to find dependensies between group name/mean/mode/median/min/max/std/nunique/count and target
* ❌⏺ Feature engineering (log, square, sqrt, plus, minus) - doesn't work for the original dataset, maybe will work for balanced
* 🟦 TabPFN, as all transformers, may be sensitive to uninformative features. And this dataset has a lot of them. Try to drop features one-by-one and check if TabPFN performance increased
* 🟦 Add similarity approach with distance features (cosine, Manhattan, Euclidean etc)
* 🟦 Add post-processing based on additional target data (look into Ideas)
* ❌ Split binary prediction into multi-label (to little data)
* ✅ Balance class samples (undersampling, post-processing, SMOTE)
* ✅ Data leakage exploit
* 🟦 Ensemble TabPFNs with different number of ensembles in settings
* 🟦 Ensemble TabPFN with LGBM, CatBoost, XGBoost and KNN
* 🟦 PCA
* 🟦 Try DART optimization for XGBoost



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
      Slightly improves CV for LGBM with ratio 1000 
* 🟦 Can try to deanonimise feachers with this: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5938178/
* 🟦 Post-processing: DO NOT use code like test[test['class_0'] < 0.13] = 0 or test[test['class_0'] > 0.87] = 1. 
     One false classified object gives an error = -log(1e-15) = 34.53 => log-loss increases dramtically! So if use
     post-processing, use test[test['class_0'] < 0.13] = 0.1/0.01 or test[test['class_0'] > 0.87] = 0.9/0.99
* 🟦 Check Greedy Bin from this solution: https://github.com/jxzly/Kaggle-American-Express-Default-Prediction-1st-solution
* 🟦 Second place in the similar competition: https://www.kaggle.com/competitions/amex-default-prediction/discussion/347637
* 🟦 Third place in the similar competition: https://www.kaggle.com/competitions/amex-default-prediction/discussion/349741
* 🟦 More winning solutions in the another similar competition here: https://www.kaggle.com/competitions/icr-identify-age-related-conditions/discussion/409596


## Experiments
* Simple *LGBM* with no fine-tuning: **LB 0.44**
* Fine-tuned *LGBM* by AutoML: **LB 0.31**
* *TabPFN*: **LB: 0.26** 
* Fine-tuned *LGBM* + Nested CV: **CV/LB: 0.2/0.17** 
* Fine-tuned with Optuna 20 *LGBMs* (10 Folds): **CV/LB: 0.166/0.17** 

## Resources:
* https://arxiv.org/abs/2207.01848
* https://arxiv.org/abs/2211.02941
* https://github.com/automl/TabPFN
* https://www.kaggle.com/code/beatwad/dealing-with-very-small-datasets/edit
* https://sebastianraschka.com/blog/2022/deep-learning-for-tabular-data.html


