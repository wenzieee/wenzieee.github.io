---
title: Python中的流程控制语句
---

# Python中的流程控制语句

## Python 条件语句

### if 语句

Python中if语句的一般形式如下所示：

```python
if condition_1:
    statement_block_1
elif condition_2:
    statement_block_2
else:
    statement_block_3
```

Python 中用 **elif** 代替了 **else if**，所以if语句的关键字为：**if – elif – else**。

**注意：**

1、每个条件后面要使用冒号 **:**，表示接下来是满足条件后要执行的语句块。

2、使用缩进来划分语句块，相同缩进数的语句在一起组成一个语句块。

3、在 Python 中没有 **switch...case** 语句，但在 Python3.10 版本添加了 **match...case**，功能也类似，详见下文。

以下是一个简单的 if 实例：

```python
sex_chromosome=input()
if sex_chromosome=="xx":
    print("girl")
elif sex_chromosome=="xy":
    print("boy")
else:
    print("???")
```

以下为if中常用的操作运算符:

| 操作符 | 描述                     |
| :----- | :----------------------- |
| `<`    | 小于                     |
| `<=`   | 小于或等于               |
| `>`    | 大于                     |
| `>=`   | 大于或等于               |
| `==`   | 等于，比较两个值是否相等 |
| `!=`   | 不等于                   |

if嵌套，在嵌套 if 语句中，可以把 if...elif...else 结构放在另外一个 if...elif...else 结构中。

```python
if 表达式1:
    语句
    if 表达式2:
        语句
    elif 表达式3:
        语句
    else:
        语句
elif 表达式4:
    语句
else:
    语句

```

### match...case

Python 3.10 增加了 **match...case** 的条件判断，不需要再使用一连串的 **if-else** 来判断了。

match 后的对象会依次与 case 后的内容进行匹配，如果匹配成功，则执行匹配到的表达式，否则直接跳过，**_** 可以匹配一切。

语法格式如下：

```python
match subject:
    case <pattern_1>:
        <action_1>
    case <pattern_2>:
        <action_2>
    case <pattern_3>:
        <action_3>
    case _:
        <action_wildcard>
```

**case _:** 类似于 C 和 Java 中的 **default:**，当其他 case 都无法匹配时，匹配这条，保证永远会匹配成功。

```python
def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 418:
            return "I'm a teapot"
        case _:
            return "Something's wrong with the internet"

mystatus=400
print(http_error(mystatus))
```

以上是一个输出 HTTP 状态码的实例，输出结果为：Bad request

一个 case 也可以设置多个匹配条件，条件使用 **｜** 隔开，例如：

```python
    case 401|403|404:
        return "Not allowed"
```

## Python 循环语句

### while 循环

Python 中 while 语句的一般形式：

```python
while 判断条件(condition)：
    执行语句(statements)……
```

在 Python 中没有 do..while 循环。

实例:

```python
num=1
sum=0
while num<=100:
    sum=sum+num
    num=num+1
    
print("1 到 %d 之和为: %d" % (n,sum))
```

**无限循环**

```python
import time
i=0
while True:
    i=i+1
    print(i)
    time.sleep(1)
```

你可以使用 **CTRL+C** 来退出当前的无限循环。

无限循环在服务器上客户端的实时请求非常有用。

**while 循环使用 else 语句**

如果 while 后面的条件语句为 false 时，则执行 else 的语句块。

语法格式如下：

```python
while <expr>:
    <statement(s)>
else:
    <additional_statement(s)>
```

`while...else` 的独特之处在于：**只有当循环完整执行完毕（没有遇到break）时，else块才会执行**。

```python
# 示例1：循环被break中断
num = 1
sum = 0
while num <= 100:
    if num == 50:  # 当num等于50时中断循环
        break
    sum = sum + num
    num = num + 1
else:
    print("循环正常结束，和为:", sum)  # 这行不会执行
print("实际和为:", sum)  # 这行会执行

# 示例2：循环正常结束  
num = 1
sum = 0
while num <= 100:
    sum = sum + num
    num = num + 1
else:
    print("循环正常结束，和为:", sum)  # 这行会执行
```

`while...else` 通常用于**搜索**或**验证**场景:

```python
# 在列表中搜索元素
numbers = [1, 3, 5, 7, 9]
target = 4
i = 0

while i < len(numbers):
    if numbers[i] == target:
        print(f"找到目标值 {target} 在位置 {i}")
        break
    i += 1
else:
    print(f"没有找到目标值 {target}")  # 只有在循环完整执行且没break时才执行

# 验证输入
password = ""
attempts = 0

while attempts < 3:
    password = input("请输入密码: ")
    if password == "secret":
        print("密码正确！")
        break
    attempts += 1
    print(f"密码错误，还剩{3-attempts}次机会")
else:
    print("尝试次数过多，账户已锁定")
```

