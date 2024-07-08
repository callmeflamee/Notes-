one of the few things we do in Feature Engineering is Feature Scaling now generally speaking Feature Scaling is the last thing that is needed to do in the Feature Engineering pipeline, but because it is feasible to do we will start from here.

**Feature Scaling is a technique to standardize the independent features present in the data in a fixed range**

---

## Why do we need Feature Scaling?

Suppose you have a dataset consisting of 3 labels, Age, Salary & Purchased?
And it is pretty obvious that the range of all of the mentioned labels will be wary by a lot, we know that the maximum age can only be of 2 digits (3 digits in exceptional cases) and the salary of the persons itself starts from 5 digits and the value of "Purchased?" would be of a single digit i.e "1" or "0".

So when applying an algorithm such as KNN which calculates the difference between two points, a non scaled data will have an ugly effect on the result and hence to improve its predictions we often scale our data 
![[Pasted image 20240629204035.png]]

---
## Types of Feature Scaling
It is split into two broad categories:
1. Standardization

2. Normalization
	1. Min-Max Scalar

---
# Standardization
It is a technique in which we scale down each value by first subtracting it with the entire columns mean and then further dividing it with the standard deviation of the column.

![[Pasted image 20240629204504.png]]
After Standardization we receive the values of which the mean is 0 and the standard deviation is 0.
### Effect on outliers?
There is no effect on outliers after standardization of the values, the values which were an outlier before scaling will continue to remain as an outlier.

---
## When to use standardization?
When we standardize our values that is no negative effect on any algorithm by default which seems like a no-brainer, however there are certain algorithms such as decision trees which have no effect of standardization so weather we apply it or not it doesn't seem to make a difference so why not save the effort of doing it. 

Here is a list of algorithms that have no effect of scaling:
![[Pasted image 20240629211350.png]]



