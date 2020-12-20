# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
The data is related with direct marketing campaigns (phone calls) of a Portuguese banking institution. The classification goal is to predict if the client will subscribe a bank term deposit

The best performing model was a Logistic Regression

The data is related with direct marketing campaigns (phone calls) of a Portuguese banking institution. The classification goal is to predict if the client will subscribe a bank term deposit


## Scikit-learn Pipeline
The pipeline architecture is based in a flow of data acsition. After the acsition, there is a phase of data cleaning where data missing is removed and categorical features are encoded. The next step occurs a data split into training and evaluation slices. Then, a Logistic Regression with only two parameters which are : Inverse of regularization strenght and max number of iterations. To find the best parameters, there is a step which runs overs the pipeline mentioned that is Hyperparameter tunning. 

Hyperparameters are adjustable parameters that let you control the model training process. For example, with neural networks, you decide the number of hidden layers and the number of nodes in each layer. Model performance depends heavily on hyperparameters.

To find the best parameters the strategy is to run in paralellel several model training with different sets of parameters. There is another feature of Hyperparameter tunning, which is Early Termination Policyu, which automatically terminate poorly performing runs with an early termination policy. Early termination improves computational efficiency.

In our case, the early stop used was Bandit Policy, which is based on slack factor/slack amount and evaluation interval. Bandit terminates runs where the primary metric is not within the specified slack factor/slack amount compared to the best performing run.

[Hyperparameters tunning documentation](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-tune-hyperparameters#early-termination)

## AutoML
There were generated around of 43 models, and the best approach was an Ensemble approach made mostly by LightGBM, XGBoost and Random Forest. I could not access the parameters that have been used.

## Pipeline comparison
Using the hyperparameter tunning for a Logist Regression approach, the Accuracy was 0.91031, in the other hand, when using AutoML approach, the best Accuracy was 0.91806. 
The arquiteture of the two approaches were totally different. In the first, it as using just on kind of algorithm, which was Logist Regression. This limited our space of possibilities to find the best algorithm and the best set of hyperparameters. In the second approach, autom ml can parallelize several different runs and each run can handle different algorithm and different set of hyperparameters. This is made automatically and then, aour searh space for the best model and hyperparameters increase.  


## Future work
Once the auto ml found that GBM approach seems better, it may be possible to use Hyperparameter tunning for Light GBM algorithm in attempt to find best hyperparameters for this model. It may result in yet best model. As well, the dataset is imbalanced. It is a good approach to avoid sintetic sampling algorithms. Another good approach is to try to balance the data before running any approach mentioned here for machine learning.

## Proof of cluster clean up
![](images/cluster_delete.png?raw=true)
