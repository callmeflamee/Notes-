![[Pasted image 20231230155212.png]]

**Generality to Specificity
Used to create our own datatypes 

## Class:

**Class is a blueprint
![[Pasted image 20231230155607.png]]

**All prebuilt datatypes in python are a class
and we define them into a variable, they are called as objects

**Class is a rule and objects follow those rules

![[Pasted image 20231230160415.png]]

**Object is an instance of a class

## Constructor function in a Class:

**It is a special function that executes our class whenever an object is created

```python
Class Atm:

	def __inint__(self): ##This is a constructor
		self.pin = ''
		self.balance = 0
		menu()

	def menu(self):
		userinput = input("""
		Hi! How can I help you?
		1.Press 1 to set PIN
		2.Press 2 to change PIN
		3.Press 3 to check balance
		4.Press 4 to widthdraw money
		5.Press anything else to exit""")
	
```

**Now whenever we create an object the constructor function gets executed:

```python
obj = Atm()

>>> Hi! How can I help you?  #OutPut
		1.Press 1 to set PIN
		2.Press 2 to change PIN
		3.Press 3 to check balance
		4.Press 4 to widthdraw money
		5.Press anything else to exit
		`                            `
```

**Any functions implemented inside a class is called as a *method

### Class diagram:
![[Pasted image 20231230165506.png]]
## Magic (Dunder) Methods:

**Magic methods are a type of methods that gets executed as soon as the class is called,
these methods gets executed without being called.

**To define a Magic method we use the following syntax:
```python
def __"<name_of_your_funtion>"__():
```

**Yes, this means that our constructor is also a magic method, and this explains why the code inside of the constructor was always getting executed.

#### What is the benefit of using a Magic method?, and why do we use them?

>We use Magic methods to write configuration code, or such type of code that we don't want the user to be in control of.

**Also, We cannot rename our constructor. There's only one constructor and it will always be named `__init__`

### What is self?

**Self is nothing but the current object

## Different types of magic methods:

```python
class Yoo():
	def __str__(self):
		return "Hello World"

	def __add__(self):
		return self.var1 + self.var2

	def __sub__(self):
		return self.var1 - self.var2

	def __true_div__(self):
		return self.var1 / self.var2
```

1. **The `__str__` method is executed whenever out class object is printed using the `print()` function
2. **The `__add__` method is executed whenever our class objects are added together ,like so `ob1 + obj2`
3. **The `__sub__` method is executed whenever our class objects are subtracted from, like so `obj1 - obj2`
4. **The `__true_div__` method is executed whenever our class objects are divided, like so `ob1 / obj2`

## There stands a lot more like:

```python
['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__getstate__', '__gt__', '__hash__', '__index__', '__init__', '__init_subclass__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'as_integer_ratio', 'bit_count', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']
```

