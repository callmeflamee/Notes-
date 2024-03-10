**Types of data used for I/O:
- Text - '12345' as a sequence of Unicode chars
- Binary - 12345 as a sequence of bytes of its binary equivalent

**Hence there are 2 file types to deal with
- Text files - All program files are text files
- Binary Files - Images,music,video,exe files

## How File I/O is done in most programming languages
- Open a file
- Read/Write data
- Close the file
---
## Writing to a Text file:
```python
# case 1 - if the file is not present
f = open('sample.txt','w') # 'w' means to open in write mode
f.write('Hello world')
f.close()
```

### Closing a file:
*Whenever we open a file with the `open()` function in python it loads the file in the buffer memory (RAM)*
**Hence, it is always necessary to close the file after doing operations on it.

```python
# write multiline strings
f = open('sample1.txt','w')
f.write('hello world')
f.write('\nhow are you?')
f.close()
```

```python
# case 2 - if the file is already present
f = open('sample.txt','w')
f.write('salman khan')
f.close()
```

**In the above code we already had a file called as 'sample.txt' which had the text `Hello World` followed by `How are you?` But after we again performed a write operation on the same file which basically replaced the entire contents of the file with `Salman Khan`. 

*The above is essentially the problem with the 'w' mode. To combat it we can use the 'a' mode i.e append*
```python
# introducing append mode
f = open('/content/sample1.txt','a')
f.write('\nI am fine')
f.close()
```

```python
# write lines
L = ['hello\n','hi\n','how are you\n','I am fine']
f = open('/content/temp/sample.txt','w')
f.writelines(L)
f.close()
```
---
## Reading a text file:
```python
# -> using read()
f = open('/content/sample.txt','r')
s = f.read()
print(s)
f.close()

>>> hello 
>>> hi 
>>> how are you 
>>> I am fine
```

```python
# reading upto n chars
f = open('/content/sample.txt','r')
s = f.read(10)
print(s)
f.close()

>>>hello 
>>>hi
>>>h
```

```python
# readline() -> to read line by line
f = open('/content/sample.txt','r')
print(f.readline(),end='')
print(f.readline(),end='')
f.close()

>>>hello
>>>hi
```

```python
# reading entire using readline
f = open('/content/sample.txt','r')
while True:
	data = f.readline()
	if data == '':
		break
	else:
		print(data,end='')
f.close()

>>> hello
>>> hi 
>>> how are you 
>>> I am fine
```
---
## Using Context Manager (With)

- It's a good idea to close a file after usage as it will free up the resources
- If we don't close it, garbage collector would close it
- with keyword closes the file as soon as the usage is over
```python
with open('/content/sample1.txt','w') as f:
f.write('selmon bhai')
```

```python
# benefit? -> to load a big file in memory
big_L = ['hello world ' for i in range(1000)]
with open('big.txt','w') as f:
f.writelines(big_L)
```

```python
with open('big.txt','r') as f:
chunk_size = 10
while len(f.read(chunk_size)) > 0:
	print(f.read(chunk_size),end='\n')
	f.read(chunk_size)
```
  ---
## Seek and Tell:
```python
# seek and tell function
with open('sample.txt','r') as f:
f.seek(15)
print(f.read(10))
print(f.tell())
print(f.read(10))
print(f.tell())
```
**The  `tell()`function tells the at which character is the buffer memory pointing at
```python
with open('sample.txt','w') as f:
f.write('Hello')
f.seek(0)
f.write('Xa')

>>> Xallo
```
**The `seek()` function replaces the buffer memory cursor to our desired place i.e the nth numbered character

---
## Problems with working in text mode
- can't work with binary files like images
- not good for other data types like int/float/list/tuples

```python
with open('sample.txt','w') as f:
f.write(5)

with open('sample.txt','r') as f:
print(dict(f.read()))
```
**All of the above code will give us an error

---
# Working with binary files
- **For further notes  [[Binary File Handling|Click Here]]
- 

