Series are 1D objects and dataframe are 2D objects
*But how exactly are they 1D or 2D??*
The dimension of [[Series]] is 1D because inorder to fetch a particular value we need to only provide one input for example, if we have the following series:

| name    | age |
| ------- | --- |
| Mukesh  | 33  |
| Flame   | 18  |
| Mustufa | 20  |
*So in order to get the age of flame we only provide one input such as `ages['Flame']`*
and we get the desired output.

---
Let's make a series with multi indexes
```python
import pandas as pd
import numpy as np

index_val = [('cse',2019),('cse',2020),('cse',2021),('cse',2022),('ece',2019),('ece',2020),('ece',2021),('ece',2022)]
a = pd.Series([1,2,3,4,5,6,7,8],index=index_val)
a
```
>(cse, 2019)    1
 (cse, 2020)    2
 (cse, 2021)    3
 (cse, 2022)    4
 (ece, 2019)    5
 (ece, 2020)    6
 (ece, 2021)    7
 (ece, 2022)    8
 dtype: int64
 
 The above is a series that has multiple indexes in a tuple and we are also required to provide 2 inputs inorder to get a particular value, But with the above method there also exist the following problem
```python
a['cse'] 
```
*The above code throws an error saying that there is no such index as 'cse'.* Hence meaning that the above is not *truly* a multi index series
Solution? To make a Multi Index series (hierarchical indexing) 
```python
index_val = [('cse',2019),('cse',2020),('cse',2021),('cse',2022),('ece',2019),('ece',2020),('ece',2021),('ece',2022)]

multiindex = pd.MultiIndex.from_tuples(index_val)
s = pd.series([1,2,3,4,5,6,7,8],index=multiindex)
s
```
cse  2019    1
     2020    2
     2021    3
     2022    4
ece  2019    5
     2020    6
     2021    7
     2022    8
