
## 面向对象编程：继承与多继承

在类名之后不需要 `object`，如果是针对 Ford 和 Nissan 的类，因为它们继承自现有的类 `car`。这不是一个严格要求。Python 2.2 引入了这些“新式”类，并推荐使用；但你也可以直接使用 `class car:`。不过，那些旧式（“经典”）类将在未来从语言中移除，因此最好使用 `(object)`。

默认情况下，Python 会赋予你父类拥有的所有方法，但你可以通过为需要的类提供新的实现来重写它们。例如：

```python
class modelt(car):
   def setColor(self, color):
      print "Sorry, Model Ts only come in black!"

myford = ford()
ford.setColor("green")
mycar = modelt()
mycar.setColor("green")
```

第一辆车被创建为 Ford，因此 `setColor()` 正常工作，因为它使用 `car` 类中的方法。然而，第二辆车被创建为 Model T，它有自己的 `setColor()` 方法，所以调用会失败。

这提供了一个有趣的场景：如果你重写了一个方法，但还想调用父类的方法怎么办？例如，如果允许改变 Model T 的颜色但需要额外付费，我们想打印一条消息“你多付了 50 美元”，然后改变颜色。为此，我们需要使用当前类继承自的类对象——本例中是 `car`。下面是一个例子：

```python
class modelt(car):
   def setColor(self, color):
      print "You owe $50 more"
      car.setColor(self, color)

mycar = modelt()
mycar.setColor("green")
print mycar.color
```

这会打印消息，然后改变车的颜色。

### 多继承

你可以继承尽可能多的类，随着进展构建功能。例如，你可以有一个类 *animalia*，一个子类 *chordata*，一个子子类 *mammalia*，以及一个子子子类 *homo sapiens*。每一个都比其父类更具体。然而，Python 的一个有趣之处在于能够进行多继承——同时从两个类获取功能。

再次通过代码展示这一点：

```python
class car(object):
    def drive(self):
        print "We're driving..."

class timemachine(object):
    def timeTravel(self):
        print "Traveling through time..."

class delorian(car, timemachine): pass
mydelorian = delorian()
mydelorian.drive()
mydelorian.timeTravel()
```

在这个例子中，我们有 `car` 类和 `timemachine` 类。两者都可以独立工作，因此你可以拥有一辆车并驾驶它，或者拥有一台时光机并穿越时间。然而，我们还有一个 `delorian` 类，它继承自 `car` 和 `timemachine`。如你所见，它能够调用 `drive()`（继承自 `car`）和 `timeTravel()`（继承自 `timemachine`）。

这引入了另一个有趣的问题：如果 `car` 和 `timemachine` 都有 `refuel()` 函数会发生什么？答案是 Python 根据你列出父类的顺序选择正确的函数使用。在之前的代码中，我们使用 `class delorian(car, timemachine)`，这意味着“继承自 `car` 然后继承自 `timemachine`”。因此，如果两个类都有 `refuel()` 函数，Python 会选择 `car.refuel()`。

当涉及更进一步的继承时，这种情况变得更复杂。也就是说，如果 `car` 从 `vehicle` 继承其 `refuel()` 方法，Python 仍然会选择它。幕后发生的事情是，Python 选择你继承的第一个类，并在该类和所有其父类中搜索匹配的方法调用。如果没找到，它会去下一个类并检查它及其父类。这个过程重复直到找到一个具有所需方法的类。

### 标准库与帕纳索斯宝库

默认的 Python 安装包括许多模块（代码块），允许你与操作系统交互、打开和操作文件、解析命令行选项、执行数据哈希和加密等。这是人们被问及为何喜欢 Python 时最常引用的原因之一——它一安装就具备大量你可以立即利用的功能。事实上，标准库中包含的模块数量如此之多，以至于专门有人撰写了整本书来描述它们——请参阅《Python Standard Library》（O'Reilly，ISBN: 0-596-00096-0），这是一份全面但略显过时的模块列表。

对于非官方的 Python 脚本和插件，推荐的起始位置是所谓的帕纳索斯宝库（Vaults of Parnassus）：http://py.vaults.ca。在那里你可以找到约 20,000 个公开脚本和代码示例，涵盖从数学到游戏的各个方面。

### 参考资料

Python 网站（http://www.python.org）信息丰富且定期更新。这应该是你的第一站，哪怕只是为了阅读最新的 Python 新闻。检查其他有用的网站：

