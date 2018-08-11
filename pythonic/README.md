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
