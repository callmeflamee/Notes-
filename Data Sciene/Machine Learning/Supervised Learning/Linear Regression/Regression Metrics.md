These metrics are used to test the efficiency of our model, there are many metrics that are used throughout the machine learning domain, let's have a look at 5 of such metrics which helps in evaluating out linear regression model.

## The metrics
---
- MAE - Mean Absolute Error
- MSE - Mean Squared Error
- RMSE - Root Mean Squared Error
- R2 Score / Co-efficient of determinant 
- Adjusted R2 Score

### MAE
---
consider the following Linear Regression line expressed in red color
![[Pasted image 20240708224545.png]]
As we can see the line drawn by our linear regression model is quite off and lets call the correct (target) value as y1 and the estimated value as y-hat1. Similarly for the 2nd,3rd and 4th point, we will subtract it from the estimated value and consider the magnitude.

The formula is as follows:
$$MAE = \frac{\sum_{i = 1}^{n}|Y_{i}-\hat{Y}_{i}|}{n}$$
And the whole Idea is to reduce the MAE



| Advantages         | Disadvantages                                        |
| ------------------ | ---------------------------------------------------- |
| Same Unit          | Graph not being differenciable at 0 cause of Modulos |
| Robust to outliers |                                                      |

### MSE 
---
To counter the disadvantage posed by MAE we use MSE,
![[Pasted image 20240709203020.png]]
Finding the square of the distances

the formula for MSE is:

$$MSE=\frac{\sum_{i=1}^{n}(Y_{i}-\hat{Y}_{i})^{2}}{n}$$
The idea is same here too, i.e to minimize the value.

| Advantage                                              | Disadvantage           |
| ------------------------------------------------------ | ---------------------- |
| Can be used in loss function since it's differentiable | Not robust to outliers |
|                                                        | Not the same unit      |

### RMSE
---
RMSE is just root over of MSE 
The advantage this gives is that it makes the same unit but is again robust to outliers

$$RMSE=\sqrt{ MSE }$$
$$RMSE=\sqrt{  \frac{\sum_{i=1}^{n}(X_{i}-\hat{X_{i}})^{2}}{n}  }$$
### R2 Score 
---
It checks by what magnitude is your linear regression line better than the mean line.

$$1-\frac{SS_{r}}{SS_{m}}$$
R2 score would be 0 when your regression line and mean line overlap meaning that your regression line is useless. And it would be 1 when your Regression Line isn't making any error and is passing through each and every point.
Therefore the more near 1 your R2 score is the better is your Linear Regression model.

Interpreting the R2 score:
Let's suppose you have 2 columns i.e {cgpa,LPA} and you plot a LR model and the R2 score you get is 0.8 i.e 80%, this means that the cgpa column in your data is able to explain 80% of the variance in the LPA col and the rest 20% is un-explainable using the cgpa column, then by adding a 3rd column let's say of IQ we might get a better R2 score of let's say 0.9 i.e 90% and this means that using both the input columns they are able to explain 90% of the variance in the LPA column.

There is also a disadvantage in R2 Score:
As we saw above how adding more relevant columns might help increase the R2 score but adding irrelevant columns will also decrease the R2 Score, like imagine if we add a column of temperature which doesn't hold any correlation with the LPA column but R2 will decrease as it will not contribute to explaining the variance.

### Adjusted R2 Score
---
To counter the above disadvantage we have adjusted R2 Score,
Mathematically can be defined as;
$$AR2=1-\frac{(1-R2)(1-n)}{n-1-k}$$
where;
n = number of rows.
k = no of independent columns i.e input columns.
R2 = original R2 Score.

