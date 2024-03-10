## Attribute creation outside of class:

**suppose we have a class of person like the following:

```python
class Person():
    def __init__(self,name_input,country_input):
        self.name = name_input
        self.country = country_input
    def greet(self):
        if self.country == : 'india':
            print(f"Namaste {self.name}")
        else:
            print(f"Hello {self.name}")
```

**now if we were to create an object of the person class like so,

**`user = person('mukesh',india)`

**Now, if we were to access an undefined attribute, let's say gender we will obviously get an error

**`user.gender`
> Error: 'user' object has no attribute 'gender'

**But, we can define a new attribute outside the class as well, like so:

**`user.gender = 'male'`

**Now let's run the code that got an error last time again:

**`user.gender`

> 'male'


## Reference variables:

**Remember in the [[Class & Objects]] we used to assigning a var to a class and call it an object?,
well it isn't so simple there's a twist, the twist is that we don't really create an object, but what we do create is a reference variable

### what is a reference variable?
> Well, To answer it simply it is just a pointer, that is pointing to the memory address where the object has been created.

**For example, lets take the following code:
```python
class Person():
	-----pass---- #some code

Person()  "<<-- Here the object has been already created"

a = Person() "<-- The var 'a' just points to the memory location that has been occupied by the object"

"Hence, we can also perfom the following operations:"
a = b
print(a.name)
print(b.name)
b.name = 'flame' 
print(a.name)
print(b.name)

>>> 'mustufa'
>>> 'mustufa'
>>> 'flame'
>>> 'flame'
```

**Changing the 'b' reference var also changes the a one and hence it is called as a reference variable.

## Keypoints:
1. **Reference Variables holds the objects.
2. **We can create objects without reference variables as well.
3. **An object can have multiple reference variables.
4. **Assigning a new reference variable to an already existing object does not create a new object.



