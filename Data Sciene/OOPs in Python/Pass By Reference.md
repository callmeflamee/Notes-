## Let's suppose we want to pass an object to a function, here's how we can do it:

```python
class Person():
	def __init__(self,name,gender):
		self.name = name
		self.gender = gender

def greet(person):
	print(f"Hi!, I am {person.name} and I am {person.age} years-old")

a = person('mukesh', 22)
greet(a)
>>> "Hi!,I am mukesh and I am 22 years old"
```

**And also because, user defined classes are mutables we can do the following too,
 ```python
def greet(person):
	person.name = 'ankit'
	return person

a = person('mukesh',22)
b = greet(a)
print(a.name)

>>> 'ankit' "<-- This happens due to the muability of the object"
```

**Even if we were to print the id's of both 'a' & 'b' we would get the same results.