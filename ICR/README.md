# ICR Kaggle Competition

## TODO list
* ✅ Run and train ***TabPFN*** model **-->** *Increased* LB position and *decreased* log_loss in during training
* ✅ Nested CV
* ✅ Filter original features (gain importance + permutation importance + BORUTA SHAP)
* ✅ Analyze time features
* 🟦 Try KNN-imputing. Or don't use imputation at all?
* 🟦 Encode Epsilon as ordinal, encode test as max(Epsilon) + 1
* 🟦 Should we delete objects with outliers? Or cap the outliers values? (Use IsolationForest to detect outliers)
* 🟦 Analyze features with high correlation, should we drop some of them?
* ⏺ Add mean distance (cosine, Manhattan, Euclidean etc) to N nearest neighbours for each class
* 🟦 Increase confidence of prediction if there are a lot of close objects of the same class
      for object class if that object has a lot of Nearest Neigbours with the same class
* 🟦 Clip features with the outliers
* 🟦 Group by first and last letter of feature name, try to find dependensies between group name/mean/mode/median/min/max/std/nunique/count and target
* ⏺ Ensemble 5-10 optimised with Optuna LGBM and CatBoost models, train all of them on full data
* ❌ Feature engineering (log, square, sqrt, plus, minus)
* 🟦 TabPFN, as all transformers, may be sensitive to uninformative features. And this dataset has a lot of them. Try to drop features one-by-one and check if TabPFN performance increased
* 🟦 Add similarity approach with distance features (cosine, Manhattan, Euclidean etc)
* 🟦 Add post-processing based on additional target data (look into Ideas)
* 🟦 Split binary prediction into multi-label
* 🟦 Balance class samples (undersampling, post-processing, SMOTE)
* ✅ Data leakage exploit
* 🟦 Ensemble TabPFNs with different number of ensembles in settings
* 🟦 Ensemble TabPFN with LGBM and CatBoost and KNN
* 🟦 PCA



✅ - Done <br>
🟦 - Planning <br>
⏺ - In progress <br>
⏸ - Put on hold <br>
❌ - Canceled <br>
⚠️ - Check it out <br>

## Ideas
* 🟦 Yo Daug I've heard you like boosting, so let's predict with TabPFN/KNN and boost it's errors with boosting
* 🟦 Denoising:
      for f in features:
         train_df[f] = np.floor(train_df[f]*100)/100 # if noise confuses model this trick helps to delete it, doesn't work for LGBM
      Slightly improves CV for LGBM with ratio 1000
* 🟦 Log:
      for f in features:
         train_df[f] = np.sign(train_df[f]) * np.log1p(np.abs(train_df[f])) # doesn't work for LGBM, maybe will work for NNs
      Slightly improves CV for LGBM with ratio 1000 
* 🟦 Post-processing: DO NOT use code like test[test['class_0'] < 0.13] = 0 or test[test['class_0'] > 0.87] = 1. 
     One false classified object gives an error = -log(1e-15) = 34.53 => log-loss increases dramtically! So if use
     post-processing, use test[test['class_0'] < 0.13] = 0.1/0.01 or test[test['class_0'] > 0.87] = 0.9/0.99
* 🟦 Check Greedy Bin from this solution: https://github.com/jxzly/Kaggle-American-Express-Default-Prediction-1st-solution
* 🟦 Second place in the similar competition: https://www.kaggle.com/competitions/amex-default-prediction/discussion/347637
* 🟦 Third place in the similar competition: https://www.kaggle.com/competitions/amex-default-prediction/discussion/349741
* 🟦 More winning solutions in the another similar competition here: https://www.kaggle.com/competitions/icr-identify-age-related-conditions/discussion/409596
* 🟦 Can try to deanonimise feachers with this: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5938178/


## Experiments
* Simple *LGBM* with no fine-tuning: **LB 0.44**
* Fine-tuned *LGBM* by AutoML: **LB 0.31**
* *TabPFN*: **LB: 0.26** 
* Fine-tuned *LGBM* + Nested CV: **LB: 0.17** 

## Resources:
* https://arxiv.org/abs/2207.01848
* https://arxiv.org/abs/2211.02941
* https://github.com/automl/TabPFN
* https://www.kaggle.com/code/beatwad/dealing-with-very-small-datasets/edit
* https://sebastianraschka.com/blog/2022/deep-learning-for-tabular-data.html

