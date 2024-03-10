**A collection of [[Series]] Is called as a [[DataFrame]] 

## Making a DataFrame:
```python
import pandas as pd
import numpy as np

student_data = [
[100,80,10],
[90,70,7],
[120,100,14],
[80,50,2]
]
  
pd.DataFrame(student_data,columns=['iq','marks','package'])
```
*Output:*

| - | IQ | Marks | Package |
| ---- | ---- | ---- | ---- |
| 0 | 100 | 80 | 10 |
| 1 | 90 | 70 | 7 |
| 2 | 120 | 100 | 14 |
| 3 | 80 | 50 | 2 |
```python
student_dict = {
'name':['nitish','ankit','rupesh','rishabh','amit','ankita'],
'iq':[100,90,120,80,0,0],
'marks':[80,70,100,50,0,0],
'package':[10,7,14,2,0,0]
}
  
students = pd.DataFrame(student_dict)
students.set_index('name',inplace=True)
students
```
|      - | iq | marks | package |
| ---- | ---- | ---- | ---- |
| **name** |  |  |  |
| nitish | 100 | 80 | 10 |
| ankit | 90 | 70 | 7 |
| rupesh | 120 | 100 | 14 |
| rishabh | 80 | 50 | 2 |
| amit | 0 | 0 | 0 |
| ankita | 0 | 0 | 0 |
*The name column is the index column where we have specified a custom name for the index*
```python
# using read_csv
movies = pd.read_csv('movies.csv')
movies.head()
```
*The `head()` function gives us the top 5 values by default*

---
## DataFrame Attributes and Methods:
*Apart from all the [[Series]] methods being applicable, here are some more:*

- **dtypes :** Returns the datatype of each column.
```python
	movies.dtypes
	>>> ID                   int64
	    City                object
		Date                object
		Season              object
		MatchNumber         object
		---
```
- **index :** Returns the range of the dataframe.
```python
	movies.index
	>>> RangeIndex(start=0, stop=1629, step=1)
```
- **columns and values :** Returns the col names and values respectively.
```python
	students.columns
	movies.values
	>>> Index(['iq', 'marks', 'package'], dtype='object')
	>>> values function will return a numpy array of all values
```
- **info :** Returns a short column wise summary of the data.
```python
	movies.info()
	>>>RangeIndex: 1629 entries, 0 to 1628 Data columns (total 18 columns):
		Column Non-Null Count Dtype
	  0 title_x 1629 non-null object 
	  1 imdb_id 1629 non-null object
	  -------------------------------
```
- **is null:** Returns the True if a null value is found in a particular row.
```python
	movies.isnull().sum()
	>>> title_x        0
        imdb_id        0
		poster_path    103
```
 - **duplicated:** Returns True if the value is duplicated.
```python
	movies.duplicated().sum()
	>>> 0
```
- **rename:** Will rename column.
```python
students.rename(columns={'marks':'percent','package':'lpa'},inplace=True)

"Inplace will make the changes permanent"
```
---
## Selection/Indexing & Slicing:
- **Selecting Columns:**
```python
movies["Actors"]
movies[["Actors", "imdb_rating", "title"]]
```
### There are two methods for selecting in a dataframe:
1. **loc:** Searches using index labels
2. **iloc:** Searches using index position

1. ***iloc:***
```python
#single row
movies.iloc[5] "Will Return the entire 5th row"
movies.iloc[:5] "Will return the first 5 rows"

#Fancy Indexing
movies.iloc[[0,4,5]] 

#Multiple columns and rows
movies.iloc[:3,:3] "Will return the first 3 rows and only 3 columns"
```

2. ***loc:***
```python
#single row
students["Nitish"] "Will return all rows of 'Nitish'"


#Fancy Indexing
students[['nitish','ankita']]

#Multiple cols and rows
students["Nitish:Rishab"]
movies.loc[0:2,'title_x':'poster_path']
```
*Note: loc will even return the last specified index unlike python or iloc*

---
## Filtering Data:
- *Find all the winners of IPL*:
```python
ipl[ipl['MatchNumber'] == 'Final'][['Season','WinningTeam']]
# Season is the year they played in
```
- *How many superover finishes have occurred?*
```python
ipl[ipl['Superover' == 'Y']].shape[0]
```
- *How many matches has CSK won in Kolkata?*
```python
ipl[(ipl['City'] == 'Kolkata') & (ipl['winning_team'] == 'CSK')].shape[0]
# Bitwise and(&) when dealing in boolean
```
- *Toss winner is match winner in percentage:*
```python
(ipl[ipl['Toss_winner'] == ipl['winning_team']].shape[0]/ipl.shape[0])*100
```
- *Movies with rating higher than 8 and no of votes >10000*
```python
movies[(movies['imdb_rating'] > 8) & (movies['imdb_votes'] > 10000)].shape[0]
```
- *Action movies with rating higher than 7.5*
```python
#Since there are multiple genres in one movie we split
movies['genre'].str.split('|').apply(lambda x:'Action' in x)
#Or we follow a cleaner apporach
movies[(movies['genre'].str.contains("Action")) & (movies['imdb_rating'] > 7.5)].shape[0]
```
---
## Adding a new column:
```python
#A new one
movies["Country"] = "India"
```
*The above will be added for all the rows*
```python
#From an existing one
movies["lead_Actor"] = movies["Actors"].str.split("|").apply(lambda x:x[0])
```
---
## Important Methods of DataFrame:
- *astype :* Changes the dtype of that particular column.
```python
movies['is_adult'] = movies["is_adult"].astype("category")
#No inplace parameter here hence we do manually
```
