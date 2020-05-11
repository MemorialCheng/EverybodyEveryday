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
### 常见字符串操作方法（以下对字符串的更新操作都是临时性的，不会改变原来字符串）
1. string.title()    将每个单词的首字母改为大写，有数字不会报错;
2. string.capitalize()  将字符串首个字符改为大写;
3. string.upper()    将字符串改为全部大写;
4. string.lower()    将字符串改为全部小写;
5. string.isalpha()  判断字符串是否全部由字母组成，是返回True，否返回False;
6. string.isdigit()  判断字符串是否全部由数字组成,是返回True，否返回False;
7. string.isalnum()  判断字符串是否全部由数字或者字母组成,是返回True，否返回False;
8. string.isspace()  判断字符串是否全部由空格组成，是返回True，否返回False;

**注意：上面判断组成的方法，字符串存在空格也会返回False**

9. string.islower()  判断字符串中字母是否全部是小写,是返回True，否返回False;
10. string.isupper()  判断字符串中字母是否全部为大写,是返回True，否返回False;

**注意：islower()和isupper()，判断的仅仅是字符串中的字母，如果存在空格、特殊字符等不影响返回结果**

11. string.isidentifier()     判断是否是一个合法的变标识符，即是否符合变量命名规则;
12. string.startswith('str')  判断字符串是否以所选字符开头，是返回True，否返回False;
13. string.endswith('str')    判断字符串是否以所选字段结尾，是返回True，否返回False;
14. string.find('str')  从左往右找第一个对应'str'的值，显示的是正向索引，**如果没找到匹配的值返回-1**;
如，
```python
# 例1
string = 'babc abd abcb'
res = string.find('bc')
print(res)
# 结果输出：
2

# 例2
res = string.find('bc',8,13)
print(res)
# 结果输出：
10
```
15. string.rfind('str')       从右往左找第一个对应的值，显示的是正向索引,如果没找到匹配的值返回-1;
16. string.index('str')       从左往右找第一个对应的值，显示的是正向索引，**如果没找到匹配的值报错**;
17. string.count('str')       显示字符个数，如果没有显示0;

18. string.strip()     删除两边空格;
19. string.lstrip()    删除左边空格;
20. string.rstrip()    删除右边空格;
21. string.center(width, 'str')  居中，width字符串长度，str填充字符，默认空格填充；
22. string.ljust(width, 'str')   左对齐;
23. string.rjust(width, 'str')   右对齐;
```python
str = 'runoob'
str.center(20, '*')
'*******runoob*******'
str.center(20)
'       runoob       '
```

***pycharm快捷键：ctrl + d:复制一行；ctrl + ?:快速注释一行|撤销 ***

### format() 格式化字符串

# 第3章 列表简介
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
**（一）在列表末尾添加元素——append()方法**

append()方法只能在列表末尾添加单个元素。
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
addbicy = 'haluo'
bicycles.append(addbicy)
print(bicycles)

# 输出结果
['trek', 'cannondale', 'redline', 'specialized', 'haluo']
```
**（二）在列表末尾添加元素——extend()方法**

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
**（三）在列表中插入元素——insert()方法**
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
bicycles.insert(1,'haluo')
print(bicycles)

# 输出结果
['trek', 'haluo', 'cannondale', 'redline', 'specialized']
```
### 3.2.2 删除列表元素
**（一）使用del语句删除列表元素**
del语句结合索引可以删除指定位置的元素； 如果不指定索引，将删除整个列表。
del语句删除元素，没有返回值，但会删除原列表的元素。
```python
bicycles = ['trek', 'haluo', 'cannondale', 'redline', 'specialized']
del bicycles[1]
print(bicycles)

# 输出结果
['trek', 'cannondale', 'redline', 'specialized']
```

**（二）使用pop()方法删除列表元素**
pop()方法删除列表元素返回值为被删除的元素（称为“弹出”）。括号中不输入索引值，则默认删除最后一个，也可指定索引删除。
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

