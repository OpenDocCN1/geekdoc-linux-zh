
## 封装行为

如果我们无法添加新帖子，博客就不成其为博客，所以让我们这样做：

```
>>> blog = blog + ['A new post.']
>>> blog
['My first post', 'Python is cool', 'A new post']
```

在这里，我们将 blog 设置为一个新值，该值由旧的博客和一个新帖子组成。仅仅为了添加一个新帖子而记住所有内容并不令人愉快，因此我们可以将其封装在所谓的函数中：

```
>>> def add_post(blog, new_post):
...      return blog + [new_post]
...      
>>>
```

`def` 是用于定义新函数或方法的关键词（关于结构化或函数式编程中的函数以及面向对象编程中的方法，我们将在本文稍后部分详细介绍）。接下来是函数的名称。在括号内，我们有形式参数。这些类似于将由函数调用者定义的变量。在冒号之后，提示符从 `>>>` 变为 `...`，以表明我们位于定义内部。函数由所有这些行组成，其缩进级别位于 `def` 行下方。

因此，在其他编程语言使用花括号或 `begin`/`end` 关键词的地方，Python 使用缩进。其理念是，如果你是一名优秀的程序员，你本来就会进行缩进，所以我们将利用这种缩进，同时使你成为一名优秀的程序员。确实，这是一个有争议的问题；我一开始并不喜欢它，但我学会了与之共存。

在使用 REPL 时，你可以安全地按下 Tab 键以创建一个缩进级别。虽然 Tab 字符可以完成此操作，但使用四个空格是强烈推荐的规范。许多文本编辑器在编辑 Python 文件时按下 Tab 键都知道要插入四个空格。无论你怎么做，我强调一遍，永远不要将 Tab 和空格混用。在其他编程语言中，这可能会让社区讨厌你，但在 Python 中，这会导致你的程序因奇怪的错误消息而失败。

为了实用起见，要重现我所做的操作，只需输入类标题 `def add_post(blog, new_post)`，按 Enter，按 Tab，输入 `return blog + [new_post]`，按 Enter，再按一次 Enter，就完成了。让我们看看函数的实际效果：

```
>>> blog = add_post(blog, "Fourth post")
>>> blog
['My first post', 'Python is cool', 'A new post',
 'Fourth post']
>>>
```

`add_post` 接受两个参数。第一个是博客本身，它被赋值给 `blog`。这有点棘手。函数内部的 `blog` 与函数外部的 `blog` 不是同一个对象。它们处于不同的作用域中。这就是为什么以下代码：

```
>>> def add_post(blog, new_post):
...      blog = blog + [new_post]
```

不起作用。`blog` 仅在函数内部被修改。到现在为止，你应该知道 `new_post` 包含传递给函数的帖子。

我们的博客正在增长，是时候看到帖子仅仅是字符串，但我们要拥有一个标题和一个正文。实现这一点的一种方法是使用元组，如下所示：

![](img/526fd434dcfcf1b461b94c24ea170f36_53_0.png)

```
>>> blog = []
>>> blog = add_post(blog, ('New blog', 'First post'))
>>> blog = add_post(blog, ('Cool', 'Python is cool'))
>>> blog
[('New blog', 'First post'),
 ('Cool', 'Python is cool')]
>>>
```

在第一行，我将博客重置为空列表。然后，我添加了两个帖子。看到双重括号了吗？外面的括号是函数调用的一部分，里面的括号是创建元组。元组由括号创建，其成员由逗号分隔。它们类似于列表，但语义上不同。例如，你不能更新元组的成员。元组用于构建具有固定元素集合的某种结构。让我们看看我们博客之外的一个元组：

```
>>> (1, 2, 3)
(1, 2, 3)
```

访问帖子的每个部分类似于访问博客的每个部分：

```
>>> blog[0][0]
'New blog'
>>> blog[0][1]
'This is my first post'
```

如果我们只想存储标题和正文，这可能是一个很好的解决方案。但是，我们多久会想添加日期和时间、摘要、标签或消息呢？你可能开始觉得需要在墙上挂一张纸，如图中 1 所示，以记住每个字段的索引——这一点也不令人愉快。为了解决这个问题和其他一些问题，Python 为我们提供了面向对象编程。

## 面向对象编程

面向对象编程诞生于 20 多年前，使开发人员能够以类似现实世界中对象分离的方式，将计算机程序的每个部分分开。Python 通过使用类来建模对象。类是对象拥有什么以及对象能做什么的抽象定义。如果觉得这听起来陌生，别担心，面向对象编程（OOP）一开始很难。

一个例子可能会有帮助。桥是一种结构，允许人或车辆跨越障碍物，如河流、运河或铁路。桥有一定的长度、宽度，甚至高度。它可能允许车辆或仅允许行人。它可能允许重型车辆或不允许。当我说“桥”时，我并没有定义其中任何细节。桥是一个类。如果我说金门大桥、诺曼底大桥或明石海峡大桥，我是在命名特定的桥梁；它们具有特定的长度、宽度、车辆通行许可和颜色。用 OOP 术语来说，它们是桥的实例。

