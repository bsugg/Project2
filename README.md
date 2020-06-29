Project 2
================
Brian Sugg
7/3/2020

  - [Introduction](#introduction)
      - [Purpose](#purpose)
      - [Data Description](#data-description)
      - [\*\*\*\*\*Methods](#methods)
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

# Introduction

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

## \*\*\*\*\*Methods

**To be filled in later** \>\> The methods you’ll use (roughly - more
detail can be given later in the document).

# \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Data

## Metadata

You should briefly describe the data and the variables you have to work
with (no need to discuss all of them just the ones you want to use).

## Import

Read in csv file.

``` r
# Read in the data
news <- read_csv("data/OnlineNewsPopularity.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_double(),
    ##   url = col_character()
    ## )

    ## See spec(...) for full column specifications.

``` r
# Filter data set on day of week using markdown parameter
filterDay <- paste0("weekday_is_", tolower(params$day))
news <- filter(news, eval(as.symbol(filterDay)) == 1)
# Create a binary variable for shares
news$sharesBi <- factor(ifelse(news$shares < 1400, 0, 1))
```

Preview of the `news` set:

``` r
head(news)
```

    ## # A tibble: 6 x 62
    ##   url   timedelta n_tokens_title n_tokens_content n_unique_tokens
    ##   <chr>     <dbl>          <dbl>            <dbl>           <dbl>
    ## 1 http~       731             12              219           0.664
    ## 2 http~       731              9              255           0.605
    ## 3 http~       731              9              211           0.575
    ## 4 http~       731              9              531           0.504
    ## 5 http~       731             13             1072           0.416
    ## 6 http~       731             10              370           0.560
    ## # ... with 57 more variables: n_non_stop_words <dbl>,
    ## #   n_non_stop_unique_tokens <dbl>, num_hrefs <dbl>, num_self_hrefs <dbl>,
    ## #   num_imgs <dbl>, num_videos <dbl>, average_token_length <dbl>,
    ## #   num_keywords <dbl>, data_channel_is_lifestyle <dbl>,
    ## #   data_channel_is_entertainment <dbl>, data_channel_is_bus <dbl>,
    ## #   data_channel_is_socmed <dbl>, data_channel_is_tech <dbl>,
    ## #   data_channel_is_world <dbl>, kw_min_min <dbl>, kw_max_min <dbl>,
    ## #   kw_avg_min <dbl>, kw_min_max <dbl>, kw_max_max <dbl>, kw_avg_max <dbl>,
    ## #   kw_min_avg <dbl>, kw_max_avg <dbl>, kw_avg_avg <dbl>,
    ## #   self_reference_min_shares <dbl>, self_reference_max_shares <dbl>,
    ## #   self_reference_avg_sharess <dbl>, weekday_is_monday <dbl>,
    ## #   weekday_is_tuesday <dbl>, weekday_is_wednesday <dbl>,
    ## #   weekday_is_thursday <dbl>, weekday_is_friday <dbl>,
    ## #   weekday_is_saturday <dbl>, weekday_is_sunday <dbl>, is_weekend <dbl>,
    ## #   LDA_00 <dbl>, LDA_01 <dbl>, LDA_02 <dbl>, LDA_03 <dbl>, LDA_04 <dbl>,
    ## #   global_subjectivity <dbl>, global_sentiment_polarity <dbl>,
    ## #   global_rate_positive_words <dbl>, global_rate_negative_words <dbl>,
    ## #   rate_positive_words <dbl>, rate_negative_words <dbl>,
    ## #   avg_positive_polarity <dbl>, min_positive_polarity <dbl>,
    ## #   max_positive_polarity <dbl>, avg_negative_polarity <dbl>,
    ## #   min_negative_polarity <dbl>, max_negative_polarity <dbl>,
    ## #   title_subjectivity <dbl>, title_sentiment_polarity <dbl>,
    ## #   abs_title_subjectivity <dbl>, abs_title_sentiment_polarity <dbl>,
    ## #   shares <dbl>, sharesBi <fct>

## Slicing

You should randomly sample from (say using sample()) the (Monday) data
in order to form a training (70% of the data) and test set (30% of the
data). You should set the seed to make your work reproducible.

``` r
# Set seed for reproducible results
set.seed(1)
# Create the train and test sets
train <- sample(1:nrow(news), size = nrow(news) * 0.7)
test <- dplyr::setdiff(1:nrow(news), train)
newsTrain <- news[train, ]
newsTest <- news[test, ]
```

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

The analysis for [Monday is available here](MondayAnalysis.md)

# \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Conclusion

No description given. Explain final model selection and evaluation of
accuracy and misclassification rate metrics.
