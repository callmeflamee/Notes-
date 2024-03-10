```python
# working with binary file
with open('screenshot1.png','rb') as f:
	with open('screenshot_copy.png','wb') as wf:
		wf.write(f.read())
```

**To perform operations on a binary file we use the mode `'rb'/wb` which stands for read binary & write binary respectively.

# Serialization & Deserialization

**Remember the problem of [[File Handling]] where we discussed about reading and writing  different python data types and python always threw an error. To combat that problem we will store the data in a `.JSON` file.

## What is a .JSON file?
> JSON stands for JavaScript Object Notation. It is a universal data file from that every programming language understands,
> 
> example of a json file: 
> ![[Pasted image 20240106220425.png]]

#### Python and JSON have different data types, with Python offering a broader range of data types than JSON. While Python is capable of storing intricate data structures such as sets and dictionaries, JSON is limited to handling strings, numbers, booleans, arrays, and objects. Let’s look at some of the differences:
 ![[Pasted image 20240106220625.png]]

- **Serialization - process of converting python data types to JSON format
- **Deserialization - process of converting JSON to python data types
---
```python
import json
```
---

# Serialization:

```python 
# serialization using json module
L = [1,2,3,4]
with open('demo.json','w') as f:
	json.dump(L,f)
```

**The above code will create a new file in the same working dir as `demo.js` which will store the list as the datatype list. 

```python
# dict
d = {
'name':'nitish',
'age':33,
'gender':'male'
}
with open('demo.json','w') as f:
	json.dump(d,f,indent=4)
```

**The above will also store the same value in the `demo.json` file but the datatype would be a dict as specified above.

---
# Deserialization
```python
# deserialization
with open('demo.json','r') as f:
	d = json.load(f)
print(d)
print(type(d))

>>>{'name': 'nitish', 'age': 33, 'gender': 'male'} 
>>> <class 'dict'>
```

**As we see the type of data that was stored onto the file was nothing other then what we provided it as i.e a dict.

---
# Custom Objects:

```python
class Person:
	def __init__(self,fname,lname,age,gender):
		self.fname = fname
	self.lname = lname
	self.age = age
	self.gender = gender

person = Person('Flame','Shaikh',33,'male')
```

**Format to printed in
-> Fname Lname age -> 33 gender -> male

```python
def show_object(person):
	if isinstance(person,Person):
		return "{} {} age -> {} gender -> {}".format(person.fname,person.lname,person.age,person.gender)
		

with open('demo.json','w') as f:
	json.dump(person,f,default=show_object)
```
**In the default parameter we pass the name of the function in which we are describing the data output

>"Flame Shaikh age -> 33 gender -> male"

```python
# As a dict
def show_object(person):
	if isinstance(person,Person):
		return {'name':person.fname + ' ' + person.lname,'age':person.age,'gender':person.gender}

with open('demo.json','w') as f:
	json.dump(person,f,default=show_object,indent=4)
```
**Output:
```json
{
"name": "Nitish Singh",
"age": 33,
"gender": "male"
}
```

```python
# deserializing

with open('demo.json','r') as f:
	d = json.load(f)

print(d)
print(type(d))

>>>{'name': 'Nitish Singh', 'age': 33, 'gender': 'male'}
>>> <class 'dict'>
```
---
# Pickling & Depickling

**`Pickling` is the process whereby a Python object hierarchy is converted into a byte stream, and `unpickling` is the inverse operation, whereby a byte stream (from a binary file or bytes-like object) is converted back into an object hierarchy.

```python
import pickle
```

```python
class Person:
	def __init__(self,name,age):
	self.name = name
	self.age = age

	def display_info(self):
	print('Hi my name is',self.name,'and I am ',self.age,'years old')

person = Person("Flame", 18)
```

```python
#pickle dump
with open("person.pkl", "wb") as f:
	pickle.dump(person,f)
```

```python
#pickle load
with open("person.pkl","rb") as f:
	p = pickle.load(f)
	p.display_info()

>>>"Hi my name is Flame and I am 18 years old"
```

---

# Pickle Vs Json
- Pickle lets the user to store data in binary format. JSON lets the user store data in a human-readable text format.