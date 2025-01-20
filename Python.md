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

- 查找：`str.find(substring, start)`，以`start`为起始点，返回子串在字符串的第一个字符的下标，找不到返回-1，从左往右查找，即使start为负，也是从左往右查找。
- 替换：`str.replace(old, new)`
- 分割：`str.split(separator)`
- 拼接：`''.join(list_of_strings)`

**7.Python有哪些局限性？**

Python作为一种广泛使用的编程语言，有很多优点，简单的语法，丰富的库函数，活跃的社区，但它也有很多局限性，包括;

1）性能限制：Python是解释型语言，执行速度较低，通常比编译型语言如C、C++慢很多。

2）多线程问题：由于全局解释器锁（GIL）的存在，Python的多线程并不能真正利用多核CPU，提高多线程并发能力有限。

3）移动开发：相比于Java或Kotlin，Python在移动开发上并不是首选。

4）内存管理：Python的内存消耗较高，不适合内存受限的环境。

5）错误检测：由于动态类型的特性，许多错误（尤其是类型错误）要在运行时才能发现，而不是编译时。

**扩展知识**

1）性能限制：Python慢主要是由于它是解释型语言，在高性能要求的场景需要其他语言来补足。例如，在需要高效计算的领域，Python通常会借助C/C++编写的库（如numpy，pandas等）来提升性能。

2）多线程问题：GIL的限制，为了解决这个问题，可以使用多进程（multiprocessing）或者选择不受GIL限制的Jython或IronPython，但这些方案也有它们自己的限制。

3）移动开发：Python有Kivy的框架可以用于移动开发，但是在移动应用开发领域的生态和支持不像Java和Swift那样成熟，所以大多数移动开发者会选择后者。

4）内存管理：Python的自动垃圾回收机制很方便，但是也带来了内存消耗高的问题，对于一些嵌入式系统或者需要精确内存管理的应用来说，Python并不是最理想的选择。

5）错误检测：动态类型的特性虽然使得编码更灵活，但是也增加了程序在运行时遇到类型错误的概率，因此很多开发者会借助静态类型检查工具（如mypy）来提高代码的安全性和可靠性。

**8.为什么Python不建议使用下划线开头的标识符？**

在Python中不建议使用下划线开头的标识符，这是因为下划线在标识符中的使用有特殊的含义和约定。
1）单个下划线开头（例如`_variable`）：表示这是一个内部使用的变量或方法，建议外部代码不要访问。这只是一个提醒，并没有真正的私有性。

2）双下划线开头（例如`__variable`）：触发名字重整（name mangling），使得类中的属性更难被直接访问，用于避免子类覆盖，但仍然不是严格的私有变量。例如;

```python
class MyClass:
    def __init__(self):
        self.__private_value = 42

obj = MyClass()
print(obj._MyClass__private_value)  # 42
# print(obj.__private_value) # 报错AttributeError: 'MyClass' object has no attribute '__private_value'
```

3）单下划线结尾（例如`variable_`）：为了避免与Python的关键字冲突，比如`class`是Python的一个保留字，因此我们可以用`class_`作为变量名

4）双下划线开头和双下划线结尾（例如`__init__`）：这是一个魔术方法（magic method），Python中有特殊用途的预定义方法。如`__init__`，`__str__`，`__repr__`等。

**8.为什么Python中没有函数重载？**

Python没有函数重载（Function Overloading），因为它的函数可以通过默认参数、*args、**kwargs等特性来实现同样的功能。Python是动态类型语言，函数的行为可以根据传入的参数类型和数量灵活调整。

1）动态类型语言：

不同于静态类型语言（如C++、Java），Python的函数参数不在编译期绑定到特定的类型上，而是在运行时进行检查，因此Python不需要依靠重载来实现多态。

2）默认参数：

Python的函数可以有默认参数，这种特性让同一个函数能够处理不同数量的参数。例如：

```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")
    
greet("Alice")
greet("Bob", "Hi")
```

> 注：编写带默认参数的函数时，带默认参数的变量必须统一在普通变量后面，我觉得这是为了保证传值时对应的关系，优先填入普通变量，而默认参数的变量可以缺省

