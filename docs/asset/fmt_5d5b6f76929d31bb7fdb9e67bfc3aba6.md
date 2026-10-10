
| Void | 与函数一起使用的特殊值，表示函数不返回任何值。其值为 undefined。 | undefined | `function doNothing():void{ }` |

### 表 3.1 - ActionScript 数据类型

#### 3.3.4 ActionScript 类和对象

要在 Flex 中创建类，您需要创建一个新的带有 `.as` 扩展名的 ActionScript 类。使用 Flex Builder，选择 `文件 -> 新建 -> ActionScript 类`，如图 3.3 所示。

![](img/c4119654311ebf24679359ca130a5ee6_61_0.png)

**图 3.3 – 使用 Eclipse – Flex Builder 插件创建 ActionScript 类**

要将类放在 `com.example1` 包中，您在上一步提供类名称时必须提供包名。现在在创建类后出现的编辑器窗口中插入 **清单 3.2** 中所示的代码。

```
package com.example1
{
    public class Car
    {
        private var speed:Number;
        private var make:String;

        public function Car()
        {
            speed=40;
            make="Honda";
        }

        public function getSpeed():Number{
            return speed;
        }

        public function getMake():String{
            return make;
        }

        public function setSpeed(mySpeed:Number):void{
            speed=mySpeed;
        }

        public function setMake(make:String):void{
            this.make=make;
        }
    }
}
```

**清单 3.2 – Car ActionScript 类**

在上面的示例中，`Car` 代表类，函数 `Car()` 是构造函数。关键字 `this` 表示正在使用的当前对象。它与其他像 Java、C++ 等面向对象编程语言的工作方式相同。

#### 3.3.5 函数和访问修饰符

要在 Flex 中创建函数，请使用以下语法：

```
[**public** | **private** | **protected** | **internal**] **function**
    <名称>([参数1:类型, 参数2:类型, ...]) : <返回类型> {
        //函数体
        //返回值
    }
```

函数可以放置在 MXML 文件中，使用 `<mx:Script>` 元素，或者作为 ActionScript 类中的方法。

上述函数定义前缀有像 `public`、`private`、`protected` 和 `internal` 这样的关键字。这些被称为**访问修饰符**，并定义其应用于的函数或变量的范围。下表 3.2 更详细地描述了这些访问修饰符的范围。

| **访问修饰符** | **同一类** | **同一包** | **不同包** |

|---|---|---|---|

| **private** | 是 | 否 | 否 |

| **internal** | 是 | 是 | 否 |

| **protected** | 是 | 是 | 是，如果是子类 |

| **public** | 是 | 是 | 是，使用 import |

**表 3.2 - 访问修饰符**

例如，如果您想在某个不同的包中使用上面定义的 `Car` 类，可以使用 `import` 如下面的清单 3.3 所示来实现。

```
package com.example2
{
   import com.example1.Car;
   public class Garage
   {
      private var car:Car;
      private var numOfCars:uint;

      public function Garage()
      {
         car = null;
         numOfCars = 0;
      }
      public function getCar() {
         return car;
      }
   }
}
```

**清单 3.3 – 在类中使用包**

那么，上述代码片段中的 `getCar()` 函数叫什么？类的组成部分函数被称为方法。您在 ActionScript 中找到的大多数类都具有一个或多个方法和属性。

#### 3.3.6 [Bindable] 标签

在 ActionScript 中，除非指定这样做，否则变量不会自动传输对其值所做的更改。为了实现这一点，使用称为 `[Bindable]` 的元数据标签。

简而言之，元数据标签是对 ActionScript 编译器的指示。当 ActionScript 编译器遇到此标签时，它会在后台进行必要的代码更改，以便变量的值更改能够传播到应用程序中使用它的不同部分。

清单 3.4 向您展示了如何使用 `[Bindable]` 标签。

```
<?xml version="1.0" encoding="utf-8"?>
<mx:Application xmlns:mx="http://www.adobe.com/2006/mxml" layout="absolute">
<mx:Script>
    <![CDATA[
        [Bindable]// 1
        var myText="Welcome to the world of Flex"; // 2
```

##### **清单 3.4 – 使用 [Bindable] 元数据标签**

在上面的示例中，如果移除第 (1) 处的 `[Bindable]` 标签，那么第 (3) 处的标签 `myLabel1` 就不会根据第 (2) 处显示的变量 `myText` 的值进行更新。Flex Builder 也会对此发出警告。

#### 3.3.7 MXML 和 ActionScript 的映射

ActionScript 和 MXML 相辅相成。虽然仅使用 ActionScript 也能构建完整的 Flex 应用程序，但 MXML 通常用于布局和结构化，而 ActionScript 为应用程序提供交互性。由于减少了需要编写的代码量，MXML 代码更具可读性且更容易编写。

当 MXML 或 Flex 应用程序被编译时，编译器在后端会生成一系列 ActionScript 文件。换句话说，ActionScript 是 Flash Player 的核心语言，Flex 中的所有功能最终都归结为 ActionScript。

表 3.3 展示了 MXML 和 ActionScript 之间的映射关系。

| MXML | ActionScript | 详情 |

|---|---|---|

| 标签 | 类中的代码 | Flex 应用程序中放置的 MXML 标签会被编译为 ActionScript 类中的相应代码，因此你可以在不依赖 MXML 的情况下动态编写 Flex 组件。 |

| 属性 | 类的属性 | 标签中出现的 MXML 属性实际上就是你创建的实例的 ActionScript 属性。 |

| 样式属性 | 使用 `setStyle()` 和 `getStyle()` 函数 | Flex 中的每个组件都有一个或多个类型的属性。其中一种属性类型是样式。样式是 Flex 组件的特殊属性，用于控制组件的外观和感觉。 |

虽然在 MXML 文件中样式是属性，但在 ActionScript 中不能直接使用点符号访问它们。在 MXML 文件中，可以使用属性直接设置样式；然而，由于样式在 Flex 框架中的实现方式不同，因此在 ActionScript 中是使用 `getStyle()` 和 `setStyle()` 方法来进行访问的。

表 3.3 - MXML 和 ActionScript 的映射

清单 3.5 和 3.6 展示了 MXML 标签和属性对应的 ActionScript 代码。

```xml
<?xml version="1.0" encoding="utf-8"?>
<mx:Application
       xmlns:mx="http://www.adobe.com/2006/mxml"
       layout="absolute">
      <mx:Button id="compute" label="Compute" borderColor="#0C6CAF"/>
</mx:Application>
```
