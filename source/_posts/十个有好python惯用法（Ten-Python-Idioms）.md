---
title: 十个有好python惯用法（Ten Python Idioms）
date: 2015-01-09 19:48:05
tags: 
- python
categories:
- 技术人生
- Python探案
---

## 1\. Make a script both importable and executable(使你的脚本可输入且可执行)

    if __name__ == '__main__':`</pre>

    #### Example

    <pre>`def main():
        print('Doing stuff in module', __name__)

    if __name__ == '__main__':
        print('Executed from the command line')
        main()

    $ python mymodule.py
    Executed from the command line
    Doing stuff in module __main__

    &gt;&gt;&gt; import mymodule
    &gt;&gt;&gt; mymodule.main()
    Doing stuff in module mymodule`</pre>
<!-- more -->

    ## 2\. Test for “truthy” and “falsy” values(测试采用真假判断)

    <pre>`if x:
    if not x:`</pre>

    #### Example

    <pre>`# GOOD
    name = 'Safe'
    pets = ['Dog', 'Cat', 'Hamster']
    owners = {'Safe': 'Cat', 'George': 'Dog'}
    if name and pets and owners:
        print('We have pets!')

    # NOT SO GOOD
    if name != '' and len(pets) &gt; 0 and owners != {}:
        print('We have pets!')`</pre>

    ## 3\. Use in where possible(如果有可能尽可能使用in)

    <pre>`Contains:
    if x in items:

    Iteration:
    for x in items:`</pre>

    #### Example (contains)

    <pre>`# GOOD
    name = 'Safe Hammad'
    if 'H' in name:
    print('This name has an H in it!')

    # NOT SO GOOD
    name = 'Safe Hammad'
    if name.find('H') != -1:
        print('This name has an H in it!')`</pre>

    #### Example (iteration)

    <pre>`# GOOD
    pets = ['Dog', 'Cat', 'Hamster']
    for pet in pets:
        print('A', pet, 'can be very cute!')

    # NOT SO GOOD
    pets = ['Dog', 'Cat', 'Hamster']
    i = 0
    while i &lt; len(pets):
        print('A', pets[i], 'can be very cute!')
        i += 1`</pre>

    ## 4\. Swap values without temp variable(交换两个数不适用temp中间值)

    <pre>`a, b = b, a`</pre>

    #### Example

    <pre>`# GOOD
    a, b = 5, 6
    print(a, b) # 5, 6
    a, b = b, a
    print(a, b) # 6, 5

    # NOT SO GOOD
    a, b = 5, 6
    print(a, b) # 5, 6
    temp = a
    a = b
    b = temp
    print(a, b) # 6, 5`</pre>

    ## 5\. Build strings using sequence(使用序列的方式来得到字符串)

    <pre>`''.join(some_strings)`</pre>

    #### Example

    <pre>`# GOOD
    chars = ['S', 'a', 'f', 'e']
    name = ''.join(chars)
    print(name) # Safe

    # NOT SO GOOD
    chars = ['S', 'a', 'f', 'e']
    name = ''
    for char in chars:
        name += char
        print(name) # Safe`</pre>

    ## 6\. EAFP is preferable to LBYL(大概意思是说使用专业的容错机制)

    <pre>`“It's Easier to Ask for Forgiveness than Permission.”

    “Look Before You Leap”

    try: v. if ...:
    except:`</pre>

    #### Example

    <pre>`# GOOD
    d = {'x': '5'}
    try:
        value = int(d['x'])
    except (KeyError, TypeError, ValueError):
        value = None

    # NOT SO GOOD
    d = {'x': '5'}
    if 'x' in d and \
        isinstance(d['x'], str) and \
        d['x'].isdigit():
        value = int(d['x'])
    else:
        value = None`</pre>

    ## 7\. Enumerate(常用该函数，得到(index, value))

    <pre>`for i, item in enumerate(items):`</pre>

    #### Example

    <pre>`# GOOD
    names = ['Safe', 'George', 'Mildred']
    for i, name in enumerate(names):
        print(i, name) # 0 Safe, 1 George etc.

    # NOT SO GOOD
    names = ['Safe', 'George', 'Mildred']
    count = 0
    for name in names:
        print(i, name) # 0 Safe, 1 George etc.
        count += 1`</pre>

    ## 8\. Build lists using list comprehensions(使用列表合成新的列表)

    <pre>`[i * 3 for i in data if i &gt; 10]`</pre>

    #### Example

    <pre>`# GOOD
    data = [7, 20, 3, 15, 11]
    result = [i * 3 for i in data if i &gt; 10]
    print(result) # [60, 45, 33]

    # NOT SO GOOD (MOST OF THE TIME)
    data = [7, 20, 3, 15, 11]
    result = []
    for i in data:
        if i &gt; 10:
            result.append(i * 3)
            print(result) # [60, 45, 33]`</pre>

    ## 9\. Create dict from keys and values using zip(尽可能使用zip()函数创建字典)

    <pre>`d = dict(zip(keys, values))`</pre>

    #### Example

    <pre>`# GOOD
    keys = ['Safe', 'Bob', 'Thomas']
    values = ['Hammad', 'Builder', 'Engine']
    d = dict(zip(keys, values))
    print(d) # {'Bob': 'Builder',
                'Safe': 'Hammad',
                'Thomas': 'Engine'}

    # NOT SO GOOD
    keys = ['Safe', 'Bob', 'Thomas']
    values = ['Hammad', 'Builder', 'Engine']
    d = {}
    for i, key in enumerate(keys):
        d[keys] = values[i]
        print(d) # {'Bob': 'Builder',
                    'Safe': 'Hammad',
                    'Thomas': 'Engine'}`</pre>

    ## 10\. And the rest … !

    <pre>`● while True:
    break # This will spark discussion!!!

    ● Generators and generator expressions.

    ● Avoid from module import *
    Prefer: import numpy as np; import pandas as pd

    ● Use _ for “throwaway” variables e.g.:
    for k, _ in [('a', 1), ('b', 2), ('c', 3)]

    ● dict.get() and dict.setdefault()

    ● collections.defaultdict

    ● Sort lists using l.sort(key=key_func)