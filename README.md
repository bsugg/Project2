Project 2 Welcome
================
Brian Sugg
7/3/2020

  - [Introduction](#introduction)
      - [Purpose](#purpose)
      - [Data Description](#data-description)
      - [Methods](#methods)
  - [Automation](#automation)

# Introduction

## Purpose

The overall theme of this exercise is determining the popularity of
online news. The goal is to create models for predicting the popularity
of news articles from *mashable.com* using binary classification to
categorize article shares in social networks. Two models will be
created: a linear regression model and a non-linear ensemble model. The
parameter functionality of markdown will be used to automatically
generate an analysis report for each day of the week that an article
might be published.

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
of predicting the response variable of article popularity using a binary
classification based on number of shares in social networks. The
provided link above goes into more detail for all variables and their
representation.

## Methods

The methods used in the creation of both models will follow a similar
approach. The cleansed data set for each day of the week will be split
into a training (70% of records) and a testing set (30% of records). The
training set will undergo k-fold cross validation for the model fit,
with a varying level of folds and resampling for each model type. The
fitted model will be selected automatically by the `caret` package based
on resulting accuracy, and then applied to the testing data set to
determine actual accuracy and associated misclassification rate.

The non-linear ensemble model for this exercise will be random forests,
and the linear model will be a logistic regression model under the
family of generalized linear regression. More detail around these two
model types is discussed further in their relevant sections.

The final *Conclusion* section will automatically select and display the
accuracy and misclassification rate from the best model, determined by
accuracy.

# Automation

``` r
# Create a vector of the elements to iterate over
days <- c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", 
    "Sunday")

# Render to .md the template for each param
purrr::map(.x = days, .f = ~rmarkdown::render(input = "Template.Rmd", params = list(day = .x), 
    output_file = paste0(.x, ".md")))
```

    ##   |                                                                              |                                                                      |   0%  |                                                                              |..                                                                    |   3%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....                                                                  |   5%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |.....                                                                 |   8%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......                                                               |  10%
    ## label: createDataSet
    ##   |                                                                              |.........                                                             |  13%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........                                                           |  15%
    ## label: dataPreview
    ##   |                                                                              |.............                                                         |  18%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............                                                        |  21%
    ## label: dataSlicing
    ##   |                                                                              |................                                                      |  23%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |..................                                                    |  26%
    ## label: contingencyTables
    ##   |                                                                              |....................                                                  |  28%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |......................                                                |  31%
    ## label: summaryStats
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................                                             |  36%
    ## label: histogram

    ##   |                                                                              |...........................                                           |  38%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................                                         |  41%
    ## label: boxPlot

    ##   |                                                                              |...............................                                       |  44%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................................                                      |  46%
    ## label: scatterPlots

    ##   |                                                                              |..................................                                    |  49%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  51%
    ## label: bar100

    ##   |                                                                              |......................................                                |  54%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......................................                               |  56%
    ## label: randomForestFit
    ##   |                                                                              |.........................................                             |  59%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........................................                           |  62%
    ## label: randomForestSelect
    ##   |                                                                              |.............................................                         |  64%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: randomForestPredict
    ##   |                                                                              |................................................                      |  69%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..................................................                    |  72%
    ## label: randomForestMisRate
    ##   |                                                                              |....................................................                  |  74%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |......................................................                |  77%
    ## label: logRegFit
    ##   |                                                                              |........................................................              |  79%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  82%
    ## label: logRegSelect
    ##   |                                                                              |...........................................................           |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................................................         |  87%
    ## label: logRegPredict
    ##   |                                                                              |...............................................................       |  90%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.................................................................     |  92%
    ## label: logRegMisRate
    ##   |                                                                              |..................................................................    |  95%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |....................................................................  |  97%
    ## label: bestModelSelection (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |......................................................................| 100%
    ##    inline R code fragments
    ## 
    ## 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Template.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output Monday.md --standalone --table-of-contents --toc-depth 3 --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\default.md" 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Monday.md --to html4 --from gfm --output Monday.html --standalone --self-contained --highlight-style pygments --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\preview.html" --variable "github-markdown-css:C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\github.css" --email-obfuscation none --metadata pagetitle=PREVIEW 
    ##   |                                                                              |                                                                      |   0%  |                                                                              |..                                                                    |   3%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....                                                                  |   5%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |.....                                                                 |   8%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......                                                               |  10%
    ## label: createDataSet
    ##   |                                                                              |.........                                                             |  13%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........                                                           |  15%
    ## label: dataPreview
    ##   |                                                                              |.............                                                         |  18%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............                                                        |  21%
    ## label: dataSlicing
    ##   |                                                                              |................                                                      |  23%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |..................                                                    |  26%
    ## label: contingencyTables
    ##   |                                                                              |....................                                                  |  28%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |......................                                                |  31%
    ## label: summaryStats
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................                                             |  36%
    ## label: histogram

    ##   |                                                                              |...........................                                           |  38%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................                                         |  41%
    ## label: boxPlot

    ##   |                                                                              |...............................                                       |  44%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................................                                      |  46%
    ## label: scatterPlots

    ##   |                                                                              |..................................                                    |  49%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  51%
    ## label: bar100

    ##   |                                                                              |......................................                                |  54%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......................................                               |  56%
    ## label: randomForestFit
    ##   |                                                                              |.........................................                             |  59%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........................................                           |  62%
    ## label: randomForestSelect
    ##   |                                                                              |.............................................                         |  64%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: randomForestPredict
    ##   |                                                                              |................................................                      |  69%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..................................................                    |  72%
    ## label: randomForestMisRate
    ##   |                                                                              |....................................................                  |  74%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |......................................................                |  77%
    ## label: logRegFit
    ##   |                                                                              |........................................................              |  79%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  82%
    ## label: logRegSelect
    ##   |                                                                              |...........................................................           |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................................................         |  87%
    ## label: logRegPredict
    ##   |                                                                              |...............................................................       |  90%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.................................................................     |  92%
    ## label: logRegMisRate
    ##   |                                                                              |..................................................................    |  95%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |....................................................................  |  97%
    ## label: bestModelSelection (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |......................................................................| 100%
    ##    inline R code fragments
    ## 
    ## 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Template.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output Tuesday.md --standalone --table-of-contents --toc-depth 3 --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\default.md" 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Tuesday.md --to html4 --from gfm --output Tuesday.html --standalone --self-contained --highlight-style pygments --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\preview.html" --variable "github-markdown-css:C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\github.css" --email-obfuscation none --metadata pagetitle=PREVIEW 
    ##   |                                                                              |                                                                      |   0%  |                                                                              |..                                                                    |   3%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....                                                                  |   5%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |.....                                                                 |   8%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......                                                               |  10%
    ## label: createDataSet
    ##   |                                                                              |.........                                                             |  13%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........                                                           |  15%
    ## label: dataPreview
    ##   |                                                                              |.............                                                         |  18%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............                                                        |  21%
    ## label: dataSlicing
    ##   |                                                                              |................                                                      |  23%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |..................                                                    |  26%
    ## label: contingencyTables
    ##   |                                                                              |....................                                                  |  28%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |......................                                                |  31%
    ## label: summaryStats
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................                                             |  36%
    ## label: histogram

    ##   |                                                                              |...........................                                           |  38%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................                                         |  41%
    ## label: boxPlot

    ##   |                                                                              |...............................                                       |  44%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................................                                      |  46%
    ## label: scatterPlots

    ##   |                                                                              |..................................                                    |  49%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  51%
    ## label: bar100

    ##   |                                                                              |......................................                                |  54%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......................................                               |  56%
    ## label: randomForestFit
    ##   |                                                                              |.........................................                             |  59%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........................................                           |  62%
    ## label: randomForestSelect
    ##   |                                                                              |.............................................                         |  64%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: randomForestPredict
    ##   |                                                                              |................................................                      |  69%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..................................................                    |  72%
    ## label: randomForestMisRate
    ##   |                                                                              |....................................................                  |  74%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |......................................................                |  77%
    ## label: logRegFit
    ##   |                                                                              |........................................................              |  79%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  82%
    ## label: logRegSelect
    ##   |                                                                              |...........................................................           |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................................................         |  87%
    ## label: logRegPredict
    ##   |                                                                              |...............................................................       |  90%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.................................................................     |  92%
    ## label: logRegMisRate
    ##   |                                                                              |..................................................................    |  95%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |....................................................................  |  97%
    ## label: bestModelSelection (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |......................................................................| 100%
    ##    inline R code fragments
    ## 
    ## 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Template.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output Wednesday.md --standalone --table-of-contents --toc-depth 3 --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\default.md" 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Wednesday.md --to html4 --from gfm --output Wednesday.html --standalone --self-contained --highlight-style pygments --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\preview.html" --variable "github-markdown-css:C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\github.css" --email-obfuscation none --metadata pagetitle=PREVIEW 
    ##   |                                                                              |                                                                      |   0%  |                                                                              |..                                                                    |   3%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....                                                                  |   5%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |.....                                                                 |   8%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......                                                               |  10%
    ## label: createDataSet
    ##   |                                                                              |.........                                                             |  13%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........                                                           |  15%
    ## label: dataPreview
    ##   |                                                                              |.............                                                         |  18%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............                                                        |  21%
    ## label: dataSlicing
    ##   |                                                                              |................                                                      |  23%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |..................                                                    |  26%
    ## label: contingencyTables
    ##   |                                                                              |....................                                                  |  28%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |......................                                                |  31%
    ## label: summaryStats
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................                                             |  36%
    ## label: histogram

    ##   |                                                                              |...........................                                           |  38%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................                                         |  41%
    ## label: boxPlot

    ##   |                                                                              |...............................                                       |  44%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................................                                      |  46%
    ## label: scatterPlots

    ##   |                                                                              |..................................                                    |  49%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  51%
    ## label: bar100

    ##   |                                                                              |......................................                                |  54%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......................................                               |  56%
    ## label: randomForestFit
    ##   |                                                                              |.........................................                             |  59%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........................................                           |  62%
    ## label: randomForestSelect
    ##   |                                                                              |.............................................                         |  64%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: randomForestPredict
    ##   |                                                                              |................................................                      |  69%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..................................................                    |  72%
    ## label: randomForestMisRate
    ##   |                                                                              |....................................................                  |  74%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |......................................................                |  77%
    ## label: logRegFit
    ##   |                                                                              |........................................................              |  79%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  82%
    ## label: logRegSelect
    ##   |                                                                              |...........................................................           |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................................................         |  87%
    ## label: logRegPredict
    ##   |                                                                              |...............................................................       |  90%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.................................................................     |  92%
    ## label: logRegMisRate
    ##   |                                                                              |..................................................................    |  95%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |....................................................................  |  97%
    ## label: bestModelSelection (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |......................................................................| 100%
    ##    inline R code fragments
    ## 
    ## 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Template.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output Thursday.md --standalone --table-of-contents --toc-depth 3 --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\default.md" 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Thursday.md --to html4 --from gfm --output Thursday.html --standalone --self-contained --highlight-style pygments --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\preview.html" --variable "github-markdown-css:C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\github.css" --email-obfuscation none --metadata pagetitle=PREVIEW 
    ##   |                                                                              |                                                                      |   0%  |                                                                              |..                                                                    |   3%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....                                                                  |   5%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |.....                                                                 |   8%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......                                                               |  10%
    ## label: createDataSet
    ##   |                                                                              |.........                                                             |  13%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........                                                           |  15%
    ## label: dataPreview
    ##   |                                                                              |.............                                                         |  18%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............                                                        |  21%
    ## label: dataSlicing
    ##   |                                                                              |................                                                      |  23%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |..................                                                    |  26%
    ## label: contingencyTables
    ##   |                                                                              |....................                                                  |  28%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |......................                                                |  31%
    ## label: summaryStats
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................                                             |  36%
    ## label: histogram

    ##   |                                                                              |...........................                                           |  38%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................                                         |  41%
    ## label: boxPlot

    ##   |                                                                              |...............................                                       |  44%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................................                                      |  46%
    ## label: scatterPlots

    ##   |                                                                              |..................................                                    |  49%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  51%
    ## label: bar100

    ##   |                                                                              |......................................                                |  54%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......................................                               |  56%
    ## label: randomForestFit
    ##   |                                                                              |.........................................                             |  59%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........................................                           |  62%
    ## label: randomForestSelect
    ##   |                                                                              |.............................................                         |  64%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: randomForestPredict
    ##   |                                                                              |................................................                      |  69%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..................................................                    |  72%
    ## label: randomForestMisRate
    ##   |                                                                              |....................................................                  |  74%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |......................................................                |  77%
    ## label: logRegFit
    ##   |                                                                              |........................................................              |  79%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  82%
    ## label: logRegSelect
    ##   |                                                                              |...........................................................           |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................................................         |  87%
    ## label: logRegPredict
    ##   |                                                                              |...............................................................       |  90%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.................................................................     |  92%
    ## label: logRegMisRate
    ##   |                                                                              |..................................................................    |  95%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |....................................................................  |  97%
    ## label: bestModelSelection (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |......................................................................| 100%
    ##    inline R code fragments
    ## 
    ## 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Template.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output Friday.md --standalone --table-of-contents --toc-depth 3 --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\default.md" 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Friday.md --to html4 --from gfm --output Friday.html --standalone --self-contained --highlight-style pygments --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\preview.html" --variable "github-markdown-css:C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\github.css" --email-obfuscation none --metadata pagetitle=PREVIEW 
    ##   |                                                                              |                                                                      |   0%  |                                                                              |..                                                                    |   3%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....                                                                  |   5%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |.....                                                                 |   8%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......                                                               |  10%
    ## label: createDataSet
    ##   |                                                                              |.........                                                             |  13%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........                                                           |  15%
    ## label: dataPreview
    ##   |                                                                              |.............                                                         |  18%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............                                                        |  21%
    ## label: dataSlicing
    ##   |                                                                              |................                                                      |  23%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |..................                                                    |  26%
    ## label: contingencyTables
    ##   |                                                                              |....................                                                  |  28%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |......................                                                |  31%
    ## label: summaryStats
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................                                             |  36%
    ## label: histogram

    ##   |                                                                              |...........................                                           |  38%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................                                         |  41%
    ## label: boxPlot

    ##   |                                                                              |...............................                                       |  44%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................................                                      |  46%
    ## label: scatterPlots

    ##   |                                                                              |..................................                                    |  49%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  51%
    ## label: bar100

    ##   |                                                                              |......................................                                |  54%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......................................                               |  56%
    ## label: randomForestFit
    ##   |                                                                              |.........................................                             |  59%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........................................                           |  62%
    ## label: randomForestSelect
    ##   |                                                                              |.............................................                         |  64%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: randomForestPredict
    ##   |                                                                              |................................................                      |  69%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..................................................                    |  72%
    ## label: randomForestMisRate
    ##   |                                                                              |....................................................                  |  74%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |......................................................                |  77%
    ## label: logRegFit
    ##   |                                                                              |........................................................              |  79%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  82%
    ## label: logRegSelect
    ##   |                                                                              |...........................................................           |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................................................         |  87%
    ## label: logRegPredict
    ##   |                                                                              |...............................................................       |  90%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.................................................................     |  92%
    ## label: logRegMisRate
    ##   |                                                                              |..................................................................    |  95%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |....................................................................  |  97%
    ## label: bestModelSelection (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |......................................................................| 100%
    ##    inline R code fragments
    ## 
    ## 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Template.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output Saturday.md --standalone --table-of-contents --toc-depth 3 --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\default.md" 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Saturday.md --to html4 --from gfm --output Saturday.html --standalone --self-contained --highlight-style pygments --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\preview.html" --variable "github-markdown-css:C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\github.css" --email-obfuscation none --metadata pagetitle=PREVIEW 
    ##   |                                                                              |                                                                      |   0%  |                                                                              |..                                                                    |   3%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....                                                                  |   5%
    ## label: setup (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |.....                                                                 |   8%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......                                                               |  10%
    ## label: createDataSet
    ##   |                                                                              |.........                                                             |  13%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........                                                           |  15%
    ## label: dataPreview
    ##   |                                                                              |.............                                                         |  18%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..............                                                        |  21%
    ## label: dataSlicing
    ##   |                                                                              |................                                                      |  23%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |..................                                                    |  26%
    ## label: contingencyTables
    ##   |                                                                              |....................                                                  |  28%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |......................                                                |  31%
    ## label: summaryStats
    ##   |                                                                              |.......................                                               |  33%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................                                             |  36%
    ## label: histogram

    ##   |                                                                              |...........................                                           |  38%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................                                         |  41%
    ## label: boxPlot

    ##   |                                                                              |...............................                                       |  44%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |................................                                      |  46%
    ## label: scatterPlots

    ##   |                                                                              |..................................                                    |  49%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |....................................                                  |  51%
    ## label: bar100

    ##   |                                                                              |......................................                                |  54%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.......................................                               |  56%
    ## label: randomForestFit
    ##   |                                                                              |.........................................                             |  59%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |...........................................                           |  62%
    ## label: randomForestSelect
    ##   |                                                                              |.............................................                         |  64%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |...............................................                       |  67%
    ## label: randomForestPredict
    ##   |                                                                              |................................................                      |  69%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |..................................................                    |  72%
    ## label: randomForestMisRate
    ##   |                                                                              |....................................................                  |  74%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |......................................................                |  77%
    ## label: logRegFit
    ##   |                                                                              |........................................................              |  79%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.........................................................             |  82%
    ## label: logRegSelect
    ##   |                                                                              |...........................................................           |  85%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.............................................................         |  87%
    ## label: logRegPredict
    ##   |                                                                              |...............................................................       |  90%
    ##   ordinary text without R code
    ## 
    ##   |                                                                              |.................................................................     |  92%
    ## label: logRegMisRate
    ##   |                                                                              |..................................................................    |  95%
    ##    inline R code fragments
    ## 
    ##   |                                                                              |....................................................................  |  97%
    ## label: bestModelSelection (with options) 
    ## List of 1
    ##  $ include: logi FALSE
    ## 
    ##   |                                                                              |......................................................................| 100%
    ##    inline R code fragments
    ## 
    ## 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Template.utf8.md --to gfm --from markdown+autolink_bare_uris+tex_math_single_backslash --output Sunday.md --standalone --table-of-contents --toc-depth 3 --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\default.md" 
    ## "C:/Program Files/RStudio/bin/pandoc/pandoc" +RTS -K512m -RTS Sunday.md --to html4 --from gfm --output Sunday.html --standalone --self-contained --highlight-style pygments --template "C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\preview.html" --variable "github-markdown-css:C:\Users\suggb\Documents\R\win-library\4.0\rmarkdown\rmarkdown\templates\github_document\resources\github.css" --email-obfuscation none --metadata pagetitle=PREVIEW

    ## [[1]]
    ## [1] "C:/Users/suggb/Documents/ST558/Projects/Project2/Monday.md"
    ## 
    ## [[2]]
    ## [1] "C:/Users/suggb/Documents/ST558/Projects/Project2/Tuesday.md"
    ## 
    ## [[3]]
    ## [1] "C:/Users/suggb/Documents/ST558/Projects/Project2/Wednesday.md"
    ## 
    ## [[4]]
    ## [1] "C:/Users/suggb/Documents/ST558/Projects/Project2/Thursday.md"
    ## 
    ## [[5]]
    ## [1] "C:/Users/suggb/Documents/ST558/Projects/Project2/Friday.md"
    ## 
    ## [[6]]
    ## [1] "C:/Users/suggb/Documents/ST558/Projects/Project2/Saturday.md"
    ## 
    ## [[7]]
    ## [1] "C:/Users/suggb/Documents/ST558/Projects/Project2/Sunday.md"

A template file has been created that utilizes the above R markdown
automation to generate a full analysis with a metadata overview, data
import and slicing, numeric summaries, model fit, model selection, model
testing, and final conclusion for best model used for each day of the
week. These individual analysis can be found within the below links:

The analysis for [Monday is available here](Monday.md).  
The analysis for [Tuesday is available here](Tuesday.md).  
The analysis for [Wednesday is available here](Wednesday.md).  
The analysis for [Thursday is available here](Thursday.md).  
The analysis for [Friday is available here](Friday.md).  
The analysis for [Saturday is available here](Saturday.md).  
The analysis for [Sunday is available here](Sunday.md).
