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
