---
layout: post
title: "Assert statements"
subtitle: 
tags: [python note]
comments: true
published: true
---

### [7.3. The assert statement](https://docs.python.org/3/reference/simple_stmts.html#assert)
### [What is the use of “assert” in Python?](https://stackoverflow.com/questions/5142418/what-is-the-use-of-assert-in-python)

Assert statements are a convenient way to insert debugging assertions into a program.

Source code: `python-code/toolkit/start_assert.py`

```python
assert expression, "AssertionError message."
```

equivalent to,
```python
if __debug__:
    if not expression: raise AssertionError("message.")
```

where `__debug__` is built-in variable with `True` value.
```python
print(f"__debug__ = {__debug__}. If __debug__ is False, it will not raise any AssertionError.")
```

#### Ex.1 
First example, check two values are equal or not:
```python
assert 0 == 1, "hello, 0 is not equal to 1 !"
```

this output will be:
```python
AssertionError 
Traceback (most recent call last)
c:\Users\user\Desktop\san\python-code\start_assert.py in 
----> 20 assert 0 == 1, "hello, 0 is not equal to 1 !"

AssertionError: hello, 0 is not equal to 1 !
```

#### Ex.2
Alert the input number should be positive number:
```python
number = int(input("Enter a number:"))
assert number > 0, "Only positive number is allowed."
```

#### Ex.2.1
same as Ex.2, to show f-string functionality can be used in `assert`:
```python
number = int(input("Enter a number:"))
assert number > 0, f"Is number <= 0 ? {number <= 0}"
```

#### Ex.3
Check the class of object `df` as we thounght:
```python
#import pandas as pd
#df = pd.DataFrame(data = list(range(10)), columns= ['number'])
df = list(range(10)) 
assert isinstance(df, pd.DataFrame), "df is not a pd.DataFrame."
```