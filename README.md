## Python基础面试题

**1.Python中如何获取字典的所有键**

使用`.keys()`来获取字典的所有键，与此同时还有`.values()`，`.items()`方法，分别用来获取字典的所有值和字典的键值对。如果你想将这些键作为一个列表处理，可以用`list()`函数来转换。

```python
my_dict = {'name': 'Alice', 'age': 25, 'city': 'New York'}
keys = my_dict.keys()
print(keys)  # 输出 dict_keys(['name', 'age', 'city'])

keys_list = list(my_dict.keys())
print(keys_list)  # 输出 ['name', 'age', 'city']
```

> 注意：在Python 3.x中，.key()方法返回的是视图对象，而在Python 2.x中返回的是一个列表。因为返回的是视图对象，并不需要生成新的列表，具有良好的性能

**视图对象(view object)**：

在Python的标准库中，一些数据结构（如列表、元组、字典等）提供了所谓的"视图"，这些视图对象允许你以某种方式观察数据结构的一部分或全部内容。例如`dict.items()`、`dict.keys()` 和 `dict.values()` 返回的是字典的视图对象，它们反映了字典的当前状态，但不是字典本身的副本。这意味着如果你修改了字典，视图对象也会反映这些变化。视图有很多不同场景，这里指的是数据结构视图，还有数据库视图，GUI视图，Web框架中的视图等。

`.keys()`返回的视图对象反映的是字典的动态变化，因为它是一个可以动态反应字典变化的对象，例如：

```python
my_dict = {'name': 'Alice', 'age': 25}
keys = my_dict.keys()
print(keys)  # 输出 dict_keys(['name', 'age'])

my_dict['city'] = 'New York'
print(keys)  # 输出 dict_keys(['name', 'age', 'city'])
```

**2.如何使用Python的random模块生成随机数，实现随机乱序和随机抽样？**

1）生成随机数：导入`random`模块，使用`random.random()`方法生成一个**[0.0, 1.0)**范围内的随机浮点数，使用`random.randint(a, b)`方法生成一个范围在**[a, b]**之间的随机整数。例如:

```python
import random

# 设置种子可以固定答案，方便复现
random.seed(45)
# 生成一个 [0.0, 1.0) 之间的随机浮点数
random_float = random.random()
print(random_float)
# 输出 0.2718754143840908

# 生成一个 [1, 10] 之间的随机整数
random_integer = random.randint(1, 10)
print(random_integer)
# 输出 8
```

2）实现随机乱序：使用`random.shuffle(list1)`对列表list1中的元素进行就地打乱。例如：

```python
import random

my_list = [1, 2, 3, 4, 5]
random.shuffle(my_list)
print(my_list)
# 输出 [5, 1, 2, 4, 3]
```

3）实现随机抽样：使用`random.sample(population, k)`从一个列表population中取k个随机且不重复（不重复不是数值不重复，而是下标不重复）的元素。例如：

```python
import random

my_list = [1, 2, 3, 4, 5]
random_sample = random.sample(my_list, 3)
print(random_sample)
# 输出 [4, 1, 3]
```

**扩展知识**

1）生成指定范围的随机浮点数：前面提到`random.random()`方法生成一个**[0.0, 1.0)**范围内的随机浮点数，此外，`random.uniform(a, b)`方法生成一个范围在**[a, b]**之间的随机浮点数，例如：

```python
import random
random_uniform = random.uniform(1.5, 10.5)
print(random_uniform)
# 输出 3.6830801978825707
```

2）生成指定范围内以n倍步长增加的随机数(n可以为0)：使用`random.randrange(start, end, step)`，例如：

```python
import random
random_range = random.randrange(1, 10, 2)
print(random_range)
# 输出 1 3 5 7 9的其中一个值
```

3）生成随机种子数，以固定接下来随机的结果，方便复现。使用`random.seed(a)`方法为随机数生成器指定种子。例如：

```python
import random
random.seed(42)
print(random.random())
# 输出 0.6394267984578837
print(random.randint(1, 10))
# 输出 1
```

4）生成随机字符，使用`random.choice()`方法搭配`string.ascii_letters`或`string.digits`生成字母或数字，使用`''.join(random.choices(string.ascii_letters + string.digits, k=8))`生成由字母和数字组成的长度为**8**的随机字符串

```python
import random
import string

random_letter = random.choice(string.ascii_letters)
print(random_letter)
# 输出 n

random_string = ''.join(random.choices(string.ascii_letters + string.digits, k=8))
print(random_string)
# 输出 aBp5vASH
```

**3.Python的pass语句有什么作用？**

`pass`语句是一个占位符，它什么都不做。它可以帮助你：

1）代码占位。帮助你在不报错的情况下搭建好代码框架，然后再逐步细化和实现各个部分

2）调试。当你调试代码时，有时希望暂时禁用某些代码块并且不想删除它们，这时可以用`pass`来代替这段代码

3）与控制结构配合。比如在写`if-elif-else`语句时，若还没有决定好某个分支的具体操作，可以用`pass`来代替

4）其他语言对比。如在C，C++，Java中，可以使用一个{}来什么都不做

**4.如何更改Python列表的数据类型？**

Python中的列表是一种灵活且强大的数据结构，列表里的元素类型可能是不同的，一种方式是使用列表推导式（list comprehension）结合类型转换函数来实现这一点。例如：

```python
original_list = [1, 2.5, '3', True]
print(original_list)
# 输出 [1, 2.5, '3', True]
modify_list = [str(item) for item in original_list]
print(modify_list)
# 输出 ['1', '2.5', '3', 'True']
```