**（三）根据元素值删除列表元素——remove()方法**
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
**remove()方法删除所有相同的值有坑（由于删除元素后列表自动收缩，1. 每一次删除一个元素，列表的长度就会发生变化，越界坑；2. 元素的索引也会发生变化，漏删坑），要注意回避，具体后面单独出文章进行分析**
```py
# 删除列表中为1的元素
# 越界坑
nums = [1,5,3,1,1,3]
for i in range(len(nums)):
     if nums[i]==1:
          nums.remove(1)
print(nums)
# 输出报错：
IndexError: list index out of range


# for循环漏删坑
nums = [1,5,3,1,1,3]
for num in nums:
     if num == 1:
          nums.remove(num)
print(nums)
# 输出结果
[5, 3, 1, 3]
# 输出报错：
IndexError: list index out of range


# 正确写法1 ，利用for循环+range从后往前遍历
nums = [1,5,3,1,1,3]
for i in range(len(nums)-1,-1,-1):
     if nums[i]==1:
          nums.remove(1)
print(nums)
# 输出结果
[5, 3, 3]

# 正确写法2 ，利用while循环。
nums = [1,5,3,1,1,3]
while 1 in nums:
     nums.remove(1)
print(nums)
# 输出结果
[5, 3, 3]

# 正确写法3 ，利用列表解析式.（还有别的实现方法这里不列举了）
nums = [1,5,3,1,1,3]
nums = [num[i]  for i in range(0, len(nums)) if nums[i] != 1]
print(nums)
# 输出结果
[5, 3, 3]
```


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
函数sorted()排序后原来的排列顺序不变，临时性的。
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
方法reverse()指的是反转列表元素的排列顺序，并且是**永久性**修改列表元素顺序。
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
2. 函数的使用格式是：函数(对象名称);
3. 函数len()可求列表的长度，返回元素个数。



# 第4章 操作列表
## 4.1 遍历整个列表

我们经常需要遍历列表的所有元素，对每个元素执行相同的操作。可以使用for循环。
**格式：**
for item in list_of_items:
    操作语句

```py
dogs = ['藏獒', '哈士奇','秋田犬','柴犬']
for dog in dogs:
    print('这是一条' + dog.title())
      
# 输出结果
这是一条藏獒
这是一条哈士奇
这是一条秋田犬
这是一条柴犬
```
## 4.2 创建数值列表
### 4.2.1 使用range()函数创建数字列表
range()函数可创建一个整数列表，一般用在 for 循环中。

**语法**

range(start, stop, step)

参数说明：

start: 计数从 start 开始。默认是从 0 开始。例如range（5）等价于range（0， 5）;

stop: 计数到 stop 结束，但不包括 stop。例如：range（0， 5） 是[0, 1, 2, 3, 4]没有5；

step：步长，默认为1。例如：range（0， 5） 等价于 range(0, 5, 1)；

左闭右开！！！
<br>
```py
for value in range(5):
    print(value)

# 输出结果
0
1
2
3
4
```
**使用函数list()将range()的结果直接转换成列表**
```py
numbers = list(range(1,6))
print(numbers)

# 输出结果
[1, 2, 3, 4, 5]
```
### 4.2.2 对数字列表执行简单的统计计算
min()最小值函数，max()最大值函数，sum()求和函数。
```py
numbers = list(0,10)
minNum = min(numbers)
maxNum = max(numbers)
sumNum = sum(numbers)
print(minNum,maxNum,sumNum)

# 输出结果
0 9 45
```
### 4.2.3 列表解析/列表生成式
**语法**

法1： [expression for iter_val in iterable]

法2： [expression for iter_val in iterable if cond_expr]

**例1. 要求：列出1~10所有数字的平方**
```py
# 1、普通方法：
squares = []
for value in range(1,11):
    squares.append(value**2)
print(squares)
# 输出结果
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

####################################################

# 2、列表解析：
squares = [value**2 for value in range(1,11)]
print(squares)
# 输出结果
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
**例2. 要求：列出1~10中小于等于2，大于等于4的数字的平方**
```py
# 1、普通方法：
squares = []
for value in range(1,11):
    if value <= 2 or value >= 4 :
        squares.append(value**2)
print(squares)
# 输出结果
[1, 4, 16, 25, 36, 49, 64, 81, 100]

####################################################

# 2、列表解析
squares = [value ** 2 for value in range(1,11) if value <= 2 or value >= 4]
print(squares)
# 输出结果
[1, 4, 16, 25, 36, 49, 64, 81, 100]
```
**例3. 要求：实现两个列表中的元素逐一配对**
```py
# 1、普通方法:
L1 = ['x','y','z']
L2 = [1,2,3]      
L3 = []
for a in L1:
    for b in L2:
        L3.append((a,b))
