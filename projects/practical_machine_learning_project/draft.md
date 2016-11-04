---
layout: default
---

# Practical Machine Learning Course Project

Using devices such as Jawbone Up, Nike FuelBand, and Fitbit it is now possible to collect a large amount of data about personal activity relatively inexpensively. These type of devices are part of the quantified self movement – a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. One thing that people regularly do is quantify how much of a particular activity they do, but they rarely quantify how well they do it.

In this project, I used data from accelerometers on the belt, forearm, arm, and dumbell of 6 participants. They were asked to perform barbell lifts correctly and incorrectly in 5 different ways. More information is available from the website [here](http://groupware.les.inf.puc-rio.br/har) (see the section on the Weight Lifting Exercise Dataset).

The training data for this project are available [here](https://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv).

The test data are available [here](https://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv).

The data for this project come from this [source](http://groupware.les.inf.puc-rio.br/har).

## What was the goal of the project?

The goal of this project is to predict the manner in which they did the exercise. This is the "classe" variable in the training set. Certain variables had to be excluded in order to correctly do the prediction. For example, it was not appropriate to use test subject as a predictor since in general we would not have information mapping who did the exercise to how they did it. This model was cross validated and correctly predicted 20 different test cases.

## Load Libraries

I haven't yet reformatted the code that follows so that there is output. To do that, I'd have to run the code with knitr. Something on my to do list.

```R
library(caret) #machine learning
library(e1071) #svm
library(rpart) #partition
library(randomForest) #random forests (is faster than caret)
```

## Reproducibility

```R
set.seed(1)
```

## Explore the Data

There are a number of different formats which values that are not available appear in.

```R
training <- read.csv("pml-training.csv", na.strings=c("", "NA", "#DIV/0!"), row.names = 1)
testing <- read.csv("pml-testing.csv", na.strings=c("", "NA", "#DIV/0!"), row.names = 1)
```

If we try `complete.cases` on train and test, we will eliminate most of the data. Fortunately, it looks like it is only some of the columns which are missing values, so we get rid of these.

```R
training <- training[,!sapply(training,function(x) any(is.na(x)))]
testing <- testing[,!sapply(testing,function(x) any(is.na(x)))]
```

Running `sum(complete.cases(training))` and similarly for the test set shows that we don't have any more NA values, so we might just use these features. But if we do, we'll run into problems later since random forests won't know what to do if it gets a new name of a person, which is one of the features. Thus, we will get rid of information that has no practical predictive ability, like people's names, so we get rid of the first 6 columns.

```R
training <-training[,-c(1:6)]
testing <-testing[,-c(1:6)]
```

## Partition Data

Now we need to split our training set into a training and validation set. We do so below.

```R
indices <- createDataPartition(y=training$classe, p=0.8, list=FALSE)
Train <- training[indices, ] 
Validation <- training[-indices, ]
```

## Train Data

This is a large data set, so we expect that random forests will perform the best. Let's try training with this algorithm. It's cheap to train different models, so let's try a few others.  Note: this will take a few minutes. We will try `svm` and `lda`. We could do many more, but limit ourselves to these cases.

```R
model_forests <- randomForest(classe ~ ., data = Train)
model_svm <- svm(classe ~. , data=Train)
model_lda <- train(classe ~. , data=Train, method="lda")
```

## Predict

Now that we have our model, we will see how well it does on the validation set with random forests.

```R
prediction_forest <- predict(model_forests, Validation, type = "class")
confusionMatrix(prediction_forest, Validation$classe)
```

We only missed a few values, so this is very good performance. Let's compare to the confusion matrix on the training set, which should be around at least as good.

```R
prediction_forest_train <- predict(model_forests, Train, type = "class")
confusionMatrix(prediction_forest_train, Train$classe)
```

Refreshingly, random forests does even better on the training data, as it should. Note that if we keep all variables, we get even better performance and appearance of good predictions on the validation data, but can't predict on the test data when we get names of new people. So we've overfit to the names of the people. The performance is still quite good, though.

Given this, we expect near perfect accuracy on the test data (validation data in the data science specialization convention).

```R
prediction_forest_test <- predict(model_forests, testing, type = "class")
prediction_forest_test
```

So random forests is probably sufficient, but let's just compare to other methods on the validation set.

```R
mean(predict(model_forests, Validation) == Validation$classe)
mean(predict(model_svm, Validation) == Validation$classe)
mean(predict(model_lda, Validation) == Validation$classe)
```

We could probably do better by combining the models, but we won't worry about that here.
