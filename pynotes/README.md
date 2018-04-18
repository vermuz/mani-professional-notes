### Python Notes

#### Collections

#### Tuple
- Immutable

```python
t = ("Norway", 4.953, 3)
t[0]
len(t)

for item in t:
    print(item)

# Concatenate
t + (2.222, 265e9)

# Nested Tuples
a = ((220, 284), (1184, 1210), (2620, 2924))
print(a[2][1])

# Single Element Tuple
k = (391,)

# Empty Tuple
e = ()

# Unmapping
minmax([83, 33, 84, 32, 85, 31, 86])
lower, upper = minmax([83, 33, 84, 32, 85, 31, 86])
lower -> 31

# Swapping
a = 'jelly'
b = 'bean'
a, b = b, a
```

### String

- Immutable sequence of unicode codepoints

```python
colors = ';'.join(['#45', '#23', '#129'])
colors.split(';')
''.join(['high', 'way', 'man']) -> 'highwayman'
### Generally used in tuple unpacking
'unforgettable'.partition('forget') -> ('un', 'forget', 'able')

# Unused or dummy value use _
origin, _, destination = "Seattle-Boston".partition('-')

# Positional args
'The age of {0} is {1}".format('Chivallry', 32)

pos = (65.2, 23.1, 82.2)
"GG position x = {pos[0]} y = {pos[1]} z = {pos[2]}".format(pos=pos)
```

### Range
- Collection rather than a container

```python
range(5)

for i in range(5):
    print(i) # 0, 1, 2, 3, 4

list(range(5, 10))
[5, 6, 7, 8, 9]

# Step Arg
list(range(0, 10, 2))

# Unpythonic
s = [0, 1, 4, 6, 13]
for i in range(len(s)):
    print(s[i])

# Pythonic way
for v in s:
    print(v)


t = [6, 372, 8862, 148800, 2096886]
for p in enumerate(t):
    print(p)

(0, 6)
(1, 372)
(2, 8862)
(3, 148800)
(4, 2096886)

for i, v in enumerate(t):
    print("i={}, v={}".format(i, v))
```

### Lists

- Mutable Sequence

```python
s = "show me how to index".split() -> ['show', 'me', 'how', 'to', 'index']

# Fifth element from the end
s[-5]

# Start stop indexes
s[1:4]

# Slicing
# All elements between first and last
s[1:-1]
# From third until end
s[3:]
# Uptil third
s[:3]

# Copying a list
# Shallow Copy - new list containing same refs
s = ['show', 'me', 'how', 'to', 'index']
full_slice = s[:]
full_slice == s
OR
u = s.copy()
OR
v = list(s)

# Inner lists example
a = [[1, 2], [3, 4]]
b = a[:]
a is b # Lists are distinct objects
a == b # Equivalent values
a[0] is b[0]
```

