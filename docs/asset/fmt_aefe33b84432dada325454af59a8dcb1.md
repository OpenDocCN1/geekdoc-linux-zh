
之前定义的 `person` 类通过 `getFirstName()` 和 `putFirstName()` 方法提供了对 `__fname` 的必要访问，就像汽车通过刹车踏提供对制动钳的必要访问一样。`person` 类的工作原理显而易见。调用 `putFirstName()` 会改变 `__fname`，调用 `getFirstName()` 则检索 `__fname`。对于姓名的方法和变量也是如此。

![](img/f36419c0b225d12fa66de83fa271829b_926_0.png)

# 开发环境

## 第四部分

现在你可以添加以下代码来练习 `person` 类代码：

```
p = person()
print "*", p.getFirstName(), p.getLastName(), "*"
p.putFirstName('John')
p.putLastName('Smith')
print "*", p.getFirstName(), p.getLastName(), "*"
```

上述代码实例化了一个名为 `p` 的 `person` 对象，打印了（目前为空的）姓和名，设置了姓名，然后再次打印了它们。输出如下：

- * *

* John Smith *

# 类构造函数

现在我们准备好添加类构造函数了。类构造函数始终被调用 `__init__()`。只能定义一个类构造函数。在这种情况下，我们创建了类构造函数，使得姓名在实例化时被定义：

```
class person:
    def __init__(self, lname, fname):
        self.__lname = lname
        self.__fname = fname
    def getFirstName(self):
        return self.__fname
    def getLastName(self):
        return self.__lname
    def putFirstName(self, s):
        self.__fname = s
    def putLastName(self, s):
        self.__lname = s
    __fname = "*"
    __lname = "*"
```

```
p = person('John', 'Paul')
print "*", p.getFirstName(), p.getLastName(), "*"
```

在上述代码中，人的姓名通过 `__init__` 方法在实例化时设置，因此 `print` 语句打印了正确的姓名：

- * John Jones *

模块化自工业革命以来一直是构建成本效益、可靠且易于维修的系统的基础。面向对象编程的潜力在软件中实现了这些优势。紧密封装使得程序具有可扩展性，这意味着它们可以不断增长，而不会导致交互组合呈几何级数增长并阻止进一步增长。紧密封装之路在于决定每个类代表什么，并创建极少数的公共函数允许其他软件实体控制其行为并向其查询信息。

# Python 编程

## 第 27 章

### 注意

继承是一个高级的 OOP 主题，主要涉及那些正在进行严肃开发的人员。如果你在做中等规模的项目，可以安全地选择跳过“继承”部分。

# 继承

面向对象允许按部分而非任务来构建程序。这些部分通常代表具体的对象或业务实体。在这种情况下，像我们在英语中那样对这些对象或实体进行分类是非常方便的。考虑以下：

- 动物

  - 鸟

    - 鸭子

    - 欧雀

    - 猫头鹰

- 鱼

  - 鳟鱼

    - 鲶鱼

你可以将这种层次结构的关系视为“是一种”关系。换句话说，鸟是一种带翅膀的动物。欧雀是一种鸟。欧雀从鸟那里继承特征（翅膀），从动物那里继承特征（运动）。

这是另一个例子：

- 人

  - 员工

员工是一个人。

现在让我们看看代码：

```
class person:
    def __init__(self, lname, fname):
        self._lname = lname
        self._fname = fname
    def getFirstname(self):
        return self._fname
    def getLastName(self):
        return self._lname
    def putfirstname(self, s):
        self._fname = s
    def putlastname(self, s):
        self._lname = s

p = person("Jones", "Paul")
print "*", p.getFirstName(), p.getLastName(), "*"
```

![](img/f36419c0b225d12fa66de83fa271829b_926_0.png)
