
对象的成员通过点 `()` 表示法访问；例如，如果 `myCar` 是 `Car` 类的实例，则通过类似 `myCar.getModel()`、`myCar.getCylinders()` 等代码访问方法。从示例中可以看出，当前对象实例是通过 `this` 关键字来引用的，它作为自身的引用。

由于 Java 是一门面向对象的语言，人们会期望从现有类派生出新类。从基类或父类派生新类的类被称为派生类。从基类派生的新类被称为派生类或子类。从父类派生子类的过程被称为继承，子类被称为扩展 `extend` 父类。理解继承的规则（或特征）以及子类与父类之间的关系，对于设计我们的应用程序和更好地理解第三方程序非常重要。子类可以访问父类的 `public` 和 `protected` 成员，而父类的 `private` 成员对其自身保持私有。因此，与 `public` 和 `private` 成员相比，父类的 `protected` 成员提供了中间级别的访问。当子类扩展父类时，父类的所有 `public` 和 `protected` 成员都可以通过点 `.` 自动可用。通常情况下，父类的数据成员是 `private` 的（约定），它们在子类中无法直接访问；但只能通过 `protected` 和 `public` 方法访问。如果父类定义了某些数据成员，它们在子类中无法直接访问；但只能通过 `protected` 和 `public` 方法访问。

关于继承，以下场景需要记住：

- 子类可以访问父类的 `public` 和 `protected` 成员，而父类的 `private` 成员对其自身保持私有。
- 因此，与 `public` 和 `private` 成员相比，父类的 `protected` 成员提供了中间级别的访问。
- 当子类扩展父类时，父类的所有 `public` 和 `protected` 成员都可以通过点 `.` 自动可用。
- 通常，父类的数据成员是 `private` 的（约定），它们在子类中无法直接访问；但只能通过 `protected` 和 `public` 方法访问。
- 如果父类定义了某些数据成员，它们在子类中无法直接访问；但只能通过 `protected` 和 `public` 方法访问。
- 默认情况下，所有方法和全局变量是非静态 `nonstatic` 的，这意味着类的每个实例都拥有自己的这些方法和全局变量的拷贝。有时需要为类的所有对象维护一个变量拷贝。当在应用程序中创建多个方法或全局变量拷贝是不合理的，或者我们可能需要在不实例化的情况下执行方法时。考虑以下方法：

```java
public void processEnginePower(java.lang.Object vehicle) {
  Car car = (Car)vehicle;
}
```

- 在上述方法中，`vehicle` 是 `java.lang.Object` 或其子类的实例。然而，在方法的文中，预计该对象代表汽车类，因此将本地对象引用赋值给右侧的强制转换。然而，如果输入参数不代表汽车类，该操作将导致运行时错误。这种情况不会引发编译时错误，因为在程序执行之前无法确定转换是否成功或失败。在运行时确定（或转换）对象类型的过程称为晚绑定 `late binding`。
- 如果一个类被声明为 `final`，意味着它应该是层级结构中的最后一个类且不被扩展。这意味着 `final` 类永远不能作为父类。

# 企业级 Linux 应用开发

是该类的对象。此类方法和变量被显式地声明为静态 `static`。正如此处提到的，只有静态方法可以从类被调用（使用类名的点表示法），而无需实例化该类的对象。在适当的地方使用静态方法和全局变量无疑有助于提高性能，因为避免了不必要的重复。静态变量也被称为类变量，因为它们的作用范围在类级别，而不是对象级别。另一方面，非静态变量被称为实例变量，因为它们的作用范围在实例级别。静态变量和方法是隐式的最终的 `final` 的，因为它们在创建后就不会发生改变。需要注意的是，静态方法不能在其代码中调用非静态方法，因为非静态方法只能在实例上执行，而不能在类上执行。例如，我们为了执行垃圾回收而调用的 `System.gc()` 方法就是一个公共静态方法。这里给出了静态变量和静态方法的示例声明。

```
static String myName = "Satya Sai Kolachina";
public static void updateStatus(java.lang.String status) {
...
..
...
}
```

虽然一个类的私有方法也是隐式的最终的，因为它们不能在子类中被重写，但私有变量并不是隐式的最终的，因为它们可以在类的任何地方被更改。

声明为抽象的类不能被实例化，类层次结构中的若干层级可以是抽象的。另一方面，可以实例化为对象的类被称为具体类 `concrete classes`。类层次结构中并不一定需要抽象类。然而，通过使用抽象类来实现多态行为非常有帮助。尽管抽象类不能实例化，但我们可以创建指向这些类的引用，以泛化层次结构中更具体的类。例如，如果 `vehicle` 是一个带有两个子类 `Car` 和 `Truck` 的抽象类，则对 `vehicle` 类的引用可以用来访问 `Car` 对象或 `Truck` 对象。类的一个方法可以写成接收 `Vehicle` 对象的引用作为输入参数，而该方法的调用实际上可能会接收一个 `Car` 对象或一个 `Truck` 对象。这是利用 Java 语言多态行为的示例。同样，该方法可以返回一个 对象给调用者程序。需要处理该对象的程序在尝试访问该对象之前，必须像之前讨论的那样，将其强制转换为相应的类型（`Car` 或 `Truck`）。

## 面向对象编程 253

抽象类包含一个或多个抽象方法。存在至少一个抽象方法意味着该类必须声明为抽象的。抽象类也可以有一个或多个非抽象方法、实例变量和构造函数。扩展抽象类的子类必须重写父类的抽象方法，而不需要重写非抽象方法。抽象父类中那些未被子类扩展的非抽象方法将为子类提供默认实现。由于抽象类必须被子类扩展，因此它们不能被声明为最终的 `final` 的。

当一个方法在抽象父类中被声明为抽象的时，它为子类提供自己的实现留下了灵活性，支持了类层次结构中的多态行为。将方法声明为抽象的表示其实现仅在子类中可用。由于抽象类和晚绑定 `late binding` 是密不可分的，它简化了在类层次结构中添加新成员的过程。

之前提到过 Java 不支持多继承，而 C++ 支持多的。那么，将多个类的行为继承到子类的机制是什么？Java 提供的解决方案是使用接口 `interfaces`。接口是对象应该如何行为的定义。因为对象的行为是通过其方法识别的，所以接口定义包含一个或多个没有实现的方法签名。当子类通过 `extends` 扩展一个父类（或仅一个父类）以继承其特征时，它实现一个或多个接口。注意 `extends` 和 `implements` 关键字。当一个类实现接口时，意味着它同意向世界其他部分提供接口承诺的行为。这意味着实现类必须实现接口定义中声明的每一个方法，否则该类无法编译。每个实现接口的类都可以对从接口定义中继承的方法有自己的实现。考虑以下与我们经典示例相关的接口定义。

```
public interface PowerTransmission {
    public void transmitPower();
}
```

```java
public class Car extends Vehicle implements PowerTransmission {
    public void transmitPower() {
        ..
    }
}
```

```
public class Truck extends Vehicle implements PowerTransmission {
    public void transmitPower() {
        ..
        ..
    }
}
```

```java
public class Ship extends Vehicle implements PowerTransmission {
    public void transmitPower() {
        ..
        ..
    }
}
```

```java
public class Plane extends Vehicle implements PowerTransmission {
    public void transmitPower() {
        ..
        ..
    }
}
```

```java
public class SewingMachine extends Vehicle implements PowerTransmission {
    public void transmitPower() {
        ..
        ..
    }
}
```
