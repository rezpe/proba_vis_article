
# TLDR

We have created a tool that creates a autoregressive and probabilistic forecasting time series model and 
provides help using it.

It enables creation by providing:
. Assisted feature selection
. Feature transformation
. Model selection
. Model evaluation through metrics on the whole test set and specific points in the test set 
. Model Use through a tested visualization method
. Timeline Visualization of all user interactions that:
    . let the user see the improvements in model performance in a histogram way
    . provide information to go back to previous steps

We compare this interactive method with a full automated one and we see an improvement in metrics and a much shorter training time. 

# Introduction

Interactive ML articles

There are lots of studies on automatic feature selection techniques and automatic ML model. Also TPOT that lets you compare whole pipelines.

No visualization on the final process - Only a number
No use of statistical tools for the comparison
No user guidance on the process
No visualization of the process

Deepar states nodel need minimal manual intervention in order to set ti but it does not explain the result of the training.

# State of Art

Interactive ML to calibrate and then use the model.

# Tool Description

The tool is comprised of 2 parts:
- Training part where the user understands the inner working of the trained model. Users can select used features, model and check the evaluation of the model for a user defined test set and specific test points.
- Forecasting part where the user can see the evaluations with an easy to use interface. The predictions are displayed in a tested visualization.

## Training part

The model is understood through the training. Users build the ML pipeline and understand the inner workings:
- feature selection
- feature transformation (scaling/standardization/normalization)
- model selection

Then users also check the evaluation for the whole test set:
- RMSE, NLL, BIAS, 
and specific points in the test set, for which the predicted distribution is compared to the real data

## Prediction Point

Then, the model does a prediction for the last point in the provided csv with the tested visualization.

# Experiments
## Training Experiment
## Visualization Experiment
# Results
# Conclusion

# Source

- DeepAR: https://www.sciencedirect.com/science/article/pii/S0169207019301888 
