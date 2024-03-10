In Formal definition [[Polymorphism]] means the occurrence of same thing in different forms.

---
**In Python, Polymorphism is implemented in the following ways:**

- _Method Overriding_
- _Method Overloading_
- _Operator Overloading_

---
## Method Overloading:

**We already saw this in Inheritance Note [[Inheritance#Method Overriding|Click Here]] for reference 

---
## Method Overloading:

**Suppose we have two functions with the same name in the same class then how do we access each one separately?
One way is to receive different inputs for ex,
```python
class Shape:
	def area(self,radius):
		return 3.14*radius*radius
	def area(self,length,breadth):
		return length * breadth

obj = shape()
obj.area(2)
obj.area(3,4)
```
**But the above code doesn't work with python, it works with other languages such as java

**In python we could do the following:
```python
class Shape:
	def area(a,b=0):
		if b == 0:
			return 3.14 *a*a
		else:
			return a*b

obj = Shape()
obj.area(2)
obj.area(3,4)
```
---

## Operator Overloading:

```python
'hello' + 'world'
>>> 	'helloworld'

3+3
>>> 6

[1,2,3] + [4,5,6]
>>> [1,2,3,4,5,6]
```
**In the above code even tho we have the same operator i.e `+` it performed different operations based on different inputs 

---
### That is essentially the casual definition of Polymorphism, i.e performing different operations based on different inputs



