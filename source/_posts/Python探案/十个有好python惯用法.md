---
title: 十个有好python惯用法
date: 2015-01-09 19:48:05
tags: 
- Python
categories:
- Python探案
---

## 1. Make a script both importable and executable(使你的脚本可输入且可执行)  

	if __name__ == '__main__':
#### Example
	def main():
		print('Doing stuff in module', __name__)

	if __name__ == '__main__':
		print('Executed from the command line')
		main()

	$ python mymodule.py
	Executed from the command line
	Doing stuff in module __main__

	>>> import mymodule
	>>> mymodule.main()
	Doing stuff in module mymodule
<!-- more -->  
## 2. Test for “truthy” and “falsy” values(测试采用真假判断)  

	if x:
	if not x:
#### Example  
	# GOOD
	name = 'Safe'
	pets = ['Dog', 'Cat', 'Hamster']
	owners = {'Safe': 'Cat', 'George': 'Dog'}
	if name and pets and owners:
		print('We have pets!')

	# NOT SO GOOD
	if name != '' and len(pets) > 0 and owners != {}:
		print('We have pets!')  
## 3. Use in where possible(如果有可能尽可能使用in)  
	Contains:
	if x in items:

	Iteration:
	for x in items:
#### Example (contains)
	# GOOD
	name = 'Safe Hammad'
	if 'H' in name:
	print('This name has an H in it!')

	# NOT SO GOOD
	name = 'Safe Hammad'
	if name.find('H') != -1:
		print('This name has an H in it!')
#### Example (iteration)
	# GOOD
	pets = ['Dog', 'Cat', 'Hamster']
	for pet in pets:
		print('A', pet, 'can be very cute!')

	# NOT SO GOOD
	pets = ['Dog', 'Cat', 'Hamster']
	i = 0
	while i < len(pets):
		print('A', pets[i], 'can be very cute!')
		i += 1
## 4. Swap values without temp variable(交换两个数不适用temp中间值)
	a, b = b, a
#### Example
	# GOOD
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
	print(a, b) # 6, 5
## 5. Build strings using sequence(使用序列的方式来得到字符串)
	''.join(some_strings)
#### Example
	# GOOD
	chars = ['S', 'a', 'f', 'e']
	name = ''.join(chars)
	print(name) # Safe

	# NOT SO GOOD
	chars = ['S', 'a', 'f', 'e']
	name = ''
	for char in chars:
		name += char
		print(name) # Safe
## 6. EAFP is preferable to LBYL(大概意思是说使用专业的容错机制)
	“It's Easier to Ask for Forgiveness than Permission.”

	“Look Before You Leap”

	try: v. if ...:
	except:
#### Example
	# GOOD
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
		value = None
## 7. Enumerate(常用该函数，得到(index, value)) 
	for i, item in enumerate(items):
#### Example
	# GOOD
	names = ['Safe', 'George', 'Mildred']
	for i, name in enumerate(names):
		print(i, name) # 0 Safe, 1 George etc.

	# NOT SO GOOD
	names = ['Safe', 'George', 'Mildred']
	count = 0
	for name in names:
		print(i, name) # 0 Safe, 1 George etc.
		count += 1
## 8. Build lists using list comprehensions(使用列表合成新的列表)
	[i * 3 for i in data if i > 10]
#### Example
	# GOOD
	data = [7, 20, 3, 15, 11]
	result = [i * 3 for i in data if i > 10]
	print(result) # [60, 45, 33]

	# NOT SO GOOD (MOST OF THE TIME)
	data = [7, 20, 3, 15, 11]
	result = []
	for i in data:
		if i > 10:
			result.append(i * 3)
			print(result) # [60, 45, 33]
## 9. Create dict from keys and values using zip(尽可能使用zip()函数创建字典)
	d = dict(zip(keys, values))
#### Example
	# GOOD
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
					'Thomas': 'Engine'}
## 10. And the rest … !
	● while True:
	break # This will spark discussion!!!

	● Generators and generator expressions.

	● Avoid from module import *
	Prefer: import numpy as np; import pandas as pd

	● Use _ for “throwaway” variables e.g.:
	for k, _ in [('a', 1), ('b', 2), ('c', 3)]

	● dict.get() and dict.setdefault()

	● collections.defaultdict

	● Sort lists using l.sort(key=key_func)