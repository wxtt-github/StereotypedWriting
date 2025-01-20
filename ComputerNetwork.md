## 计算机网络面试题

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