3）\*args和\*\*kwargs：

可变参数(*args)和关键字参数(\*\*kwargs)允许函数接受任意数量和类型的参数，这些特性在某种程度上弥补了没有函数重载的缺憾。例如：

```python
def add(*args):
    return sum(args)


print(add(1, 2))  # 输出: 3
print(add(1, 2, 3, 4))  # 输出: 10
```

```python
def print_kwargs(**kwargs):
    # kwargs是一个字典，包含了所有传递给函数的关键字参数
    for key, value in kwargs.items():
        print(f"{key}: {value}")
    print(kwargs)

# 调用函数，传递一些关键字参数
print_kwargs(name="Kimi", age=30, country="Moonshot")

# 输出：
# name: Kimi
# age: 30
# country: Moonshot
# {'name': 'Kimi', 'age': 30, 'country': 'Moonshot'}
```

4）虽然Python本身不支持函数重载，但可以使用一些第三方库来实现类似的功能，例如`functools.singledispatch`，这是Python的标准库中提供的一种实现函数重载的方式。

```python
from functools import singledispatch

@singledispatch
def fun(arg):
    print("default", arg)

@fun.register(int)
def _(arg):
    print("int", arg)

@fun.register(str)
def _(arg):
    print("str", arg)

fun(10)    # 输出: int 10
fun("10")  # 输出: str 10
fun(10.5)  # 输出: default 10.5
```

**9.你知道哪些Python的编码规范？**

PEP 8是Python语言的官方编码规范，它涵盖了很多方面，比如代码的缩进、注释、命名风格等等。遵循这些规范能够让你的代码更易读、更易维护。

1）缩进：使用4个空格进行缩进，而不是使用Tab

2）最大行长度：每行代码尽量不超过79个字符

3）空行：类和顶级函数定义之间保留两个空行，方法定义之间保留一个空行

4）注释：注释分为行内注释、块注释和文档字符串。应该使用完整的英文句子，并且要简洁明了

5）命名规范：模块、函数、变量名使用小写字母和下划线（snake_case），类名使用单词首字母大写（CamelCase）

6）导入顺序：导入模块时，标准库、第三方库和本地库的导入要分开书写

**扩展知识**

1）静态代码检查工具：使用pylint、flake8或者black等工具可以自动检测并修复代码中的风格问题，不仅检查PEP 8规范，还可以配置成检查团队内部的编码规范。

2）单元测试：编写单元测试并行代码风格检查工具一起使用，可以保证代码质量。unittest是Python内置的单元测试框架，pytest是一个非常流行的第三方框架，它更加灵活，功能更强大。

**10.请介绍Python中变量的作用域？**

变量的作用域（scope）指的是一个变量在程序中可以被访问的范围。Python中的变量作用域大致分为这几种：

1）局部作用域（Local Scope）：函数内部定义的变量，它们只能在该函数内部使用。

2）局部作用域-嵌套（Enclosing Scope）：在嵌套函数中，外层函数的局部变量对内层函数是可见的。

3）全局作用域（Global Scope）：在整个模块或程序中都能访问的变量。它们通常在函数外部定义。

4）内置作用域（Built-in Scope）：Python语言内置的作用域，包含了内置函数、变量、类，比如`print()`、`len()`、`True`、`False`等

**扩展知识**

1）内置作用域

```python
print(len("Hello, World!"))  # 内置函数 len()
```

在这里，我们使用了Python内置的`len()`函数，它属于内置作用域

2）调整变量的作用域

- 使用global关键字

```python
a = 100  # 全局变量

def modify_global_variable():
    global a
    # 为了能够修改全局变量，不加global a的话，直接a = 200只能反映在局部作用域中，无法修改到全局变量中
    a = 200

modify_global_variable()
print(a)  # 输出 200，表明全局变量 a 被修改
```

- 使用nolocal关键字

```python
def outer_function():
    b = 50
    def inner_function():
        nonlocal b
        b = 60
    inner_function()
    print(b)  # 输出 60，内层函数修改了外层函数的变量

outer_function()
```

**11.init方法在Python中有什么作用？**

`__init__`方法在Python中是类的构造方法。它在创建一个类的实例时被自动调用，用来初始化实例的属性。

