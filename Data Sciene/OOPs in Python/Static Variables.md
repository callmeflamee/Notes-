**Consider the Atm class we made in the [[Class & Objects]] file and let's say we want to add a new feature called customer_id which will be unique for every customer.

#### Now, how might we go about that? We cannot create another instance variable inside of our constructor since that will be the dependent for every other user.

**This is where the Static Variable come into play, static variables are the  same for every object created and then we can increment it by one in the  constructor class so that whenever a new object is created it will increment it by one.

```python
class Atm():
	__counter = 0

	def __init__(self):
	self.cid = Atm.__counter
	Atm.__counter = Atm.__counter + 1

	@staticmethod
	def get_counter():
		return Atm.__counter
```

## KeyPoints:
- Static attributes are created at class level.
- Static attributes are accessed using ClassName.
- Static attributes are object independent. We can access them without creating instance (object) of the class in which they are defined.
- The value stored in static attribute is shared between all instances(objects) of the class in which the static attribute is defined.