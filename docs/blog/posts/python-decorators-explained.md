---
date: 2026-04-22
authors:
  - liyao
title: 深入浅出 Python 装饰器
slug: python-decorators-explained
description: >
  解密 Python 装饰器 —— 它是什么、如何工作、什么时候该用它。
categories:
  - Python
---

# 深入浅出 Python 装饰器

装饰器是 Python 最优雅的特性之一，但初学者往往觉得难以理解。让我们把它拆开来看。

## 什么是装饰器？

装饰器本质上是一个函数，它接收另一个函数作为参数，在不修改原函数的情况下扩展其功能。

```python
def my_decorator(func):
    def wrapper():
        print("函数执行前")
        func()
        print("函数执行后")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

输出：

```
函数执行前
Hello!
函数执行后
```

## 原理揭秘

`@my_decorator` 语法只是以下代码的语法糖：

```python
say_hello = my_decorator(say_hello)
```

## 实战示例：计时装饰器

```python
import time
from functools import wraps

def timer(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        end = time.perf_counter()
        print(f"{func.__name__} 耗时 {end - start:.4f} 秒")
        return result
    return wrapper

@timer
def compute_heavy():
    total = sum(i * i for i in range(10_000_000))
    return total

compute_heavy()
```

## 为什么用 `@wraps`？

不使用 `functools.wraps` 的话，被装饰的函数会丢失元数据 —— `__name__`、`__doc__` 等。所以务必加上它。

## 装饰器的应用场景

- **日志记录** — 自动记录函数调用
- **缓存** — 使用 `@lru_cache` 实现记忆化
- **权限校验** — 在执行前检查权限
- **参数验证** — 处理前校验参数
- **重试机制** — 失败时按退避策略重试

装饰器让你能干净地分离横切关注点。一旦掌握了它，你会发现到处都能用上。

---

*对装饰器有疑问？欢迎在评论区交流！*