回到我们的博客，让我们创建一个类来建模我们的帖子：

```python
>>> class Post(object):
...     pass
>>> 
>>> 
```

我们从 `class` 开始，这是创建新类的关键词。接下来是类的名称——在本例中为 `Post`。在括号内，我们有超类——暂时忽略它。

再次，提示符从 `>>>` 变为 `...`，Python 期望在类中放入*某些东西*。因为我们暂时不想放任何内容，所以我们写 `pass`，它代表“某些东西”，但事实上它什么也不做。Python 通过缩进来知道类何时开始和结束，这与函数相同。

要重现我所做的操作，只需输入类标题 `class Post(object):`，按 Enter，按 Tab，输入 `pass`，按 Enter，再按一次 Enter，就完成了。

现在，我们可以创建一个 Post：

```python
>>> cool = Post()
>>> cool
<_main__.Post object at 0xb7c6642c>
```

注意，当我们评估一个帖子时，打印出来的是对象的通用表示。我们可以设置它的标题和正文：

```python
>>> cool.title = "Cool"
>>> cool.body = "Python is cool."
```

并获取它们：

```python
>>> cool.title
'Cool'
>>> cool.body
'Python is cool.'
```

到目前为止，Post 就像一个简单的容器，你可以想象放入任何内容。这样做的缺点是，我们可能会迷失关于该放什么或不放什么。回到那张纸吗？不！虽然我们不能再通过那种方式让帖子变成容器，但我们可以放入一些方法，让用户对帖子可能包含什么有一个概念。为此，我们在类 Post 中编写了自己的方法：

```python
>>> class Post(object):
...     def set_title(self, title):
...         self._title = title
...     def get_title(self):
...         return self._title
... 
```

## 面向开源社区的硬件系统
**自 1989 年起**
(Linux, FreeBSD, NetBSD, OpenBSD, Solaris, MS, 等)

AMD Opteron™ 处理器为最先进的应用程序提供高性能、可扩展的服务器解决方案。可以同时运行 32 位和 64 位应用程序

- **AMD Opteron 价值服务器 - $795**
  1U 14.3” 深
  AMD Opteron 140 1M 缓存
  1 GB DDR2 ECC REG PC-3200
  1 个 2 个 40GB SATA 硬盘之一
  2 X 10/100/1000 NIC
  选项：CD、FD 或第二块硬盘、Raid
  添加您的标志

- **iSCSI 双 AMD Opteron 1U 至 8U，请询价**
  1TB 至 30TB iSCSI 存储
  双 AMD Opteron 266
  1 GB DDR2 ECC REG PC-3200
  双 GigE：LAN
  冗余电源，热插拔硬盘
  RAID 选项，RAID 5, 10, 50
  可提供更多定制

![](img/526fd434dcfcf1b461b94c24ea170f36_54_0.png)

- **1U SCSI 四核 AMD Opteron - (Rev.f) 起始价 $5293.20**
  1 个 4 个 AMD Opteron 8212 CPU 之一
  12 GB DDR2 ECC REG PC-3200
  1 个 2 个 74GB SCSI 硬盘之一
  2 GigE, CD, FD
  可选远程管理卡 (PMM)
  请就更多 AMD socket F 服务器选择进行询价。

- **30TB AMD Opteron 存储解决方案 - 起始价 $26,395**
  8U 中的 30TB SATA 存储
  包含所有 Raid 卡，Raid 5, 10
  双 AMD Opteron 246
  2 GB DDR2 ECC REG PC-3200
  双 GigE, FD, CD

![](img/526fd434dcfcf1b461b94c24ea170f36_54_1.png)

![](img/526fd434dcfcf1b461b94c24ea170f36_54_2.png)

## 您的定制设备解决方案
告诉我们您的需求，我们将为您提供解决方案

![](img/526fd434dcfcf1b461b94c24ea170f36_54_3.png)

## 定制服务器、存储、集群等解决方案
请就所有类型的存储解决方案、NAS、DAS、iSCSI、光纤 RAID、SATA、SAS 与我们联系。

*部分服务器和所有笔记本电脑免费送货*

![](img/526fd434dcfcf1b461b94c24ea170f36_54_4.png)

![](img/526fd434dcfcf1b461b94c24ea170f36_54_5.png)

2354 Calle Del Mundo, Santa Clara, CA 95054
www.asacomputers.com
邮箱：sales@asacomputers.com
电话：1-800-REAL-PCS | 传真：408-654-2910

价格和可用性可能随时变更，恕不另行通知。不对排版错误负责。所有品牌名称和标志均为其各自公司的商标。

