

![](img/53ede4f4266a5731b93bff15d85fa06a_46_0.png)

## 3.1.2 “as” 关键字和接口聚类

`as` 关键字允许签名为接口提供一个替代名称。例如，MainC 使用 `as` 关键字使其签名对读者更清晰一些，通过使用名称 SoftwareInit 来表示其 Init 接口：

```
uses interface Init as SoftwareInit;
```

某些签名必须使用该关键字来区分同一接口的多个实例。如果一个组件提供或使用接口不止一次，其签名必须使用 `as` 关键字为它们赋予不同的名称。例如，LedsC 通过 Leds 接口提供三个 LED 的抽象，但它是一个配置而不是可执行代码。LedsC 配置将 LED 模块 LedsP 连接到提供为 LED 供电的数字输入输出线的组件。LedsP 的签名如下：

```
module LedsP {
  provides {
    interface Init;
    interface Leds;
  }
  uses {
    interface GeneralIO as Led0;
    interface GeneralIO as Led1;
    interface GeneralIO as Led2;
  }
}
```

清单 3.4 LedsP 模块

签名只需要确保每个接口实例都有唯一名称即可。例如，上面 LedsP 的例子也可以只使用两次 `as`，并让一个接口实例保留为 GeneralIO，这样三个名称就分别是 Led0、Led1 和 GeneralIO。然而，在这种情况下会令人困惑，因此 LedsP 重命名了 GeneralIO 的全部三个实例。技术上讲，接口声明隐含使用了 `as`。语句

```
uses interface Leds;
```

实际上是

```
uses interface Leds as Leds;
```

的简写。一般来说，`as` 关键字是有用的工具，可以使组件及其需求更清晰，就像变量和函数名称极大地影响代码可读性一样。

### 编程提示 1 慷慨地使用 “as” 关键字。

## 3.1.3 聚类接口

LedsP 示例展示了签名关于的另一个细节：它们可以把使用的和提供的接口聚类在一起。例如，这两个版本的 PowerupC 是等价的：

```
configuration PowerupC {
  uses interface Boot;
  uses interface Leds;
}
```

```
configuration PowerupC {
  uses {
    interface Boot;
    interface Leds;
  }
}
```

清单 3.5 PowerupC 及其替代签名

由于两者等价，在语法或代码效率上没有优势：这只是风格问题，以及哪种方式对读者更易读。组件签名通常先声明它们提供的接口，然后再声明它们使用的接口。这让读者能够清楚地看到可用功能和依赖关系。然而，对于执行许多功能的非常复杂的组件，这种方法会失效，签名会把相关的接口放在彼此附近。

TinyOS 细节：上面描述的所有组件的名称都以字母 C 和 P 结尾。这不是强制要求。它是 TinyOS 代码中使用的编码约定。名称以 C 结尾的组件是其他组件可以自由使用的抽象：C 代表 “component”。一些组件名称以 P 结尾，代表 “private”。在 TinyOS 中，P 组件不应直接使用，因为它们通常是复杂系统的内部部分。组件使用这两个字母是为了清楚地将它们与接口区分开。

## 3.2 接口

接口描述了两个或多个不同组件之间的功能关系。组件在此关系中所扮演的角色取决于它提供或使用接口。与组件一样，接口在名称和文件之间有一一映射：文件 Leds.nc 包含接口 Leds，而文件 Boot.nc 包含

![](img/53ede4f4266a5731b93bff15d85fa06a_48_0.png)

图 3.2 接口具有命令和事件。用户调用命令，提供者发出事件。

接口 Boot。就像组件一样，接口处于全局命名空间中。然而在语法上，接口与组件大不相同。它们只有一个块，即接口声明：

```
interface Boot {
    // functions
}

interface Leds {
    // functions
}
```

清单 3.6 Leds 和 Boot 的接口声明

接口声明包含一个或多个函数。接口有两种函数：命令和事件。Init 和 Boot 是两个简单的接口，各自只有一个函数。Init 有一个命令，而 Boot 有一个事件：

```
interface Init {
    command error_t init();
}

interface Boot {
    event void booted();
}
```

清单 3.7 Init 和 Boot 接口

TinyOS 细节：`init` 返回的 `error_t` 类型是 TinyOS 报告成功或失败的常规方式。值 SUCCESS 代表成功，FAIL 代表一般失败。特定的 Exxx 常量，部分受 Unix 的 errno 启发，表示特定失败，例如 EINVAL 表示 “无效值”。

函数是命令还是事件决定了接口的哪一侧 —— 用户或提供者 —— 实现该函数，以及哪一侧可以调用它。用户可以调用命令，提供者可以发出事件。反之，用户必须实现事件，提供者必须实现命令。图 3.3 用我们描述 nesC 程序的视觉语言展示了这种关系。例如，回到 MainC

