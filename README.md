# The power of the Continuous Wavelet Transform (CWT) in machine learning
An investigation into the potential benefits of utilising the Continuous Wavelet Transform (CWT) to improve the accuracy of a machine learning model. In this case human gesture recognition using smartphone accelerometers.

# Investigation

The contents of this repository is a single Jupyter notebook, which contains the complete workings for the investigation detailed in the [associated article on my website.](https://www.thetestspecimen.com/posts/continuous-wavelet-transform-cnn/)

# A general overview

To give a general overview of the methodology of the notebook please see below. However, it is better to reference the article on my website which is more complete.

### Data split

Initially, I will use 7 of the 8 people as training and validation, and the 8th person as a holdout test set.

The 7 people will be completely randomised and then split 85%-15% (train-validation). The final outcome of the models being judged on the holdout test 'person'.

This should result in:

* training timeseries --> 2380 sequences
* validation timeseries --> 420 sequences
* testing timeseries --> 400 sequences

Total timeseries: 3200

### Models

The models that will be created are as follows:

1. Model 1 - A CNN model (Conv1D) used as a baseline on the raw timeseries data - **this is the benchmark**
2. Model 2 - A CNN model (Conv2D) utilising a CWT on the timeseries before input into the model
3. Model 3 - A CNN model (Conv2D) utilising a complex CWT on the timeseries before input into the model

All the above models will use the same parameters and number/type of layers to keep them as comparable as possible. 

### Comparison

#### Stage 1

A single run of the model to get an idea of accuracy and see where the model is failing (or succeeding) to generalise. 

(Users 1 to 7 as train/validation, User 8 as holdout test).

#### Stage 2

Ten repeat runs to get a more accurate average accuracy, which removes any variation due to numerical randomness / initialisation parameters. 

(Users 1 to 7 as train/validation, User 8 as holdout test).

#### Stage 3 

For Model 1 and either Model 2 or 3 (depending which performs best), a cross validation of users will be performed. 

Essentially, each individial user (1 to 8) will be used as the hold out test set in a completely independent set of tests. Each set of tests will be repeated 10 times (like Stage 2) to get an average accuracy. 

This will give a good indication as to how the models perform for each individual, ultimately giving a better indication as to how the model will likely perform with a completely new user in the future.

