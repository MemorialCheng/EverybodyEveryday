《Python编程从入门到实践》学习笔记，每天坚持python编程学习ing...
# Updated 20200420 变量和简单数据类型
## 变量的命名规则
1. ☆ 变量名只能包含字母、数字和下划线。变量名可以字母或下划线开头，但不能数字开头。
2. ☆ 变量名不能包含空格，可使用下划线来分隔其中的单词。如，greeting_message.
3. ☆ 不要将Python关键字和函数名作为变量名。如，print,详见下图。
4. 变量名应既简短又具有描述性。如，student_name.
5. 慎用小写字母l和大写字母O，因为他们很容易被人错看成数字1和0.

### 动手试一试
No.1 将一条消息存储再变量中，将其打印出来；再将变量的值修改为一条新消息，并打印出来。
```python
example_message = "Hello, world! "
print(example_message)
example_message = "I like python, I'll study it well.And I will be devoted to AI,ML,DL."
print(example_message)
```
