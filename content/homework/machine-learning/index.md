---
title: "HW07: Machine learning"
date: 2022-10-26T13:30:00-06:00  # Schedule page publish date
publishdate: 2019-04-01

draft: false
type: post
aliases: ["/hw06-stat-learn.html", "/homework/statistical-learning"]

summary: "Implement machine learning methods for regression and classification."
---



# Overview

Due by 11:59pm on November 1st.

# Accessing the `hw07` repository

Go [here](https://github.coecis.cornell.edu/cis-fa22) and find your copy of the `hw07` repository. It follows the naming convention `hw07-<USERNAME>`. Clone the repository to your computer.

# Part 1: Student debt

Median student debt in the United States has increased substantially over the past twenty years.

{{< figure src="avg-median-debt.png" caption="Median federal debt for students has increased since 2006. Source: <a href='https://www.stlouisfed.org/on-the-economy/2020/january/rising-student-debt-great-recession'>Federal Reserve Bank of St. Louis</a>" >}}

`rcis::scorecard` includes `debt`, which reports the median debt of students after leaving school in 2019.

 

For all models, exclude `unitid` and `name` as predictors. These serve as id variables in the data set and uniquely identify each observation. They are not useful in predicting an outcome of interest.

 

1. Split `scorecard` into training and test sets with 75% allocated to training and 25% allocated to testing.
1. Split the training set into 10 distinct folds for cross-validation.
1. Estimate a linear regression model to predict `debt` as a function of all the other variables in the dataset except for `state`, using 10-fold cross-validation. Report the RMSE for the model.[^rmse]
1. Estimate a decision tree model to predict `debt` using 10-fold cross-validation. Use the `rpart` engine. Report the RMSE for the model.

## For those looking to stretch themselves

Estimate one or more models which utilize some aspect of feature engineering or [model tuning](/notes/tune-models/). Discuss the process you used to estimate the model and report on its performance.

# Part 2: Predicting attitudes towards marijuana legalization

The [General Social Survey](http://gss.norc.org/) is a biannual survey of the American public.

 

[The GSS gathers data on contemporary American society in order to monitor and explain trends and constants in attitudes, behaviors, and attributes. Hundreds of trends have been tracked since 1972. In addition, since the GSS adopted questions from earlier surveys, trends can be followed for up to 70 years. The GSS contains a standard core of demographic, behavioral, and attitudinal questions, plus topics of special interest. Among the topics covered are civil liberties, crime and violence, intergroup tolerance, morality, national spending priorities, psychological well-being, social mobility, and stress and traumatic events.](http://gss.norc.org/About-The-GSS)

 

Over the past twenty years, American attitudes towards marijuana have softened extensively. In the early 2010s, the number of Americans who believed marijuana should be legal began to outnumber those who thought it should not be legal.







`rcis::gss` contains a selection of variables from the 2018 GSS. The outcome of interest `grass` is a factor variable coded as either `"legal"` (respondent believes marijuana should be legal) or `"not legal"` (respondent believes marijuana should not be legal).

 

Make sure you have the most recent version of `rcis`. If the version is less than 0.2.6, reinstall `rcis` using the most recent version.

```r
if (packageVersion("rcis") < 0.2.6) {
  remotes::install_github("cis-ds/rcis")
}
```



For all models, exclude `id` and `wtss` as predictors. These serve as id variables in the data set and uniquely identify each observation. They are not useful in predicting an outcome of interest.



1. Split `gss` into training and test sets with 75% allocated to training and 25% allocated to testing.
2. Estimate a logistic regression model to predict `grass` as a function of `age`, `degree`, `happy`, `partyid`, and `sex,`. Implement 10-fold cross-validation. Report the accuracy of the model.
3. Estimate a random forest model to predict `grass` as a function of all the other variables in the dataset (except `id` and `wtss`). In order to do this, you need to **impute** missing values for all the predictor columns. This means replacing missing values (`NA`) with plausible values given what we know about the other observations.
    - Remove rows with an `NA` for `grass` - we want to omit observations with missing values for outcomes, not impute them
    - Use median imputation for numeric predictors
    - Use modal imputation for nominal predictors
    
    Implement 10-fold cross-validation. Report the accuracy of the model.
4. Estimate a $5$-nearest neighbors model to predict `grass`. Use `recipes` to prepare the data set for training this model (e.g. scaling and normalizing variables, ensuring all predictors are numeric). Be sure to also perform the same preprocessing as for the random forest model. **Make sure your step order is correct for the recipe.** Implement 10-fold cross-validation. Report the accuracy of the model.
5. Estimate a ridge logistic regression model to predict `grass`.[^ridge] Use the same recipe as for the $5$-nearest neighbors model. Implement 10-fold cross-validation, and utilize the same recipe as for the $k$-nearest neighbors model. Report the accuracy of the model.
6. Revisit the random forest model used previously. This time, implement hyperparameter tuning over the `mtry` and `min_n` to find the optimal settings. Use at least ten combinations of hyperparameter values. Report the best five combinations of values.
7. Select the best performing model. Train that recipe/model using the full training set and report the accuracy/ROC AUC using the held-out test set of data. Visualize the ROC curve.

 

Documentation for the other predictors (if the variable is not clearly coded) can be viewed [here](https://gssdataexplorer.norc.org/variables/vfilter). You can also run `?gss` to open a documentation file in R.

 

# Submit the assignment

Your assignment should be submitted as a set of two Quarto documents using the `gfm` (GitHub Flavored Markdown) format. Follow instructions on [homework workflow](/faq/homework-guidelines/#homework-workflow).

# Rubric

Needs improvement: Cannot get code to run or is poorly documented. No documentation in the `README` file. Severe misinterpretations of the results. Overall a shoddy or incomplete assignment.

Satisfactory: Solid effort. Hits all the elements. No clear mistakes. Easy to follow (both the code and the output). Nothing spectacular, either bad or good.

Excellent: Interpretation is clear and in-depth. Accurately interprets the results, with appropriate caveats for what the technique can and cannot do. Code is reproducible. Writes a user-friendly `README` file. Implements appropriate visualization techniques for the statistical model. Results are presented in a clear and intuitive manner.

[^rmse]: View the [documentation for `yardstick`](https://yardstick.tidymodels.org/reference/index.html#section-regression-metrics) to find the appropriate function for RMSE.
[^ridge]: `logistic_reg(penalty = .01, mixture = 0)`
