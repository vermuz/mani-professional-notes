### Python Idioms

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

### Eliminate duplicate entries

list or dict with duplicate values.

```python
unique_names = []
for surname in surnames:
    if name not in unique_names:
        unique_names.append(name)
#-------------------------------------
unique_names = set(surnames)
```

### NamedTuples

namedtuples give you the ability to access fields by names rather than by index.

```python
from collections import namedtuple

EmployeeRow = namedtuple('EmployeeRow', ['f_name', 'l_name', 'department', 'salary', 'hiring_date'])
```
### Ignore extra data with _

```python
(name, age, temp, temp1) = user_info(user)
(name, age, _, _) = user_info(user)
```

### unpack data

```python
list = ['dog', 'Rexxx', 10]
animal = list[0]
name = list[1]
age = list[2]

output = ('{name} the {animal} is {age} years old'.format(
animal=animal, name=name, age=age))

# -----------------------------------------------------------

list = ['dog', 'Rexxx', 10]
(animal, name, age) = list
output = ('{name} the {animal} is {age} years old'.format(
animal=animal, name=name, age=age))
```

### Return multiple values

```python
def stat(list):
    mean = float(sum(list) / len(list)) 
    median = list[int(len(list) / 2)]
    mode = Counter(list).most_common(1)[0][0]
    return (mean, median, mode)

(mean, median, mode) = stat([10, 20, 20, 30])
```

### Classes

### @classmethod

```python
class Student():
    __tablename__ = 'student'

    def table_name(self):
        return Student.__tablename__

class DerivedStudent(Student):
    __tablename__ = 'derived_student'

b = DerivedBlog()
print(b.table_name()) # prints 'student'

#---------------------------------

class Student():
    __tablename__ = 'student'

    def table_name(self):
        return self.__tablename__
    # Properly defined as a classmethod , using the decorator of the same name.
    @classmethod
    def other_table_name(cls):
        return cls.__tablename__

class DerivedStudent(Studen):
    __tablename__ = 'derived_student'
    
b = DerivedBlog()
print(b.table_name()) # prints 'derived_student'
# if a derived class calls table_name , the cls parameter is set to the derived class, rather than Student
```

### In Python, the module is the unit of encapsulation.

### isinstance

```python
def get_size(object):
    if isinstance(object, (list, dict, str, tuple)):
        return len(object)
    return int(object)
```

### “private” data

- Attributes to be ‘protected’, which are not meant to be used directly by clients, should be prefixed with a single underscore. 
- ‘private’ attributes not meant to be accessible by a subclass should be prefixed by two underscores.
- Prepending a single underscore means that the symbol won’t be imported if the ‘all’ idiom is used. 
- Prepending two underscores to an attribute name invokes Python’s
name mangling

```python
class Test1():
    def __init__(self):
        self.id = 5
        self.value = self.get_value()
    
    def get_value(self):
        pass

    def should_destroy_target(self):
        return self.id == 52

class Test2(Test1):
    def get_value(self, some_new_parameter):
    """Since 'get_value' is called from the base class's
    __init__ method and the base class definition doesn't
    take a parameter, trying to create a Test2 instance will
    fail.
    """
    pass

class Test3(Test1):
    """We aren't aware of Test1's internals, and we innocently
    create an instance attribute named 'id' and set it to 42.
    This overwrites Test1's id attribute and we inadvertently
    blow up the target.
    """
    def __init__(self):
        super(Test3, self).__init__()
        self.id = 42
        # No relation to Test1's id, purely coincidental

q = Test3()
b = Test2() # Raises 'TypeError'
q.should_destroy_target() # returns True
q.id == 42 # returns True
#----------------------------------------
class Test1():
    def __init__(self):
        """Since 'id' is of vital importance to us, we don't
        want a derived class accidentally overwriting it. We'll
        prepend with double underscores to introduce name
        mangling.
        """
        self.__id = 8
        self.value = self.__get_value() # Our 'private copy'

    def get_value(self):
        pass

    def should_destroy_target(self):
        return self.__id == 42
    # Here, we're storing a 'private copy' of get_value,
    # and assigning it to '__get_value'. Even if a derived
    # class overrides get_value in a way incompatible with
    # ours, we're fine
    __get_value = get_value

class Test2(Test1):
    def get_value(self, some_new_parameter):
        pass

class Test3(Test1):
    def __init__(self):
        """Now when we set 'id' to 42, it's not the same 'id'
        that 'should_destroy_target' is concerned with. In fact,
        if you inspect a Test3 object, you'll find it doesn't
        have an __id attribute. So we can't mistakenly change
        Test1's __id attribute even if we wanted to.
        """
        self.id = 42
        # No relation to Test1's id, purely coincidental
        super(Test3, self).__init__()

q = Test3()
b = Test2() # Works fine now
q.should_destroy_target() # returns False
q.id == 42 # returns True
with pytest.raises(AttributeError):
getattr(q, '__id')
```

## Properties

```python
class StoreItem():
    def __init__(self, name, price):
        self.name = name
        # We could try to apply the tax rate here, but the item's price
        # may be modified later, which erases the tax
        self.price = price
#---------------------------------------
class StoreItem():
    def __init__(self, name, price):
        self.name = name
        self._price = price

    @property
    def price(self):
        # if we need to change how price is calculated, we can do it
        # here (or in the "setter" and __init__)
        return self._price * TAX_RATE

    @price.setter
    def price(self, value):
        # The "setter" function must have the same name 
        # as the property
        self._price = value
```

### Repr

- __repr__ is used for machines to read
- __repr__ should contain all the information necessary to reconstruct the object
- It’s especially useful in logging

```python
class Test():
    def __init__(self, a=10, b=12, c=None):
        self.a = a
        self.b = b
        self._c = c or {}
    
    def __str__(self):
        return 'A is {}, B is {}'.format(self.a, self.b)

    def console(instance):
        print(instance)

console([Test(), Test(c={'x': 'y'})])
#---------------
class Test():
    def __init__(self, a=10, b=12, c=None):
        self.a = a
        self.b = b
        self._c = c or {}

    def __str__(self):
        return '{}, {}'.format(self.a, self.b)

    def __repr__(self):
        return 'Test({}, {}, {})'.format(self.a, self.b, self._c)

def console(instance):
    print(instance)

console([Test(), Test(cache={'x': 'y'})])
```

### __str__ method

```python
class Test():
    def __init__(self, x, y):
        self.x = x
        self.y = y

a = Test(5, 7)
print(a)
# Prints '<__main__.Point object at 0x91ebd0>'
#-------------------------
class Test():
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return '{0}, {1}'.format(self.x, self.y)

b = Test(5, 7)
print(b)
# Prints '5, 7'
```
