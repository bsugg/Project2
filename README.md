Project 2
================
Brian Sugg
7/3/2020

  - [\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Introduction](#introduction)
      - [Purpose](#purpose)
      - [Data Description](#data-description)
      - [Methods](#methods)
  - [\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Data](#data)
      - [Metadata](#metadata)
      - [Import](#import)
      - [Slicing](#slicing)
  - [\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Summarizations](#summarizations)
      - [Numeric Summaries](#numeric-summaries)
      - [Visuals](#visuals)
  - [\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Modeling](#modeling)
      - [\*\*\*\*\*\*\*\*\*\*Ensemble Model](#ensemble-model)
          - [Fit](#fit)
          - [Selection](#selection)
          - [Test Set Predictions](#test-set-predictions)
      - [\*\*\*\*\*\*\*\*\*\*Linear Regression
        Model](#linear-regression-model)
          - [Fit](#fit-1)
          - [Selection](#selection-1)
          - [Test Set Predictions](#test-set-predictions-1)
  - [\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Automation](#automation)
  - [\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Conclusion](#conclusion)

# \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Introduction

## Purpose

The overall theme of this exercise is determining the popularity of
online news. The goal is to create models for predicting the number of
times a news article from *mashable.com* will be shared in social
networks. Two models will be created: a linear regression model and a
non-linear model. The parameter functionality of markdown will be used
to automatically generate an analysis report for each day of the week
that an article might be published.

## Data Description

The data comes from the *UC Irvine Machine Learning Repository* and can
be found in its original form at this
[link](https://archive.ics.uci.edu/ml/datasets/Online+News+Popularity#).

This data set covers a two year period, listing all published articles
from Mashable and several variables of associated characteristics, such
as:

  - Published Day of Week
  - Channel, or Genre (Lifestyle, Business, World, Entertainment, etc.)
  - Word Count
  - Number of Images
  - *…and several others…*

In total there are **58 possible predictive attributes** with the goal
of predicting the **response variable of number of shares** in social
networks. The provided link above goes into more detail for all
variables and their representation.

## Methods

**To be filled in later** \>\> The methods you’ll use (roughly - more
detail can be given later in the document).

# \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Data

## Metadata

You should briefly describe the data and the variables you have to work
with (no need to discuss all of them just the ones you want to use).

## Import

Read in csv file.

## Slicing

You should randomly sample from (say using sample()) the (Monday) data
in order to form a training (70% of the data) and test set (30% of the
data). You should set the seed to make your work reproducible.

# \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Summarizations

You should produce some basic (but meaningful) summary statistics about
the **training** data you are working with.

## Numeric Summaries

Numeric summaries, with contingecy tables for categorical variables.

## Visuals

A few plots help illustrate the above numeric summaries, and offer
additional views.

The general things that the plots describe should be explained but,
since we are going to automate things, there is no need to try and
explain particular trends in the plots you see (unless you want to try
and automate that too\!).

# \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Modeling

Once you have your training data set, we are ready to fit some models.
You should fit two types of models to predict the shares. One model
should be an ensemble model (bagged trees, random forests, or boosted
trees) and one should be a linear regression model (or collection of
them that you’ll choose from).

The article referenced in the UCI website mentions that they made the
problem into a binary classification problem by dividing the shares into
two groups (\< 1400 and ≥ 1400), you can do this if you’d like or simply
try to predict the shares themselves.

Feel free to use code similar to the notes or use the caret package.

## \*\*\*\*\*\*\*\*\*\*Ensemble Model

### Fit

Fit model on training data set.

### Selection

Your methodology for choosing your model during the training phase
should be explained.

### Test Set Predictions

After training/tuning your two types of models (linear and non-linear)
using cross-validation, AIC, or your preferred method (all on the
training data set only\!) you should then compare them on the test set.

Include metrics for accuracy and misclassification rate.

## \*\*\*\*\*\*\*\*\*\*Linear Regression Model

### Fit

Fit model on training data set.

### Selection

Your methodology for choosing your model during the training phase
should be explained.

### Test Set Predictions

After training/tuning your two types of models (linear and non-linear)
using cross-validation, AIC, or your preferred method (all on the
training data set only\!) you should then compare them on the test set.

Include metrics for accuracy and misclassification rate.

# \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Automation

Once you’ve completed the above for Monday, adapt the code so that you
can use a parameter in your build process that will cycle through the
weekday\_is\_\* variables.

# \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Conclusion

No description given. Explain final model selection and evaluation of
accuracy and misclassification rate metrics.
