**Remember in the [[Class & Objects]] file we created a class called as "Atm". In that class there were some very important and confidential information like `Account_Balence` & `PIN`. Now we wouldn't allow anyone to just edit out the above two var's information.

**This is where the concept of [[Encapsulation]] comes into play, Python allow's us programmers to private out some instance variables in our constructor method so that not everyone will be able to access such type of info

### The need for encapsulation:
```python
class Atm():
	def __init(self):
		self.pin = ''
		self.balance = 0
```

**In the above code, any programmer can easily just override the `self.balance` like so:
`user1.balance = 1000000`

**Hence, to prevent the such misuse, we private out some information.

**We can private out information by adding two underscores before the variable name, like so: `self.__balance`

**Now, the balance variable won't be accessible to them directly, even if they tried to do so by writing `self.__balance` 

### This is what happens when someone tries to override by adding two underscores before the var name:

```python
class Atm():
	def __init(self):
		self.pin = ''
		self.__balance = 0

user1 = Atm
user1.__balance = 4032573457295
```
> ![[Pasted image 20240102204739.png]]

**If someone were to access the hidden element by adding `__` in the end they still wont be able to access the element as python will automatically rename the hidden attribute as `_Classname__balance`
and python will also create a new variable called as `__balance` as shown  in the above image, but the actual power will be in the original var.

#### However, if someone were to use the notation mentioned above to change the value of a variable then, they would be able to as python will allow this type of overwrite.

```python
user1._Atm__balance = 43904732947
```
**Now, they would absolutely be able to make the above change

## Since there is no such thing as completely private in python!

## Getter & Setter methods:

**What if you want to give someone the access of those private attributes?
>We can actually do so by creating two new methods called get & set, like so:

```python
class Atm():

	def get_balance(self):
		return self.__balance
	def set_balance(self,value):
		self.__balance = value
```
