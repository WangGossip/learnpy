[toc]

# Python解释器

参考资料：[Python解释器 - 廖雪峰的官方网站 (liaoxuefeng.com)](https://www.liaoxuefeng.com/wiki/1016959663602400/1016966024263840)

## CPython

这是官方解释器，用C语言开发。

## IPython

相比于CPython交互方式有所增强，功能一样，提示符不同。

## PyPy

采用JIT技术，动态编译Python，执行速度显著提高。

## Jython

运行在Java平台的Python解释器，可以将Python代码变异成Java字节码执行。

## IronPython

类似Jython，是运行在微软的.Net平台的解释器。

## 小结

最好的办法还是使用CPython

# 数据类型和变量

能够直接处理的数据有以下几种：

## 整数

`1`, `100`, `-8000`

十六进制：`0xff00`,`0xa5b4c3d2`

可以使用 `_`作为分隔符：`10_000_000_000`

## 浮点数

较大or较小，必须用科学计数法

`1.23e9`

## 字符串

使用单引号 `'`或双引号 `"`括起来的任意文本，可使用转义符 `\`来代表字符本身

例如：

```python
'I \'m \"OK\"!'
```

实际内容为：

```bash
I'm "OK"!
```

转义符也可转义很多其他字符，也可以使用 `r''`表示字符串内部默认不转义

```python
>>> print('\\\t\\')
\       \
>>> print(r'\\\t\\')
\\\t\\
```

为了简化出现多个换行符，Python允许使用 `'''...'''`格式表示多行内容，其中 `...`是命令行的提示符，非代码部分

```python
>>> print('''line1
... line2
... line3''')
line1
line2
line3

```

多行字符串前面也可以加 `r`使用

## 布尔值

与布尔代数表示完全一致，只有 `True`和 `False`两种值，可直接表示或计算出来

### 运算

可以使用 `and` 、`or`、 `not`运算

## 空值

特殊的值，使用 `None`表示，但是不能理解为0

## 变量

动态的

## 常量

常用全部大写的变量名作为常量，实际Python没有机制保证这样的变量不会被改变

# 字符串和编码

## 字符编码

`ASCII`码：1字节

`Unicode`编码：通常2字节

`UTF-8`可变长的编码，把一个Unicode字符编码成1-6字节，英文1，汉字3，生僻字符4-6

## Python字符串

`ord()`获取字符的整数表示，`chr()`将编码转换为字符

```python
>>> ord('A')
65
>>> ord('中')
20013
>>> chr(66)
'B'
>>> chr(25991)
'文'
```

也可用16进制写字符串

```python
>>> '\u4e2d\u6587'
'中文'
```

Python在内存中用Unicode表示字符串，如果要传输或保存，要改成以字节为单位的 `bytes`，用带 `b`的前缀表示

`x=b'ABC'`

Unicode格式的字符串可以重新编码为指定的类型，用 `encode`

反之，bytes类型也可以解码为指定格式，用 `decode`，若有无法解码的字节会报错

若只有一部分无效，用 `erros='ingnore'`忽略错误

`len()`函数计算长度，如str的字符数或者是bytes的字节数

Python源代码如果包含中文，保存源码时要保存为UTF-8编码，所以荣昌在文件开头写下如下两行：

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```

第一行说明解释器位置，第二行告诉Python解释器要使用什么编码来读取

要注意.py文件本身也使用了UTF-8 without BOM

## 格式化

格式化方法和C语言保持一致

| 符号 | 内容         |
| ---- | ------------ |
| %d   | 整数         |
| %f   | 浮点数       |
| %s   | 字符串       |
| %x   | 十六进制整数 |

`%s`永远有用，`%%`用来转义

### format()

稍麻烦一些

### f-string

使用 `f`开头的字符串，如果其中包括 `{xxx}`会自动替换变量

```python
>>> r = 2.5
>>> s = 3.14 * r ** 2
>>> print(f'The area of a circle with radius {r} is {s:.2f}')
The area of a circle with radius 2.5 is 19.62
```

# 使用list和tuple

## list

列表，可随时添加或删除其中的元素，索引从0开始

索引可以用负数，从列表尾部计数

list可追加元素到末尾，也可在指定位置插入

删除元素，使用 `pop()`删末尾，`pop(i)`删除索引i的元素

list中数据类型也可不同

## tuple

元组，一旦初始化不可修改，实际是tuple指向不变

# 条件循环

## 条件判断

`if`

# 循环

`range()`

## break

## continue


# 使用dict和set

## dict

内置了字典，在其他语言中称之为map，用键-值对存储

数据可初始化指定，也可以通过key放入

可用 `in`判断key是否已经存在；或用 `get()`方法看返回值（`None`在命令行不会显示）

用 `pop(key)`删除键值对

## set

集合

类似dict，是一组key的组合，但是不存储value，其中没有重复的key

`add(key)`可添加元素，重复添加无效

`remove(key)`可删除元素

不能放入可变元素

## 关于不可变对象

# 函数

## 调用函数

### 数据类型转换

`int()`

## 定义函数

### 空函数

使用 `pass`

### 多个返回值

实际上返回的是一个tuple，语法上可以省略括号

## 函数的参数

### 位置参数

### 默认参数

***默认参数必须指向不变对象***

### 可变参数

形式如 `*nums`

### 关键字参数

形式： `**kw`，可扩展函数功能

### 关键字参数

可以限制仅接收某些作为关键字参数

```python
def person(name, age, *, city, job):
    print(name, age, city, job)

def person(name, age, *args, city, job):
    print(name, age, args, city, job)
```

### 参数组合

对于任意函数，都可以通过类似 `func(*args, **kw)`的形式调用它，无论它的参数是如何定义的。

## 递归函数
