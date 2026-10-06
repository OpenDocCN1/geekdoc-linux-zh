
`protected`:

    void resizeEvent(QResizeEvent *);

`private`:

    QLCDNumber *lcd;

    int value;

};

包含文件 `qwidget.h` 和 `qlcdnumber.h` 包含了 Qt 库中 C++ 类 `QWidget` 和 `QLCDNumber` 的定义。对于实际应用程序，`StateLCDWidget` 类通常会继承自 `QLCDNumber` 类，但为了演示如何定义槽函数的简单示例中，让 `StateLCDWidget` 继承自更简单的 `QWidget` 类并使用组合关系会稍微简单。`StateLCDWidget` 类包含一个 `QLCDNumber` 类实例。

在 `state_lcd.hxx` 文件中，我们看到一些看起来不合的代码：

```cpp
public slots:

    void increaseValue();

    void decreaseValue();
```

`Q_OBJECT` 符号导致 `moc` 工具生成所谓的“元对象协议”信息，允许在运行时检查对象以确定某些类属性。对元对象协议的支持内置在像 Common LISP/CLOS 等某些面向对象的编程系统中。Qt 的架构师基于对象运行时内省的思想构建，以便支持将代码绑定到特定对象的槽上，而不是该类的所有实例。

> 标记 `slots` 并不是 C++ 中的保留字。

C++ 编译器会会编译这段代码；`slots` 标记在 Qt 包含文件 `qwidget.h` 中被定义为空。当我们使用此小部件构建程序时，我们必须在 `Makefile` 中添加命令来运行 Qt 工具 `moc`，它会创建一个包含该类额外代码的新 C++ 源文件。在我们完成 `state_lcd` 文件中的 `StateLCDWidget` 类实现后，我们将再次查看 `moc`。我们需要两个包含文件来定义 `StateLCDWidget` 和 `LCDNumber` 小部件：

```cpp
#include "state_lcd.hxx"

#include <qlcdnumber.h>
```

类构造函数非常简单；它调用父类构造函数并创建一个 `LCDNumber` 类实例，在 `LCDNumber` 实例中指定了最多四位数字：

```cpp
StateLCDWidget::StateLCDWidget(QWidget *parent, const char *name)
: QWidget(parent, name) {
    lcd = new LCDNumber(4, this, "lcd");
}
```

需要 `resizeEvent` 方法通过调用 `LCDNumber` 类方法 `resize` 来处理大小调整事件：

```cpp
void StateLCDWidget::resizeEvent(QResizeEvent *) {
    lcd->resize(width(), height());
}
```

在这里，`width` 和 `height` 方法用于计算 `LCDNumber` 实例的大小。这些 `width` 和 `height` 指 `StateLCDWidget`；这些方法继承自 `QWidget` 类。类实现的其余部分是两个方法 `increaseValue` 和 `decreaseValue` 的定义，它们负责增减私有变量：

```cpp
void StateLCDWidget::increaseValue() {
    value++;
    lcd->display(value);
}
```

```cpp
void StateLCDWidget::decreaseValue() {
    value--;
    lcd->display(value);
}
```

现在我们将讨论类槽的创建和 Qt `moc` 工具。我们将涵盖在本节中定义的 `StateLCDWidget` 类和下一节中开发的 `UpDown` 类使用 `moc` 的情况。`Makefile` 中的以下规则规定了程序如何处理使用信号和槽的源码：

```makefile
moc_lcd.cxx: state_lcd.hxx
$(moc) state_lcd.hxx -o moc_state_lcd.cxx
moc_up_down.cxx: up_down.hxx
$(moc) up_down.hxx -o moc_up_down.cxx
```

假设 `(MOC)` 指向 Qt de二进制目录下 `moc` 工具的绝对路径。如果头文件发生变化，`moc` 会自动生成一个新的源文件（此处为 `moc_state_lcd.cxx` 和/或 `moc_up_down.cxx`）。`Makefile` 中的以下规则编译生成的源文件：

- `moc_state_lcd.o`: `moc_state_lcd.cxx` `state_lcd.hxx`
- `moc_up_down.o`: `moc_up_down.cxx` `up_down.hxx`

`Makefile` 包含了从 C 或 C++ 源文件构建 `.o` 文件的规则。`moc` 文件包含了小部件既声明槽又将信号绑定到其他小部件中包含的槽所需的代码。

## 使用信号和槽

我们在上一节中开发了 `StateLCDWidget` 类，作为一个定义了其他 Qt 小部件可以使用槽的类示例。在本节中，我们将开发另一个小部件类——`UpDownWidget`，它包含了 `StateLCDWidget` 类实例和 Qt `QPushButton` 类的实例。一个按钮的 `clicked` 信号将绑定到 `StateLCDWidget` 类的 `decreaseValue` 槽，另一个按钮的 `clicked` 信号将绑定到 `StateLCDWidget` 实例的 `increaseValue` 槽。

