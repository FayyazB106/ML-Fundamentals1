# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Fayyaz Baig

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
There wasn't any issue when trying to submit the predictions. There were no negative values and the minimum was 2.417776.

### What was the top ranked model that performed?
WeightedEnsemble_L3 with validation score of -52.971009.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
The graphs of 'temp','atemp' and 'humidity' showed a normal distribution while it was skewed to the left for 'windspeed', 'casual', 'registered' and 'count'. The rest seems to confusing to interpret.
I seperated the 'datetime' column into 'month', 'day' and 'hour' columns. In addition, he datatypes for 'weather' and 'season' were changed to category.

### How much better did your model preform after adding additional features and why do you think that is?
The model improved. The training saw improvement as the best validation score was -30.819281 for WeightedEnsemble_L3. Testing also didn't result in negative values and the Kaggle score was better (0.74796) than before (1.79568).

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
Results were mixed. In training, best validation score was -34.405536 for WeightedEnsemble_L3, slightly worse than the best result overall. In testing, negative values were encountered for the first time but the Kaggle score did improve to 0.6241.
After using 'hyperparameter_tune_kwargs' where I used a local FIFO scheduler and Bayes optimization, the model got worse in training and testing. The best validation score was -129.900063 for WeightedEnsemble_L3 and the Kaggle score was 1.34311. However, there were no negative values.

### If you were given more time with this dataset, where do you think you would spend more time?
I would try to analyze the features a bit more but I would focus more on the hyperparameters and individual models.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|hpo1|hpo2|hpo3|score|
|--|--|--|--|--|
|initial|default|default|default|1.79568|
|add_features|default|default|default|0.74796|
|hpo|XGB = max_depth: 5, eta: 0.01, gamma: 0.1, colsample_bytree: 0.7, objective: reg:squarederror|default|default|0.62410|
|hpo_p2|XGB = max_depth: 5, eta: 0.01, gamma: 0.1, colsample_bytree: 0.7, objective: reg:squarederror|default|default|1.34311|

### Create a line plot showing the top model score for the three (or more) training runs during the project.

![model_train_score.png](img/model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

![model_test_score.png](img/model_test_score.png)

## Summary
In this project I created a model to predict bike sharing demand. The initial model created a lot of errors. Adding features helped improved the model dramatically and using custom hyperparameters caused a slight improvement. Using 'hyperparameter_tune_kwargs' made the model worse. The customization wasn't heavy so more of it may significantly improve the model again as well as figuring out which features can be helpful. Understanding how to use 'hyperparameter_tune_kwargs' can also be helpful.
