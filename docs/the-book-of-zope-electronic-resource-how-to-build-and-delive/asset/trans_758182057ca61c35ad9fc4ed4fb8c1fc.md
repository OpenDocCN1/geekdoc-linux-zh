

在上方的方法定义中，第 2 行和第 5 行属于方法体，第 3 行和第 4 行属于 for 循环体。

## 13.5 类与方法

接下来的部分将展示如何定义带有自定义属性和方法的类，以及如何派生（或实例化）对象。还将介绍继承原则。

### 13.5.1 示例：创建类

类定义之前使用 `class` 关键字，如下所示：

```python
class animal:
```

类定义之后可以紧跟一个构造方法：`__init__()`（两边有两个下划线）。每当创建类的实例时，都会调用该构造方法，它通常用于将新实例设置成初始状态。例如，可以在构造方法中初始化实例变量，并在必要时用它们设置初始值，如列表 13-2 所示。`def` 语句定义了一个 Python 方法。

列表 13-2：带有构造方法 `__init__` 的 Animal 类

```python
class animal:
    # Animal Class
    def __init__(self, age, gender):
        """Constructor Method"""
        self.age=age
        self.gender=gender
        self.awake=1
```

列表 13-2 所示构造方法表示，每个 Animal 类的实例必须提供年龄和性别（第 3、5 和 6 行）。此外，每个参数都被自动视为清醒状态（第 7 行）。

构造方法的第一个参数是 `self`，Python 通过它将类的当前实例传递给方法。当方法需要检查或操作类的当前实例时，你可以像第 5 行到第 7 行那样使用 `self` 参数，我们在那里为实例分配了三个新属性。`self` 参数位于方法参数列表的第一位；Python 在调用它时会自动传递此参数。

第 2 行和第 4 行包含一个特殊的注释，称为 doc string（文档字符串），它描述了类和方法。三引号字符串通常紧跟在类或方法之后（如上方的第 4 行所示），以便在必要时指定多行 doc string。类方法若要从 Zope 访问，doc string 是强制性的；如果不包含，当你尝试从 Zope 调用它时，将会显示错误信息。

列表 13-3 可以用作 Animal 类的更多方法。

列表 13-3：Animal 类的 `sleep()` 和 `wakeUp()` 方法

```python
def sleep(self):
    """The animal is sleeping"""
    self.awake=0
    print 'ZZZZZ'
def wakeUp(self):
    """The animal is awake"""
    self.awake=1
```

到此时，我们对 Animal 类做不了什么，只能创建具有名称和性别、且处于清醒或睡眠状态的 Animal 对象。这对真实动物世界的描述还不够详细。

### 13.5.1 创建子类

为了更好地表示真实的动物世界，我们需要创建子类，它们继承自基类。子类继承基类的属性，并允许我们添加新的属性。通过*继承*，我们可以实现。

Reptile 类定义如列表 13-4 所示。

列表 13-4：继承 Animal 类的 Reptile 类

```python
class reptile(animal):
    """Reptiles"""
    def swim(self):
        """The reptile swims"""
        if self.awake:
            print 'paddle splash'
```

Bird 类定义如列表 13-5 所示。

列表 13-5：继承 Animal 类的 Bird 类

```python
class bird(animal):
    """Bird"""
    def fly(self):
        """The bird flies"""
        if self.awake:
            print 'flap flutter'
```

### 13.5.2 实例化

要实例化，我们使用类名后跟括号。例如：

```python
my_animal = animal(5, 'female')
```

一旦有了实例，我们可以通过点符号访问它的属性：

```python
print my_animal.age
print my_animal.gender
```

我们还可以调用实例的方法：

```python
my_animal.sleep()
my_animal.wakeUp()
```

## 14 使用 Python 脚本

Zope 提供了两种 Python 函数集成到 Zope 中的方法：Python 脚本和外部方法。通过本章介绍的技术，可以在 Zope 中编写复杂的逻辑，例如 DTML 文档。

### 14.1 Python Python 脚本

Python 脚本是 Zope 2.3 及更高版本的特性。它们允许你通过管理界面直接在 Zope 中包含 Python 代码，类似于 DTML。尽管对访问的内置函数和 Python 模块有一些限制，但 Python 脚本是为 Zope 应用编写复杂逻辑的一种强大方式。

Python 脚本无法执行的操作包括访问文件系统文件、调用系统程序、导入任意模块以及调用受限的方法。要执行这些操作，你仍需要使用外部方法或 Python 产品（见 14.2 节和第 15 章）。但是你可以调用任何其他未限制的方法或对象，进行复杂的计算或数据处理，并导入特定的 Python 模块。

### 14.1.1 创建 Python 脚本

你可以像创建其他 Zope 对象一样，通过文件夹菜单创建 Python 脚本；在菜单中选择 Script (Python)。在出现的表单上指定 id、可选标题以及包含要上传到脚本的 Python 代码文件。然后点击 Add 按钮创建脚本对象，如图 14-1 所示。

创建脚本后，你应该看到图 14-2 所示的管理界面。前三个管理界面标签页——Edit（编辑）、Bindings（绑定）和 Test（测试）是 Python 脚本特有的。

