《Python编程从入门到实践》学习笔记，每天坚持python编程学习ing...
本文记录的是自己学习笔记，以及一些小结，不代表python完整知识体系，与君共勉。
# 第2章 变量和简单数据类型
## 2.1 变量的命名规则
1. ☆ 变量名只能包含字母、数字和下划线。变量名可以字母或下划线开头，但不能数字开头。
2. ☆ 变量名不能包含空格，可使用下划线来分隔其中的单词。如，greeting_message.
3. ☆ 不要将Python关键字和函数名作为变量名。如，print,详见下图。
4. 变量名应既简短又具有描述性。如，student_name.
5. 慎用小写字母l和大写字母O，因为他们很容易被人错看成数字1和0.
<img src="https://github.com/MemorialCheng/EverybodyEveryday/blob/master/Python/python_images/python关键字.png" width = "500">

### 动手试一试
No.1 将一条消息存储在变量中，将其打印出来；再将变量的值修改为一条新消息，并打印出来。
```python
example_message = "Hello, world! "
print(example_message)
example_message = "I like python, I'll study it well.And I will be devoted to AI,ML,DL."
print(example_message)
```
## 2.2 字符串
字符串就是一系列字符。在Python中，用引号括起来的都是字符串，其中引号可以是单引号，也可以是双引号。
### 常见字符串操作方法
1. string.title()    将每个单词的首字母改为大写，有数字不会报错;
2. string.upper()    将字符串改为全部大写;
3. string.lower()    将字符串改为全部小写;
4. string.isalpha()  判断字符串是否全部由字母组成，是返回True，否返回False;
5. string.isdigit()  判断字符串是否全部由数字组成,是返回True，否返回False;
6. string.isalnum()  判断字符串是否全部由数字或者字母组成,是返回True，否返回False;
7. string.isspace()  判断字符串是否全部由空格组成，是返回True，否返回False;
**注意：上面存在空格也会False**
8. string.find('str')  从左往右找第一个对应'str'的值，显示的是正向索引，如果没找到匹配的值返回-1;
如，
```python
例1
string = 'babc abd abcb'
res = string.find('bc')
print(res)
结果输出：2

例2
res = string.find('bc',8,13)
print(res)
结果输出：10
```
9. string.rfind('str')        从右往左找第一个对应的值，显示的是正向索引,如果没找到匹配的值返回-1;
10. string.index('str')        从左往右找第一个对应的值，显示的是正向索引，如果没找到匹配的值报错;
11. string.count('str')       显示字符个数，如果没有显示0;
12. string.startswith('str')  判断字符串是否以所选字符开头，是返回True，否返回False;
13. string.endswith('str')    判断字符串是否以所选字段结尾，是返回True，否返回False;
14. string.isspace('str')     判断是否是由空格组成，是返回True，否返回False;
15. string.strip()   删除两边空格;
16. string.lstrip()  删除左边空格;
17. string.rstrip()  删除右边空格;
18. string.center(width, 'str')  居中，width字符串长度，str填充字符，默认空格填充；
19. string.ljust(width, 'str')   左对齐;
20. string.rjust(width, 'str')   右对齐;
```python
>>>str = 'runoob'
>>> str.center(20, '*')
'*******runoob*******'
>>> str.center(20)
'       runoob       '
```
21. string.capitalize()    将字符串首个字符变为大写;
22. string.count('str')    统计字符出现的次数;
23. string.isidentifier()  判断是否是一个合法的变标识符，即是否符合变量命名规则;
24. string.islower()       判断字符串是否全部是小写,是返回True，否返回False;
25. string.isupper()       判断字符串是否全部为大写,是返回True，否返回False;

*** pycharm快捷键：ctrl + d:复制一行；ctrl + ?:快速注释一行|撤销 ***

### format() 格式化字符串

# 第3章 列表
列表是由一系列按特定顺序排列的元素组成。用方括号[]表示列表，用逗号分隔元素。
print(列表)，输出结果是带中括号的。
## 3.1 访问列表
### 3.1.1 根据索引访问单个元素
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[1])

# 输出结果(没有方括号和引号):
cannondale
```
此时输出了字符串cannondale，还可以利用第二章学到的对字符串操作：
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[1].title())  # 每个单词首字母大写

# 输出结果(没有方括号和引号)
Cannondale
```

__特别解析__
支持负数索引，-1最后一位，-2倒数第二位......
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[-1])

# 输出结果(没有方括号和引号)
specialized
```

### 3.1.2 根据切片访问多个元素
此时返回值仍然是列表。左闭右开区间
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[0:2])

# 输出结果
['trek', 'cannondale']
```

## 3.2 增、删、改列表
### 3.2.1 添加列表元素
（一）在列表末尾添加元素——append()方法

append()方法只能在列表末尾添加单个元素。
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
addbicy = 'haluo'
bicycles.append(addbicy)
print(bicycles)

# 输出结果
['trek', 'cannondale', 'redline', 'specialized', 'haluo']
```
（二）在列表末尾添加元素——extend()方法

extend()方法可以在列表末尾添加多个元素，可以理解为两个列表合并。
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
addbicy = ['haluo','mobai']
bicycles.extend(['haluo','mobai'])
print(bicycles)

# 输出结果
['trek', 'cannondale', 'redline', 'specialized', 'haluo', 'mobai']
```
__特别解析:__
extend()方法通过在列表末尾追加可迭代对象中的元素来扩展列表。可迭代对象包括字符串、列表、元祖、字典。
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
bicycles.extend('haluo')
print(bicycles)

