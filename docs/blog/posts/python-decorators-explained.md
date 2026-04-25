---
date: 2026-04-22
authors:
  - liyao
title: Python Decorators Explained Simply
slug: python-decorators-explained
description: >
  Demystifying Python decorators — what they are, how they work, and when to use them.
categories:
  - Python
---

# Python Decorators Explained Simply

Decorators are one of Python's most elegant features, but they can be confusing at first. Let's break them down.

## What Is a Decorator?

A decorator is simply a function that takes another function and extends its behavior without modifying it explicitly.

```python
def my_decorator(func):
    def wrapper():
        print("Something before the function")
        func()
        print("Something after the function")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

Output:

```
Something before the function
Hello!
Something after the function
```

## How It Works

The `@my_decorator` syntax is syntactic sugar for:

```python
say_hello = my_decorator(say_hello)
```

## A Real-World Example: Timing Functions

```python
import time
from functools import wraps

def timer(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        end = time.perf_counter()
        print(f"{func.__name__} took {end - start:.4f}s")
        return result
    return wrapper

@timer
def compute_heavy():
    total = sum(i * i for i in range(10_000_000))
    return total

compute_heavy()
```

## Why Use `@wraps`?

Without `functools.wraps`, the decorated function loses its metadata — `__name__`, `__doc__`, etc. Always use it.

## When to Use Decorators

- **Logging** — log function calls automatically
- **Caching** — `@lru_cache` for memoization
- **Authorization** — check permissions before executing
- **Validation** — validate arguments before processing
- **Retry logic** — retry on failure with backoff

Decorators let you separate cross-cutting concerns cleanly. Once you understand them, you'll find uses everywhere.

---

*Got questions about decorators? Let me know in the comments!*