- http://www.zope.org —— Zope 内容管理系统（CMS）的主页，它是周围最受欢迎的 CMS 之一，更重要的是，完全用 Python 编写。
- http://www.jython.org/ —— Python 还有一个优秀的基于 Java 的解释器，允许它在其他平台上运行。如果你更喜欢微软的 .NET，请尝试 http://www.ironpython.com。
- http://www.pythonline.com —— Guido van Rossum 从《蒙提·派森飞行马戏团》中借用了语言的名字，因此许多 Python 代码示例使用了斜向的蒙提·派森参考。访问官方蒙提·派森网站以提升你的 Python 知识是高度推荐的！

关于 Python 的优秀书籍很少；然而，你可以在 http://www.python.org/moin/PythonBooks 找到提供列表。如果你急于立即拿起一本书，选择《Learning Python》（O'Reilly，ISBN: 0-596-00281-5）错不了多少。

## 第 31 章：编写 PHP 脚本

本章向你介绍 PHP 编程的世界，从将其用作 web 脚本语言和命令行工具的角度出发。PHP 最初代表 personal home page（个人主页），因为它是一组 Perl 脚本，旨在简化创建访客簿、消息板和其他常见于主页的交互式脚本。然而，自那些早期日子以来，它经历了两次重大更新（PHP 3 和 PHP 4），加上 PHP 5 的重大修订，这是 Fedora 捆绑的版本。

PHP 成功的一部分在于它与数据库的强大集成——其最早的使用几乎总是利用数据库后端。然而，在 PHP 5 中，引入了两种新的数据存储机制：SQLite，这是一种强大且本地的数据库系统，以及 SimpleXML，这是一种旨在简化 XML 解析和查询的 API。随着时间推移你会发现，PHP 开发者做得很好，因为 SQLite 和 SimpleXML 都容易学习和使用。

如果你之前使用过 PHP 5 之前的版本，你应该知道面向对象系统发生了重大演变，我们强烈建议你阅读“对象导向”部分。

**注意**
PHP 的安装包属于“添加/删除应用程序”中的 Web 服务器类别。基本包仅称为 php，但你可能还想添加扩展，如 php_idap、php_mysql 或 php_pgsql。只选择你打算使用的扩展；否则，它将浪费系统资源。

### 本章内容

- PHP 简介
- 基本函数
- 对象导向
- 处理 HTML 表单
- 数据库
- 参考资料

## 引言到 PHP

就外观而言，PHP 是 Java 和 Perl 的结合，成功地将两者的最佳方面合并为一种语言。Java 部分包括强大的对象导向系统、抛出程序异常的能力，以及两种语言都从 C 借用的通用编写风格。从 Perl 借来的是“它应该就能工作”的心态，其中易用性优于严格性。因此，你会发现 PHP 中有许多“不止一种方法来做这件事”。

如果你没有使用 PHP 的先前经验，接下来的五个部分正是为你准备的：如何开始和停止 PHP 处理、使用变量、执行操作、控制程序流以及处理多个文件。如果你有较多经验，可以跳过到“基本函数”部分。

### 进入和退出 PHP 模式

与 PHP 的前身不同，你将 PHP 代码嵌入 HTML 内部，而不是相反。在 PHP 之前，许多网站对大多数内容使用标准 HTML 页面，在需要时链接到 Perl CGI 页面进行后端处理。使用 PHP 时，你所有的页面都能处理和包含 HTML。

每个 .php 文件由 PHP 处理，查找要执行的代码。PHP 认为它找到的所有文本都是 HTML，直到它发现以下四种情况之一：

- `<?php`
- `<?`
- `<%`
- `<script language="php">`

第一种方法是进入 PHP 模式的推荐方式，因为它保证能工作。第二种方法称为短标签，默认禁用，如果你同时提供 XML 文档和 PHP，也可能导致问题。第三种方法称为 ASP 标签，因为它模仿微软 ASP 进入代码块的方式——这很少使用。最后一种方法是最后的选择，如果你使用不喜欢 `<?php` 的奇异代码生成器——它看起来像是用于封装 JavaScript 的相同脚本块，大多数编辑器会保留原样。

你可以随时进入和退出 PHP 模式，尽可能频繁地这样做，并且——与流行信念相反——在 HTML 模式下打印你的 HTML 或在 PHP 模式下打印它之间几乎没有速度差异。

一旦进入 PHP 模式，你可以使用 `?>`（对于 `<?php` 和 `<?`）；`%>;`（对于 `<%>`）或 `</script>`（对于 `<script language="php">`）退出。此代码示例演示了进入和退出 PHP 模式：

```html
In HTML mode
<?php
   echo "In PHP mode";
```
