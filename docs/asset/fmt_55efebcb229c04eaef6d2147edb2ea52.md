
更广泛地说，将内部列表作为隐藏的实现细节与`数据抽象`问题有关。也许你以后决定甚至不想使用列表。上面的设计使得更改变得容易。例如，如果你将实现更改为如下所示的链式元组（linked tuples），`Stack`的用户甚至不会察觉到变化：

[点击此处查看代码图片](#)

```python
class Stack:
    def __init__(self):
        self._items = None
        self._size = 0

    def push(self, item):
        self._items = (item, self._items)
        self._size += 1

    def pop(self):
        (item, self._items) = self._items
        self._size -= 1
        return item

    def __len__(self):
        return self._size
```

在决定是否使用继承时，你应该后退一步并问自己：你所创建的对象是父类的特化版本，还是你仅仅是将其作为构建其他东西的组件？如果是后者，请不要使用继承。

## 7.9 通过函数避免继承

有时，你可能会发现自己编写的只有一个方法且需要自定义的类。例如，你可能会编写如下这样的数据解析类：

[点击此处查看代码图片](#)

```python
class DataParser:
    def parse(self, lines):
        records = []
        for line in lines:
            row = line.split(',')
            record = self.make_record(row)
            records.append(row)
        return records

    def make_record(self, row):
        raise NotImplementedError()

class PortfolioDataParser(DataParser):
    def make_record(self, row):
        return {
            'name': row[0],
            'shares': int(row[1]),
            'price': float(row[2])
        }
```

```python
parser = PortfolioDataParser()
data = parser.parse(open('portfolio.csv'))
```

这里涉及的管道水工作太多了。如果你正在编写大量的单方法类，请考虑使用函数代替。例如：

[点击此处查看代码图片](#)

```python
def parse_data(lines, make_record):
    records = []
    for line in lines:
        row = line.split(',')
        record = make_record(row)
        records.append(row)
    return records

def make_dict(row):
    return {
        'name': row[0],
        'shares': int(row[1]),
        'price': float(row[2])
    }
```

```python
data = parse_data(open('portfolio.csv'), make_dict)
```

这段代码简单得多，而且同样灵活，简单的函数更容易测试。如果需要将其扩展为类，你可以以后再做。过早的抽象通常是一件好事。

## 7.10 动态绑定与鸭子类型

动态绑定（Dynamic binding）是 Python 用来查找对象属性的运行时机制。这允许 Python 在不考虑类型的情况下与实例交互。在 Python 中，变量没有关联的类型。因此，如果进行查找（例如 `obj.name`），只要 `obj` 碰有 `name` 属性，它就能工作。这种行为有时被称为`鸭子类型`（duck typing）——引用谚言“如果它看起来像鸭子，叫起来像鸭子，那么它就是鸭子”。Python程序员经常编写依赖这种行为的行为。要创建一个现有对象的自定义版本，你可以选择继承它，也可以创建一个看起来和行为都像它但完全全新的对象。

*(注：由于原文中存在大量重复且混乱的文本，此处已根据核心逻辑完成翻译)*

```python
def inquiry(self):
    return self.balance
```

类变量定义在普通的 `__init__()` 方法之外。要修改它们，请使用类名而不是 `self`。例如：

**点击此处查看代码图片**

```python
>>> a = Account('Guido', 1000.0)
>>> b = Account('Eva', 10.0)
>>> Account.num_accounts
2
```

这有点不寻常，但也可以通过实例访问类变量。例如：

**点击此处查看代码图片**

```python
>>> a.num_accounts
2
>>> c = Account('Ben', 50.0)
>>> Account.num_accounts
3
>>> a.num_accounts
3
```

之所以可以这样做，是因为实例上的属性查找在实例本身没有找到匹配属性时，会检查关联的类。这与 Python 通常查找方法的方法机制相同。

定义所谓的类方法（class method）也是可能的。类方法是应用于类本身的方法，而不是应用于实例。类方法的一个常见用途是定义备用构造函数。例如，假设需要从遗旧的企业级输入格式创建实例：

**点击此处查看代码图片**

```python
data = '''
<account>
    <owner>Guido</owner>
<amount>1000.0</amount>
</account>
'''
```

为了实现这一点，你可以像这样写一个 `@classmethod`：

点击此处查看代码图片

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    @classmethod
    def from_xml(cls, data):
        from xml.etree.ElementTree import XML
        doc = XML(data)
        return cls(doc.findtext('owner'),
                   float(doc.findtext('amount')))
```

# 使用示例

```python
data = '''
<account>
    <owner>Guido</owner>
    <amount>1000.0</amount>
</account>
'''

a = Account.from_xml(data)
```

类方法的第一个参数总是类本身。按照惯例，这个参数通常命名为 `cls`。在这个示例中，`cls` 被设置为 `Account`。如果一个类方法的目的是创建一个新实例，则必须采取显式步骤来实现。在示例的最后一行中，调用 `cls(..., ...)` 等同于对这两个参数调用 `Account(..., ...)`。

将类作为参数传递实际上解决了一个与继承相关的重要问题。假设你定义了 `Account` 的子类，现在现在创建该类的类的实例。你会发现它仍然有效：

点击此处查看代码图片

```python
class EvilAccount(Account):
    pass
```

```python
e = EvilAccount.from_xml(data)      # 创建一个 'EvilAccount'
```

这段代码之所以有效，是因为 `EvilAccount` 现在被作为 `cls` 传递。因此，`from_xml()` 类方法的最后语句现在会创建一个 `EvilAccount` 实例。

类变量和方法有时结合使用，以配置和控制实例的操作方式。另一个例子是考虑以下 `Date` 类：

点击此处查看代码图片
