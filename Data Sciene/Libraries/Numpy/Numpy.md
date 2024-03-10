
**We will directly start these notes from the advanced version

## Advanced indexing

*There are 3 types of Indexing and Slicing
- Normal 
- Fancy 
- Boolean
---
## Normal Slicing & Indexing:

**We have already seen how these work let's just look at one example:
```python
a = np.arange(24).reshape(6,4)
a

>>> array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11],
       [12, 13, 14, 15],
       [16, 17, 18, 19],
       [20, 21, 22, 23]])

a[1,2]
>>> 5
```

---
## Fancy Indexing:

**In Fancy indexing we pass the index of the row and column in a list that we want to access
```python
a[:,[0,2,3]]

>>> array([[ 0,  2,  3],
       [ 4,  6,  7],
       [ 8, 10, 11],
       [12, 14, 15],
       [16, 18, 19],
       [20, 22, 23]])
```
*We selected the all the rows & columns leaving only the 2nd column.*

We wouldn't have been able to get the same output using the normal indexing because there is no pattern to be found here.

---
## Boolean Indexing:

*We can index out items using some conditions using comparing operators and the like, for ex.*
```python
a = np.random.randint(10,100,24).reshape(4,6)
a
>>>array([[76, 98, 99, 39],
       [91, 46, 88, 23],
       [45,  6, 83,  1],
       [37, 43, 78, 85],
       [54, 73, 61, 53],
       [40, 93, 85, 77]])
```
Let's Index in the above array
```python
a[a > 50] #Elements greater than 50

a[a % 2 == 0] #Only Even Numbers

a[(a > 50) & (a % 2 == 0)] #Multiple conditions using bitwise AND operator

a[~(a % 7 == 0)] #Bitwise NOT operator
```
---
# Broadcasting
*The term broadcasting describes how NumPy treats arrays with different shapes during arithmetic operations.

*The smaller array is “broadcast” across the larger array so that they have compatible shapes.
for example:
```python
a = np.arange(6).reshape(2,3)
b = np.arange(3).reshape(1,3)

print(a+b)
>>> [[0 2 4] 
	[3 5 7]]
```
#### Broadcasting Rules

**1. Make the two arrays have the same number of dimensions.**  

- If the numbers of dimensions of the two arrays are different, add new dimensions with size 1 to the head of the array with the smaller dimension.
 ![[Pasted image 20240110170250.png]]

**2. Make each dimension of the two arrays the same size.**  

- If the sizes of each dimension of the two arrays do not match, dimensions with size 1 are stretched to the size of the other array.
- If there is a dimension whose size is not 1 in either of the two arrays, it cannot be broadcasted, and an error is raised.

 ![[Pasted image 20240110170650.png]]![[Pasted image 20240110170715.png]]
---
**This is how broadcasting is done:
 ![[Pasted image 20240110195737.png]]
 However the numpy package already takes care of such complex operations we only need to know when it will work and where it won't.

*Let's look at some examples to get a better understanding,*
```python
a = np.arange(12).reshape(4,3)
b = np.arange(3)

print(a+b)
>>>[[ 0 2 4] 
	[ 3 5 7] 
	[ 6 8 10] 
	[ 9 11 13]]
```
*The above works because we first have a (4,3) matrix and we are adding it with (3,) matrix*

Therefore python first adds 1 in front of the 2nd matrix (rows)
**`(1,3)`**
Now it will stretch that one to match with the number of rows of the first matrix:
**`(3,3`
(3,3) + (3,3)**

And that's how they get added.

```python
a = np.arange(12).reshape(3,4)
b = np.arange(3)

print(a+b)
```
*By just switching the shape of the matrix python throws us an error, as after adding 1 and stretching it to the number of rows we get (4,3), which is not equal to (3,4)*

```python
a = np.array([1])
# shape -> (1,1)
b = np.arange(4).reshape(2,2)
# shape -> (2,2)

print(a+b)
```
The above will work too.

---
