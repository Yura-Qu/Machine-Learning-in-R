# Statistical Learning 

## $f$ 
### $Y=f(X)+\epsilon $
- $Y$ -- Response variables
- $X = (X_1, X_2,...,X_p)$ -- Predictors
- We assume that there is some relationship between Y and X
- $f$ is some fixed but unknown function of $X_1,...,X_p$
- ε Random error term, which is independent of X and has mean zero

### Why Estimate $f$
1. **Prediction**
   - $\hat{Y}=\hat{f}(X)$
     - $\hat{f}$ is the estimate of $f$
     - $\hat{Y}$ is the estimate of $Y$
     - the error term averages to zero
   - The accuracy of $\hat{Y}$ as a prediction for $Y$ depend on:
     > These 2 errors are the error introduced by the inaccurate estimate of $\hat{f}$
     > 
     > $E(Y −\hat{Y})^2 =  {\underset{Reducible}{[f(X) − \hat{f(X)}]^2}} + \underset{Irreducible}{Var(\varepsilon)}$
     1. Reducible error
        - we can potentially improve the accuracy of $\hat{f}$ by using the most appropriate statistical learning technique to estimate $f$
        - So that $\hat{Y} = f(X)$
     2. Irreducible error
        - The error introduced by ϵ
        - ϵ, which, by definition, cannot be predicted using $X$
        - The quantity ϵ may also contain unmeasured or unmeasurable variation, For example, the risk of an adverse reaction might vary for a given patient on a given day, depending on
manufacturing variation in the drug itself or the patient’s general feeling of well-being on that day
2. **Inference**
   > The association between $Y$ and $X_1,...,X_p$
   1. **Which predictors are associated with the response?**
      It is often the case that only a **small fraction** of the available predictors are substantially associated with Y
   2. **What is the relationship between the response and each predictor?**
      - Some predictors may have a positive relationship with Y , in the sense that larger values of the predictor are associated with larger values of Y .
      - Other predictors may have the opposite relationship.
      - Depending on the complexity of f, the relationship between the response and a given predictor may also depend on the values of the other predictors.
   3. Can the relationship between Y and each predictor be adequately summarized using a **linear equation**, or is the relationship more complicated?

### How Do We Estimate $f$?

- Generate 2 random sub-samples:
  1. Training dataset
  2. Test dataset
-  Apply a statistical learning method to the training data in order to estimate the unknown function $f$
  
```r
# Use 70% of dataset as training set and remaining 30% as testing set
sample <- sample(c(TRUE, FALSE), nrow(iris), replace=TRUE, prob=c(0.7,0.3))
train <- iris[sample, ]
test <- iris[!sample, ]
```
>
> ```r
> sample(x, size, replace = FALSE, prob = NULL)
> ```
> x: either a vector of one or more elements from which to choose, or a positive integer.
>
> size: a non-negative integer giving the number of items to choose.
>
> replace: should sampling be with replacement?
>
> prob: a vector of probability weights for obtaining the elements of the vector being sampled.

## Parametric Methods and Non-Parametric Methods

### Parametric methods / model-based approach
Parametric methods involve a two-step model-based approach.
1. First, we make an assumption about the functional form, or shape, of $f$.
   e.g. we can assume $f$ is linear in $X$
   ![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/0ad1a88f-e1f5-446a-886d-a33e75d3866e)
2. After a model has been selected, we need a procedure that uses the training data to fit or train the model. The most common approach to fitting the model is referred to
as least squares
> But we need to test our assumption about the shape of Y

### Non-Parametric Methods
Non-parametric methods do not make explicit assumptions about the functional form of $f$. Instead they seek an estimate of f that gets as close to the data points as possible without being too rough or wiggly. 
- Pro:
  **Accuracy**
  By avoiding the assumption of a particular functional form for $f$, they have the potential to accurately fit a wider range of possible shapes for $f$.
- Con:
  **Sample Size**
  A very large number of observations (far more than is typically needed for a parametric approach) is required in order to obtain an accurate estimate for f.

##  Supervised Versus Unsupervised Learning
### Supervised learning 
> For each observation of the predictor measurement(s) $x_i, i = 1,...,n$ there is an associated response measurement y_i. **(i.e. the y or the labelling is available)**
We wish to fit a model that relates the response to the predictors, with the aim of accurately predicting the response for future observations (prediction) or better understanding the relationship between the response and the predictors (inference).
- e.g.
  - Linear Regression
  - logistic Regression
  - GAM
  - Boosting
  - Support Vector Machines
> In **supervised learning (SML)**, the response variables or the labels are available. SML itself is composed of :
- classification, where the output is qualitative
   - Binary classification: two sets of labels, or classes. A classical example thereof is labelling an email as spam or not spam.
   - Multi-class problem: more than two classes
   - Multi-label classification: multiple labels may be assigned to each example
 - regression, where the output is quantitative.
### Unsupervised learning 
>  For every observation i = 1,...,n, we observe a vector of measurements $x_i$ but no associated response $y_i$. **(i.e. the y or the labelling is not available)**

Thus, we can study the relationships between the variables or between the observations.
- e.g. Clustering

> In unsupervised learning (UML), no labels are provided, and the learning algorithm focuses solely on detecting structure in unlabelled input data. One generally differentiates between
- Clustering, where the goal is to find homogeneous subgroups within the data; the grouping is based on distance between observations.
- Dimensionality reduction, where the goal is to identify patterns in the features of the data. Dimensionality reduction is often used to facilitate visualisation of the data, as well as a pre-processing method before supervised learning.


### Semi-supervised learning 
For instance, suppose that we have a set of n observations. For m of the observations, where m<n, we have both predictor measurements and a response measurement. For the remaining n − m observations, we have predictor measurements but no response measurement. The semi-supervised learning can incorporate the m observations for which response measurements are available as well as the n − m observations for which they are not.

##  The Trade-Off Between Prediction Accuracy and Model Interpretability
![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/09d6bdb1-33a3-418b-bafe-25f387e911d4)

For instance, 
- when inference is the goal, the linear model may be a good choice since it will be quite easy to understand the relationship between Y and $X_1, X_2,...,X_p$.
- In contrast, very flexible approaches, such as the splines and the boosting methods can lead to such complicated estimates of f that it is difficult to understand how any individual predictor is associated with the response.

> How to balance the trade-off between prediction accuracy and the model interpretability? The answer is **what is the question of interest**
> 
> We have established that when inference is the goal, there are clear advantages to using simple and relatively inflexible statistical learning methods. In some settings, however, we are only interested in prediction, and the interpretability of the predictive model is simply not of interest.
