《Python编程从入门到实践》学习笔记，每天坚持python编程学习ing...
# Updated 20200420 变量和简单数据类型
## 变量的命名规则
1. ☆ 变量名只能包含字母、数字和下划线。变量名可以字母或下划线开头，但不能数字开头。
2. ☆ 变量名不能包含空格，可使用下划线来分隔其中的单词。如，greeting_message.
3. ☆ 不要将Python关键字和函数名作为变量名。如，print,详见下图。
4. 变量名应既简短又具有描述性。如，student_name.
5. 慎用小写字母l和大写字母O，因为他们很容易被人错看成数字1和0.
<img src="https://github.com/MemorialCheng/EverybodyEveryday/blob/master/Python/python_images/python关键字.png" width = "500">

### 动手试一试
No.1 将一条消息存储再变量中，将其打印出来；再将变量的值修改为一条新消息，并打印出来。
```python
example_message = "Hello, world! "
print(example_message)
example_message = "I like python, I'll study it well.And I will be devoted to AI,ML,DL."
print(example_message)
```
## 字符串
字符串就是一系列字符。在Python中，用引号括起来的都是字符串，其中引号可以是单引号，也可以是双引号。
### 常见字符串操作方法
1. string.title()    将每个单词的首字母改为大写;
2. string.upper()    将字符串改为全部大写;
3. string.lower()    将字符串改为全部小写;
4. string.isalpha()  判断字符串是否全部由字母组成，是返回True，否返回False;
5. string.isdigit()  判断字符串是否全部由数字组成,是返回True，否返回False;
6. string.isalnum()  判断字符串是否全部由数字或者字母组成,是返回True，否返回False;

**注意：上面存在空格也会False**
7. string.find('str')  从左往右找第一个对应'str'的值，显示的是正向索引，如果没找到匹配的值返回-1
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
8. string.rfind('str')  从右往左找第一个对应的值，显示的是正向索引,如果没找到匹配的值返回-1