# 输出结果
['trek', 'cannondale', 'redline', 'specialized', 'h', 'a', 'l', 'u', 'o']

# 因为这里是将字符串'haluo'视为一个可迭代对象进行处理的。
```
（三）在列表中插入元素——insert()方法
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
bicycles.insert(1,'haluo')
print(bicycles)

# 输出结果
['trek', 'haluo', 'cannondale', 'redline', 'specialized']
```
### 3.2.2 删除列表元素
（一）使用del语句删除列表元素
del语句结合索引可以删除指定位置的元素； 如果不指定索引，将删除整个列表。
del语句删除元素，没有返回值，但会删除原列表的元素。
```python
bicycles = ['trek', 'haluo', 'cannondale', 'redline', 'specialized']
del bicycles[1]
print(bicycles)

# 输出结果
['trek', 'cannondale', 'redline', 'specialized']
```

（二）使用pop()方法删除列表元素
pop()方法删除列表元素返回值为被删除的元素。括号中不输入索引值，则默认删除最后一个，也可指定索引删除。
```py
bicycles = ['trek', 'haluo', 'cannondale', 'redline', 'specialized']
bic = bicycles.pop()
print(bicycles)
print(bic)

# 输出结果
['trek', 'haluo', 'cannondale', 'redline']
specialized
```
__特别解析:__
删除列表元素如何选择使用del语句还是pop()方法？
答：如果你要从列表中删除一个元素，且不再以任何方式使用这个元素时，使用del语句；
如果你要在删除元素后继续使用这个元素，就使用pop()方法。

（三）根据元素值删除列表元素——remove()方法
remove()方法如果成功删除值则返回None;如果列表没有该值则报错list.remove(x): x not in list

```py
bicycles = ['trek', 'haluo', 'cannondale', 'redline', 'specialized']
bic = bicycles.remove('haluo')
print(bicycles)
print(bic)

# 输出结果
['trek', 'cannondale', 'redline', 'specialized']
None
```
__特别解析:__
remove()方法只删除第一个指定的值，如果要删除的值在列表中多次出现，需要使用循环来判断是否删除了所有这样的值。


### 3.2.3 修改列表
用索引指定要修改的元素，然后直接赋值。
```py
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
bicycles[2] = 'red'
print(bicycles)

# 输出结果
['trek', 'cannondale', 'red', 'specialized']
```
__也可多个元素一起修改__
```py
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
bicycles[0:2] = ['tr','ca']
print(bicycles)

# 输出结果
['tr', 'ca', 'redline', 'specialized']
```
## 3.3 组织列表
Python提供了很多组织（排序）列表的方法
### 3.3.1 对列表进行永久性排序——方法sort()
默认正序，如果需要倒序，向sort()方法传递参数 reverse=True.
sort()排序后原来的排列顺序无法恢复。
__格式：__
列表名称.sort()

```py
# 正序
cars = ['bmw', 'audi', 'toyota', 'subaru','abdi','12345','ABDI','AB!#','!#']
cars.sort(reverse=True)
print(cars)

# 输出结果:
['!#', '12345', 'AB!#', 'ABDI', 'abdi', 'audi', 'bmw', 'subaru', 'toyota']
```
```py
# 倒序
cars = ['bmw', 'audi', 'toyota', 'subaru','abdi','12345','ABDI','AB!#','!#']
cars.sort(reverse=True)
print(cars)

# 输出结果:
['toyota', 'subaru', 'bmw', 'audi', 'abdi', 'ABDI', 'AB!#', '12345', '!#']
```

__特别解析__
排序优先级：特殊字符 > 数字 > 大写字母 > 小写字母

### 3.3.2 对列表进行临时性排序——函数sorted()
默认正序，如果需要按相反顺序排列，需向sorted()函数传递参数 reverse=True.
__格式：__
sorted(列表名称)

```python
# 正序
oldcars = ['bmw', 'audi', 'toyota', 'subaru','abdi','12345','ABDI','AB!#','!#']
newcars = sorted(cars)
print(oldcars)
print(newcars)

# 输出结果
['bmw', 'audi', 'toyota', 'subaru', 'abdi', '12345', 'ABDI', 'AB!#', '!#']
['!#', '12345', 'AB!#', 'ABDI', 'abdi', 'audi', 'bmw', 'subaru', 'toyota']
```
```python
# 倒序
oldcars = ['bmw', 'audi', 'toyota', 'subaru','abdi','12345','ABDI','AB!#','!#']
newcars = sorted(cars,reverse=True)
print(oldcars)
print(newcars)

# 输出结果
['bmw', 'audi', 'toyota', 'subaru', 'abdi', '12345', 'ABDI', 'AB!#', '!#']
['toyota', 'subaru', 'bmw', 'audi', 'abdi', 'ABDI', 'AB!#', '12345', '!#']
```

### 3.3.3 反转列表顺序——方法reverse()
方法reverse()指的是反转列表元素的排列顺序，并且是永久性修改列表元素顺序。
__格式：__
列表名称.reverse()

```python
cars = ['bmw', 'audi', 'toyota', 'subaru','abdi']
cars.reverse()
print(cars)

# 输出结果
['abdi', 'subaru', 'toyota', 'audi', 'bmw']
```

__特别解析__
1. 方法的使用格式是：对象名称.方法();
2. 函数的使用格式是：对象名称.函数();
3. 函数len()可求列表的长度，返回元素个数。






