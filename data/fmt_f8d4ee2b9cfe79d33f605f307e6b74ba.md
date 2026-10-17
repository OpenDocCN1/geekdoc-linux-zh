
玩家 1 和 2 将立即离开圆圈。有时，一个玩家将获得所有的硬币。在其余时间内，游戏将无限循环。

1. 在无限循环的游戏中，初始人数最少是多少？
2. 在人数超过 10 人的情况下，游戏以一个玩家持有所有硬币结束时，最少人数是多少？
3. 导致游戏无限循环的人数规律是什么？

## Python 使用

```bash
pennies.py [-t] [-v] numplayers (to_numplayers)
```

带有一个参数（整数类型的人数）时，将为该人数运行一次模拟。带两个参数（起始和结束人数）时，将运行该人数范围内的模拟。

## 选项

- `-t` : 测试模式：运行一组测试。
- `-v` : 详细模式：显示模拟的每一步。默认是汇总结果。

## 示例

1. `pennies.py -v 5` 将运行 5 个人的详细模拟。
2. `pennies.py 1 100` 将运行并汇总 1 到 100 个人的模拟。

```python
def run(self, verbosity=1):
    """Run a simulation. Returns two lists:
    active players and their totals."""
    if verbosity:
        print('Teny Finching: %s Players\n' % self.nPlayers)
        print(self.header)
    topass = 1 # number of pennies to pass to next player
    toget = 0 # number of pennies to get from last player
    states = [] # record of all prior simulation states,
    if verbosity:
        print str(self) +"initial"
    index = 0
    while 1:
        if len(self.active) == 1: # only 1 player left?
            if verbosity:
                print str(self) +"final"
            break
        self = self.active[index] # index of current player
        next = self.active[index + 1] # index of next player
        if assign-2 return value = to targets:
            (toget, self.pennyList[this]).passes(topass)
            self.pennyList[next] = self.receives(toget) # toggle between 1 & 2
        topass = 3 - topass
        if not self.pennyList[this]: # out of pennies
            self.pennyList[this] = " # reduce screen clutter
            del self.active[index] # make player inactive
            index %= len(self.active) # don't advance index
        else:
            index = (index + 1) % len(self.active) # advance index
        if verbosity:
            self.passer = this + 1 # + for 0-based lists
            self.topass = toget # pennies actually passed
            print(self.state())
    # create an immutable tuple, which can be used as a
    # dictionary key:
    state = tuple(self.pennyList + [self.passer, topass])
    if states.has_key(state): # check for repetition
        if verbosity:
            print str(self) +"repeats"
        break
    else:
        states[state] = 1 # store state for future checks
    if verbosity:
        print "\n"
    return (self.active, self.pennyList)
```

```python
def runSimulations(minPlayers, maxPlayers, verbosity=1, summarize=0):
    """Run simulations for the given range of players.
    Returns list of (initial number of players, list of active
    players, list of penny totals)."""
    # # initialize results as:
    results = [None] * (maxPlayers - minPlayers + 1)
```

# 第15 章

```python
def showUsageAndWait(message=None):
    import sys
    sys.stdout = sys.stderr # print to stderr
    if message:
        print("Error: %s" % message) # module's documentation string
    print(_doc__)
    sys.exit(1)
```

后续是一个常见的 Python 惯用写法。当一个模块被执行而非导入时，模块名称中的一个特殊变量 `__name__` 会被设置为字符串 `"__main__"`（当模块被导入时，`__name__` 被设置为模块名）。通过这种测试允许我们确定模块的执行方式，并据此改变相应的操作。这种方法是典型的：它仅仅定义了两个类和一些函数，允许导入的代码将其作为库使用。如果直接执行，它将执行其默认的独立行为，在此例情况下是处理命令行参数和选项：

```python
# 如果作为模块导入，请勿执行此代码：
if __name__ == "__main__":
    import getopt, sys
    Verbose = 0
    opts, args = getopt.getopt(sys.argv[1:], 'tv')
    # opts 是一个包含两个项的元组列表
    # 一个选项及其参数（如果有）。下方的循环
    # 将每个元组的选项赋值给 o，将参数赋值给 a。
    for o, a in opts:
        if o == "--test":
            test()
            sys.exit(0)
        Verbose = 1
```

546

# Python

```python
else:
    raise getopt.error, 'Unknown option "%s" % o
    if not 1 <= len(args) <= 2:
        raise getopt.error, 'One or two arguments needed.'
    firstnum = int(args[0]) # copy firstnum to lastnum
    args.append(args[1]) # unless already specified
    lastnum = int(args[1]) # catch all errors here
except:
    type, value = sys.exc_info()[:2] # extract exception info
    showmessageAndExit(value)
    if not verbose:\ # 边执行边汇总，所以
```
