

默认情况下，Python 会提供父类拥有的所有方法，但你可以通过为需要这些方法的类提供新的实现来覆盖它们。例如：

```
class modelT(car):
    def setColor(self, color):
        print 'Sorry, Model Ts only come in black!'
```

```
myford = ford()
ford.setColor('green')
mycar = modelT()
mycar.setColor('green')
```

第一辆车是作为 Ford 创建的，因此 setColor() 可以正常工作，因为它使用 car 类的方法。但是，第二辆车是作为 Model T 创建的，它有自己的 setColor() 方法，因此调用会失败。

这就引出了一个有趣的场景：如果你已经覆盖了一个方法，但仍想同时调用父类的方法，该怎么办？例如，如果允许更改 Model T 的颜色，但需要额外付费，我们可以打印一条消息说“您还需支付 50 美元”，然后再更改颜色。为此，我们需要使用当前类所继承的类对象——在此示例中即 car。下面是一个示例：

```
class modelT(car):
    def setColor(self, color):
        print 'You owe $50 more'
        car.setColor(self, color)
```

```
mycar = modelT()
mycar.setColor('green')
print mycar.color
```

这会打印该消息，然后更改汽车的颜色。

## 标准库与帕纳萨斯宝库

默认的 Python 安装包含许多模块（代码块），使你可以与操作系统交互、打开和操作文件、解析命令行选项、执行数据哈希和加密等。当被问及为什么如此喜欢 Python 时，这是人们最常引用的原因之一——它装满了你可以立即使用的功能。事实上，标准库中包含的模块数量非常多，以至于有整本书专门介绍它们——可以阅读《Python 标准库》（O’Reilly，ISBN：0-596-00096-0），其中有一份全面（虽然略显过时）的模块清单。

对于非官方的 Python 脚本和插件，推荐的起点是帕纳萨斯宝库（Vaults of Parnassus）：http://py.vaults.ca。在那里你可以找到大约 20,000 个公共脚本和代码示例，涵盖从数学到游戏的方方面面。

## 参考资料

Python 网站（http://www.python.org）信息丰富且定期更新。即使只是想了解最新的 Python 新闻，也应该首先访问它。

- http://www.zope.org——Zope 内容管理系统（CMS）的主页，它是当下最流行的 CMS 之一，更重要的是，它完全用 Python 编写。
- http://www.jython.org——Python 还有一个优秀的基于 Java 的解释器，允许它在其他平台上运行。如果你更喜欢 Microsoft .NET，可以试试 http://www.iron-python.com。
- http://www.pythonline.com——吉多·范罗苏姆（Guido van Rossum）将其语言的名称借自《巨蟒剧团的飞行马戏团》（Monty Python's Flying Circus），因此许多 Python 代码示例都隐晦地引用了巨蟒剧团。强烈建议访问巨蟒剧团官方网站来提升你的 Python 知识！

真正出色的 Python 书籍并不多；不过，你可以在 http://www.python.org/moin/PythonBooks 找到一份现有书籍的列表。如果你急于立即入手一本书，选择《学习 Python》（O'Reilly，ISBN：0-596-00281-5）绝不会差到哪里去。

## 第25章

## 编写 PHP 脚本

## 本章内容

- ► PHP 简介
- ► 基本函数
- ► 处理 HTML 表单
- ► 数据库
- ► 参考资料

本章将从 PHP 作为 Web 脚本语言和命令行工具的角度，带你进入 PHP 编程的世界。PHP 最初代表“个人主页”，因为它是一个 Perl 脚本集合，旨在简化留言簿、留言板以及主页上常见的其他交互式脚本的创建。然而，自那时起，它经历了两次重大更新（PHP 3 和 PHP 4），并在 PHP 5 中进行了大幅修订，PHP 5 也是 Ubuntu 所捆绑的版本。

PHP 的成功部分源于其与数据库的强大集成——其最早的应用几乎总是利用数据库后端。然而，在 PHP 5 中，引入了两大新的数据存储机制：SQLite（一个功能强大的本地数据库系统）和 SimpleXML（一个应用程序编程接口（API），旨在让 XML 解析和查询变得简单）。随着时间的推移你会发现，PHP 开发者做得非常出色：SQLite 和 SimpleXML 都易于学习和使用。

> 注意
> 通过 synaptic 可以获得许多 PHP 软件包。基础包名为 php5，但你也可以添加 php5-ldap、php5-mysql 或 php5-pgsql 等扩展。只选择你计划使用的扩展，否则会浪费系统资源。

## PHP 简介

从外观上看，PHP 是 Java 和 Perl 的混合体，它吸取了两者的最佳特性，并成功地将它们融合为一种语言。Java 部分包括

