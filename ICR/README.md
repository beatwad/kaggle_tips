# ICR Kaggle Competition

## TODO list
* ✅ Run and train ***TabPFN*** model **-->** *Increased* LB position and *decreased* log_loss in during training
* ✅ Nested CV
* 🟦 TabPFN, as all transformers, may be sensitive to uninformative features. And this dataset has a lot of them. Try to drop features one-by-one and check if TabPFN performance increased
* ⏺ Feature engineering (log, square, sqrt, plus, minus)
* 🟦 Should we delete objects with outliers? Or cap the outliers values? (Use IsolationForest to detect outliers)
* 🟦 Analyze features with high correlation, should we drop some of them?
* 🟦 Add mean distance (cosine, Manhattan, Euclidean etc) to N nearest neighbours for each class, increase confidence
     for object class if that object has a lot of Nearest Neigbours with the same class
* 🟦 Add similarity approach with distance features (cosine, Manhattan, Euclidean etc)
* 🟦 Add post-processing based on additional target data (look into Ideas)
* 🟦 Split binary prediction into multi-label
* 🟦 Balance class samples (undersampling, post-processing, SMOTE)
* ✅ Data leakage exploit
* 🟦 What type of imputation must be used? median/mean imputing of KNN-imputing? is NaNs are zero? or don't use at all?
* 🟦 Ensemble TabPFNs with different number of ensembles in settings
* 🟦 Ensemble TabPFN with LGBM and CatBoost and KNN
* 🟦 


✅ - Done <br>
🟦 - Planning <br>
⏺ - In progress <br>
⏸ - Put on hold <br>
❌ - Canceled <br>
⚠️ - Check it out <br>

## Ideas
* 🟦 Yo Daug I've heard you like boosting, so let's predict with TabPFN/KNN and boost it's errors with boosting
* 🟦 Post-processing: DO NOT use code like test[test['class_0'] < 0.13] = 0 or test[test['class_0'] > 0.87] = 1. 
     One false classified object gives an error = -log(1e-15) = 34.53 => log-loss increases dramtically! So if use
     post-processing, use test[test['class_0'] < 0.13] = 0.1/0.01 or test[test['class_0'] > 0.87] = 0.9/0.99

## Experiments
* Simple *LGBM* with no fine-tuning: **LB 0.44**
* Fine-tuned *LGBM* by AutoML: **LB 0.31**
* *TabPFN*: **LB: 0.26** 

## Resources:
* https://arxiv.org/abs/2207.01848
* https://arxiv.org/abs/2211.02941
* https://github.com/automl/TabPFN
* https://www.kaggle.com/code/beatwad/dealing-with-very-small-datasets/edit
* https://sebastianraschka.com/blog/2022/deep-learning-for-tabular-data.html

