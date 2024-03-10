The concept of [[Inheritance]] comes from the real world, like how a child inherits their parent's bloodline, DNA, genetics,etc.

Similarly in python we have a parent class and then a child class that inherits attributes and methods from the parent class.

**Let's take a coding example:
```python
class Parent:
	def __init__(self,name):
		self.name = name

class Child(Parent):
	def print_name(self):
		return self.name
```

**Whenever we define a child class, we put the name of the parent class in parenthesis so that python knows which is the parent class and which is the child's.

---
## What get's inherited?
> 1. Constructors
> 2. Non Private Attributes
> 3. Non Private Methods

### Yes, Private attributes and Private Methods doesn't get inherited meaning that the child class can't have access to those things.

```python
class Phone:
	def __init__(self, price, brand, camera):
		print ("Inside phone constructor")
		self.__price = price
		self.brand = brand
		self.camera = camera
	#getter
	def show(self):
		print (self.__price)

class SmartPhone(Phone):
	def check(self):
		print(self.__price)


s=SmartPhone(20000, "Apple", 13)
s.show()
s.check() #This line will throw an error
```
---
## Method Overriding:
**If the child class has a method with the same name as the parent's class then the methods get overridden and the child class method is preferred.

**Let's take the example of a constructor:

```python
  
class Phone:
	def __init__(self, price, brand, camera):
		print ("Inside phone constructor")
	self.__price = price
	self.brand = brand
	self.camera = camera

class SmartPhone(Phone):
	def __init__(self, os, ram):
	self.os = os
	self.ram = ram
	print ("Inside SmartPhone constructor")

s=SmartPhone("Android", 2)
s.brand
```

**The above code will throw an error like `'SmartPhone' object has no attribute 'brand'`

#### This is because the child class and the parent class both have a constructor and when executing  the child class methods have more priority than parent's class methods, since the child class constructor didn't have an attribute as 'brand' python gave us an error
---
### Accessing Private and Overridden Methods:
> Python provides us with a special keyword with which we can bypass overriding of methods and even access private methods

**The keyword is called a `super()`

```python
class Phone:
	def __init__(self, price, brand, camera):
	print ("Inside phone constructor")
	self.__price = price
	self.brand = brand
	self.camera = camera

class SmartPhone(Phone):
	def __init__(self, price, brand, camera, os, ram):
	print('Inside smartphone constructor')
	super().__init__(price, brand, camera)  
	self.os = os
	self.ram = ram
	print ("Inside smartphone constructor")


s=SmartPhone(20000, "Samsung", 12, "Android", 2)
print(s.os)
print(s.brand)
```
## Output:
>Inside smartphone constructor
>Inside phone constructor
>Inside smartphone constructor
>Android
>Samsung
---
## KeyPoints:
- A class can inherit from another class.
- Inheritance improves code reuse
- Constructor, attributes, methods get inherited to the child class
- The parent has no access to the child class
- Private properties of parent are not accessible directly in child class
- Child class can override the attributes or methods. This is called method overriding
- super() is an inbuilt function which is used to invoke the parent class methods and constructor
---
 
# Types of Inheritance:
---
- Single : **Only one Child class inheriting from only one Parent class 
---
- Multilevel : **When the parent class is also inheriting from their parent is called as Multilevel Inheritance
---
- Multiple : **When the child inherits from more than one parent it is called as Multiple Inheritance.
---
- Hierarchical : **When more than one child is inheriting from the same parent it is called as Hierarchical inheritance.
---
- Hybrid : **When more than one type of inheritance is being used in a class it is called as Hybrid Inheritance
---


