# Mani Professional Notes

### Table of Contents

1. [Introduction](#introduction)
2. [Programming Language Concepts](#language-concepts)
  
### Introduction
In my professional career, I have always considered learning to be one constant. While acquiring new skills, it would
be great to keep track of certain principles that can be applied in any new environment. This is my repo to help me
remember the foundations that I shouldnt lose sight of in everyday professional work.

### Programming Language Concepts

### Values and Symbols
Symbols are variables, names that can be given to entities. *A symbol refers to a value. A value can be referred by many
symbols*. A value is stored in memory, symbol is a reference to that stored memory location. Multiple symbols can reference
one value. Changing the value will affect all symbols referencing that value.
### Immutability
When your language does not have features of changing the value itself. (Mostly to help against bug introduced by mutability)
Some languages will allow you to assign new value to an existing symbol but without overwriting the actual value, so just a new memory location and it will bind your variable to that new location.
In Java,
- Passing a primitive into function -> `passes value itself`
- Passing an object to a function -> `passes reference to the object`
### Types
- Primitive Types: integers, characters, strings, floats etc
- Complex Data Types: Arrays, Maps, Lists, Sets, Maps (Dictionaries, hashes, Associative Arrays) etcetera
### Bindings
```python
# n inside function is different from n variable which is being assigned a value of 1.
n = 1
def testAddition(n):
    return n+1
```
Binding of n is different inside function from outside. Definition of a parameter in a function creates a new binding, introducing new bindings -> **Scope**
### Typing
Type System: Different types of data can be distinguished from another i.e values of type string and values of type integer.

| Statically Typed languages  | Dynamically Typed languages |
| ------------- | ------------- |
| Type is bound to symbol  | Type is bound to value  |

#### Static typing
Type of data that a symbol refers to is known at compile time. You will have to declare the type of variable. e.g C, Java.

#### Type Inference
If a language lets you get away with not declaring types because the compiler is smart enough to figure out what type the symbol must have been. e.g. Haskell, Scala.

Note: These languages are still statically typed as types are still bound to symbols not values.

##### Pros/Cons
- Type safety, compiler can check errors in type handling.
- Early recognition of errors.
- Optimization of compiled code, compiler knows the types and can apply optimizations for the data types.
- Code is very verbose (symbol types, function params, custom types to hold data) also if your code is handling type A, it will need changes to support type B or use advanced language features to support multiple types flexibly.

#### Dynamic Typing
Type of data that a symbol refers to is only known at runtime. Symbols are free of types and can refer to any type so you will not see in type declarations, e.g. PHP, JavaScript, Perl

##### Pros/Cons
- No type safety at compile time.
- Types only become clear at runtime.
- Fewer optimizations from compiler since types are unknown.
- Less verbose code.
- No need for type declarations, and no need for definitions.
- You can use language's native collection types rather than build your own.
- Life will become difficult if you write functions that accept many different “shapes” of data structures.
- You can write a function and apply it to data without being forced to define custom data types for your use case.

#### Type Hints
You can annotate symbols with type declarations, so that the compiler can act on that regarding its optimization. 
This can be very beneficial for performance critical sections of your code and can often result in very fast object code, 
that is just as fast as code compiled from a statically typed language. (Common Lisp and Clojure)

#### Strong Typing
Strong typing means that the language is quite restrictive about casting data of one type to another. Some type safety check is in place.  Java for example is a strongly typed language and thus does not allow a Double to be cast to an Integer. Instead, the language usually provides functions that will convert one type to another type.

#### Weak typing
Weak typing means that the language is not restrictive about casting data of one type to another. e.g. C

### Lifetime stages a program runs through
Source code -> Preprocessor -> Compiler -> Runtime

### Compile Time vs Runtime

#### Compile Time
- Source code is being transformed into machine code, bytecode or source for a different language
- Compilation usually consists of multiple stages e.g optimization

#### Runtime
- Code runs natively on virtual machine. Garbage collection, dynamic typing etc happen here.

#### Just in time compilation (JIT)
While running an interpreted program, runtime may call the compilation stage whenever code is to be run that has not yet been compiled. This can happen quite a lot depending on the interpreter being used.

### Mutable State
When the state of a program changes over time, it is said to have Mutable state. This makes code unmanageable
and error prone. It should be avoided if possible however if we want to introduce it somwhere in code, it should
not impact other parts of the code. e.g When the user moves the mouse for example, it is in fact a change in state of the external world.

### Recursion and Iteration
- Every iterative implementation can be converted to a recursive one and vice versa.
- Recursion may lead to a stack overflow, as each nested recursive call consumes space
on the stack.
- Iterative programs usually rely on mutable state, as you have to make use of a
variable that counts the iterations or something similar

```python
def sum(list):
    sum = 0
 
    # Add every number in the list.
    for i in range(0, len(list)):
        sum = sum + list[i]
 
    # Return the sum.
    return sum
 
print(sum([5,7,3,8,10]))
```
```python
 To do this recursively:

#!/usr/bin/env python
 
def sum(list):
   if len(list) == 1:
        return list[0]
   else:
        return list[0] + sum(list[1:])
 
print(sum([5,7,3,8,10]))
```
If the length of the list is one it returns the list (the termination condition).

### Statements vs Expressions
- Statements don't evaluate to a value.
- Expressions evaluate to something, i.e a + b is an expression
- In functional languages everything is an expression,
a function definition evaluates to a function object that
can be passed around afterwards.

In Clojure for example if evaluates to to then or else branch

```ruby
def fn(x,y)
  y * if x > 10.0
         0.1
      else
         1.0
      end
end

printf(“%.2f\n”, fn(8.0, 123.4))
printf(“%.2f\n”, fn(11.1, 123.4))
```

Many languages support ternary operator, (? :) but that is mainly syntactic sugar - languages in which everything is an expression do not need such special operators and have conciseness in mind.

Diagrams/mermaid-diagram-20180331200051.svg
![Screenshot](Diagrams/mermaid-diagram-20180331200051.svg)
