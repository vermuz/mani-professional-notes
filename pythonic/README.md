### *args and **kwargs

 *args and **kwargs allow you to pass a variable number of arguments to a function.
 
 *args is used to send a non-keyworded variable length argument list to the function.

```python
def test_var_args(f_arg, *argv):
    print("first normal arg:", f_arg)
    for arg in argv:
        print("another arg through *argv:", arg)

test_var_args('mani', 'python', 'sea', 'test')
```

**kwargs allows you to pass keyworded variable length of arguments to a function.

```python
def greet_me(**kwargs):
    for key, value in kwargs.items():
        print("{0} = {1}".format(key, value))

>>> greet_me(name="mani")
name = mani
```

### Debugging

Running from commandline

```
$ python -m pdb my_script.py
```

Running from inside a script

```python
import pdb

def make_bread():
    pdb.set_trace()
    return "no time"

print(make_bread())

Commands:

c: continue execution
w: shows the context of the current line it is executing.
a: print the argument list of the current function
s: Execute the current line and stop at the first possible occasion.
n: Continue execution until the next line in the current function is reached or it returns.
```

### Iterators

#### Iterable
_An iterable is any object in Python which has an __iter__ or a __getitem__ method defined which returns an iterator or can take indexes. In short an iterable is any object which can provide us with an iterator._

#### Iterator
_An iterator is any object in Python which has a next (Python2) or __next__ method defined._

#### Iteration
_In simple words it is the process of taking an item from something e.g a list. When we use a loop to loop over something it is called iteration. It is the name given to the process itself._

#### Generators
- Generators are iterators, but you can only iterate over them once.
- They do not store all the values in memory, they generate the values on the fly. 
- You use them by iterating over them, either with a ‘for’ loop or by passing them to any function or construct that iterates. 
- Most of the time generators are implemented as functions. However, they do not return a value, they yield it.
- Generators are best for calculating large sets of results where you don’t want to allocate the memory for all results at the same time.
- next() allows us to access the next element of a sequence.
```python
def generator_function():
    for i in range(3):
        yield i

gen = generator_function()
print(next(gen))
# Output: 0
```
- iter. It returns an iterator object from an iterable. 
```python
my_string = "Mani"
my_iter = iter(my_string)
print(next(my_iter))
# Output: 'M'
```

```python
def generator_function():
    for i in range(10):
        yield i

for item in generator_function():
    print(item)
```

```python
def fibon(n):
    a = b = 1
    result = []
    for i in range(n):
        result.append(a)
        a, b = b, a + b
    return result
```
OR
```python
# generator version
def fibon(n):
    a = b = 1
    for i in range(n):
        yield a
        a, b = b, a + b
```
