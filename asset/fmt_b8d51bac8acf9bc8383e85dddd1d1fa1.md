
`total_shares = { s[0]: 0 for s in portfolio }`

```python
for name, shares, _ in portfolio:
    total_shares[name] += shares
```

```python
# total_shares = {'IBM': 125, 'ACME': 50, 'PHP': 40}
```

```python
from collections import Counter

total_shares = Counter()

for name, shares, _ in portfolio:
    total_shares[name] += shares

# total_shares = Counter({'IBM': 125, 'ACME': 50, 'PHP': 40})
```

```python
prices = {} # 一个空字典
prices = dict() # 一个空字典
```

```python
pairs = [('IBM', 125), ('ACME', 50), ('PHP', 40)]
d = dict(pairs)
```

```python
syms = list(prices)    # syms = ['AAPL', 'MSFT', 'IBM', 'GOOG']
```

```python
>>> d = { 'x': 2, 'y': 3 }
>>> k = d.keys()
dict_keys(['x', 'y'])
>>> d['z'] = 4
>>> k
dict_keys(['x', 'y', 'z'])
>>>
```

```python
for sym, price in prices.items():
    print(f'{sym} = {price}')
```

```python
for n in range(1, 2, 3, 4, 5, 6, 7, 8, 9, 10):
    print(f'2 to {n} power is {2**n}')
```

```python
def mul(self):
    self.push(self.pop() * self.pop())

def sub(self):
    right = self.pop()
    self.push(self.pop() - right)

def div(self):
    right = self.pop()
    self.push(self.pop() / right)
```

# readport.py

读取包含 '名称,股数,价格' 数据的数据的文件

```python
def read_portfolio(filename):
    portfolio = []
    with open(filename) as file:
        for line in file:
            row = line.split(',')
            try:
                name = row[0]
                shares = int(row[1])
                price = float(row[2])
                holding = (name, shares, price)
                portfolio.append(holding)
            except ValueError as err:
                print('Bad row:', row)
                print('Reason:', err)
    return portfolio
```

# pcost.py

```python
import readport

def portfolio_cost(filename):
    """
    计算投资组合的总价值（股数*价格）
    """
    port = readport.read_portfolio(filename)
    return sum(shares * price for _, shares, price in port)
```

```python
import readport as rp
port = rp.read_portfolio('portfolio.dat')
```

```python
from readport import read_portfolio
port = read_portfolio('portfolio.dat')
```

```python
>>> import readport
>>> dir(readport)
['__builtins__', '__cached__', '__doc__', '__file__', '__loader__', 
 '__name__', '__package__', '__spec__', 'read_portfolio']
...
>>>
```

# readport.py

读取包含 '名称,股数,价格' 数据的文件

```python
import csv

def read_portfolio(filename):
    portfolio = []
    with open(filename) as file:
        rows = csv.reader(file)
        for row in rows:
            try:
                name = row[0]
                shares = int(row[1])
                price = float(row[2])
                holding = (name, shares, price)
                portfolio.append(holding)
            except ValueError as err:
                print('Bad row:', row)
                print('Reason:', err)
    return portfolio
```

# readport.py

读取包含 '名称,股数,价格' 数据的文件

```python
import csv

def read_portfolio(filename):
    ...

def main():
    portfolio = read_portfolio('portfolio.csv')
    for name, shares, price in portfolio:
        print(f'{name:>10s} {shares:10d} {price:10.2f}')
```

```python
if __name__ == '__main__':
    main()
```

```python
def main(argv):
    if len(argv) == 1:
        filename = input('Enter filename: ')
    elif len(argv) == 2:
        filename = argv[1]
    else:
        raise SystemExit(f'Usage: {argv[0]} [ filename ]')
    portfolio = read_portfolio(filename)
    for name, shares, price in portfolio:
        print(f'{name:>10s} {shares:10d} {price:10.2f}')

if __name__ == '__main__':
    import sys
    main(sys.argv)
```

```bash
bash % python readport.py
Enter filename: portfolio.csv
...
bash % python readport.py portfolio.csv
...
bash % python readport.py a b c
Usage: readport.py [ filename ]
bash %
```

```python
import tutorial.readport
port = tutorial.readport.read_portfolio('portfolio.dat')
```

```python
from tutorial.readport import read_portfolio
port = read_portfolio('portfolio.dat')
```
