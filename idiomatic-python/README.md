### Writing Idiomatic Python

### error
```python
if a is not result:
    return 'error'
elif b is not result:
    return 'error'
a = doSomething()
return
```
### Comparison 

```python
if x <= y and y <= z:
    return True
```
```python
if x <= y <= z:
    return True
```

### Comparison again
```
is_generic_name = False
name = 'A'
if name == 'B' or name == 'C' or name == 'D':
is_generic_name = True
```
```
name = 'A'
is_generic_name = name in ('A', 'B', 'C')
```

### True

```python
if something == True
```
```python
if something
```

### conditional

```python
if foo:
    value = 1
```
```python
value = 1 if foo else 0
```

### enumerate

```python
names = ['Mani', 'Ali', 'Chaali']
index = 0
for name in names:
    print('{} {}'.format(index, element))
    index += 1
```
```python
names = ['Mani', 'Ali', 'Chaali']
for index, element in enumerate(names):
    print('{} {}'.format(index, element))
```

### in

```python
names = ['Mani', 'Ali', 'Chaali']
index = 0
while index < len(names):
    print(names[index])
    index += 1
```
```python
names = ['Mani', 'Ali', 'Chaali']
for name in names:
    print(name)
```

### For Else

```python
for user in users():
    print('Checking {}'.format(user))
    for address in user.get_all_addresses():
        if email_is_malformed(email_address):
        print('Has a bad address!')
        break
    else: # this else matches the `for` loop, not the if!
        print('All addresses are valid!')
```

### Mutable Objects

- list , dict , set , and most class instances are mutable
- string , int , and tuple objects are all examples of immutable objects.

```python
def func(a, List=[]):
    List.append(a)
    return List
    
print(func(1))
print(func(2))
print(func(3))
```
```python
# If you don't want the default to be shared between subsequent
# calls
def f(a, List=None):
    if List is None:
        List = []
    List.append(a)
    return List
```

### Return

```python
def all_equal(a, b, c):
    result = False
    if a == b == c:
        result = True
    return result
```
```python
def all_equal(a, b, c):
    return a == b == c
```