print(L3)
# 输出结果
[('x', 1), ('x', 2), ('x', 3), ('y', 1), ('y', 2), ('y', 3), ('z', 1), ('z', 2), ('z', 3)]

####################################################

# 2、列表解析:
L1 = ['x','y','z']
L2 = [1,2,3]  
L3 = [(a, b) for a in L1 for b in L2]
print(L3)
# 输出结果
[('x', 1), ('x', 2), ('x', 3), ('y', 1), ('y', 2), ('y', 3), ('z', 1), ('z', 2), ('z', 3)]
```
## 4.3 切片
可用于访问列表的部分元素。

**注：取的是列表索引，左闭右开，支持负数索引。返回值仍然是列表**

推荐参考博客https://www.jianshu.com/p/15715d6f4dad ，博客介绍很清晰，这里不再赘述。

**切片操作基本表达式：object[start_index:end_index:step]**
### 切片小结
（一）start_index、end_index、step三者可同为正、同为负，或正负混合。但必须遵循一个原则，即：当start_index表示的实际位置在end_index的左边时，从左往右取值，此时step必须是正数（同样表示从左往右）；当start_index表示的实际位置在end_index的右边时，表示从右往左取值，此时step必须是负数（同样表示从右往左），即两者的取值顺序必须相同。

（二）当start_index或end_index省略时，取值的起始索引和终止索引由step的正负来决定，这种情况不会有取值方向矛盾（即不会返回空列表[]），但正和负取到的结果顺序是相反的，因为一个向左一个向右。

（三）step的正负是必须要考虑的，尤其是当step省略时。比如a[-1:]，很容易就误认为是从“终点”开始一直取到“起点”，即a[-1:]= [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]，但实际上a[-1:]=[9]（注意不是9），原因在于step省略时step=1表示从左往右取值，而起始索引start_index=-1本身就是对象的最右边元素了，再往右已经没数据了，因此结果只含有9一个元素。

## 4.4 元组(tuple)

Python的元组与列表类似，不同之处在于**元组的元素不能修改。**

元组使用小括号，列表使用方括号。

元组创建很简单，只需要在括号中添加元素，并使用逗号隔开即可。
```py
# 示例
tup1 = ('physics', 'chemistry', 1997, 2000)
tup2 = (1, 2, 3, 4, 5 )
```
元组中只包含一个元素时，需要在元素后面添加逗号
```py
tup1 = (50,)
```
### 4.4.1 访问元组
使用索引访问其元素
```py
dimensions = (200, 50)
print(dimensions[0])
print(dimensions[1])

# 输出结果
200
50
```
### 4.4.2 修改元组
元组的元素不能修改！！！
```py
# 错误示例
dimensions = (200, 50)
dimensions[0] = 250
报错
TypeError: 'tuple' object does not support item assignment
```
**可对元组进行连接组合**
```py
tup1 = (12, 34.56)
tup2 = ('abc', 'xyz')
tup3 = tup1 + tup2
print(tup3)

# 输出结果
(12, 34.56, 'abc', 'xyz')
```
**可对元组进行重新赋值**
```py
dimensions = (200, 50)
print("Original dimensions:")
for dimension in dimensions:
    print(dimension)

#  重新赋值
dimensions = (400, 100)
print("\nModified dimensions:")
for dimension in dimensions:
    print(dimension)
```
### 4.4.3 删除元组——del语句
元组中的元素不能删除，但可使用del语句删除真个元组。
```py
tup = (12, 34.56)
del tup
```
# 第5章 if语句
## 5.1 条件测试
每条if语句的核心都是一个值为True或False的表达式，这种表达式被称为**条件测试**。
### 5.1.1 检查是否相等(==)
双等号两边的值相等，返回True;不等则返回False.
```py
# 例1
car = 'bmw'
car == 'bmw'
# 输出结果
True
===============================
# 例1
car = 'audi'
car == 'bmw'
# 输出结果
False
```
**特别解析：**
1. 一个等号(=)，表示赋值，解读为“将变量car的值设置为audi”;
2. 两个等号(==),表示判断，检查两边值是否相等；
3. 双等号判断两边是否相等时严格区分大小写;
```py
# 大小写不同将返回False
car = 'Audi'
car == 'audi'
# 输出结果
False
```
4. 若只想检查变量的值，不考虑大小写，可将变量的值先转换为小写，再进行比较。
```py
car = 'Audi'
car.lower() == 'audi'
# 输出结果
True
```
### 5.1.2 检查是否不相等(!=)
```py
answer = 17
if answer != 42:
    print('That is not the correct answer, please try again!')
