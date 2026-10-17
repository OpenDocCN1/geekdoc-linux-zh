
# 实战 Flutter

```
Row(

  children: [

    Image.asset('assets/flutter_icon.png'),

    Image.asset('assets/flutter_icon.png'),

  ]

)
```

当上述代码添加到 `Scaffold` 组件的 `body` 中时，第二个图像会溢出屏幕右侧，如图 8.1 所示。

将 `Row` 组件封装在 `FittedBox` 中，可以确保两个 `Image` 组件都包含在 `FittedBox` 内部，不会溢出屏幕。

```
FittedBox(

  Row(

    children: [

      Image.asset('assets/flutter_icon.png'),

      Image.asset('assets/flutter_icon.png'),

    ]

  )

)
```

图 8.2 显示两个图像都调整到了屏幕内部，没有向右侧溢出。

![](img/ffb84d2e382861a17088a545dbd2b0c6_144_0.png)

**图 8.1** 未使用 `FittedBox` 时溢出的组件

## 在线源码

此示例的源代码（响应式界面：`FittedBox` 组件）可以在 GitHub 上在线查看。

## Expanded 组件

`Expanded`（`Expanded` 类）组件是一个单子节点布局组件。该布局用于 `Row`、`Column` 和 `Flex` 等多子节点布局组件的特定子组件。包裹在 `Expanded` 组件中的子组件会沿主轴扩展以填满可用空间。对于 `Row` 父组件，它在水平方向扩展；对于 `Column` 父组件，它在垂直方向扩展。它使用 `flex` 因子（flex factor）让子组件知道它们可以占据多少可用空间。被 `Expanded` 组件包裹的子组件会占据所有剩余空间。当 `Expanded` 组件之间存在可用空间竞争时，它使用 `flex` 属性来分配空间。

## 响应式界面

![](img/ffb84d2e382861a17088a545dbd2b0c6_145_0.png)

图 8.2 使用 `FittedBox` 的响应式布局

让我们查看一个 `expandedDefault()` 组件，它由 `Row` 组件及其三个子组件组成，假设 `childWidget()` 方法返回一个被作为子组件添加到 `Row` 中的组件。在下方的代码段中，每个子组件都被包裹在 `Expanded` 组件中。每个 `Expanded` 组件都平分了可用的水平空间，如图 8.3 所示。

```
Widget expandedDefault() {

  return Row(

    children: [

      Expanded(

        child: childWidget(""),

      ),

      Expanded(

        child: childWidget(""),

      ),

      Expanded(

        child: childWidget(""),

      ),

    ],

  );

}
```

## 带有 `flex` 属性的 Expanded

在下面的示例中，每个子组件都被包裹在 `Expanded` 组件中，并使用了 `flex` 属性。每个子组件根据 `flex` 属性的值占据空间。第一个子组件的 `flex` 分配为4，第二个分配为3，第三个子组件的 `flex` 属性为1。在这种情况下，总空间将分为8份（4 + 3 + 1 = 8）。第一个子组件占据8份中的4份，即总空间的 4/8。

![](img/ffb84d2e382861a17088a545dbd2b0c6_146_0.png)

**图 8.3** 未使用 'flex' 属性的 `Expanded` 组件

![](img/ffb84d2e382861a17088a545dbd2b0c6_147_0.png)

**图 8.4** 使用 'flex' 属性的 `Expanded` 组件

第二个子组件占据8份中的3份，即总空间的 3/4，最后一个子组件占据总空间的1/2，如图 8.4 所示。

```
Widget expandedWithFlex() {

  return Row(

    children: [

      Expanded(

        flex: 4,

        child: childWidget("4/8"),

      ),

      Expanded(

        flex: 3,

        child: childWidget("3/8"),

      ),

      Expanded(

        flex: 1,

        child: childWidget("1/8"),

      ),

    ],

  );

}
```

## 在线源码

此示例的源代码（响应式界面：`Expanded` 组件）可以在 GitHub 上在线查看。

## Flexible 组件

`Flexible`（`Flex` 类）组件与 `Expanded` 组件相似，但有一个不同之处。它允许根据 `flex` 属性的约束让 `Row`、`Column` 和 `Flex` 布局组件的子组件在可用空间内扩展。`Flexible` 组件只根据 `flex` 属性声明的占据空间。它们默认不会占据额外的空间。

### `Flex.tight` 属性

`Flex.tight` 强制子组件占据整个可用空间。当 `fit` 属性设置为 `Flex.tight` 时，`Flexible` 组件的行为类似于 `Expanded` 组件。`Expanded(child: Text())` 等于 `Flexible(fit: Flex.tight, child: Text())`。在下面的代码段中，`Row` 组件的三个子组件分别分配了四、三、一份。当 `flex` 属性设置为 `Flex.tight` 时，它们会分配给它们的空间并填满。

```
Row(

  children: [

    Flexible(

      fit: Flex.tight,

      flex: 4,

      child: childWidget("4/8"),

    ),

    Flexible(

      fit: Flex.tight,

      flex: 3,

      child: childWidget("3/8"),

    ),

    Flexible(

      fit: Flex.tight,

      flex: 1,

      child: childWidget("1/8"),

    ),

  ],

)
```

参考图 8.5 查看使用 `Flex.tight` 的 `Flexible` 组件。

### `FlexFit.loose` 属性

`FlexFit.loose` 将保持默认并允许它们 own最大 own。在下面的代码段中，`Row` 的三个子组件分别分配了四、三、一份。当 `fit` 属性设置为 `FlexFit.loose` 时，它们只占据分配给它们的空间，而不占据剩余空间。

![](img/ffb84d2e382861a17088a545dbd2b0c6_149_0.png)

**图 8.5** 使用 'fit' 属性为 `FlexFit.tight` 的 `Flexible` 组件

```
Row(

  children: [

    Flexible(

      fit: FlexFit.loose,

      flex: 4,

      child: childWidget("4/8"),

    ),

    Flexible(

      fit: FlexFit.loose,

      flex: 3,

      child: childWidget("3/8"),

    ),

    Flexible(

      fit: FlexFit.loose,

      flex: 1,

      child: childWidget("1/8"),

    ),

  ]

)
```
