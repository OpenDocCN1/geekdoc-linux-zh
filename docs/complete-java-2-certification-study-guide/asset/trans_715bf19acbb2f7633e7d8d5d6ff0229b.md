
这个类非常容易出错。任何修改该类或调用 `getState()` 的人都必须知道 1 代表红色，2 代表黄色，3 代表绿色。如果任何人的代码在某一刻对哪个值代表什么颜色产生了困惑，产生的 bug 可能会很难追踪。

常见的解决方案是引入常量：

```
public class TrafficLight {
    public final static int RED = 1;
    public final static int YELLOW = 2;
    public final static int GREEN = 3;

    private int state;

    public int getState() {
        return state;
    }
}
```

这样好了一点。事实上，在发布 5.0 版本之前，这是除了编写一页冗长的支持代码之外最好的方法。然而，这个版本的 `TrafficLight` 仍然存在问题。你可以希望每个调用 `getState()` 的人都能恰当地处理返回值，如下所示：

```
switch (nextTrafficLight().getState()) {
    case TrafficLight.RED:
        stop();
        break;
    case TrafficLight.YELLOW:
        floorIt();
        break;
    case TrafficLight.GREEN:
        proceed();
        break;
    default:
        assert false: "Strange-colored light";
}
```

这段代码仅将灯的状态与 `TrafficLight` 类定义的常量进行比较，而不是与字面量值。你可以希望调用 `getState()` 的人员使用这种方法；在日常邮件备中确保他们这样做；但你无法保证他们会这样做。我们的代码到为止有许多缺点，特别是这些：

- 可能会给灯的状态分配一个超出范围的值。
- 打印灯的状态没有提供足够的有用信息。

# 枚举 197

这里展示了一种更健壮的方法：

```
public class LightState {
    protected final String name;

    public final static LightState RED = new LightState("red");
    public final static LightState YELLOW = new LightState("yellow");
    public final static LightState GREEN = new LightState("green");

    private LightState(String s) {
        name = s;
    }

    public String name() {
        return name;
    }
}
```

新方法通过 `LightState` 类的实例而不是 `int` 来表示状态。注意，构造函数是私有的，因此你永远无法从类或其子类的外部构造任何实例；你需要的实例都是静态构造的。你不能将新类作为 `switch` 语句的参数（就像上一个示例中使用 `int` 那样），但这是很小的代价。我们原来的切换逻辑变成了

```
LightState state = nextTrafficLight.getState();
if (state == LightState.RED)
    stop();
else if (state == LightState.YELLOW)
    floorIt();
else if (state == LightState.GREEN)
    proceed();
else
    assert false : "null light state";
```

这种设计确保了交通灯唯一的意外状态值是 `null`。此外，调试代码可以打印任何 `LightState` 实例并产生富有信息的结果。事实上，这种方法非常有用，以至于它有一个名字：枚举设计模式。它被认为是类型安全的，因为有一个专门的类型，其唯一目的就是编码几个枚举状态，避免了使用分配整数的危险（任意分配的整数或其他被称为枚举常量的其他原始类型）。某些编程语言（例如 Pascal）内置了对类型枚举的支持。Java 直到 1.5 版本才支持。

# 第 6 章 · 对象与类

类型枚举模式唯一的缺点：它需要大量的代码。上述的 `LightState` 类虽然易于创建，但一个包含许多形式化状态的大程序可能需要几十个枚举类，即使是经验丰富的开发者也可能想走捷径。

Java 5.0 的类型枚举支持以极少的编程工作提供了 `LightState` 类的所有用处。传统类和枚举之间的相似之处包括：

- 你可以在任何可以可以声明类的地方声明枚举。
- 编译枚举会生成一个 .class 文件，其名称源于枚举名称。
- 枚举从 `Object` 继承数据和方法。
- 枚举转换和强制转换的规则与任何扩展 `Object` 的类的规则相同。
- 枚举可以拥有 `main( )` 方法并作为应用程序调用。
- 枚举没有显式构造函数；获得默认的无参构造函数。

枚举具有受限的功能。它们与传统类在以下方面不同：

- 枚举使用 `enum` 关键字而不是 `class` 关键字声明。
- 枚举不能继承任何内容，也不能被扩展。
- 枚举可以作为 `switch` 语句的参数。
- 枚举拥有内置的 `name( ` 和 `toString()` 方法，两者都返回当前实例的名称。

枚举的第一条语句具有特殊格式，如下所示。这里是将 `LightState` 重写为枚举：

```
public enum LightState {
  RED, YELLOW, GREEN;
}
```

注意第一条（也是唯一的）语句，它是用逗号分隔的标识符列表，以分号结束。当枚举被类加载时，会为列表中的每个标识符创建一个实例；你可以将标识符理解为实例的名称。这些名称成为枚举的 `public static final` 成员，因此你可以引用实例，例如 `LightState.YELLOW`。这些实例被称为枚举常量。

接下来的代码展示了如何使用 `LightState` 枚举。假设 `getState()` 方法返回的是 `LightState` 而不是 `int`：

```
switch (nextTrafficLight.getState()) {
  case LightState.RED:
    stop();
    break;
case LightState.YELLOW:
    floorIt();
    break;
case LightState.GREEN:
    proceed();
    break;
default:
  assert false: "null light state";
}
```

这段代码与原始版本几乎完全相同。主要区别是 `RED`、`YELLOW` 和 `GREEN` 现在定义在 `LightState` 中而不是 `TrafficLight` 中。这是它们更合适的地方。唯一的区别是 `assert` 语句打印的消息（原始版本打印的是 "Strange-colored light"）。有了枚举，灯就不会有奇怪的颜色。编译器确保了存在的 `TrafficLight` 实例只有 `RED`、`YELLOW` 和 `GREEN`。如果 `getState()` 返回的值不是这些值之一，那么它必须是 `null`。

通常，一个包含名称列表的简单枚举就是你需要的。然而，你可以为枚举添加数据、方法和构造函数。假设你想创建一个枚举来表示扑牌的花色。这里是一个添加了色的示例：

```
public enum Suit {
  DIAMOND(true), HEART(true), CLUB(false), SPADE(false);
  private boolean red;

  Suit(boolean b) {
    red = b;
  }

  public boolean isRed() {
    return red;
  }

  @Override
  public String toString() {
    String s = name();
    s += red ? ":red" : ":black";
    return s;
  }
}
```
