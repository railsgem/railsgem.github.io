---
layout: post
title:  "Python Class"
date:   2016-04-23 08:15:09 +1100
categories: Python
---
* 目录
{:toc}

### keyword-only arguments

With complex functions like this, it’s better to require that callers are clear about their intentions. In Python 3, you can demand clarity by defining your functions with keyword-only arguments. These arguments can only be supplied by keyword, never by position.

Here, I redefine the safe_division function to accept keyword-only arguments. The * symbol in the argument list indicates the end of positional arguments and the beginning of keyword-only arguments.

def safe_division_c(number, divisor, *,
                    ignore_overflow=False,
                    ignore_zero_division=False):
    # ...
Now, calling the function with positional arguments for the keyword arguments won’t work.

safe_division_c(1, 10**500, True, False)

>>>
TypeError: safe_division_c() takes 2 positional arguments but 4 were given
Keyword arguments and their default values work as expected.

safe_division_c(1, 0, ignore_zero_division=True)  # OK

try:
    safe_division_c(1, 0)
except ZeroDivisionError:
    pass  # Expected