### for 语句

Python for 循环可以遍历任何可迭代对象，如一个列表或者一个字符串。

for循环的一般格式如下：

```python
for item in iterable:
    # 循环主体
else:
    # 循环结束后执行的代码
```

实例：

```python
for i in range(10):
    print(i)
#打印0到9
```

**break 和 continue 语句及循环中的 else 子句**

**break** 语句可以跳出 for 和 while 的循环体。如果你从 for 或 while 循环中终止，任何对应的循环 else 块将不执行。

**continue** 语句被用来告诉 Python 跳过当前循环块中的剩余语句，然后继续进行下一轮循环。

```python
n = 5
while n > 0:
    n -= 1
    if n == 2:
        break
    print(n)
print('循环结束。')
#输出结果为：
#4
#3
#循环结束。

n = 5
while n > 0:
    n -= 1
    if n == 2:
        continue
    print(n)
print('循环结束。')
#输出结果为：
#4
#3
#1
#0
#循环结束。
```

循环语句可以有 else 子句，它在穷尽列表(以for循环)或条件变为 false (以while循环)导致循环终止时被执行，但循环被 break 终止时不执行。

```python
for n in range(2,10):
    for x in range(2,n):
        if n%x==0:
            print(n,"等于",x,"*",n//x)
            break

    else:
        print(n,"是质数")
```

**pass 语句**

`pass` 是 Python 中的一个特殊语句，它被称为 **"空操作"语句**或 **"占位"语句**。它的主要特点是：**什么都不做**。

| 特性         | 说明                         |
| :----------- | :--------------------------- |
| **作用**     | 空操作，什么都不做           |
| **主要用途** | 语法占位符                   |
| **使用场景** | 空函数、空类、待实现的代码块 |
| **语法要求** | 满足Python的语法完整性       |
| **性能**     | 几乎零开销                   |

```python
#pass vs ...（省略号）
# 两者都可以作为占位符
def func1():
    pass

def func2():
    ...

# 但语义略有不同：
# - pass: 明确表示"这里故意留空"
# - ...:  表示"这里暂时省略，以后补充"
```



### **range() 函数**

`range()` 是 Python 中非常常用且强大的内置函数，用于生成一个不可变的整数序列。

基本语法：

```python
range(stop)
range(start, stop[, step])
```

- `start`：序列的起始值（包含），默认为 0
- `stop`：序列的结束值（不包含）
- `step`：步长，默认为 1

```python
#1.只有一个参数（stop）
# 生成 0 到 4 的整数
r = range(5)
print(list(r))  # 输出: [0, 1, 2, 3, 4]

#2. 两个参数（start, stop）
# 生成 2 到 6 的整数
r = range(2, 7)
print(list(r))  # 输出: [2, 3, 4, 5, 6]

#3. 三个参数（start, stop, step）
# 生成 1 到 9 的奇数
r = range(1, 10, 2)
print(list(r))  # 输出: [1, 3, 5, 7, 9]

# 生成 10 到 1 的递减序列
r = range(10, 0, -1)
print(list(r))  # 输出: [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

# 步长为负数，从大到小
r = range(5, -1, -1)
print(list(r))  # 输出: [5, 4, 3, 2, 1, 0]
```

`range()`支持索引和切片

```python
r = range(10, 21)  # 10到20
print(r[0])        # 输出: 10
print(r[5])        # 输出: 15
print(r[-1])       # 输出: 20

# 切片操作
sliced = r[2:6]    # 从第2个到第5个元素
print(list(sliced)) # 输出: [12, 13, 14, 15]
```

**常见应用场景**

1. for 循环迭代

```python
# 重复执行指定次数
for i in range(5):
    print(f"第 {i+1} 次循环")

# 遍历列表索引
fruits = ['apple', 'banana', 'cherry']
for i in range(len(fruits)):
    print(f"索引 {i}: {fruits[i]}")
```

2. 创建列表

```python
# 生成数字列表
numbers = list(range(1, 6))
print(numbers)  # 输出: [1, 2, 3, 4, 5]

# 生成偶数列表
evens = list(range(0, 11, 2))
print(evens)    # 输出: [0, 2, 4, 6, 8, 10]
```

3.数学运算

```python
# 计算 1 到 100 的和
total = sum(range(1, 101))
print(total)  # 输出: 5050

# 计算阶乘
def factorial(n):
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result

print(factorial(5))  # 输出: 120
```

4.生成复杂序列

```python
# 生成平方数序列
squares = [x**2 for x in range(1, 6)]
print(squares)  # 输出: [1, 4, 9, 16, 25]

# 生成时间序列（每15分钟）
time_slots = [f"{h:02d}:{m:02d}" for h in range(24) for m in range(0, 60, 15)]
print(time_slots[:5])  # 输出: ['00:00', '00:15', '00:30', '00:45', '01:00']
```

