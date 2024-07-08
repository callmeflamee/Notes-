Normalization is a technique often applied as part of data preparation for machine learning.The goal of normalization is to change the values of numeric columns in a dataset to use a common scale without distorting differences in the range of values or losing information.

There are many different techniques one can use to normalize the data such as:

## MinMax Scaling
---
The most popular form of normalization is MinMax Scaling and to achieve this we take every value of the column and then apply the following formula:
$$X_{i}=\frac{X_{i}-X_{min}}{X_{max}-X_{min}}$$
The values after applying the formula will always range between {0,1}

## Mean Normalization
---
Just like [[Feature Scaling & Standardization|Standardization]] we do mean centering here too by using the formula:
$$X_{i}=\frac{X_{i}-X_{mean}}{X_{max}-X_{min}}$$

This will range from {-1,1}

## MaxAbs Scaling
---
Also called as Mean Absolute Scaling is achieved by using the following formula:
$$X_{i}=\frac{X_{i}}{|X_{max}|}$$
It is used when our data consists of a lot of zeros i.e having a sparse data

## Robust Scaling
---
$$X_{i}=\frac{X_{i}-X_{median}}{IQR}$$
This is robust to outliers meaning if your data has a lot of outliers this method may help.

## Normalization vs Standardization
---
Most of the problems will be fixed using [[Feature Scaling & Standardization|Standardization]] tho there will be certain cases when you have to perform Normalization, (Normalization is often said when need be  to perform MinMax Scaling) when your dealing  with some values that have a fixed set of range for ex. image pixels have fixed color range i.e {1,255}.