头文件 `up_down.h` 需要三个包含文件来定义 `QWidget`、`QPushButton` 和 `StateLCDWidget` 类：

```cpp
#include <widget.h>

#include <pushbutton.h>

#include "state_lcd.hxx"
```

## 运行信号/槽示例程序

我们已经开发了 `StateLCDWidget` 和 `UpDown` 小部件。`main.cxx` 文件包含一个简单的示例程序来测试这些小部件：

```cpp
#include <application.h>

#include "up_down.hxx"

int main(int argc, char **argv) {
  Application a(argc, argv);
  QWidget top;
  top.setGeometry(0, 0, 222, 222);
  UpDownWidget w(&top);
  w.setGeometry(0, 0, 220, 220);
  a.mainWidget(&top);
  top.show();
  return a.exec();
}
```

# 使用 Qt 进行 GUI 编程
第 31 章

只有顶层控件（Top-Level widget）必须使用 `show` 方法设置为可见。顶层控件中的任何控件也会随变得可见。图 31.2 显示了 `main.cpp` 中示例程序的运行。点击“向上”按钮会将数字显示的值加一；点击“向下”按钮则减一。

# 31 使用 Qt 编程

图 31.2
两个 Push Button 按钮控件的点击信号已连接到 StateConnection 控件中的槽函数。

![](img/69b363a7d7f58dc8d0b8c78c0052826f_582_0.png)

## 总结

用于 GUI 编程的 Qt C++ 类库提供了一系列丰富的控件，用于使用 C++ 语言构建 Linux 应用程序。Qt 的设计和实现非常出色，Qt 可能会成为为 Linux 开发自由软件应用程序的 Linux C++ 程序员的首选 GUI 库。C 语言程序员可能更倾向于第 30 章介绍的 GTK 库。支付合理的许可费用（参见 www.troll.no），Qt 可用于商业 Linux 应用程序和 Windows 应用程序。

即使你的 Linux 发行版包含了 Qt 运行时和开发库（你可能需要将它们作为独立的安装选项），你可能仍然想访问 www.troll.no 获取在线教程、Postscript 文档文件以及最新的 Qt 发行版。

作者：Mark Watson

## 本章内容

- Java 简述 560页
- 使用 Sockets 编写聊天引擎 575页
- AWT 简介 580页
- 使用 AWT 编写聊天程序 583页
- JFC 简介 586页
- 使用 JFC 编写聊天程序 590页
- 使用原生 Java 编译器 594页

# 用户界面编程
第四部分

本章的目的是向 Linux 程序员介绍 Java 语言，并介绍使用两个 Java API 编写 GUI 应用程序：抽象窗口工具包（AWT）和 Java 基础类（JFC）。Sun 的 Java 网站上有 Java 编程和 GUI 编程的良好教程：http://java.sun.com。本章从 Java 编程的简要介绍开始，包括读取和写入文件、处理线程以及简单基于 socket 的 JFC 的短代码段。我们将看到一个使用 AWT API 编写的示例“聊天”程序，然后使用 JFC API 重写该程序。我使用 Linux 版 Java 开发工具包（JDK） 1.1.7 版本编写了本章，对应的 JFC 版本为 1.1。JFC 也称为 Swing。本章中的示例也用 JDK 2（预发布版）进行了测试。

我们将通过忽略某些理想话题在本章中涵盖大量内容；通常对于许多 Java 编程任务只涵盖一种方法。例如，在 Java GUI 程序中处理事件有三种常用方法。我在本章示例中使用我最喜欢的方法（匿名内部类），并在文中完全忽略了其他两种方法。如果读者在 Java 中运行示例程序并阅读源码列表以及描述示例代码的文本，她至少将知道如何开始编写一个新的 Java 程序。我不会尝试在本章中教授面向对象的编程。

Java 是一门优秀的编程语言，我希望它被 Linux 程序员广泛使用。我在一家人工智能软件公司工作，我们所有的编程都使用 Java。我会在我的网站上发布对本章内容的任何更正或补充。我还有几个在我的网站上免费提供的开源 Java 程序。

# Java 简述

Java 最初由 Sun Microsystems 开发用于消费级设备编程。当 Netscape 和微软都在其网络浏览器中为 Java applet 提供运行时支持时，Java 作为一种客户端编程平台变得极其流行。在本章中，我们不使用 Java applet；所有示例程序都是独立的 Java 程序。然而，Java 编程语言的真正实力在于用它编写多线程服务器应用程序。Java 相比 C 和 C++ 的巨大优势之一是自动内存管理。在 C 中，当你使用 `malloc` 等分配内存时，在完成后必须显式释放内存。在 Java 中，程序中不再被任何变量访问的内存最终由 Java 运行时垃圾回收器释放。另一个优势是

