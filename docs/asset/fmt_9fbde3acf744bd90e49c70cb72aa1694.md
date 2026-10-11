
```python
        self.body = body
```

### 发布还是不发布

`get_posts` 方法返回所有文章。当我们写新文章时，我们不希望全世界在完成之前都能阅读它。文章不需要一个新的成员来告诉我们是否已发布。在 `Post` 初始化函数 `__init__` 中，我们添加：

```python
    def set_title(self, title):
        self.title = title
```

```python
    def get_title(self):
        return self.title
```

```python
    self._published = False
```

这使得每篇新文章默认都是私有的。为了切换状态，我们

```python
    def set_body(self, body):
        self.body = body
```

```python
    def get_body(self):
        return self.body
```

```python
    def get_publish(self):
        self._published = True
```

```python
    def hide(self):
        self._published = False
```

```python
    def __repr__(self):
        return "Post: %s" % self.title
```

```python
    def is_published(self):
        return self._published
```

在后续中，让我们专注于博客并进一步。

在这些方法中，我引入了一个新变量——布尔值，它可以是真或假。为了配合 `that` 使用它：

### 博客

现在我们有了文章，可以创建 `Blog` 类了。初始实现可能如下：

```python
>>> cool = BlogPost('Cool', 'Python is cool')
>>> cool.is_published()
False
>>> cool.publish()
>>> cool.is_published()
True
>>> cool.hide()
>>> cool.is_published()
False
```

```python
class Blog(object):
    def __init__(self, post):
        self.posts = [post]
```

```python
    def add_post(self, post):
        self.posts.append(post)
```

```python
    def get_posts(self):
        return self.posts
```

我们正在使用列表来维护文章，但接口是完全抽象的，巨大的优势是：我们可以用整个列表替换 SQL 查询，而代码需要很少 `if` 语句。

如果，当你进行规则判断时，你可以看到：

```
Traceback (most recent call last):
  File "stdin.py", line 3, in <module>
    File "blog.py", line 25, in is_published
    return self._published
AttributeError: 'Post' has no attribute '_published'
```

注意，没有删除文章的方法。配合 `_posts`，但只要 `published` 被创建，它就可以使用，并且想要。各种类型的错误，一种是 `AttributeError`。`traceback` 给了很多信息。`traceback` 并没有提供太多信息，可能与你在 REPL 中输入的行有关。第二行显示了问题。另一个例子在大项目中可能有调用方法等等。在这些情况下，看到 `tracebacks` 超过 50 行并不罕见，下一步是修改 `Blog` 类来选取所有文章。

```python
def get_published(self):
    published_posts = []
    for post in self.posts:
        if post.is_published():
            published_posts.append(post)
```

Python 尽可能的可读，但这需要仔细的解释。

### 循环

Python 的构造之一是 `for`。它被设计用于遍历列表、集合和其他迭代对象。在这种情况下，它执行循环体。`while` 循环构造比 `for` 有用得多。但今天，有了强大的构造，如 `range` 函数，将迭代器周围的使用比 `while` 高得多。这里是为你旅程的一个例子：

```python
for i in range(3):
    print i
```

这更短，而且更可读。`for` 循环有什么用？它有助于知道何时停止循环。这里是一些例子：

- 从文件读取字符直到遇到末尾 (EOF)。
- 从用户处读取命令直到用户按键。
- 从传感器读取次数直到温度太高。
- 从用户界面读取事件直到用户按下窗口底部的按钮关闭程序。

这里形成了一个模式——做其他事情是我们需要的。以前，当语言中没有选择时，我们使用 C 顶层的时间时间，这种构造比 `for` 有用得多。循环作为迭代器的可能性。这里是你的旅程的一个例子：

```python
for i in "Hello World":
    print i

Hello World
```

### 条件

在某些示例代码的第四行 `if post.is_published():`，我们有了另一个新构造——`if`。这允许程序根据数据做出选择。它需要一个布尔值和一段代码。代码只有在为 `True` 时才运行。如果你提供不是真的东西，Python 会尽力将其解释为。例如，数字 0 被解释为 `False`，但所有其他数字都被解释为 `True`。这里是一些例子：

```python
>>> True:
    print "It is true!"

>>> False:
    print "It is false?"
```

我们可以对不同类型的对象执行许多不同的比较。注意相等运算符是 `==`，而不是 `=`（即两个等号）：

```python
>>> a = 10
>>> if a == 10:
    print "Ten!"
```

十！还有其他比较，比如大于 (>)、小于 (<) 和不同于 (!)。你可以直接在 REPL 上实验比较：

```python
>>> a = 3

False

>>> a != 10

True

>>> a > 1

True
```

如果某事为真运行一段代码，为假运行另一段代码是常见的。例如，我们可以这样做：

```python
if a == 10:
    print "A is ten"

elif a != 10:
    print "A is not ten."
```

这是一个问题。如果我们在第一种情况下将 `a` 改为 `b`，我们必须记得在第二种情况下也修改。以及我们做的任何其他更改。解决方案是对此的扩展：

```python
if a == 10:
    print "A is ten"
else:
    print "A is not ten."
```

如果第一部分没有执行，将执行后面的代码。

另一种常见情况是为不同情况设置条件。在这种情况下，我们可以使用一系列：

为了这样做，我们使用 `while`：

```python
>>> a = 0
>>> while a < 3:
...     print a
...     a = 1
```

各种任务通过循环解决。一种任务是执行三次。

```python
>>> list = [1,2,"a","b"]
>>> for item in list:
...     print item

1

2

a

b
```

### 深入

### 继承

椅子是家具。桌子也是。这种相似性

76 | 2007 www.linuxjournal.com

位于 `Furniture` 类中。让我们让 `Furniture` 类拥有一个默认材料并具备设置其他材料的能力：

```python
class Furniture(object):
    def __init__(self):
        self.material = "wood"

    def set_material(self, material):
        self.material = material
```

现在，有一个继承 `Furniture` 的 `Chair` 类：
