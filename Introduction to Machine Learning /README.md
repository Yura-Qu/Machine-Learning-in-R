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
