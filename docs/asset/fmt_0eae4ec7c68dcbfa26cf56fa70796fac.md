
```python
if linecount > 0:
    index = data.index(b'\n')
    line = bytes(data[:index])
    data = data[index+1:]
    linecount -= 1
else:
    line = None
```

```python
>>> r = line_receiver()
>>> r.send(None)    # 运行生成器
>>> r.send(b'hello')
'hello'
>>> r.send(b'world\n')
'hello world\n'
>>> r.send(b'works!')
'it works!\n'
>>>
```

```python
class LineReceiver:
    def __init__(self):
        self.data = bytearray()
        self.linecount = 0

    def send(self, part):
        self.linecount += part
        self.data.extend(part)
        if self.linecount > 0:
            index = self.data.index(b'\n')
            return bytes(self.data[:index])
```

```python
class Awaitable:
    def __await__(self):
        print('About await')
        yield  # 必须是一个生成器
        print('Resuming')

# 与 await 。返回一个 "awaitable"
def function():
    return Awaitable()

async def main():
    await function()
```

```python
>>> s = "Hello World"
>>> s.upper()
'HELLO WORLD'
>>> s.replace('Hello', 'Helloel')
'Helloel World'
>>> s.split()
['Hello', 'World']
>>>
```

```python
>>> type(names)
<class 'list'>
>>>
```

一个对象被称为其类型的`实例`。例如，`names`是`list`的实例。

```python
class Account:
    """
    一个简单的银行账户
    """
    owner: str
    balance: float

    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __repr__(self):
        return f'Account({self.owner!r}, {self.balance!r})'

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.balance -= amount

    def inquiry(self):
        return self.balance
```

## 创建几个账户

```python
a = Account('Guido', 1000.0)
# 调用 Account.__init__(a, 1000.0)
```

```python
b = Account('Eva', 10.0)
# 调用 Account.__init__(b, 10.0)
```

```python
a.deposit(100.0)
b.withdraw(50.0)
owner = a.owner
```

```python
# 调用 Account.deposit(a, 100.0)
# 调用 Account.withdraw(b, 50.0)
# 获取账户所有者
```

```python
>>> a = Account('Guido', 1000.0)
>>> b = Account('Eva', 10.0)
>>> vars(a)
{'owner': 'Guido', 'balance': 1000.0}
>>> vars(b)
{'owner': 'Eva', 'balance': 10.0}
>>>
```

```python
>>> type(a)
<class 'Account'>
>>> type(b)
<class 'Account'>
>>> type(a).deposit
<function Account.deposit at 0x...>
>>> type(a).inquiry
<function Account.inquiry at 0x...>
>>>
```

```python
>>> a = Account('Guido', 1000.0)
>>> a.owner  # 获取
```

```python
>>> a.balance = 750.0 # 设置
>>> del a.balance # 删除
>>> a.balance
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Account' object has no attribute 'balance'
>>>
```

```python
>>> a = Account('Guido', 1000.0)
>>> getattr(a, 'owner')
'Guido'
>>> setattr(a, 'balance', 750.0)
>>> delattr(a, 'balance')
>>> hasattr(a, 'balance')
False
>>> getattr(a, 'withdraw')(100)  # 方法调用
>>> a
Account('Guido', 650.0)
>>>
```

```python
>>> a = Account('Guido', 1000.0)
>>> getattr(a, 'balance', 'unknown')
1000.0
>>> getattr(a, 'creation_date', 'unknown')
'unknown'
>>>
```

```python
>>> a = Account('Guido', 1000.0)
>>> w = a.withdraw
>>> w
<bound method Account.withdraw of Account('Guido', 1000.0)>
>>> w(100)
>>> a
Account('Guido', 900.0)
>>>
```

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __repr__(self):
        return f'Account({self.owner!r}, {self.balance!r})'

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.deposit(-amount)  # 必须使用 self.deposit()

    def inquiry(self):
        return self.balance
```

```python
class AccountPortfolio:
    def __init__(self):
        self.accounts = []

    def add_account(self, account):
        self.accounts.append(account)

    def total_funds(self):
        return sum(account.inquiry() for account in self)

    def __len__(self):
```
