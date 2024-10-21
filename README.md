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











































































