**扩展知识**

1）多种类型转换函数。除了`str()`，还有`int()`，`float()`，`bool()`等等类型转换函数

2）错误处理。转换过程可能会遇到一些无法转换的值，可以用`try...except`结构来处理

```
original_list = ['1', 'two', '3.0', True]
def safe_convert_to_int(item):
    try:
        return int(item)
    except Exception as e:
        print(e)
        return None  # 或者其他替换值
int_list = [safe_convert_to_int(item) for item in original_list]
print(int_list)
# 输出 [1, None, None, 1]
```

3）转换类型的潜在问题。比如`True`转换为整数会变成1，而`False`会变成0，浮点数转换成整数只保留整数部分，不会进行四舍五入。

4）使用`map()`函数对列表进行处理。`map()`函数用来对列表中的每个元素应用同一个函数。

```python
original_list = ['1', 'two', 3.0, True]
string_list = list(map(str, original_list))
print(string_list)
# 输出 ['1', 'two', '3.0', 'True']
```

5）互相嵌套类型，例如列表和字典。若元素是复杂的嵌套类型时，需要递归地进行转换。

```python
original_list = [1, [2.5, '3'], {'key': True}]
def recursive_str_convert(item):
    if isinstance(item, list):
        return [recursive_str_convert(elem) for elem in item]
    elif isinstance(item, dict):
        return {k: recursive_str_convert(v) for k, v in item.items()}
    else:
        return str(item)

string_list = recursive_str_convert(original_list)
print(string_list)
# 输出 ['1', ['2.5', '3'], {'key': 'True'}]
```

**5.Python中单引号和双引号有什么区别？**

在Python中，单引号''和双引号""基本是等价的，可以将这两个组合起来，当字符串包含另一种引号时，方便处理，比如`"It's a car."`或`'He said "Hello!"'`。

**扩展知识**

1）多行字符串。可以使用三引号'''或"""来定义多行字符串，这在编写多行注释或需要包括多个段落的字符串时非常有用。例如

```python
multi_line_str = """This is a
multi-line
string."""
```

2）字符串中的引号处理。加入字符串中包括单引号，而整体用双引号包裹，那么就不需要转义，反之一样。

```python
quote_within_string = "He said 'Hello!'"
print(quote_within_string)
# 输出 He said 'Hello!'
```

如果是单引号中包括单引号或者是双引号中包括双引号，那就需要转义。

```python
escaped_quote = 'It\'s a car.'
print(escaped_quote)
# 输出 It's a car.
```

3）字符串拼接

- 使用 + 运算符

```python
first = "Hello"
second = "World"
result = first + " " + second  # "Hello World"
```

- 使用格式化方法

```python
name = "Alice"
age = 30
formatted_string = f"{name} is {age} years old."  # "Alice is 30 years old."
```

- 使用`join()`方法

```python
words = ["Python", "is", "fun"]
sentence = " ".join(words)  # "Python is fun"
```

4）字符串方法。Python提供了丰富的字符串操作方法，如`upper()`，`lower()`，`replace()`，`split()`，`strip()`，比如：

```python
text = "*Hello, World!*"
print(text.lower())
# 字符串变小写，输出 *hello, world!*
print(text.replace("World", "Python"))
# 替换字符串，输出 *Hello, Python!*
split_text = text.split(',')
print(split_text)
# 分割字符串成列表，输出 ['*Hello', ' World!*']
print(text.strip('*'))
# 移除两端的字符，输出 Hello, World!
```

5）Unicode

在Python中，字符串是Unicode字符的序列，意味着可以在字符串中包含各种语言的字符。特别是Python 3.x，天然地支持Unicode字符串

```python
unicode_str = "안녕,welt!"  # "Hello，World！" in Korea and Germany
print(unicode_str)
```

**6.Python中如何使用索引反转字符串？**

通过字符串切片（slicing）的方法，设置切片范围为全部，步长为-1，即从末尾开始，每次向前走1步，可以很简洁地反转字符串。例如：

```python
original_string = "hello"
reversed_string = original_string[::-1]
print(reversed_string)  # 输出：olleh
```

同理，列表也可以这么反转。

**扩展知识**

1）字符串是不可变的。Python中的字符串是不可变类型（immutable），因此我们每次对字符串进行操作时，实际上都创建了一个新的字符串对象。例如：

```python
a = '123'
print(hex(id(a)))
# 输出 0x2131662bc30
a += '4'
print(hex(id(a)))
# 输出 0x2131662bb70
```

2）其他方法反转字符串

- 使用`reversed()`函数并结合`''.join()`方法

```python
reversed_string = ''.join(reversed(original_string))
# reversed返回的不是列表，是一个reversed object，我也不懂是什么√8，评价是别用
print(reversed_string)  # 输出：olleh
```

- 使用`for`循环，有点类似头插法的感觉

```python
reversed_string = ''
for char in original_string:
    reversed_string = char + reversed_string
print(reversed_string)  # 输出：olleh
```

- 递归，为了炫技才会写这种√8，没啥意义

```
def reverse_string(s):
    if len(s) == 0:
        return s
    else:
        return reverse_string(s[1:]) + s[0]

reversed_string = reverse_string(original_string)
print(reversed_string)  # 输出：olleh
```

3）其他字符串操作

- 查找：str.find(substring, start)，以start为起始点，返回子串在字符串的第一个字符的下标，找不到返回-1，从左往右查找，即使start为负，也是从左往右查找。
- 替换：str.replace(old, new)
- 分割：str.split(separator)
- 拼接：''.join(list_of_strings)





































