```
**特别解析**
数字的比较，还有大于 > ，大于等于 >= ，小于 < ，小于不等于 <=

### 5.1.3 检查多个条件
**（一）且的关系用and**

多个条件同时满足才返回True!
```py
age = 20
sex = 'man'
if age >= 18 and sex == 'man':
    print("You're a grown man.")
    
# 输出结果
You're a grown man.
```
**（二）或的关系用or**

多个条件只要有一个满足即返回True!
```py
phone = 'huawei'
if phone == 'huawei' or phone == 'xiaomi':
    print("This is a Mobile phone.")
    
# 输出结果
This is a Mobile phone.
```
### 5.1.4 检查特定值在列表中(in)、不在列表中(not in)
```py
# 在列表中返回True
requested_toppings = ['mushrooms', 'onions', 'pineapple']
'mushrooms' in requested_toppings
# 输出结果
True

# 不在列表中返回True
'pepperoni' in requested_toppings
# 输出结果
False
```
```py
banned_users = ['andrew', 'carolina', 'david']
user = 'marie'
if user not in banned_users:
    print(user.title() + ", you can post a response if you wish.")
# 输出结果
Marie, you can post a response if you wish.
```
# 5.2 if语句

很简单，感觉没太多好说的，就举例说明各种if表达式吧。


### 5.2.1 简单的if语句
**注意if后要有冒号： 后面的代码块要缩进**
```py
age = 19
if age >= 18:
    print("You are old enough to vote!")

# 输出结果
You are old enough to vote!
```
### 5.2.2 if-else 语句
**注意if,else后要有冒号： 后面的代码块要缩进**
```py
age = 17
if age >= 18:
    print("You are old enough to vote!")
    print("Have you registered to vote yet?")
else:
    print("Sorry, you are too young to vote.")
    print("Please register to vote as soon as you turn 18!")
    
# 输出结果
Sorry, you are too young to vote.
Please register to vote as soon as you turn 18!
```
### 5.2.3 if-elif-else语句
**注意if,elif,else后要有冒号，后面代码块要缩进**
```py
age = 12
if age < 4:
    price = 0
elif age < 18:
    price = 5
else:
    price = 10
print("Your admission cost is $" + str(price) + ".")

# 输出结果
Your admission cost is $5.
```
### 5.2.4 可以有个elif代码块
```py
age = 12
if age < 4:
    price = 0
elif age < 18:
    price = 5
elif age < 65:
    price = 10
else:
    price = 5
print("Your admission cost is $" + str(price) + ".")

# 输出结果
Your admission cost is $5.
```
### 5.2.5 省略else代码块
else是一条包罗万象的语句，只要不满足任何if或elif中的条件测试，其中的代码就会执行，这可能会引入无效甚至恶意的数据。
如果知道最终要测试的条件，应考虑使用一个elif代码块来代替else代码块。这样，你就可以肯定，仅当满足相应的条件时，你的代码才会执行。
```py
age = 12
if age < 4:
     price = 0
elif age < 18:
     price = 5
elif age < 65:
     price = 10
elif age >= 65:
     price = 5
print("Your admission cost is $" + str(price) + ".")

# 输出结果
Your admission cost is $5.
```
### 5.2.6 测试多个条件
if-elif-else结构功能强大，但仅适合用于只有一个条件满足的情况。有时候我们需要检查多个条件，每个条件为True时都采取相应措施。
这是就使用多个简单的if语句（不包含elif和else).
```py
requested_toppings = ['mushrooms', 'extra cheese']
if 'mushrooms' in requested_toppings:
     print("Adding mushrooms.")
if 'pepperoni' in requested_toppings:
     print("Adding pepperoni.")
if 'extra cheese' in requested_toppings:
     print("Adding extra cheese.")
print("\nFinished making your pizza!")

# 输出结果
Adding mushrooms.
Adding extra cheese.

Finished making your pizza!
```
**特别解析**
如果你只想执行一个代码块，就使用if-elif-else结构；如果要运行多个代码块，就使用一系列独立的if语句。

# 第6章 字典
## 访问字典中的值

