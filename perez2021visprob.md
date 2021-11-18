# Interactive Machine Learning for Probabilistic Forecasting of Pollution levels in Madrid

## Introduction

There has been a recent push in reseearch towards automatic solutions like AutoML. [1]

We also have papers like DeepAR which underlines the merits of creating an algorithm with minimal human intervention. [2]

In the case of time series, the M4 competition are also a cause for this [3]: 100 000 time series are forecasted, which leaves no space for human intervention in the models due to the scale of the competition.

However, no human in the ML buildind results in:

- Loss of trust in the results
- No understanding of the ml model
- No visibility on the process and experiments done by the machine

In order to overcome those problems, we propose as a solution:

- Interactive ML pipeline (Feature selection + ML Model selectin) built iteratively in a UI
- It shows the evaluation of the model for every iteration with low interaction friction:
    - For individual points in the test set chosen by the user: comparison of time series with its probabilistic prediction
    - For the whole test set, the following metrics: RMSE, BIAS, CRPS, MAPE
    - Metrics are shown instantly: great care on optimizing the models have been taken to ensure this.
- Analyst can see the evolution of the metrics for every iteration, so he can monitor the improvements/downgrade of the model as the consequence of its actions.
    - The evolution of the metrics is show as a line chart for every iteration
    - A summary of the improvement/downgrade in metrics per feature is also displayed
- The final model is then used to forecast new values and the prediction is displayed using natural frequencies for higher readability

## State of the art

(References: [4] [5] [6] [7])

Existing frameworks: Several papers have defined the interactive ML pipeline with a common vocabulary.

ML Pipeline:

- Types of variables
- Models
- Metrics
- Visualization
- Applied to Time Series:
    - Variables: lagged, exogenous, other time series
    - models: probabilistic AR ml models
    - Visualization: Dot plot time series visualization

Loop:

- User is in a loop where he executes and then evaluates its action

Iterative way:

- Example of user building its own classifier which is not that worst than algorythm

Knowledge Generation:

- Interactive ML let analyst build knowledge on the model and features by testing hypothesis, generating insights and then synthesizing the results.
- Help for decision making and generating trust in the model

## Experiments

Description of the Interactive ML tool:

- Implemented with Streamlit
- 2 parts:
    - Time series description: analyst uploads data and describes the different features in the dataset
    - Feature selection and ML model selection: analyst builds a ML model by iteratively selecting features, models and its hyperparameter
- Dot plot time series evaluation:
    - Based on natural frequencies [8]
    - Use of Amazon Mechanical Turk to compare the dot plot with several types of visualizations [9]

## Experiment

ML Model:
- Measure of training times and metrics: RMSE, CRPS, BIAS and MAPE.

Dot plot time series evaluation:
    - Use of Amazon Mechanical Turk to compare the dot plot with several types of visualizations [9]

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

1.  AUTOML: [https://ai.googleblog.com/2020/12/using-automl-for-time-series-forecasting.html](https://arxiv.org/abs/1908.00709)
2. DeepAR: [https://www.sciencedirect.com/science/article/pii/S0169207019301888](https://www.sciencedirect.com/science/article/pii/S0169207019301888) 
3. M4 Competition: [https://www.sciencedirect.com/science/article/pii/S0169207019301128](https://www.sciencedirect.com/science/article/pii/S0169207019301128)
4. Manual Classifier: [https://www.cs.waikato.ac.nz/~ml/publications/2000/00MW-etal-Interactive-ML.pdf](https://www.cs.waikato.ac.nz/~ml/publications/2000/00MW-etal-Interactive-ML.pdf)
5. Knowledge Generation: [https://ieeexplore.ieee.org/document/6875967](https://ieeexplore.ieee.org/document/6875967) 
6. What you see: [https://www.sciencedirect.com/science/article/pii/S0925231217307609](https://www.sciencedirect.com/science/article/pii/S0925231217307609) 
7. Three experiments: [https://www.sciencedirect.com/science/article/pii/S1071581909000457](https://www.sciencedirect.com/science/article/pii/S1071581909000457)
8. [https://idl.cs.washington.edu/files/2016-WhenIsMyBus-CHI.pdf](https://idl.cs.washington.edu/files/2016-WhenIsMyBus-CHI.pdf)
9. Amazon Mechanical Turk: [https://dl.acm.org/doi/10.1145/3170427.3188649](https://dl.acm.org/doi/10.1145/3170427.3188649)  
10. Gulf of evaluation: [http://www-ihm.lri.fr/~mbl/ENS/FONDIHM/2013/papers/Hutchins-HCI-85.pdf](http://www-ihm.lri.fr/~mbl/ENS/FONDIHM/2013/papers/Hutchins-HCI-85.pdf)
