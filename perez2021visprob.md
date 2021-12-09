# Understanding time series probabilistic forecasting models by building them iteratively

Structure:
- X Introduction: Why this topic is relevant ?
- X Related Work: Interactive ML state
- X Our Approach
- Experiment
- Results
- Conclusion

## Introduction

Machine learning models have achieved great results in the field of time series forecasting. When describing the state of the art of the field, the machine learning forecasting models are listed and compared on performance, accuracy or training times. Those comparisons do not help users who must take informed decisions: they are required to choose from a series of black boxes whose inner workings are not fully understood.

Machine learning interpretability tries to solve this problem with different strategies: understanding specific models or methods to render any model interpretable. However both methods start from the same situation: users are confronted with already trained models.
We believe the lack of user involvement during the building of the model is also a cause for this issue.

As a solution to this problem, we propose an interative machine learning application that produces a time series machine learning pipeline from users' interaction. The model is therefore influenced by the user's knowledge and exposes how the model is built.
## Related Work

Ware et al. [4] described a way to create a classifier without an algorythm. Although the training times can not be comparable, users have a deeper understanding on how things work as they built the classifier and performance is on par with the classifier created with an automatic algorithm like ID3. Stumpf et al [7] describes how to integrate feedback on the ML model when training: choosing the right data for training and labelling the data and it brings better results. This shows how the integration of user fedback not only improves the cognition of the model, but also the results and performance of it.

Sasha et al. [5] defines a framework for knowledge generation through human-machine interaction. In this framework, analyst are in an exploration loop: they observe the feedback from their actions and they build the knowledge in an iterative way. Their actions are driven by thier intuition and they can confirm or rebunk their hypothesis. In their article, they also state that users should be able to see past analysis and backtrack to check results. 

In another article, Sasha et al. [6] integrate ML algorithms with interactive visualization as a way to interact directly with data and models. Therefore, machine learning is not a black box to be trained and used, but another layer in the analysis of data. The paper identifies the different stages of a machine learning pipeline creation and how they can be integrated in the execution/evaluation loop of an analyst: Data gathering and cleaning, preprocessing, ML Model, Visualization.

Direct Manipulation as described by Norman et al [10] describes how direct manipulation can reduce of gulf of evaluation, the difference in time between the action of the user and the evaluation of the results from the actions.

Kay et Al. \cite{kay_when_2016} investigation noted that users prefer to think in terms of natural frecuencies (2/10) instead  of probabilities (.2), and therefore it's better to use discrete outcomes to communicate probabilities. A discrete solution would improve readability and understanding of the charts.

Brennen et al. [9] devise the use of use of Amazon Mechanical Turk to compare several visualizations and use the following metrics: time to understand and accuracy.
## Our approach

Our approach relies on a streamlit application that forecast time series data. Users upload a time series csv and then they create iteratively a forecasting machine learning model through lagged features and periodic features creation, exogenous variables selection, model selection and hyperparameters adjustment. 
Users are therefore guiding the training and model selection process based on their expertise. Users can start on any position they deemed necessary: either from scratch with no feature selected and they select iteratively or they select all features and they removed features or they select an initial set of features/model and they try to improve from there: Users are not testing all features combination, based on their expertise they can discard certain combinations.

Users track automatically the performance of the created model by reading the RMSE, Bias and predictions around a selected point in test. So we reduce the gap of evaluation for the user interaction. Also, they can check the performance of the model for the overall test set or for a very particular point or context. Users can then decide which is more important for them and reach a compromise. For example, if they are more interested in peak detection, they might focus more on peak points on test than the overal RMSE metric.

Users can analyze all the interactions to visualize the improvements to the model they were introducing. This is important as users can see the importance of certain features or compare models.
Visualizations were designed to improve fast reading of those improvements. Users see the evolution of the RMSE/BIAS metric on a line chart during the users interactions and a box plot represents the impact of RMSE of each feature removal/addition.
This exposes the differences between experiments and can motivate or not to continue with the experiments if performance is deemed good enough or improvements are not worth the effort. Also the feature importance is better understood as it comes from the user's actions. Finally, this is more efficient than SHAP that tests all the improvements of a feature from every subset of the data and is a local metric.

