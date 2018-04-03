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

### Arguments
Keywords arguments are distinguished from “normal” arguments by the presence of an = and a default value.

```python
def list(list_value, separator):
    print('{}'.format(separator).join(list_value))
```
```python
def list(list_value, separator=' '):
    print('{}'.format(separator).join(list_value))
```
Using `*args and **kwargs` as parameters allows a function to accept an arbitrary list of positional and keyword arguments

```python
def wrap_add_for_console_output(x, y):
    print('--------------------------------')
    print(str(x + y))
    print('--------------------------------')

wrap_add_for_console_output(2,3)
```
```python
def for_console_output(func):
    def wrapper(*args, **kwargs):
        print('--------------------------------')
        print(str(func(*args, **kwargs)))
        print('--------------------------------')
    return wrapper

@for_console_output
def add(x, y):
    return x + y
    
add(3, 2)
```

### Treat functions as values

```python

def addition_table():
    for x in range(1, 3):
        for y in range(1, 3):
            print(str(x + y) + '\n')

def subtraction_table():
    for x in range(1, 3):
        for y in range(1, 3):
            print(str(x - y) + '\n')

def multiplication_table():
    for x in range(1, 3):
        for y in range(1, 3):
            print(str(x * y) + '\n')

def division_table():
    for x in range(1, 3):
        for y in range(1, 3):
            print(str(x / y) + '\n')

addition_table()
subtraction_table()
multiplication_table()
division_table()
```

```python
import operator as op

def print_table(operator):
    for x in range(1, 3):
        for y in range(1, 3):
            print(str(operator(x, y)) + '\n')

for operator in (op.add, op.sub, op.mul, op.itruediv):
    print_table(operator)
```

### Exceptions

```python
def getlevel(dict):
    if 'ENABLE_LOG' in dict:
        if dict['ENABLE_LOG'] != True:
            return None
        elif not 'DEFAULT_LEVEL' in dict:
            return None
        else:
            return dict['DEFAULT_LEVEL']
    else:
        return None
```
```python
def getlevel(config_dict):
    try:
        if dict['ENABLE_LOG']:
            return dict['DEFAULT_LEVEL']
    except KeyError:
        # if either value wasn't present, a
        # KeyError will be raised, so
        # return None
        return None
```

### Raise Exceptions

```python
import requests
def get_response(url):
    try:
        r = requests.get(url)
        return r.json()
    except:
        print('Oops, something went wrong!')
        return None
```
```python
import requests

def get_response(url):
    return requests.get(url).json()

# If we need to make note of the exception, we
# would write the function this way...

def alternate_get_response(url):
    try:
        r = requests.get(url)
        return r.json()
    except:
    # do some logging here, but don't handle the exception
    # ...
        raise
```

### Data

```python
a = 'foo'
b = 'foo'
c = 'foo'
#--------------------------------
a = b = c = 'foo'
```

### Swapping via tuples

```python
x = 'First'
y = 'Second'
temp = x
x = y
y = temp
```
#--------------------------------
```python
x = 'First'
y = 'Second'
(x, y) = (y, x)
```

### Chain String functions

```python
name = ' Pragmatic Books'
format_name = name.strip()
format_name = format_name.upper()
format_name = format_name.replace(':', ' by')
#--------------------------------
name = ' Pragmatic Books'
format_name = name.strip().upper().replace(':', ' by')
```

### Single String from list

```python
list = ['True', 'False', 'File not found']
res_string = ''
for str in list:
    res_string += str
#--------------------------------
list = ['True', 'False', 'File not found']
res_string = ''.join(list)
```
### ASCII Code

```python

hash_value = 0
char_hash = {
    'a': 97,
    'b': 98,
    'c': 99,
    # ...
    'y': 121,
    'z': 122,
}

for element in some_string:
    hash_value += char_hash[e]
return hash_value

#--------------------------------
hash_value = 0
for element in some_string:
    hash_value += ord(e)
return hash_value
```

### Formatting using format

```python
def get_user_info(user):
    return 'Name: ' + user.name + ', Age: ' + \
        str(user.age) + ', Sex: ' + user.sex
#--------------------------------
def get_user_info(user):
    return 'Name: %s, Age: %i, Sex: %c' % (
        user.name, user.age, user.sex)
#--------------------------------
def get_user_info(user):
    output = 'Name: {user.name}, Age: {user.age}, Sex: {user.sex}'.format(user=user)
    return output
```

### list comprehension

```python
list1 = range(10)
list2 = list()
for element in list1:
    if is_prime(element):
        list2.append(element + 5)
#--------------------------------
list1 = range(10)
list2 = [element + 5
         for element in list1
         if is_prime(element)]
```

