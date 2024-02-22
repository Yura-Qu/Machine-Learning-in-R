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

### Making prediction using Logistic Regression Model 

![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/2605cdb2-9960-4f7b-afe3-4879b5cf46ea)

![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/b2ab029c-36a9-4b82-8da7-22ff2b87bf4f)

> The Default data set contains the qualitative variable student. To fit a model that uses student status as a predictor variable, we simply create a dummy variable that takes on a value of 1 for students and 0 for non-students.

![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/c0195b1f-a762-4d75-9fa7-79528c9cb575)

> The coefficient associated with the dummy variable is positive, and the associated p-value is statistically significant. This indicates that students tend to have higher default probabilities than non-students

### Other Variation of Logistic Regression Model

1. Multiple Logistic Regression
   predicting a binary response using multiple predictors
   
   ![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/127db8e4-3a99-435c-b006-c710da51d86f)

   ![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/0a134111-bcc6-480f-9cba-df4d0a2c62e0)

   - P-value
     - P-values associated with balance and the dummy variable for student status are very small, indicating that each of these variables is associated with the probability of default.
   - Value of Coefficients
     - Negative (e.g. student[Yes] = -0.6468)
       students are less likely to default than non- students.
       > However, in the second above, when we only use the student to predict default, the coefficient associated with the dummy variable is positive (i.e. student[Yes] = 0.4049)
       >
       > The negative coefficient for student in the multiple logistic regression indicates that for a fixed value of balance and income, a student is less likely to default than a non-student.
       >
       > This simple example illustrates the dangers and subtleties associated with performing regressions involving only a single predictor when other predictors may also be relevant. 
     - Positive (e.g. balance = 0.0057)
       
2. Multinomial Logistic Regression
   a response variable that has more than two classes.

## Linear Discriminant Analysis

It is a technique used to find a linear combination of features that best separates the classes in a dataset.

LDA works by projecting the data onto a lower-dimensional space that maximizes the separation between the classes. It does this by finding a set of linear discriminants that maximize the ratio of between-class variance to within-class variance. 

LDA assumes that the data has a Gaussian distribution and that the covariance matrices of the different classes are equal. It also assumes that the data is linearly separable, meaning that a linear decision boundary can accurately classify the different classes.

### Assumption 

1. Linearity: The relationships between the variables and the classes are assumed to be linear.
2. Normality: The variables within each class are assumed to be normally distributed.
3. Homoscedasticity: The variance of the variables is assumed to be equal across all classes.
4. Independence: The observations within each class are assumed to be independent.
5. Equal covariance matrices: The covariance matrices of the variables within each class are assumed to be equal.

### Pros and Cons 
**Pros:**

- **Dimensionality Reduction with Class Separation:** LDA maximizes class separation while reducing dimensions, enhancing efficiency and performance, especially with clear class distinctions.
  
- **Utilizes Class Information:** LDA leverages class labels for better separation compared to unsupervised methods.
  
- **Works Well for Small Sample Sizes:** Suitable for scenarios with limited training data relative to features.
  
- **Interpretable Results:** Reduced-dimensional representation aids understanding of classification factors.
  
- **Data Visualization:** LDA's reduced-dimensional space enables easy visualization of class separation and data distribution.
  
- **Robust to Outliers:** Less sensitive to outliers due to reliance on class means and variances.

**Cons:**

- **Sensitive to Class Distribution:** Performance degrades if classes violate assumptions of equal covariance matrices and Gaussian distribution.
  
- **Prone to Overfitting:** Can overfit with high feature-to-sample ratio; regularization or dimensionality reduction may be needed.
  
- **Doesn’t Handle Nonlinear Relationships:** Limited accuracy with nonlinear relationships.
  
- **Requires Well-Defined Classes:** Relies on clear class labels for optimal performance.
  
- **Doesn’t Incorporate Feature Interaction:** Ignores interactions between features, potentially impacting classification accuracy.
  
- **May Not Capture Complex Patterns:** Linear nature struggles with complex decision boundaries compared to nonlinear methods.