Once the user is satisfied, the latest prediction as per the submitted csv is displayed on a dot plot time series. This innovative visualization has been designed to better read the probability the target will be in a certain range of values. 

## Experiment

How is it better ?

- Comparison of times between automatic+shap and manual.
- Feature importance recognition
- Dot plot time series evaluation: Use of Amazon Mechanical Turk to compare the dot plot with several types of visualizations
## Results

- Analyst explores a much smaller feature space, which takes less time than algorithms.
- The feature space is smaller but is more meaningful. It is a way to guide to ML build with its expertise. For example, analyst can try different lag combinations that make sense.
- Feature importance in the model:
    - Analyst can test hypothesis:
        - Forecast only with time variable
        - Improvements if additional information is added
        - Comparison of models + Feature combination: This can not be done automatically as all combinations are too much
    - Comparison with other models like SHAP or Lime: SHAP tests the importance of the feature as the mean of its contribution for every subset of the data, and some subsets do not make sense.  LIME evaluates the feature importance as the local contribution to the prediction. Our method evaluates the improvement in metrics thanks to the feature.
- Finally, we obtain better readability of final prediction, evaluated through Amazon Mechanical Turk

## Conclusion and Next steps

- This tool is the first step to improve interaction of probabilistic ML model with analyst and results in:
    - less time training as the feature space is limited by analyst knowledge
    - better understanding of the model and evaluation.
    - higher transparency the model
- We could improve upon this result  with
    - a combined user/automatic algorithm for guided experiments: the analyst selects a set of features or models and runs an automatic comparison
    - the use more advanced models
    - the use of advanced visualization that show the inner working of the probabilistic models: for example seeing the decision trees partitions and its histogram, or the different layers of a neural network.
    - provide guidance to the analyst

## Reference

1.  https://pubmed.ncbi.nlm.nih.gov/33048694/: PipelineProfiler: A Visual Analytics Tool for the Exploration of AutoML Pipelines
2. DeepAR: [https://www.sciencedirect.com/science/article/pii/S0169207019301888](https://www.sciencedirect.com/science/article/pii/S0169207019301888) 
3. M4 Competition: [https://www.sciencedirect.com/science/article/pii/S0169207019301128](https://www.sciencedirect.com/science/article/pii/S0169207019301128)
4. Manual Classifier: [https://www.cs.waikato.ac.nz/~ml/publications/2000/00MW-etal-Interactive-ML.pdf](https://www.cs.waikato.ac.nz/~ml/publications/2000/00MW-etal-Interactive-ML.pdf)
5. Knowledge Generation: [https://ieeexplore.ieee.org/document/6875967](https://ieeexplore.ieee.org/document/6875967) 
6. What you see: [https://www.sciencedirect.com/science/article/pii/S0925231217307609](https://www.sciencedirect.com/science/article/pii/S0925231217307609) 
7. Three experiments: [https://www.sciencedirect.com/science/article/pii/S1071581909000457](https://www.sciencedirect.com/science/article/pii/S1071581909000457)
8. [https://idl.cs.washington.edu/files/2016-WhenIsMyBus-CHI.pdf](https://idl.cs.washington.edu/files/2016-WhenIsMyBus-CHI.pdf)
9. Amazon Mechanical Turk: [https://dl.acm.org/doi/10.1145/3170427.3188649](https://dl.acm.org/doi/10.1145/3170427.3188649)  
10. Gulf of evaluation: [http://www-ihm.lri.fr/~mbl/ENS/FONDIHM/2013/papers/Hutchins-HCI-85.pdf](http://www-ihm.lri.fr/~mbl/ENS/FONDIHM/2013/papers/Hutchins-HCI-85.pdf)