### Negative Indexes

Negative indexes count backwards starting at the end of a list

```python
def suffix(word):
    word_len = len(word)
    return word[word_len - 2:]

def suffix(word):
    return word[-2:]
```

### Prefer list comprehensions to the built-in map() and filter()

```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

def is_odd(number):
    return number % 2 == 1

odd_nums = filter(is_odd, nums)
odd_nums_times_two = list(map(lambda x: x * 2, odd_nums))

#---------------------------------

nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
odd_nums_times_two = [n * 2 for n in nums if n % 2 == 1]
```

### Sum

```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
sum = 0
for element in nums:
    sum += element
#------------------------
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
sum = sum(nums)
```

### all

Takes an iterable and returns True if bool(element) is True for all elements

```python
def contains_zero(iterable):
    for e in iterable:
        if e == 0:
            return True
    return False
#-------------------------
def contains_zero(iterable):
    # 0 is "Falsy
    return not all(iterable)
```

### Rest of list -> *

```python
>>> chars = ['a', 'b', 'c', 'd', 'e']
>>> (first, second, *rest) = chars
>>> print(rest)
['c', 'd', 'e']
>>> (first, *middle, last) = chars
>>> print(middle)
['b', 'c', 'd']
>>> (*head, penultimate, last) = chars
>>> print(head)
['a', 'b', 'c']
```

### dict as a substitute for a switch...case

- Python doesn’t have a switch...case construct.functions are
- first-class objects in Python, so we can treat them the same as any other variable.

```python
def apply_operation(l_operand, r_operand, operator):
    if operator == '+':
        return l_operand + r_operand
    elif operator == '-':
        return l_operand - r_operand
    elif operator == '*':
        return l_operand * r_operand
    elif operator == '/':
        return l_operand / r_operand

#---------------------------
def apply_operation(l_operand, r_operand, operator):
    import operator as op
    operator_mapper = {'+': op.add, '-': op.sub,
        '*': op.mul, '/': op.truediv}
    return operator_mapper[operator](l_operand, r_operand)
```

### default parameter of dict.get to provide default values

```python
log_severity = None
if 'severity' in config:
    log_severity = config['severity']
else:
    log_severity = 'Info'
#---------------------
log_severity = config.get('severity', 'Info')
```

### Dict Comprehension

```python
user_email = {}
    for user in users:
        if user.email:
            user_email[user.name] = user.email
#--------------------------
user_email = {user.name: user.email
              for user in users if user.email}
```

### Sets

```python
def get_both_popular_and_active_users():
    # Assume the following two functions each return a
    # list of user names
    most_popular_users = get_list_of_most_popular_users()
    most_active_users = get_list_of_most_active_users()
    popular_and_active_users = []
    for user in most_active_users:
        if user in most_popular_users:
        popular_and_active_users.append(user)
    return popular_and_active_users
    
#-----------------------------------------------
def get_both_popular_and_active_users():
    # Assume the following two functions each return a
    # list of user names
    return(set(
        get_list_of_most_active_users()) & set(
            get_list_of_most_popular_users()))
```

### Set comprehension

```python
users_first_names = set()
for user in users:
    users_first_names.add(user.first_name)
#-----------------------------------------------
users_first_names = {user.first_name for user in users}
```

### Determine if two lists share any common values

The & set operator gracefully solves a very common task: given two lists, do any of the elements in the first list appear in the second?

```python
list_one = ['Manny', 'Mani', 'Ali']
list_two = ['Chaudhry', 'Usman', 'Ali']

def has_duplicate(list_one, list_two):
duplicate_name = False
    for name in list_one:
        if name in list_two:
            duplicate_name = True
    return duplicate_name
#--------------------------------------
list_one = ['Manny', 'Mani', 'Ali']
list_two = ['Chaudhry', 'Usman', 'Ali']

def has_duplicate(list_one, list_two):
    return set(list_one) & set(list_two)
```

## Eliminate duplicate entries

list or dict with duplicate values.

```python
unique_names = []
for surname in surnames:
    if name not in unique_names:
        unique_names.append(name)
#-------------------------------------
unique_names = set(surnames)
```

# NamedTuples

namedtuples give you the ability to access fields by names rather than by index.

```python
from collections import namedtuple

EmployeeRow = namedtuple('EmployeeRow', ['f_name', 'l_name', 'department', 'salary', 'hiring_date'])
```
# Ignore extra data with _

```python
(name, age, temp, temp1) = user_info(user)
(name, age, _, _) = user_info(user)
```
