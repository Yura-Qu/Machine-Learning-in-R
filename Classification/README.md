# Classification 
![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/2ada1d2d-3fde-4a55-bcec-a91cb48665f5)

> When the response variable is qualitative or categorical

## Logistic Regression

> When the response falls into one of two categories, Yes or No. Rather than modeling this response Y directly, logistic regression models the probability that Y belongs to a particular category.
> 
> $p(X)=\text{Pr}(Y=1|X)$ --- how likely it is for the variable Y to be 1 given a specific value of the variable X
> - $p(X)$ typically denotes the probability distribution of the variable X, which represents the probability of different outcomes or values that X can take.
> - $Pr(Y=1∣X)$ denotes the conditional probability that the random variable Y equals 1 given the value of X.

### Logistic Regression Model 

![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/bf62df94-71d5-49fa-8778-2f07a6b0ff8e)
-  $p(X)$  gives outputs between 0 and 1 for all values of X
- ![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/16f5da3d-8f9f-443f-943c-afa42d45e8b4)
  - The quantity **p(X)/[1−p(X)]** is called the odds
  - between 0 and ∞, 0 and ∞ indicate very low and very high probabilities of default
- ![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/b9306a9c-6f05-4c1a-8e37-268daf8100bf)
  - The left-hand side is called the log odds or logit
  - if β1 is positive then increasing X will be associated with increasing p(X)
  - if β1 is negative then increasing X will be associated with decreasing p(X)
  - there is not a straight-line relationship between p(X) and X
- **Interpretation of the logistic regression**
  - ![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/9a0b8810-ea0f-44f7-8d99-9b0a3f7cca1f)
  - $\hat{\beta_1}$ = 0.0055; this indicates that an increase in balance is associated with an increase in the probability of default. To be precise, a one-unit increase in balance is associated with an increase in the log odds of default by 0.0055 units.




### Logistic Regression V.S. Linear Regression 
1. **Nature of the dependent variable**: If your dependent variable is continuous, you should use linear regression. If it's categorical, especially binary or multinomial, logistic regression is more appropriate.
2. **Type of relationship**: Linear regression assumes a linear relationship between the independent and dependent variables, while logistic regression models the logarithm of the odds of the dependent variable. Logistic regression is better suited for modeling probabilities and handling non-linear relationships between variables.
3. **Interpretation**: In linear regression, the coefficients represent the change in the dependent variable for a one-unit change in the independent variable. In logistic regression, the coefficients represent the change in the log odds of the dependent variable for a one-unit change in the independent variable.

