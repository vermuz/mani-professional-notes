### Python Notes

#### Collections

###### Tuple
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

###### String

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

###### Lists

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


# List repetition is SHALLOW !

# Index of an element in a list
w = "the quick fox".split()
i = w.index("fox")
w.count("the")
36 in [1, 7, 34]
78 not in [1, 7, 34]
# ------------------------------
u = ["jack", "love"]
del u[1]
OR
u.remove("jack")
```

###### Dictionary

```python
# Dictionary copying is shallow by default
d = dict(golden='xxx', indigo='yyy', seashell='zzz')
e = d.copy()
f = dict(e)
g = dict(golden1='xxx', indigo1='yyy', seashell1='zzz')
# Update Dictionary
f.update(g)

# Keys and Values
for value in colors.values():
    print(value)
for key in colors.keys():
    print(key)

for key, value in colors.items():
    print("{key} => {value}".format(
        key=key,
        value=value)
    )

# in, not in
'nz' in countries
'm' not in countries

# Deletion
del z['Un']

# Keys in a dictionary should be immutable
# Values in a dictionary can be modified

m = {
    'H': [1, 2, 3],
    'I': [4, 5, 6],
    'J': [7, 8, 9]
}
m['H'] += [4, 5, 6, 7]
# Add new items
m['N'] = [3, 1]
```

### Pprint Pretty Print

```python
from pprint import pprint as pp
pp(m)
```


###### Set

- Unordered collection of unique element
- Collection is mutable
- Set is unordered
- Sets are iterable but the order is arbitrary

```python
p = {6, 28, 496}
# Empty set
e = set()

# Discarding duplicates
s = set([2, 4, 6, 6, 6, 30, 28])

# Add Single Element
k ={81, 108}
k.add(54)
# Add multiple elements
k.update([37, 128, 97])
# Removal will give error, discard will not
k.remote(82)
k.discard(82)

# Set copying is shallow copying, copying references rather than objects
# Sets have intersection, union , difference operations..
# issubset(), issuperset(), isdijoint() -> nothing in common
```

### Iterables

#### Comprehensions
```
[expr(item) for item in iterable]
```

```python
# String -> List
words = "Why sometimes do i feel as something".split()
# Comprehension
[len(word) for word in words]

# Another example
from math import factorial
f = [len(str(factorial(x))) for x in range(20)]
# Above list as a set will remove duplicates
{len(str(factorial(x))) for x in range(20)}
# Dictionary comprehension
country_to_capital = {
    'UK': 'London',
    'US': 'DC',
    'INDIA': 'Delhi'
}
# Items for both keys and values
capital_to_country = {capital: country for country, capital in country_to_capital.items()}
pp(capital_to_country)

words = ["hi", "hello", "foxtrot"]
{ x[0]: x for x in words }
```

```python
# Filtering Predicate if clause
def is_prime():
    pass

[x for x in range(101) if is_prime(x)]

# Prime Square Divisors
prime_square_divisors = {x*x:(1, x, x*x) for x in range(101)}
```

### Iterable, Iterator

Iterable objects can be passed to the built-in iter() function to get an
iterator.
```
iterator = iter(iterable)
```
Iterator objects can be passed to the built-in next() function to fetch
the next item.
```
item = next(interator)
```

```python
iterable = ['Spring', 'Summer', 'Autumn', 'Winter']
iterator = iter(iterable)
next(iterator) # -> 'Spring'
next(iterator) # -> 'Summer'
```


### Generators in Python
- Specify iterable sequences
- All generators are iterators
- lazily evaluated
- are composable into pipelines
- Each call to generator function returns no generator object
- Generators are lazy - only when requested by the caller (can produce
never ending sequences)

```python
def gen123():
    yield 1
    yield 2
    yield 3


g = gen123()
# Returns a generator object -> python iterator
next(g) # returns 1
next(g) # returns 2
next(g) # returns 3
next(g) # Stop iterator exception
```

```python
for v in gen123():
    print(v)
```

```python
# Mainitaining state in generators in local variables
def take(count, iterable):
    counter = 0
    for item in iterable:
        if counter == count:
            return
        counter += 1
        yield item

def run_take():
    items = [2, 4, 6, 8, 10]
    for item in take(3, items):
        print(item)
```

```python
# Infinite Generator
def testFunc():
    yield 2
    a = 2
    b = 1
    while True:
        yield b
        a, b = b, a + b

for x in testFunc():
    print(x)
```

#### Generator Comprehension


```
(expr(item) for item in iterable)
```

```python
# 40 MBs of memory
million_squares = (x*x for x in range(1, 1000000))
list(million_squares)
```

#### Generators are single use objects

```python
sum(x*x for x in range(1, 1000000))
```

###### Iteration Operations
- itertools
- any (any true)
- all (all true)
- zip

```
any(is_prime(x) for x in range(1328, 1361))
```

```python
# Proper noun check
all(name == name.title() for name in ['London', 'New York'])
```

```python
sunday = [12, 14, 15, 14]
monday = [12, 14, 14, 14]

for item in zip(sunday, monday):
    print(item)

(12, 12)
(15, 14)
```

### Classes

Define structure and behaviour of objects.

```python
class Flight:
    # Not a constructor just an intializer
    def __init__():
        self._number = number
    def number(self):
        return "ewe"
```