dtype: int64
**Now the above is a truly multi index series**,*now you may recognize this from [[Merging#Multi-Index Dataframe|here]] but those `keys` are different yet the fundamental idea is the same*
Now the problem we talked about above is solved here
```python
s['cse']

>>> 2019    1
	2020    2
	2021    3
	2022    4
	dtype: int64
```
---
## Unstack and Stack
There are 2 functions related to this very topic, 
 - Unstack : this method makes the first level of index into columns
 - stack : this method makes the columns into the first level of index
*What are levels?*
```python
multiindex = pd.MultiIndex.from_product([['cse','ece'],[2019,2020,2021,2022]])
multiindex.level[0]
multiindex.level[1]

>>>Index(['cse', 'ece'], dtype='object')
>>>Int64Index([2019, 2020, 2021, 2022], dtype='int64')
```
The outermost index of the series/dataframe is the 0th level of index

---
## MultiIndex Dataframe
```python
branch_df1 = pd.DataFrame(
[
[1,2],
[3,4],
[5,6],
[7,8],
[9,10],
[11,12],
[13,14],
[15,16],
], index = multiindex, columns = ['avg_package','students'])

branch_df1
```

|  |  | avg_package | students |
| ---- | ---- | ---- | ---- |
| cse | 2019 | 1 | 2 |
|  | 2020 | 4 | 4 |
|  | 2021 | 6 | 6 |
|  | 2022 | 8 | 8 |
| ece | 2019 | 9 | 10 |
|  | 2020 | 12 | 12 |
|  | 2021 | 14 | 14 |
|  | 2022 | 16 | 16 |
**The above is a 3D dataframe since we would need to provide it with 3 inputs to get a particular value for e.g. `branch_df1[['cse',2022]][student]`**
Are columns really different from indexes?
```python
#Multi index dataframe from cols perspective
branch_df2 = pd.DataFrame(
[
[1,2,0,0],
[3,4,0,0],
[5,6,0,0],
[7,8,0,0],
],index = [2019,2020,2021,2022],
columns = pd.MultiIndex.from_product([['delhi','mumbai'],['avg_package','students']]))

branch_df2
```
>![[Pasted image 20240207195435.png]]
```python
branch_df3 = pd.DataFrame(
[
[1,2,0,0],
[3,4,0,0],
[5,6,0,0],
[7,8,0,0],
[9,10,0,0],
[11,12,0,0],
[13,14,0,0],
[15,16,0,0],
],index = multiindex,
columns = pd.MultiIndex.from_product([['delhi','mumbai'],['avg_package','students']]))
 
branch_df3
```
>![[Pasted image 20240207195619.png]]

***Perfroming multiple stack and unstack operations***
```python
branch_df3.stack()
```
>![[Pasted image 20240207195745.png]]

```python
branch_df3.stack().stack()
```
>![[Pasted image 20240207195833.png]]

```python
branch_df3.unstack()
```
>![[Pasted image 20240207195941.png]]
```python
branch_df3.unstack().unstack()
```

```python
branch_df3.loc[('cse',2022)]
branch_df3.loc[('cse',2019):('ece',2020):2]
```
**iloc:**
```python
branch_df3.iloc>![[Pasted image 20240207200127.png]]
---
## Indexing and slicing
**loc:*[0:5:2]
branch_df3.iloc[:,1:3]
branch_df3.iloc[[0,4],[1,2]]
```
---
## Sort Index
```python
branch_df3.sort_index(ascending=False)
branch_df3.sort_index(ascending=[False,True])
branch_df3.sort_index(level=0,ascending=[False])
```
---
### Transpose and Swaplevel
**transpose:**
```python
branch_df3.transpose()
```
>![[Pasted image 20240207200742.png]]

**swaplevel**
```python
branch_df3.swaplevel()
#set axis = 1 for columns wise
```
>![[Pasted image 20240207200900.png]]
---
## Long data VS Wide data

![[Pasted image 20240207203412.png]]
**Wide format** is where we have a single row for every data point with multiple columns to hold the values of various attributes.

**Long format** is where, for each data point we have as many rows as the number of attributes and each row contains the value of a particular attribute for a given data point.
### Melt method:
The melt method is used to convert wide data to long data
```python
df = pd.DataFrame({'cse':[120],'ece':[100],'mech':[50]})

>>>|cse|ece|mech|
 |0|120|100|50|

df.melt()

>>>| |variable|value|
  |0 |   cse  | 120 |
  |1 |   ece  | 100 |
  |2 |  mech  | 50 |

df.melt(var_name='branch',val_name='num_of_students')

>>>| |branch|num_of_students|
  |0 | cse  | 120 |
  |1 | ece  | 100 |
  |2 | mech | 50  |
```
**Real world example**
```python
death = pd.read_csv('/content/time_series_covid19_deaths_global.csv')

confirmed = pd.read_csv('/content/time_series_covid19_confirmed_global.csv')
```
*In the above 2 datasets there are 1081 columns in each and the reason is that there is a column for every date from 2020 to 2023*

Our task is to create a new dataset that has only these 4 columns
**Country, Date, Confirmed Cases & Death Count**

To do that we need to merge the two dataset and then make the date column into one.
```python
death = death.melt(id_vars=['Province/State','Country/Region','Lat','Long'],var_name='Date',value_name='num_deaths')

confirm = confirm.melt(id_vars=['Province/State','Country/Region','Lat','Long'],var_name='Date',value_name='num_cases')
```
*Now we have reduced the number of columns as we have transfered all the dates into one single column*
The `id_vars` parameter, allows us to skip the specified columns into being melted.
```python
new_df = pd.merge(confirmed,death, on=['Date','Country/Region','Lat','Long'])['Country/Region','Date','num_cases','num_deaths']

>>>311253 rows x 4 columns
```
We can also perform grouby on the country columns to further reduce the number of rows as well.

---
# Pivot Table
**The pivot table takes simple column-wise data as input, and groups the entries into a two-dimensional table that provides a multidimensional summarization of the data.**
```python
df = sns.load_dataset('tips')
df.head()
```
>![[Pasted image 20240210160012.png]]
```python
df.groupby('sex')[['total_bill']].mean()
df.groupby(['sex','smoker'])[['total_bill']].mean().unstack()
```
The above code(s) helps us to better visualize the data, however the same functionality can be achived with pivot tables with much ease and efficenciy 
```python
df.pivot_table(index='sex',column='smoker',values='total_bill')
```
>![[Pasted image 20240210160350.png]]

*By default, the aggregate function is set to mean, but we can change it or even pass multiple aggregation ways*
```python
df.pivot_table(index='sex',columns='smoker',values='total_bill',aggfunc='std')
#Multi Dimensional
df.pivot_table(index=['sex','smoker'],columns=['day','time'],aggfunc={'size':'mean','tip':'max','total_bill':'sum'},margins=True)
```
The `margins` parameter shows an extra row and also a column at the end of the dataframe that computes the agg of all the rows and is called "ALL"  
>![[Pasted image 20240210161732.png]]
