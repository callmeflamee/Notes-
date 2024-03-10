*There are 2 stages where error may happen in a program
- During compilation -> **Syntax Error
- During execution -> **Exceptions

## Syntax Error:
- Something in the program is not written according to that programming language's grammar.
- Error is raised by the interpreter/compile
- You can solve it by rectifying the program
**Some examples of syntax error
```python
print"Hello" #no barckets
if num == 5  # no colon
	print("wow")
iff num == 5: # wrong spell error
print("wow")  # no indentation error
```

### In python there are a lot of different errors, for the entire list check the [official python docs](https://docs.python.org/3/tutorial/errors.html)
---
# Exceptions:
**if things go wrong during the execution of the program(runtime). It generally happens when something unforeseen has happened.
- Exceptions are raised by python runtime
- You have to tackle is on the fly
#### Examples
- Memory overflow
- Divide by 0 -> logical error
- Database error
---
### Why is it important to handle errors/exceptions?
>Well, there are 2 reasons:
>	1. Being specific and verbose to the user and not overwhelming them with a huge pile of red text that python throws at us
>	2. Better security, when python throws us an error it shows a lot of sensitive program information that we wouldn't want everyone to know

### How to handle exceptions
> Python's `try & except`

---
**In code:
```python
try:
with open('sample1.txt','r') as f:
	print(f.read())
except:
	print('sorry file not found')
```
Now if the file wasn't found or was renamed by somebody then the user will simply get an error saying `"sorry file not found"` 
 
**Catching specific exception:
```python
try:
	m=5
	f = open('sample1.txt','r')
	print(f.read())
	print(m)
	print(5/0)
	L = [1,2,3]
	L[100]

except FileNotFoundError: #If file was renamed or deleted
	print('file not found')
except NameError:  #If m variable wasn't declared
	print('variable not defined')
except ZeroDivisionError: #If divided by zero
	print("can't divide by 0")
except Exception as e: #General error If something else is wrong
	print(e)
```
### Else block:
```python
try:
	f = open('sample1.txt','r')
except FileNotFoundError:
	print('File not found')
except Exception:
	print('Some error occured')
else:
	print(f.read())
```
**Now if the file did infact exist then we go and execute the else block or if the file didn't exist then we don't execute the else block.**
### Finally block:
```python
try:
f = open('sample1.txt','r')
except FileNotFoundError:
	print('file nai mili')
except Exception:
	print('kuch to lafda hai')
else:
	print(f.read())
finally:
	print('ye to print hoga hi')
```
**In the above code we have a new block called `finally` this block will always execute, it doesn't matter if the file existed or not the `finally` block will always get executed**

---
## Raise Exception:
*In Python programming, exceptions are raised when errors occur at runtime.
We can also manually raise exceptions using the raise keyword.
We can optionally pass values to the exception to clarify why that exception was raised

```python
raise ZeroDivisionError("Hello")
```
**The above code when executed will result in the following output:
```traceback
ZeroDivisionError                         Traceback (most recent call last)

<ipython-input-106-5a07d7d89433> in <module>
----> 1 raise ZeroDivisionError('Hello')

ZeroDivisionError: Hello
```

**With the `raise` keyword we can throw any error we want at anytime and anywhere in the program

#### Use case of **`raise`**
 *Suppose you have a bank class and in which you have a method called as `withdraw` and there are certain errors associated with it for ex. if the user inputs a `-ve` number or if he inputs a number that is greater than his actual bank balance*

```python
class Bank:
	def __init__(self,balance):
		self.balance = balance

	def withdraw(self,amount):
	if amount < 0:
		raise Exception('amount cannot be -ve')
	if self.balance < amount:
		raise Exception('paise nai hai tere paas')

	self.balance = self.balance - amount

obj = Bank(10000)
try:
	obj.withdraw(15000)
except Exception as e:
	print(e)
else:
	print(obj.balance)
```
---
### **Using a class to deal with exceptions:

*Why would we want to create a class to handle exceptions when we can already do it anywhere we want to?*
> The answer is because of extra functionality, take the above code for instance. When withdrawing cash from an atm we are required to put in our pin in order to withdraw money, but what if we enter the wrong pin 3 times or we enter the reverse of our actual pin, the bank immediately blocks all monetary transactions, in such a case using a class would be much more beneficial

---
### Summary code
```python
class SecurityError(Exception):
  def __init__(self,message):
    print(message)

  def logout(self):
    print('logout')

class Google:
  def __init__(self,name,email,password,device):
    self.name = name
    self.email = email
    self.password = password
    self.device = device

  def login(self,email,password,device):
    if device != self.device:
      raise SecurityError('Untrusted OS used')
    if email == self.email and password == self.password:
      print('welcome')
    else:
      print('login error')


obj = Google('flame','flame@gmail.com','1234','linux')

try:
  obj.login('flame@gmail.com','1234','windows')
except SecurityError as e:
  e.logout()
else:
  print(obj.name)
finally:
  print('database connection closed')
```