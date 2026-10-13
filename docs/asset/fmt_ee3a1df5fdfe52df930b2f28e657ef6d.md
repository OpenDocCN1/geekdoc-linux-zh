
所以，狗的默认颜色是棕色——`fluffy` 和 `poppy` 这两个 `dog` 对象最初都是棕色的。然后，使用 `dog.color`，我们将默认颜色设置为黑色，由于这两个对象都没有设置自己的颜色值，它们被更新为黑色。倒数第三行使用 `poppy.color` 为 `poppy` 对象设置自定义颜色值——`poppy` 变为黄色，但 `fluffy` 以及整体上的 `dog` 类仍然保持黑色。

## 构造器和析构器

为了帮助自动创建和删除对象，你可以轻松覆盖两个默认方法：`__init__` 和 `__del__`。这些方法分别被称为构造器（constructor）和析构器（destructor），是 Python 在类被实例化和释放时调用的方法。

当你需要为每个正在创建的对象接受一组参数时，拥有自定义构造器是非常好的。例如，你可能希望每只狗在创建时拥有自己的名字，你可以用以下代码实现：

```python

class dog(object):

 def __init__(self, name):

  self.name = name

fluffy = dog("Fluffy")

print fluffy.name

```

如果在创建 `dog` 对象时不提供 `name` 参数，Python 会报告错误并停止。当然，你可以要求任意多的构造器参数，但通常最好只请求需要的参数，并使用其他函数来填充其余部分。

另一方面是析构器方法，它允许你在对象被销毁时拥有更多的控制权。结合这两者，我们可以通过在对象创建和删除时打印消息来展示对象的生命周期：

```python

class dog(object):

 def __init__(self, name):

  self.name = name

  print self.name + " is alive!"

 def __del__(self):

  print self.name + " is no more!"

fluffy = dog("Fluffy")

```

析构器存在的意义在于给你机会释放分配给对象的资源，或者将某些内容记录到文件中。

## 类继承

Python 允许你通过从一个或多个其他类继承来重用代码。例如，狮子、老虎和熊都是哺乳动物，因此共享许多相似属性。在那种场景中，你不想在它们之间复制粘贴函数；拥有定义所有共享功能的 `mammal` 类，然后让每种动物继承自该类，会更聪明（也更容易！）。

考虑以下代码：

```python

class car(object):

    color = 'black'

    speed = 0

    def accelerateTo(self, speed):

        self.speed = speed

    def setColor(self, color):

        self.color = color

mycar = car()

print mycar.color

```

这创建了一个带有默认颜色的 `car` 类，并提供了一个 `setColor()` 函数，以便人们可以更改自己的颜色。现在，你开车去上班坐的是什么？是一辆车？是的，但很可能是一辆福特（Ford）、道奇（Dodge）、吉普（Jeep）或其他品牌——没有品牌就没有车。另一方面，你也不想定义一个 `ford` 类，给它 `accelerateTo()`、`setColor()` 以及基础 `car` 所拥有的其他任何方法，然后对法拉利（Ferrari）、日产（Nissan）等做完全相同的事情，对吧？

解决方案是使用继承：定义一个包含所有品牌共享函数和变量的 `car` 类，然后继承自它。在 Python 中，你通过在类声明的括号内放入要继承的类名来实现这一点，例如：

```python

class car(object):

    color = 'black'

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

`pass` 指令是一个空语句——它意味着我们的类中没有包含任何新内容。然而，由于 `ford` 类和 `nissan` 类继承自 `car` 类，它们自动获得了父类提供的 `color`、`speed`、`accelerateTo()` 和 `setColor()`。请注意，对于 `ford` 和 `nissan`，我们在类名后面不需要加 `object`，因为它们是从一个现有的类（`car`）继承而来的。

默认情况下，Python 会赋予子类父类拥有的所有方法，但你可以通过为需要这些方法的类提供新的实现来重写（override）这些方法。例如：

```python

class modelt(car):

    def setColor(self, color):

        print "Sorry, Model Ts only come in black!"

myford = ford()

ford.setColor("green")

mycar = modelt()

mycar.setColor("green")

```

第一辆车被创建为福特（Ford）车型，因此 `setColor()` 工作正常，因为它使用的是 `car` 类中的方法。然而，第二辆车被创建为 `modelt` 车型，该车型拥有自己独立的 `setColor()` 方法，因此调用会失败。

这提供了一个有趣的场景：如果你已经重写了某个方法，但仍然希望调用父类的方法，该怎么办？例如，如果允许更改 Model T 的颜色，但只是需要额外付费，我们希望打印一条消息说：“您还需支付 50 美元”，然后变更颜色。为此，我们需要使用当前类所继承的那个类对象——在本例中即 `car`。以下是一个示例：

```python

class modelt(car):

    def setColor(self, color):

        print "You owe $50 more"

        car.setColor(self, color)

mycar = modelt()

mycar.setColor("green")

print mycar.color

```

这会打印出该消息，然后变更汽车的颜色。

## 多重继承

你可以继承任意数量的类，在构建过程中逐步增加功能。例如，你可以有一个 `anomaia` 类，一个子类 `chordata`，一个子子类 `mammalia`，以及一个子子子类 `homospapiens`。每一个都比其父类更具体。然而，Python 中一个有趣的新特性是支持多重继承——即同时从两个类中获取功能。

再次说明，这最好通过代码来展示：

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
