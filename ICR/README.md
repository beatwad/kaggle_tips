# ICR Kaggle Competition

## TODO list
* ✅ Run and train ***TabPFN*** model **-->** *Increased* LB position and *decreased* log_loss in during training
* 🟦 TabPFN, as all transformers, may be sensitive to uninformative features. And this dataset has a lot of them. Try to drop features one-by-one and check if TabPFN performance increased
* ⏺ Feature engineering (log, square, sqrt, plus, minus)
* 🟦 Add mean distance (cosine, Manhattan, Euclidean etc) to N nearest neighbours for each class
* 🟦 Add similarity approach with distance features (cosine, Manhattan, Euclidean etc)
* 🟦 analyze time (Epsilon) feature
* 🟦 Add time (Epsilon) to train/test dataset, encode it as ordinal. For the test dataset use max(time) + 1 value 
* 🟦 Add post-processing based on additional target data (e.g. use threshold: if target <= threshold: target = 0 else 1)
* 🟦 Split binary prediction into multi-label
* 🟦 Balance class samples (undersampling, post-processing, SMOTE)
* ✅ Data leakage exploit
* 🟦 What type of imputation must be used? median/mean imputing of KNN-imputing? is NaNs are zero? or don't use at all?
* 🟦 Ensemble TabPFNs with different number of ensembles in settings
* 🟦 Ensemble TabPFN with LGBM and CatBoost


✅ - Done <br>
🟦 - Planning <br>
⏺ - In progress <br>
⏸ - Put on hold <br>
❌ - Canceled <br>
⚠️ - Check it out <br>

## Ideas
* 🟦 Yo Daug I've heard you like boosting, so let's predict with TabPFN/KNN and boost it's errors with boosting

## Experiments
* Simple *LGBM* with no fine-tuning: **LB 0.44**
* Fine-tuned *LGBM* by AutoML: **LB 0.31**
* *TabPFN*: **LB: 0.26** 

## Resources:
* https://arxiv.org/abs/2207.01848
* https://arxiv.org/abs/2211.02941
* https://github.com/automl/TabPFN

