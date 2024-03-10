# Let's create our very own data-type of fractions:
## We will represents our values in fractional notations rather than like how we receive decimal output from python by default.

### Let's get coding!

```python
class Fractions():
	
	def __init__(self,x,y):
		self.num = x
		self.den = y

	def __str__(self):
		return f"{self.num} / {self.den}"

	def __add__(self,other):
		return ((self.num*other.den) + (other.den*self.num)) + 
		' / ' + (self.den*other.den)

	def __sub__(self,other):
		return ((self.num*other.den) - (other.den*self.num)) + 
		' / ' + (self.den*other.den)

	def __true_div__(self,other):
		return (self.num*other.num) + " / " + 
		(self.den*other.den)
```

