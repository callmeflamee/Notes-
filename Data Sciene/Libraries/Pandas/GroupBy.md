We will be performing some group-by functions on the top 1000 movies dataset by IMDB
```python
import numpy as np
import pandas as pd
movies = pd.read_csv("IMDB_Top-1000_Movies")
movies.head()
```
>![[Pasted image 20240128195832.png]]

*Group-by is a builtin pandas function that makes a group of the specified column in the dataset*
```python
#Grouping by genres
genre = movies.groupby('Genre')
genre.mean()
```
>![[Pasted image 20240128200152.png]]
---
## Questions
- *Find the top 3 genres by total earnings*
```python
genres['Gross'].sum().sort_values(ascending=False).head(3)
```
- *Find the genre with the highest avg IMDB Rating*
```python
genres['IMDB_Rating'].mean().sort_values(ascending=False).head(1)
```
- *Director with the most popularity*
```python
movies.groupby('Director')['No_of_Votes'].sum().sort_values(ascending=False).head(1)
```
- *Highest rated movie of each genre*
```python
genres["IMDB_Rating"].max().sort_values(ascending=False)
```
- *Find the number of movies played by each actor*
```python
movies.groupby("Star1")["Series_Title"].count().sort_values(ascending=False)
```
---
## Attributes & Methods:
- *len :* find total number of groups. 
```python
len(genres)
>14

genres.nunique() #Gives the number of unique genres
>14
```
- *size :* find items in each group.
```python
genres.size()

>>> Action       172
Adventure     72
Animation     82
Biography     88
...
```
- *First, Last & Nth :* Returns the respective occurrence of value
```python
genres.first()  #Returns the first movie of all genres
genres.last() #Returns the last movie of all genres
genres.nth(7) #Returns the nth movie of all genres
```
- *Value_Counts :* Returns the number of value that group holds
```python
genres.value_counts()

>>>Drama        289
Action       172
Comedy       155
...
```
- *Get_Group :* Returns all the values of the specified group item
```python
genres.get_group("Fantasy") #Will return all the Fantasy movies
```
- *Groups :* Returns the index position of occurrence in an dictionary
```python
genres.groups()

>>>{'Action': [2, 5, 8, 10, 13, 14, 16, 29, 30, 31, 39, 42, 44, 55, 57, 59, 60, 63, 68, 72, 106, 109, 129, 130, 134, 140, 142, 144, 152, 155, 160, 161, ...]
```
- *Describe :* Describe function but for each group item
```python
genres.describe()
```
>![[Pasted image 20240128225818.png]]
- *Sample :* Randomly returns n number of values of every group item
```python
genres.sample(2,replace=True) #Replace is set to True because in some genres there are >=2 movies hence replace just returns them as is
```
- *Nunique :* Returns how many unique values are there in every group
```python
genres.nunique()

>>>
|Action|172|61|78|15|123|121|172|172|50|
|Adventure|72|49|58|10|59|59|72|72|3|...
```
- *AGG :* Aggregation method.
*Helps in selection of columns and also functions*
```python
#passing a dictionary
genres.agg(
{
'Runtime':'mean',
'IMDB_Rating':'mean',
'No_of_Votes':'sum',
'Gross':'sum',
'Metascore':'min'
}
)
```
>![[Pasted image 20240128230934.png]]
```python
#passing a list
genres.agg(['min','max','mean','sum'])
```
>![[Pasted image 20240128231030.png]]
```python
#Passing both dict and list
genres.agg(
{
'Runtime':['min','mean'],
'IMDB_Rating':'mean',
'No_of_Votes':['sum','max'],
'Gross':'sum',
'Metascore':'min'
}
)
```
>![[Pasted image 20240128231137.png]]
- *Looping :* Looping through all the values in all the group items
```python
#Highest rated movie of each genre
df = pd.DataFrame(columns=movies.columns)
for group,data in genres:
	df = df.append(data[data['IMDB_Rating'] == 
	data['IMDB_Rating'].max()])

df
```
>![[Pasted image 20240128231424.png]]
- *Apply :* Applying a user created function on all the group items
```python
def rank_movie(group):
	group['genre_rank'] =             
	group['IMDB_Rating'].rank(ascending=False)
	return group

genres.apply(rank_movies)
```
---
## Multiple Columns grouping
- *Find the most earning Actor & Director duo*
```python
duo = movies.groupby(["Star1","Director"])
duo["Gross"].sum().sort_values(ascending=False).head(1)

>>> Akira Kurosawa  Toshirô Mifune    2.999877e+09
```
- *Duo that has the best avg metascore*
```python
duo["Metascore"].mean().sort_values(ascending=False).head(1)
```
---
***NOTE:*** *Adding `.reset_index()` before `sort_values()` and then providing a parameter as index name in the sort function will return a dataframe rather than a series*

