# Namespaces
*A namespace is a space that holds names(identifiers). Programmatically speaking, namespaces are dictionary of identifiers(keys) and their objects(values)

There are 4 types of namespaces:
- Builtin Namespace
- Global Namespace
- Enclosing Namespace
- Local Namespace
---
## Scope and LEGB Rule

**A scope is a textual region of a Python program where a namespace is directly accessible.

**The interpreter searches for a name from the inside out, looking in the local, enclosing, global, and finally the built-in scope. If the interpreter doesn’t find the name in any of these locations, then Python raises a NameError exception.

**Whenever we define a variable we create a new scope, let's understand this with code examples

```python
#Global Scope
a = 5
b = 'hello'
def greet(name):
	print(f"Hello {name}. How are you today?")
```
**The vars and functions we create in our main program are created in the _Global Scope_.

```python
#Local Space
def func(num):
	a = 5
	print(a)
```
**In the above program we are defining a var inside of a function and  they create a new scope in your program called as _Local Scope_.

```python
#Enclosing Space
def func():
	def wrapper():
	print("********")
	func()
	print("********")
```

**In the above program we have defined a function inside of another function the bottom-most function (wrapper) is in the _Local Scope_ and the the uppermost function (func) is in the _Enclosing Scope_.

```python
#Built-in Scope
print()
max()
type()
...
```
**All the built in function in python are in the _Built-In Scope_.

---
*The LEGB rule in python basically is a priority sequence in which the compiler searches for a variable or a functions*
**The sequence is as follows**
- Local Scope
- Enclosing Scope
- Global Scope
- Built-in Scope

What the above basically means is that if a variable or function existed  with the same name python will prefer that one which has the highest priority.

```python
a = 5
def wow():
	a = 3
	print(a)
wow()
print(a)

>>> 5
>>> 3
```
---
# Decorators
  
*A decorator in python is a function that receives another function as input and adds some functionality(decoration) to and it and returns it.

_This can happen only because python functions are 1st class citizens._

_There are 2 types of decorators available in python_
- `Built in decorators` like `@staticmethod`, `@classmethod`, `@abstractmethod` and `@property` etc
- `User defined decorators` that we programmers can create according to our needs

```python
#Simple Example
def my_decorator(func):
	def wrapper():
		print('***********************')
		func()
		print('***********************')
	return wrapper

def hello():
	print('hello')

def display():
	print('hello Flame')


a = my_decorator(hello)
a()

>>> *********************** 
>>> "hello Flame"
>>> ***********************
```

**Perhaps a more functional Decorators would prove to be better understanding example

```python 
def sanity_check(data_type):
	def outer_wrapper(func):
		def inner_wrapper(*args):
			if type(*args) == data_type:
				func(*args)
			else:
				raise TypeError('Ye datatype nai chalega')
		return inner_wrapper
	return outer_wrapper

  
@sanity_check(int)
def square(num):
	print(num**2)

  
@sanity_check(str)
def greet(name):
	print('hello',name)

square(2)
square('hehe')

>>> 4
>>> TypeError: Ye datatype nai chalega
```

