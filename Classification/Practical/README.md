## Logistics Rregression in R

### 1. Dataset `quality.csv`
```r
quality <- read_csv("quality .csv")
str(quality)
```
![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/642217f9-c6e8-4897-8add-404bfa3f7bc1)

- `PoorCare` is the outcome or dependent variable and is equal to 1 if the patient had poor care, and equal to 0 if the patient had good care.
- `OfficeVisits` and `Narcotics` as independent variables

### 2. Splitting Training & Testing Data

```r
> set.seed(123)
> sample <- sample(c(TRUE, FALSE), nrow(quality), replace=TRUE, prob=c(0.75,0.25))
> quality.train <- quality[sample, ]
> nrow(quality.train)
[1] 97
> quality.test <- quality[!sample, ]
> nrow(quality.test)
[1] 34
```
- 75% of the data in the training set -- build the model
- 25% of the data in the testing set -- test our model.

### 3. Fit the model 

```r
> logistic <- glm(PoorCare~OfficeVisits + Narcotics,
+                 data = quality.train,
+                 family = binomial)
> summary(logistic)

Call:
glm(formula = PoorCare ~ OfficeVisits + Narcotics, family = binomial, 
    data = quality.train)

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-1.4980  -0.6375  -0.4969   0.2184   2.1563  

Coefficients:
             Estimate Std. Error z value Pr(>|z|)    
(Intercept)  -2.79184    0.54675  -5.106 3.29e-07 ***
OfficeVisits  0.08676    0.02954   2.937  0.00331 ** 
Narcotics     0.15481    0.05564   2.782  0.00540 ** 
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 112.772  on 96  degrees of freedom
Residual deviance:  84.862  on 94  degrees of freedom
AIC: 90.862

Number of Fisher Scoring iterations: 5
```
- `family = binomial` for logistic regression
- The coefficients for `OfficeVisitsand` `Narcotics` are both positive, which means that higher values in these two variables are indicative of poor care as we suspected from looking at the data.
- AIC value: A low AIC is desirable.

### 4. Choose the Threshold

> The output of a Logistic regression model is a probability. We can select a threshold value "t". If the probability is greater than this threshold value, the event is predicted to happen otherwise it is predicted not to happen.
If the probability of poor care is greater than this threshold value, t, we predict poor quality care. But if the probability of poor care is less than the threshold value, t, then we predict good quality care.

**Choosing the t value use ROC curve**

```r
ROCRpred = prediction(log_pre, quality.train$PoorCare)
ROCRperf = performance(ROCRpred, "tpr", "fpr")
plot(ROCRperf, 
     colorize=TRUE, 
     print.cutoffs.at=seq(0,1,by=0.1), 
     text.adj=c(-0.2,1.7))
```
![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/d42508b6-1a85-470e-b505-5ff93b519f24)

- y-axis: sensitivity, or true positive rate
- x-axis: false positive rate, or 1 - specificity
- The line shows how these two outcome measures vary with different threshold values
  - (0, 0) i.e threshold of value 1: at this threshold we will not catch any poor care cases(sensitivity of 0) but will correctly label all the good care cases(FP = 0)

    **the higher the specificity and the lower the sensitivity**
  - (1, 1) i.e threshold of value 0: at this threshold we will catch all the poor care cases(sensitivity of 1) but will incorrectly label of all the good care case as poor cases(FP = 1)

    **the higher the sensitivity and lower the specificity**
  - (0, 0.4), we’re correctly labeling about 40% of the poor care cases with a very small false positive rate.
  - (0.6, 0.9), we’re correctly labeling about 90% of the poor care cases, but have a false positive rate of 60%
  - (0.3, 0.8), we’re correctly labeling about 80% of the poor care cases, with a 30% false-positive rate.
 
> Selection criterion: which one is more concerning? The sensitivity or the specificity?
- **Confusion Matrix**
  A confusion matrix is used to describe the performance of a classification model
  
  ![image](https://github.com/Yura-Qu/Machine-Learning-in-R/assets/143141778/eb8c1d84-446a-4ccc-b4ff-1bcb626e3905)
  - True positives (TP): These are cases in which we predicted yes (employees will leave the organisation), and employees actually leave i.e 100
  - True negatives (TN): We predicted no(employees will not leave the organisation) and they don’t leave i.e 50
  - False positives (FP): We predicted yes they will leave, but they don’t leave. (Also known as a “Type I error.”) i.e 10
  - False negatives (FN): We predicted no they will not leave, but they actually leave (Also known as a “Type II error.”) i.e 5
  - **Accuracy : (TP+TN)/Total**
  - Sensitivity/Recall = TP/(TP + FN). When it’s actually yes, how often does it predict yes? i.e 100/(100+5)
  - Specificity = TN/(TN + FP) .When it’s actually no, how often does it predict no?? i.e 50/(50+10)
- **ROC curve**
  - One should select the best threshold for the trade-off you want to make.
  - According to the criticality of the business, we need to compare the cost of failing to detect positives vs cost of raising false alarms.
  - High Threshold **closer to 1**
    - High specificity
    - Low sensitivity
  - Low Threshold:**Closer to 0**
    - Low specificity
    - High sensitivity
### 5. Making prediction on the test set
> threshold value = 0.3 
```r
> log_test <- predict(logistic,
+                      newdata = quality.test,
+                      type = "response")
> 
> table(quality.test$PoorCare,log_test >= 0.3)
   
    FALSE TRUE
  0    20    7
  1     2    5
> 
> (20+5)/(20+5+2+7)
[1] 0.7352941
```
The model can accurately identify patients receiving low-quality care with test set accuracy being equal to 74% which is greater than our baseline model.
