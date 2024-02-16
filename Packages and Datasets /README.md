# Installing the packages 

```{r}
install.packages("caret")
install.packages("mlbench")
install.packages("caTools")
install.packages("randomForest")
install.packages("ranger")
install.packages("kernlab")
install.packages("glmnet")
install.packages("naivebayes")
```

# Loading the packages 

```{r}
library("caret")
library("ggplot2")
library("mlbench")
library("class")
library("caTools")
library("randomForest")
library("ranger")
library("kernlab")
library("glmnet")
library("naivebayes")
library("rpart")
library("rpart.plot")
library("MASS")
```

# Datasets 

```{r}
data("iris")
data(mtcars)
data(diamonds)
data(Sonar)
data(Boston)
data(mlc_churn, package = "modeldata")
churnTrain <- mlc_churn[1:3333, ]
churnTest <- mlc_churn[3334:5000, ]
```

