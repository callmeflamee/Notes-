## Strings
There are some probelms in vanilla python
such as the following,
```python
a = ['snake','cat',None,'bat','sat']
[i.endswith('t') for i in a]
```
Now the above code throws an error because there is a 'None' object in the middle of the list and hence python is not able to perform operations on a non-homogenous list.
*How does pandas solve this issue?*
```python
s = pd.Series(['cat','mat',None,'rat'])
# string accessor
s.str.startswith('c')
```
The `.str` method is a string operator that we must use whenever we try to acess an 'object' dtype in a series or a dataframe.

*For the following code, we will be using the [titanic dataset](https://www.kaggle.com/competitions/titanic/data)*
```python
df = pd.read_csv("titanic.csv")
df['name']

>Braund, Mr. Owen Harris
1      Cumings, Mrs. John Bradley (Florence Briggs Th...
2                                 Heikkinen, Miss. Laina
3           Futrelle, Mrs. Jacques Heath (Lily May Peel)
```
Let's seprate the names into thier individual columns as title, first name, last name.
```python
df['last_name'] = df['name'].str.split(',').str.get(0) 
```
>![[Pasted image 20240210163250.png]]
```python
df[['title','first_name']] = df['Name'].str.split(',').str.get(1).str.strip().str.split(' ',n=1,expand=True)
```
*There are few new parameters used in the above code, such as `expand` when this is set as "True" the output which is a series gets converted into a dataframe. And the `n=1` says to only split on the first space and not at anyother space*

Now if we print the title column we will see some titles being named differently, but they mean the same thing such as "Miss","Mlle" and "Ms."
so we use the `replace` function in python to correct them.
```python
df['title'].str.replace(['Ms.','Mlle'],'Miss')
```
---
# DateTime
*DateTime is functionality that exists both in python and in pandas*
To use DateTime in vanilla python we need to import it:
```python
import datetime as dt
x = pd.Timestamp(dt.datetime(2023,1,5,9,21,56))
x
>>> Timestamp('2023-01-05 09:21:56') #Time is stored in 24 hour format
```
In Pandas, there are two objects in the DateTime category
1. TimeStamp
2. TimeIndex

So what was the reason to create a [[Class & Objects|class]] when it already existed as a builtin library in vanilla python?
→Because of the uniform type in NumPy datetime64 arrays, this type of operation can be accomplished much more quickly than if we were working directly with Python's datetime objects, especially as arrays get large 
->Pandas Timestamp object combines the ease-of-use of python datetime with the efficient storage and vectorized interface of numpy.datetime6    
→From a group of these Timestamp objects, Pandas can construct a DatetimeIndex that can be used to index data in a Series or DataFrame

---
## TimeStamp
Time stamps reference particular moments in time (e.g., 25th Dec, 2023 at 7:00pm)

*Let's create a timestamp*
```python
pd.Timestamp('2023-1-5')
pd.Timestamp('2023, 1, 5')
#Time is automatically set to midnight if not provided
pd.Timestamp('2024')
#Auto chooses the first day of the first month at midnight
pd.Timestamp('5th January 2024')
pd.Timestamp('1st January 2024 at 12AM')
#Pandas is able to interpret text as date&time too
```

*Using datetime attribute and also its attribute*
```python
import datetime as dt
x = pd.Timestamp(dt.datetime(2024,1,21,21,26,42))
>>> Timestamp('2023-01-05 09:21:56')

x.year
x.month
x.month_name
x.day
x.day_name
...
```

Even numpy has a datetime datatype
```python
import numpy as np
date = np.array('2010-09-01', dtype=np.datetime64)
>>>array('2015-07-04', dtype='datetime64[D]')

date + np.arange(12) #Performing vertorized operations
```
->Because of the uniform type in NumPy datetime64 arrays, this type of operation can be accomplished much more quickly than if we were working directly with Python's datetime objects, especially as arrays get large 
->Pandas Timestamp object combines the ease-of-use of python datetime with the efficient storage and vectorized interface of numpy.datetime64
->From a group of these Timestamp objects, Pandas can construct a DatetimeIndex that can be used to index data in a Series or DataFrame

---
## DateTime Index
*A collection of pandas TimeStamps* 
```python
# using python datetime object
pd.DatetimeIndex([dt.datetime(2023,1,1),dt.datetime(2022,1,1),dt.datetime(2021,1,1)])

# using pd.timestamps
dt_index = pd.DatetimeIndex([pd.Timestamp(2023,1,1),pd.Timestamp(2022,1,1),pd.Timestamp(2021,1,1)])
```
---
### Date_Range Method: 
- Generate daily dates in a given range:
```python
pd.date_range(start='2023/1/5',end='2023/2/28',freq='D')
```
- Alternate days in the given range:
```python
pd.date_range(start='2023/1/5',end='2023/2/28',freq='2D')
```
- **B**: Buisness Days
```python
pd.date_range(start='2023/1/5',end='2023/2/28',freq='B')
```
- **W:** One week per day 
```python
pd.date_range(start='2023/1/5',end='2023/2/28',freq='W')
#Start week from custom day
pd.date_range(start='2023/1/5',end='2023/2/28',freq='W-Fri')
```
- **H:** Hourly Basis
```python
pd.date_range(start='2023/1/5',end='2023/2/28',freq='H')
#Set custom hourly interval
pd.date_range(start='2023/1/5',end='2023/2/28',freq='8H')#8hours
```
- **M/MS:** Month end and start respectively
```python
pd.date_range(start='2023/1/5',end='2023/2/28',freq='M')
pd.date_range(start='2023/1/5',end='2023/2/28',freq='MS')
```
- **A:** Year End
```python
pd.date_range(start='2023/1/5',end='2023/2/28',freq='A')
```
- **Periods:** Using peroids instead of end parameter to get n results
```python
pd.date_range(start='2023/1/5',periods=25,freq='M')
```
---
### To_Datetime Method:
*Convert existing string to pandas Timestamp/DateTime Index object*
```python
s = pd.Series(['2023/1/1','2022/1/1','2021/1/1'])
pd.to_datetime(s).dt.day_name()
```
Now, sometimes the data may be inaccurate in such a way that the month number is >1 or the day number is >31. In such cases pandas will simply throw an error, so to avoid it we have a parameter:
```python
s = pd.Series(['2023/1/1','2022/1/1','2021/130/1'])
pd.to_datetime(s,errors='coerce').dt.month_name()
```
*In the above the `errors` parameter is set to the value "coerce" which basically returns a null value towards the date that threw the error*
There are a total of 3 values that can be passed in the `errors` parameter:
- *raise:* `default` Invalid parsing will throw an error
- *coerce:* Will replace the invalid parsing will be replaced with "NaT"
- *ignore:* Invalid prasing will retrun the input
