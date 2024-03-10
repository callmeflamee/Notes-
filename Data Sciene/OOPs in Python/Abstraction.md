**Making our programs abstract is called as abstraction, it the 3rd principle of OOP(S).

**It basically means that hiding irrelevant information in out main program.  

```python
class Bank:
	def database(self):
		return "Connected to Database"

	@abstractmethod
	def security(self):
		return "Secured!"

class BankApp(Bank):
	def login(self):
		return "Login Now"
```

**If we were to create an object of the class `BankApp` python would throw us an error

**Because we have a abstract method in our Parent class and we don't have the same method in our child class, The object won't be created till the `security` function has been coded in our child class.

```python
class BankApp(Bank):
	@abstractmethod
	def securtiy(self):
		return "Not Secured!"
```

*Now we can create an object of the child class without getting an error.*

