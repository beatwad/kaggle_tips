# ICR Kaggle Competition

## TODO list
* ✅ Run and train ***TabPFN*** model **-->** *Increased* LB position and *decreased* log_loss in during training
* ⏺ feature engeneering (log, square, sqrt, plus, minus)
* 🟦 Calculate and research cosine or different distances between objects
* 🟦 Add similarity approach with distance features (cosine, Manhattan, Euclidean etc)
* 🟦 add time (Epsilon) to train dataset, for test dataset use time + 1 value, analyze Epsilon feature
* 🟦 Add post-processing based on additional target data
* 🟦 Split binary prediction into multi-label
* 🟦 Balance class samples (undersampling, post-processing, SMOTE)
* ✅ data leakage exploit
* 🟦 what type of imputation must be used? median/mean imputing of KNN-imputing? is NaNs are zero?
* 🟦 Ensemble TabPFNs with different number of ensembles in settings


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
