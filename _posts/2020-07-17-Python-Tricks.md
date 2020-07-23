---
title: Python Tricks
date: 2020-07-17 9:12:00 -0500
categories: [Programming, Python]
tags: [python]
---

This is my note for the book [Python Tricks: The Book A Buffet of Awesome Python Features](https://realpython.com/products/python-tricks-book/) written by Dan Bader from RealPython. Personally, I like RealPython very much. The tutorials on this website are mostly thorough and clear. I would recommend it to you if you want to dive deeper into some python features or functions.

## Self Test
1. When do we use `assert` and how to use it?
2. What is a context manager? How to use `with`? How to write a self-defined context manager? (Two ways.)
3. List commonly used magic methods, or say, dunder methods, and think about their usage.
5. try-except-finally
6. What is a class method? What is a static method? What are the differences?
7. Underscore in variable names. `_var`, `var_`, `__var`, `__var__`, `_`
8. What are the differences between private variables and protected variables?
9. Formatting options for literal string `f''`?
10. Write a function with closures. Write an object that can behave like functions, namely, a callable object.
4. What is a decorator? How to write a debuggable decorator that accepts arguments? How to use the decorator? 

11. `*args`, `**kwargs`. What are the difference between positional and keyword arguments?
12. What is an iterable? List five common iterables. Are sets and dictionaries iterables?
13. What are the differences between `__str__` and `__repr__`?



## Effective Functions

### Decorators
```python
import functools
def uppercase(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        original_result = func(*args, **kwargs)
        modified_result = original_result.upper()
        return modified_result

@uppercase
def greet(time):
    """A greeting function."""
    if time == 'morning':
        print('Good morning!')
    else:
        print('Hello!')

greet('morning')
print(greet.__name__)
print(greet.__doc__)
```

What is a generator? What is an iterator? When would we use them? How to use them? How to write them?


### Functions With *args and **kwargs
When we input arguments to a function, we can either input according to the order of the arguments in the definition of the function, or use keywords to specify which argument we are inputting. The former is called positiona arguments and the latter is called keyword argument. Since positional arguments follow strictly the order, so it is proper to use a tuple to represent it. While for keyword arguments, order doesn't matter, and with the key and value structure, a dictionary would be a good choice.


### Iterables
References:
- [Iterables](https://www.pythonlikeyoumeanit.com/Module2_EssentialsOfPython/Iterables.html)


## Classes & OOP

### 

## Pythonic Coding Habits
1. import packages