We will be discussing the important functions in numpy

---
## Sort:

```python
a = np.random.randint(1,100,27) # 1D Array
np.sort(a) # acending order
np.sort(a)[::-1] #Desencing order

a = np.random.randint(1,100,12).reshape(3,4) # 2D Array
np.sort(a,axis=0) # Colunm Sorting
np.sort(a,axis=1) # Row Sorting
```
---
## Append:
**To insert an item into the end of the list
```python
a = np.array([x for x in range(1,60,6)])
np.append(a,200)

>>> array([6,12,18,24,30,36,42,48,54,60,200])

a = np.random.randint(1,100,12).reshape(3,4)
np.append(b,np.ones((b.shape[0],1)),axis=1) # New Column append
np.append(b,no.ones((1,b.shape[1])),axis=0) # New Row append
```
---
## Concatenate:
**To merge two or more arrays. (kinda like hstack and vstack)
```python
a = np.arange(6).reshape(3,2)
b = np.arange(7,13).reshape(3,2)

np.concatenate((a,b),axis=0) #Row 
np.concatenate((a,b),axis=1) #Column

>>> array([[ 0,  1,  2],  # axis = 0
          [ 3,  4,  5],
	      [ 6,  7,  8],
          [ 9, 10, 11]])
          
>>> array([[ 0,  1,  2,  6,  7,  8],
          [ 3,  4,  5,  9, 10, 11]])
```
---
## Unique:
**To find unique values in a given array.**
```python
a = np.random.randint(1,101,25).reshape(5,5)
np.unique(a)
```
---
## Expand Dims:
**Expanding dimensions of an array.**
```python
a = np.arange(15)
a.shape()

>>> (15,)

np.expand_dims(a,axis=0).shape #Expand Row
np.expand_dims(a,axis=1).shape #Expand Column

>>> (1,15)
>>> (15,1)
```
---
## Where:
**To locate an item in an array and return it's index and also modify those elementss.**
```python
np.where(a>50) #Give index of all no. bigger than 50
np.where(a>50,0,a) #Replace no smaller than 50 with 0
```
---
## Argmax & Argmin:
**Return the index of the largest and smallest number respectively in a given array.**
```python
np.argmax(a)
np.argmin(a)
```
---
## Cumsum:
**Cumulative summation series.**
```python
a = array([11, 53, 28, 50, 38, 37, 94, 92,  5, 30, 68,  9, 78,  2, 21])
np.cumsum(a)

>>> array([11,64,92,142,180,217,311,403,408,438,506,515,593,595,616])
```
```python
b = np.random.randint(0,101,24).reshape(3,4)
np.cumsum(b,axis=0) # Row Series
np.cumsum(b,axis=1) # Column Series
```
**Also a thing called as cumprod that returns the multiplicative series.**

---
## Percentile:
**Returns the index of the element that matches the specified percentile.**
```python
a = np.random.randint(0,100,20)
np.percentile(a,35)
```
---
## Histogram:
**Tells us the quantity present in the specified bins.**
```python
a = np.random.randint(0,101,25)
np.histogram(a,bins=[x for x in range(1,101,10)])
```
---
## Corrcoef:
**Tells us the co-relation coefficient between arrays.**
```python
alary = np.array([20000,40000,25000,35000,60000])
experience = np.array([1,3,2,4,2]
np.corrcoef(salary,experience)

>>>array([[1.        , 0.25344572],
          [0.25344572, 1.        ]])
```
---
## Isin:
**To check if certain items are in your array**
```python
items = [x for x in range(0,101,10)]
a[np.isin(a,items)]

>>> array([30,40,80])
```
---
## Flip:
**Reverses the order of the given array.**
```python
np.flip(a)
np.flip(b,axis=0)#Row Flip
np.flip(b,axis=1)#Column Flip
```
---
## Put:
**To insert an item at the specified index**
```python
np.put(a,[0,1],[110,530]) #Replace elements at [0][1] with 110,530 respectively 
```
---
## Clip:
**To limit values in an array.**
```python
np.clip(a,a_min=10,a_max=99)
```
*Now any value smaller than 10 will be replaced with 10 and any value greater than 99 will be replaced with 99*

---
