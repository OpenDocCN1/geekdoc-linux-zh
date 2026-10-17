
`fluffy.color = "yellow"`

`print fluffy.color`

`print poppy.color`

```
```

因此，狗的默认颜色是棕色——`fluffy` 和 `poppy` 两个狗对象最初都是棕色。然后，使用 `dog.color`，我们将默认颜色设置为黑色，并且由于这两个对象都没有设置自己的颜色值，它们都会更新为黑色。倒数第三行使用 `poppy.color` 为 `poppy` 对象设置自定义颜色值——`poppy` 变成了黄色，而 `fluffy` 和狗类总体上仍然是黑色。

## 构造函数和析构函数

为了帮助你自动化对象的创建和删除，你可以轻松重写两个默认方法：`__init__` 和 `__del__`。这些是 Python 在类被实例化和释放时调用的方法，分别称为构造函数和析构函数。

拥有自定义构造函数在你需要为每个创建的对象接受一组参数时非常有用。例如，你可能希望每只狗在创建时都有自己的名字，你可以用这段代码实现：

```
class dog(object):
    def __init__(self, name):
        self.name = name

fluffy = dog('fluffy')
print fluffy.name
```

如果你在创建狗对象时没有提供 `name` 参数，Python 会报告错误并停止。当然，你可以要求任意多的构造函数参数，但通常最好只要求你需要的参数，并通过其他函数来填充其余部分。

另一方面是析构函数方法，它允许你在对象被销毁时更好地控制会发生什么。使用这两个方法，我们可以通过在对象创建和删除时打印消息来展示对象的生命周期：

```
class dog(object):
    def __init__(self, name):
        self.name = name
        print self.name + " is alive!"
    def __del__(self):
        print self.name + " is no more!"

fluffy = dog('fluffy')
```

析构函数的作用是给你一个机会来释放分配给对象的资源，或许向文件记录某些内容。

## 类继承

Python 允许你通过继承一个或多个其他类来重用代码。例如，狮子、老虎和熊都是哺乳动物，因此共享许多相似的属性。在这种情况下，你不希望在它们之间复制粘贴函数；更明智、更简单的做法是创建一个哺乳动物类来定义所有共享功能，然后让每个动物从该类继承。

考虑以下代码：

```
class car(object):
    color = 'black'
    speed = 0
```

```
def accelerateTo(self, speed):
    self.speed = speed
def setColor(self, color):
    self.color = color
mycar = car()
print mycar.color
```

这创建了一个 `car` 类，具有默认颜色，并且还提供了一个 `setColor()` 函数，以便人们可以更改自己的颜色。现在，你开车去上班吗？是汽车吗？当然是，但很可能是一辆福特，或道奇，或吉普，或其他品牌——你不会得到没有品牌的汽车。另一方面，你也不想必须定义一个 `Ford` 类，给它 `accelerateTo()`、`setColor()` 以及基础汽车所拥有的所有其他方法，然后对 `Ferrari`、`Nissan` 等做完全相同的事情。

解决方案是使用继承：定义一个 `car` 类，包含所有品牌共享的函数和变量，然后从中继承。在 Python 中，你通过在类声明中的括号内放置要继承的类的名称来实现，如下所示：

```
class car(object):
    color = "black"
    speed = 0
    def accelerateTo(self, speed):
        self.speed = speed
    def setColor(self, color):
        self.color = color

class ford(car): pass
class nissan(car): pass
mycar = ford()
print mycar.color
```

`pass` 指令是一个空语句——它意味着我们的类没有新内容。然而，由于 `ford` 和 `nissan` 类继承自 `car` 类，它们获得了父类提供的 `color`、`speed`、`accelerateTo()` 和 `setColor()`。请注意，我们不需要在 `ford` 和 `nissan` 的类名后加上 `object`，因为它们是从已存在的类 `car` 继承的。

默认情况下，Python 会给你父类拥有的方法，但你可以通过为需要它们的类提供新的实现来覆盖它。例如：

```
class modelT(car):
    def setColor(self, color):
        print "Sorry, Model Ts only come in black!"

myford = ford()
ford.setColor("green")
```

- `http://www.jython.org`—Python 也有一个出色的基于 Java 的解释器，可使其在其他平台上运行。如果你更喜欢 Microsoft .NET，可以试试 `http://www.ironpython.com`。

- `http://www.pythonline.com`—Guido van Rossum 从 *Monty Python’s Flying Circus* 中借用了他语言的名字，因此许多 Python 代码示例都使用了偏斜的 *Monty Python* 引用。访问官方 *Monty Python* 网站以提升你的 Python 知识是强烈推荐的！

关于 Python 的真正优秀书籍很少；不过，你可以在 `http://www.python.org/main/PythonBooks` 上找到一份可供选择的清单。如果你急于立即挑选一本书，选择 *Learning Python*（O’Reilly，ISBN：0-596-00281-5）不会错。

## CHAPTER 25

## Writing PHP Scripts

##### IN THIS CHAPTER

- Introduction to PHP
- Basic Functions
- Handling HTML Forms
- Databases
- Reference

本章将从将其用作 Web 脚本语言和命令行工具的角度，向你介绍 PHP 编程的世界。PHP 最初代表 personal home page，因为它是一组 Perl 脚本，旨在简化访客簿、留言板以及常见于主页上的其他交互式脚本的创建。然而，自那些早期日子以来，它已收到两次重大更新（PHP 3 和 PHP 4），以及 PHP 5 中的一次重大修订，PHP 5 是随 Ubuntu 捆绑的版本。

PHP 成功的一部分在于其与数据库的强大集成——其最早的使用几乎总是利用了数据库后端。然而，在 PHP 5 中，引入了两种新的大型数据存储机制：SQLite，它是一种功能强大且本地的数据库系统；以及 SimpleXML，它是一个应用程序编程接口（API），旨在使 XML 解析和查询变得简单。正如你将随着时间的推移所看到的，PHP 开发人员做得非常出色：SQLite 和 SimpleXML 都易于学习和使用。

#### NOTE

许多 PHP 包可通过 `synaptic` 获得。基本包仅称为 `php5`，但你可能还想添加诸如 `php5-ldap`、`php5-mysql` 或 `php5-pgsql` 之类的扩展。仅选择你计划使用的扩展；否则会浪费系统资源。

## Introduction to PHP

就其外观而言，PHP 是 Java 和 Perl 的结合体，取两者之长并成功融合为一种语言。Java 部分包括强大的面向对象系统、抛出程序异常的能力，以及两种语言都从 C 借鉴的一般编写风格。借鉴自 Perl 的是“它应该就能工作”的理念，其中易用性优先于严格性。因此，你会在 PHP 中发现很多“做同一件事的方法不止一种”。

### Entering and Exiting PHP Mode

与 PHP 的前身不同，你将 PHP 代码嵌入到 HTML 中，而不是相反。在 PHP 之前，许多网站的大部分内容都是标准的 HTML 页面，链接到 Perl CGI 页面以在需要时进行后端处理。有了 PHP，你的所有页面都能够处理并包含 HTML。

每个 `.php` 文件都由 PHP 处理，PHP 会查找要执行的代码。PHP 将找到的所有文本都视为 HTML，直到找到以下四种情况之一：

- `<?php`
- `<?`
- `<%`
- `<script language="php">`

第一个选项是进入 PHP 模式的首选方法，因为它保证能工作。

进入 PHP 模式后，你可以通过使用 `?>`（用于 `<?php` 和 `<?`）；`?>` 用于 `<%`）或 `</script>`（用于 `<script language="php">`）退出。这种代码示例演示了进入和退出 PHP 模式：
