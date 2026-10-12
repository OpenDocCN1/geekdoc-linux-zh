
```python
import threading
import queue
import time

def producer(q):
    for i in range(10):
        print('Producing:', i)
        q.put(i)
print('Done')
q.put(None)

def consumer(q):
    while True:
        item = q.get()
        if item is None:
            break
        print('Consuming:', item)
print('Goodbye')
```

```python
q = queue.Queue()
threading.Thread(target=producer, args=[q]).start()
threading.Thread(target=consumer, args=[q]).start()
```

```python
from urllib.request import urlopen
u = urlopen('http://www.python.org')
```

```python
data = u.read()
```

```python
from urllib.parse import urlencode
from urllib.request import urlopen

form = {
    'name': 'Mary A',
    'email': 'mary@python.org'
}

data = urlencode(form)
u = urlopen('http://httpbin.org/post', data.encode('utf-8'))
response = u.read()
```

```python
url = 'http://httpbin.org/get?name=Dave&42'
from urllib.parse import urlparse
urlparse(url)
ParseResult(scheme='http', netloc='httpbin.org', path='/get', query='name=Dave&42', fragment='')
```

```python
d = {}
d['jalapeño'] = 'spicy'
d['jalapeño'] = 'mild'
```

```xml
<?xml version="1.0" encoding="iso-8859"?>
<recipe>
  <title>Guacamole</title>
  <description> southwest favorite!</description>
  <ingredients>
    <item num="4">Large avocados</item>
    <item num="2">Tomato, chopped</item>
    <item num="1">White onion, diced</item>
    <item num="1">Fresh lemon juice</item>
    <item num="1">Jaleno pepper, diced</item>
    <item num="3">Salt</item>
    <item num="12">Fresh cilantro, minced</item>
  </ingredients>
  <directions>
    Combine all ingredients and
    Serve with ice-cold beers.
  </directions>
</recipe>
```

```python
from xml.etree.ElementTree import ElementTree

doc = ElementTree("recipe.xml")
title = doc.find('title')
print(title.text)

# 另一种方法：直接获取元素文本
print(doc.findtext('description'))

# 遍历多个元素
for item in doc.findall('ingredients/item'):
    num = item.get('num')
    units = item.get('units', '')
    text = item.text.strip()
    print(f'{num} {units} {text}')
```

```python
delattr(object, attr)
```

```python
dict([m]) or dict(key1=value1, key2=value2, ...)
```

```python
enumerate(iter, start=0)
```

```python
eval(expr, globals, locals)
```

```python
exec(code, globals, locals)
```

```python
filter(function, iterable)
```

```python
max(s, args, ...], *, default=obj, key=func)
```

```python
min(s [, args, ...], *, default=obj, key=func)
```

```python
open(filename, mode, bufsize, encoding, errors, newline, closefd)
```

```python
print(value, ..., *, sep=separator, end=ending, file=outfile)
```

```python
property(fget, fset, fdel, doc)
```

```python
class SomeClass:
    x = property(doc='This is property x')
    @x.getter
    def x(self):
        print('getting x')

    @x.setter
    def x(self, value):
        print('setting x to', value)

    @x.deleter
    def x(self):
        print('deleting x')
```

```python
range([start,] stop [, step])
```

```python
setattr(object, name, value)
```

```python
slice([start, , step])
```

```python
sorted(iterable, *, default=obj, key=func)
```

```python
class B(A):
    def foo()
```

- 4.12 转换协议
- 4.13 容器协议
- 4.14 迭代器协议
- 4.15 属性协议
- 4.16 函数协议
- 4.17 上文管理器协议
- 4.18 结语：论 Pythonic 化

## 5. 函数

- 5.1 函数定义
- 5.2 默认参数
- 5.3 变长参数
- 5.4 关键字参数
- 5.5 变长关键字参数
- 5.6 接收所有输入的函数
- 5.7 仅位置参数
- 5.8 名称、文档字符串与类型提示
- 5.9 函数应用与参数传递
- 5.10 返回值
- 5.11 错误处理
- 5.12 作用域规则
- 5.13 递归
- 5.14 lambda 表达式
- 5.15 高阶函数
- 5.16 回调函数中的参数传递
- 5.17 从回调返回结果
- 5.18 装饰器
- 5.19 Map, Filter 和 Reduce
- 5.20 函数内省、属性与签名
- 5.21 环境检查
- 5.22 动态代码执行与创建
- 5.23 异步函数与 await
- 5.24 结语：关于函数与组合的思考

# 6. 生成器

- 6.1 生成器与 yield
- 6.2 可重启的生成器
- 6.3 生成器委托
- 6.4 实践中生成器的使用
- 6.5 增强型生成器与 yield 表达式
- 6.6 增强型生成器的应用
- 6.7 生成器与通往 await 的桥梁
- 6.8 结语：生成器简史与展望

## 7. 类与面向对象编程

- 7.1 对象
- 7.2 class 语句
- 7.3 实例
- 7.4 属性访问
- 7.5 作用域规则
- 7.6 运算符重载与协议
- 7.7 继承
- 7.8 通过组合避免继承
- 7.9 通过函数避免继承
- 7.10 动态绑定与鸭子类型
- 7.11 继承内置类型的危险
- 7.12 类变量与类方法
- 7.13 静态方法
