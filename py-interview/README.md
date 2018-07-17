# Python Interview

## Variable Assignment
```python
a = b = c = 1
a, b, c = 1, 2, "John"
```

### Tuples
```python
# Empty, Single data type, multiple data type
tuple_1 = ()
tuple_2 = (1, 2, 3)
tuple_3 = (1, "Hello", 3.4)
tuple_3[0]

# String, list, tuple within tuple
tuple_4 = ("mouse", [8, 4, 6], (1, 2, 3))
tuple_4[0]
tuple_4[0][0]
```
##### Tuple Packing
```python
m = 1, 2.4, "cat" # Packing
a, b, c = m  # Unpacking
```

```python
tuple_1 = ("hello") # Type string
tuple_2 = ("hello",) # Type Tuple
tuple_3 = "hello", # Type Tuple
```

```python
tuple_1 = ('p', 'q', 'r', 's', 't', 'u')
tuple_1[6] # Index out of range
tuple_1[-1] # 'u'
```

```python
# use slicing
tuple_1 = ('a','l','g','o','r','i','t','h','m')
tuple_1[1:4] # l, g, o
tuple_1[:-7] # 'a','l'
tuple_1[7:] # h, m
tuple_1[:] # a','l','g','o','r','i','t','h','m'
tuple_1[7:-7] # ()
```

```python
# Convert tuple to list
msg = "Hello world"
print list(msg)
print tuple(msg)
print list(tuple(list(message)))
```

```python
# Check existence in tuple
tuple_1 = ('a', 'b', 'c')
print('a' in tuple_1)
```

```python
for name in ('mani', 'ali'):
   print("Hello...", name)
```

```python
# Concatenate
print((1, 2, 3) + (4, 5, 6)) # 1, 2, 3, 4, 5, 6
print(("Mani", ) * 3) # Mani, Mani, Mani
```

```python
# Deletion
tuple_1 = ("hello", [1, 2, 3])
del tuple_1[1][0] # "hello", [2, 3]
```

### Lists

```python
states = ["Washington", "NY", "NC", "MO", "MA"]
for i in states:
    print(i[0]) # W, N, N, M, M
```

```python
# For each value in r1, get sum of ascii values
# and push into new list
r1 = ["Manchester", "Concord", "Bow", "Helsinki"]
r2 = []
# Each string in the list
for i in r1:
    sum = 0
    # Each and every character of the string
    for j in i:
        sum = sum + ord(j) # ord gives ascii value
 # Append ascii value of each string into the new list r2
 r2.append(r1)
```

```python
# Print all duplicated values in a string
list_1 = [1, 2, 3, 1, 2, 4, 5, 6, 7], # 1, 2 are repeated

# Empty array, insert 0 for for the 10 elements in the array, for each
# number in list_1, convert number into index into hash array, increment slot
# in hash array
hash = []
for i in range(10):
    hash.append(0)
for i in list_1:
    hash[i]+=1
i = 0
index = 0
for i in hash:
    if i > 1:
       print(index)
     index +=1
```

```python
# Perform left rotate on the given list
import collections
list = [4, 5, 6, 7]
d = collections.deque(list)
d.rotate(3)
```

### Shallow Copy, Deep Copy

- Shallow Copy effects original list (addresses are copied)
- Deep Copy does not effect the original list (values are copied)

### __str__ method
```python
num = 123
print(str(num))
```
### __repr__ method

```python
eval function needs to operate on an object
# repr -> returns an object
# str -> returns string literal

y = "test string"
y2 = eval(repr(y))
if (y==y2):
   print("strings are equal")
```

### main

```python
if __name__ == "__main__":
     print("direct method")
```

### Classes

```python
class SampleClass:
       a = 10
       def fun(self):
            print('Hello')
            
print(SampleClass.a)
print(SampleClass.fun) 
```

### Call via class is unbound, call via object is bound

```python
class SampleClass:
       a = 10
       def fun(self):
            print('Hello')
            
obj = SampleClass()
obj.a
obj.fun()
```


```python
class A:
   def fun():
      print("a")

A.func() Instance
a = A()  via Class

a.func()
```

