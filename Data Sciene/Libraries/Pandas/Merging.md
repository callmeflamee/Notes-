## Concatenation
*Concatenation means to add a dataset on to another dataset weather vertically (by default) or horizontally by specifying `axis=1`*
```python
courses = pd.read_csv('courses.csv')
students = pd.read_csv('students.csv')
nov = pd.read_csv('reg-month1.csv')
dec = pd.read_csv('reg-month2.csv')
matches = pd.read_csv('matches.csv')
delivery = pd.read_csv('deliveries.csv')
```
**The above are the 6 datasets used in the following content.**

Let's concat the month November and December first,
```python
pd.concat(["nov","dec"])
```
*The above will give us a merged [[DataFrame]], this dataframe will have a index starting at 0 and ending at the last index of `nov` and after will again start from zero till the last index of `dec`*
**We can eliminate the above thing by setting the parameter `ignore_index` as True.**
```python
regs = pd.concat(["nov","dec"],ignore_index=True)
```
There is another way of concatenating by using the `append` method.
```python
nov.append(dec,ignore_index=True)
```
**Horizontal concatenation**
```python
pd.concat(["nov","dec"],axis=1,ignore_index=True)
```
>![[Pasted image 20240201200436.png]]

---
## Multi-Index Dataframe:
```python
multi = pd.concat([nov,dec],keys=['Nov','Dec'])
```
>![[Pasted image 20240201200015.png]]

**Indexing on a Multi-Index dataframe:**
```python
multi.iloc["Dec",4]
```
---
## Joins

**Joins are a way of merging two dataframes on the basis of a common column.
![[Pasted image 20240201200555.png]]
**There are 4 types of joins as seen above**
1. Inner Join
2. Right Join
3. Left Join
4. Outer Join / Full Join

*Pandas provides all the above types of joins with simplicity in pandas we call joins as "merge"*
For performing join operations we need to have one common columns between the two datasets.

### Inner Join:
*An inner join will join the two dataframes on the specified common column and will only provide the values which are present in both the dataframe.*
```python
students.merge(regs,how="inner",on="student_id")
```
- *merge :* This is how pandas refer to joins as
- *how :* This parameter will differentiate between different joins
- *on :* We specify the common column here
>![[Pasted image 20240201201416.png]]

### Left Join:
*A left join will also join the two dataframes on the basis of the common column but unlike inner which only outputs the values present in both the dataframe it will output all the values from the left dataframe regardless of their commonness*
```python
courses.merge(regs,how='left',on='course_id')
```
As we can see there are certain missing values on the right table
>![[Pasted image 20240201201825.png]]

### Right Join:
*Similar to [[Merging#Left Join|Left Join]] but in the opposite directions*

### Outer Join / Full Join:
*An outer join will output all the values form both the tables regardless of their commonness*
```python
students.merge(regs,how='outer',on='student_id').tail(10)
```
>![[Pasted image 20240201202240.png]]

**Besides the four general joins specified above we also have one more specialized join that is called as "Self Join" in which the dataframe basically merges with it self like so:
```python
students.merge(students,how='inner',left_on='partner',right_on='student_id')
```
In the above we are specifying the `on` parameter twice as `left_on`&`right_on` for left and right dataframes respectively.**

---
## Questions:
- find total revenue generated:
```python
regs.merge(courses,on="course_ID")["price"].sum()
#Since inner join is default we don't have to specify here
```
- Find month by month revenue
```python
tdf = pd.concat(["nov","dec"],keys=["Nov","Dec"]).reset_index()
tdf.merge(courses,on="course_id").groupby("level_0")['price'].sum()
#Level_0 is the col created by reset_index method
```
- Print the registration table in the following format:                           cols -> name -> course -> price
```python
regs.merge(students,on="student_id").merge(course,on="course_id")[["name","course_name","price"]]
```
- Plot a bar chart for revenue/course
```python
regs.merge(courses,on="course_id").groupby("course_name")["price"].sum().plot(kind="bar")
```
>![[Pasted image 20240201203610.png]]

- Find the students who enrolled in both the months
```python
common_id = np.intersect1d(nov['student_id'],dec["student_id"])
students[students['student_id'].isin(common_id)]
```
- Find the courses that got no enrollment
```python
course_id_list = np.setdiff1d(courses["course_id"],regs["course_id"])
courses[courses["course_id"].isin(course_id_list)]
```
- Find the students who did not enroll into any course
```python
student_id_list = np.setdiff1d(students['student_id'],regs['student_id'])
students[students['student_id'].isin(student_id_list)]
```
- Print student name and partner name for every student
```python
students.merge(students,right_on="student_id",left_on="partner_id")[["name_x","name_y"]]
```
- Top 3 students who did the most number of enrollments
```python
regs.merge(students,on="student_id").groupby(["name","student_id"])["name"].count().sort_values(ascending=False).head(3)
```
- Top 3 students who spent the most number of money on courses
```python
regs.merge(students,on="student_id").merge(courses,on="course_id").groupby(["name","student_id"])["price"].sum().sort_values(ascending=False).head(3)
```
- Find the most number of sixes scored in a stadium
```python
temp_df = delivery.merge(matches,right_on="id",left_on="match_id")

six_df = temp_df[temp_df["batsman_runs"] == 6]

six_df.groupby("venue")["venue"].count().sort_values(ascending=False)
```
- Find the orange cap winners of all season
```python
temp_df.groupby(["season","batsman_runs"])["batsman"].sum().reset_index().sort_values("batsman_runs",ascending=False).drop_duplicates(subset=["season"],keep='first').sort_values("season")
```
---