# 使用 Java 进行 GUI 编程
第 32 章

Java 缺乏指针变量。虽然指针确实有用，但它是程序漏洞的大来源。使用异常处理的 C++ 程序员会发现 Java 拥有类似的机制，可以捕捉几乎任何类型的运行时错误。

# Java 是一门面向对象的语言

Java 是一门强类型面向对象的语言。Java 程序通过定义对象类来构建。新定义创建了带有“行为”的结构化数据类型，这些行为通过编写类方法来实现。方法与函数相似，但它们与类或类的实例关联。Java 是强类型的，体现在调用具有错误名称或错误类型参数的方法是非法的（即编译器会生成错误）。例如，如果你尝试将一个整数值赋给一个浮点变量，而没有显式地将浮点值转换为整数（反之亦然），编译器也会生成错误。

清晰地理解 Java 类与类实例之间的关系至关重要。为了展示如何编写类以及如何创建类实例，我们将看一个简单的示例。列表 32.1 显示了 `Car.java` 的内容。

# 列表 32.1 Car.java

```java
import java.io.*;

public class Car implements Serializable {
    private String name;
    private float price;
    static int countInstances = 0;
    public Car(String name, float price) {
        // 类的实例计数：
        countInstances++;
        this.name = name;
        this.price = price;
        System.out.println("Creating Car(" + name + ", " + price + ")");
    }
    public String getName() {
        return name;
    }
    public float getPrice() {
        return price;
    }
    // 静态 main 方法
    public static void main(String[] args) {
        // 此程序不任何参数，但如果提供了
        // 命令行参数，至少
        // 打印它们
        if (args.length > 0) {
            for (int i=0; i<args.length; i++) {
                System.out.println("args[" + i + "]=" + args[i]);
            }
        }
        // 创建几个类的实例：
        Car mustang = new Car("Mustang", 15000.0f);
        Car ford = new Car("Thunderbird", 22000.0f);
        String name = ford.getName();
        float price = mustang.getPrice();
        System.out.println("name: " + name + ", price: " + price);
        System.out.println("Number of instances of Car: " + countInstances);
    }
}
```

我们看到 Car 定义了三个私有类变量：name、price 和 countCarInstances。每当创建一个新的 Car 实例时，该新实例都将拥有它自己私有的 `name` 和 `price` 变量。然而，由于我们在定义 `countCarInstances` 类变量时使用了 `static` 关键字，所有的 Car 实例都共享同一个变量。列表 32.1 显示 `main` 方法也被声明为 `static`。在类定义中，将变量和方法都声明为 `static` 是可能的，而且通常是一种良好的编程技术。列表 32.1 中的以下语句开始了创建 Car 类实例的类构造函数的定义：

```
public Car(String name, float price) {
```

此方法需要两个参数：一个 `String` 类型变量 `name` 和一个 `float` 类型变量 `price`。Java 是一种面向对象的语言，但它并不是一种“纯”面向对象的语言，因为除了类和对象之外，Java 语言还使用 `float`、`int`、`long` 等原始数据类型。类构造函数的体做了几件事：它将参数复制到同名的局部变量中（使用 `this` 关键字可以让编译器知道像 `this.price` 这样的表达式指的是类变量 name，而不是构造函数的参数）。类构造函数还会增加 `countCarInstances` 静态变量，这样我们就能知道在程序中创建了多少个 Car 实例。由于类变量和 price 被声明为 `private`，我们需要提供相应的方法来获取它们的值，以便我们引用这些值：

```
public String getName() { return name; }
public float getPrice() { return price; }
```

最后，通常的做法是在名为 `main` 的静态方法中为新类编写测试代码。任何具有返回 `void` 的 `public static void main` 并且以 `String` 数组作为参数的类，也可以作为独立程序运行。

静态方法 `main` 方法签名中的符号表示：

```
String [] args
```

意味着该参数是 `String` 变量的数组。在 `main` 中，我们通过以下表达式看到该数组中有多少个元素：

```
args.length
```

在这里，变量 `length` 是标准 Java 类 `Array` 的公有类变量。如果 `args` 数组至少有两个元素，那么我们可以通过以下表达式访问数组中的第二个元素，例如：

```
args[1]
```

## 编程用户界面
第四部分

测试用 `main` 方法没有使用 `args` 数组中的命令行参数，但它们被打印出来作为独立 Java 程序中访问命令行参数的示例。任何你想作为独立程序运行的类都必须包含一个 `static public void main` 方法，该方法有一个参数：用于命令行参数的字符串数组。测试方法使用 `new` 操作符创建了两个 Car 实例：

```
Car mustang = new Car("Mustang", 155000.0);
Car ford = new Car("Ford Thunderbird", 22000.0);
```
