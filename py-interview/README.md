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

### Lists

### Shallow Copy, Deep Copy

### __str__ method

### __repr__ method

### Strings

### Numbers

### File Ops
