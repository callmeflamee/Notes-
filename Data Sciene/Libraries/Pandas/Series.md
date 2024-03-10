## What is Pandas
**Pandas is a fast, powerful, flexible and easy to use open source data analysis and manipulation tool, built on top of the Python programming language. Check [Official Documentation](https://pandas.pydata.org/about/index.html)

---
## Pandas Series
**A Pandas Series is like a column in a table. It is a 1-D array holding data of any type.**
```python
install micropip
await micropip.install('numpy')
await micropip.install('pandas')
import numpy as np
import pandas as pd
```
*It is a good practice to always import numpy together with pandas* 

---
### Series from different data types.
```python
#Strings
country = ['India','Usa','Brazil','Pakistan','Saudi Arab']
pd.Series(country)
'Series is written in pascal scale'
runs = [13,64,657,68,546,35,40]
pd.Series(runs)
etc..
```

**Adding a custom index**
```python
marks = [90,98,35,170]
subs = ['English','Maths','Physics','Computer Science']
pd.Series(marks,index=subs)
```

**Setting a name to the series**
```python
marks = pd.Series(marks,index=subjects,name="Flame's marks")
```

**Making a series from dictionary**
```python
marks = {
'maths':67,
'english':57,
'science':89,
'hindi':100
}

marks_series = pd.Series(marks,name="Flame's marks")
```

## Common Attributes:
1. *Size* : Tells the size of series
	```python
	marks_series.size
	```
2. *dtype* : Tells the dtype of series
```python
	marks_series.dtype
```
3. *is_unique* : Return True if the values are unique (not dupes)
```python
	marks_series.is_unique
```
4. *index* : Tells the index of the series
```python
	marks_series.index
```
5. *name* : Tells the name of the series
```python
	marks_series.name
```
6. *values* : Returns the value of series
```python
	marks_series.values
```
---
### Series from csv
**By default whenever we read a csv using pandas it is always shown as a dataframe, however we can convert it into a Series by setting the `squeeze` parameter as `True`

```python
movies = pd.read_csv("<Path/of/file>",index_col='title',squeeze=True)
```
---
## Series Methods:
- *Head :* Returns the first 5 values from the series by default
```python
movies.head(n) #The 'n' will only fetch 'n' number of values 
```
- *Tail :* Returns the last 5 values from the series by default
```python
movies.tail(n) #The 'n' will only fetch the 'n' number of values
```
- *Sample :* Returns a set of random rows from the series
```python
movies.sample(n) 
```
- *Value_counts :* Returns the frequency of the values in the series
```python
movies.value_counts()
```
- *Sort_values/index :* Returns the sorted version of the the series
```python
movies.sort_values()
```
- *Inplace :* (parameter) If set true, will make the changes permanent
```python
movies.sort_index(ascending=False,inplace=True)
```
- *Count :* Returns the count of the rows in the series
```python
movies.count()
```
- *Sum :* Returns the sum of all the values
```python
runs.sum()
```
- *Mean/Median/Mode/STD,Var :* Statistical methods
```python
runs.mean()
runs.median()
runs.mode()
runs.std() #Standard Deviation
runs.var() #Variance
```
- *Min/Max :* Returns the Min/Max of the series
```python
marks_series.min()
marks_series.max()
```
- *Describe :* Describes the series by providing statistical output at once
```python
runs.describe()

>>>count    365.000000
	mean     135.643836
	std       62.675023
	min       33.000000
	25%       88.000000
	50%      123.000000
	75%      177.000000
	max      396.000000
	Name: "Runs gained", dtype: float64
```
---
## Indexing & Slicing:
- **Integer Indexing:**
```python
runs[13] #Returns the 13th value from the series
```
- *Negative Indexing*
```python
runs[-1]
movies[-1]
```
  ***NOTE :*** **Negative indexing doesn't work on integer data type series
- *Slicing*  
```python
runs[-5:]
movies[10::10]
```
- *Fancy Indexing*
```python
movies[[1,3,56,60,4,33,44]]
```
- *Indexing with Index Labels*
```python
movies['2 States']
```
- *Boolean Indexing*
```python
runs[runs == 0].count() #Finding the number of ducks
runs[runs > 200]
movies[movies.value_counts > 20] #Actor played more than 20
```
- *Relational Operators*
```python
100 + marks_series #Will add 100 to all the values in the marks series
```
- *Membership Operator*
```python
'Alia Bhatt' in movies

>>> True
```

