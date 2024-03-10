
### There are two types of relationship in Python OOP(s)
1. Aggregation
2. Inheritance

**Let's have a look at each one of them

1. <b>Aggregation </b>
>This defines that a type of Has-A(n) Relationship. For ex. A customer "HAS AN" Address, A User "HAS A" Phone, etc..

**Let's look at the coding definition:

```python
class Customer:
	def __init__(self,name,gender,address):
		self.name = name
		self.gender = gender
		self.address = address

	def print_address(self):
		print(self.state,self.address._Address__city,self.pin)

class Address:
	def __init__(self,state,city,pin):
		self.state = state
		self.__city = city
		self.pin = pin

add1 = Address("Maharastra","Mumbai",400061)
cust = Customer("flame","male",add1)
cust.print_address()

```
**The above code will print out the address.

**As we saw, in aggregation we pass objects of other class as inputs and hence we define a relationship
Let's see how to use methods inside of other class

```python
class Customer:
	def edit_profile(self,new_name,new_gender):
		self.name = new_name
		self.gender = new_gender
		self.Address.edit_address()

class Address:
	def edit_address(self,new_state,new_city,new_pin)
		self.state = new_state
		self.__city = new_city
		self.pin = new_pin 
```

**So to use another class's methods we need to write that very class name followed by the name of the function.

### Class diagram of Aggregation:
 ![[Pasted image 20240103223832.png]]

 2. [[Inheritance]]

For Inheritance notes [[Inheritance |Click Here.]]