> 注：`__new__`方法与`__init__`方法的区别，`__new__`方法和`__init__`方法都是类的构造方法，但它们有各自不同的功能，`__new__`方法用于创建并返回一个新的实例对象，是类级别的方法，而`__init__`方法则用于初始化实例对象，是实例级别的方法。通常情况下，我们只需重写`__init__`方法，而很少需要重写`__new__`方法。

**12.你使用过哪些Python标准库模块？**

在日常开发工作中，以下是一些比较常用的模块及其用途：

1）os：用于与操作系统进行交互，如文件和目录操作。

2）sys：提供对Python解释器使用环境的访问，可以获取和修改解释器的不同部分。

3）re：用于处理正则表达式，支持复杂度的字符串匹配和替换。

4）datetime：处理日期和时间，支持日期时间算术运算。

5）json：用于解析和生成JSON数据，常用于API请求和数据存储。

6）math：提供标准数学函数。

7）random：用于生成随机数和随机选择。

8）collections：提供了高级的数据结构如namedtuple、deque、Counter等

9）itertools：提供高效的迭代器操作工具。

10）functolls：提供高阶函数和操作，比如partial和lru_cache。

等等

**13.说明Python中的zip函数？**

Python中的zip函数是一个在标准库中非常有用的函数，主要用于将多个可迭代对象（例如列表、元组等）“压缩”到一起，形成一个迭代器，每次迭代返回一个包含来自各个可迭代对象的元素的元组。简而言之，zip函数可以将很多行平铺的数据“拉链”起来，使其变成便于逐行访问的形式。例如;

```python
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']
result = zip(list1, list2)
print(list(result))  # 输出 [(1, 'a'), (2, 'b'), (3, 'c')]
for a, b in zip(list1, list2):
    print(f'{a}-{b}')
# 输出
# 1-a
# 2-b
# 3-c
```

**扩展知识**

1）拆包技巧

zip函数不仅可以"拉链"多个列表，还可以通过"*"运算符进行反转，例如;

```python
zipped = [(1, 'a'), (2, 'b'), (3, 'c')]
list1, list2 = zip(*zipped)
print(list1)  # 输出 (1, 2, 3)
print(list2)  # 输出 ('a', 'b', 'c')
```

2）处理不同长度的可迭代对象

默认情况下，zip函数会在最短的输入可迭代对象耗尽时停止（不会因为长度不同而报错），如果你有不同长度的数据集合，使用`itertools.zip_longest`可以方便地处理，这个函数会用指定的填充值填充较短的可迭代对象。例如：

```python
from itertools import zip_longest
list1 = [1, 2, 3]
list2 = ['a', 'b']
result = zip_longest(list1, list2, fillvalue='x')
print(list(result))  # 输出 [(1, 'a'), (2, 'b'), (3, 'x')]
```

3）兼容问题

在Python 2和Python 3之间zip存在一些差异，在Python 2中，zip返回的是列表，而在Python 3中，zip返回的是迭代器。因此考虑到内存使用，使用迭代器而不是列表可能是更优的选择，这时Python 3的zip函数会更省内存。

**14.说明Python中enumerate()的用法？**

enumerate()是Python中的一个内置函数，它用于将一个可迭代对象（如列表、元组、字符串等）组合为一个索引序列，同时返回下标和数据（从0开始）。例如;

```python
items = ['a', 'b', 'c']
for index, value in enumerate(items):
    print(index, value)
# 输出
# 1 a
# 2 b
# 3 c
```

**扩展知识**

指定起始索引：

```python
for index, value in enumerate(items, start=1):
    print(index, value)
# 输出
# 1 a
# 2 b
# 3 c
```

使用在字典上：

字典的键会作为索引，而值作为值

```python
dict_items = {'a': 1, 'b': 2, 'c': 3}
for key, value in enumerate(dict_items):
    print(key, value)
# 输出
# a 1
# b 2
# c 3
```

使用在文件读取上：

当读取文件时，用来跟踪行号

```python
with open('file.txt', 'r') as file:
    for line_number, line in enumerate(file, start=1):
        print(line_number, line)
```









































