
### BoxConstraints.loose()

`BoxConstraints.loose()` 将子组件限制在给定尺寸内。它不能超过提供的尺寸。

```
...
body: Center(
  child: ConstrainedBox(
    constraints: BoxConstraints.loose(
      Size(100, 200),
    ),
    child: Container(
      color: Colors.grey,
      child: Text(message),
    )
  )
),
```

三个约束都在图 7.11 中并列显示。

![](img/ffb84d2e382861a17088a545dbd2b0c6_117_0.png)

图 7.11 ConstrainedBox 组件 – 属性

## 源码 (Source Code Online)

此示例（构建布局：ConstrainedBox 组件）的源代码可以在 GitHub 获取。

## SizedBox 组件 (SizedBox Widget)

`SizedBox`（`SizedBox` 类）组件是一个单组件布局组件。它具有特定尺寸，可以添加另一个组件作为子组件。当你知道组件的尺寸时它非常有用。`width` 属性用于设置框的宽度，`height` 属性用于设置高度。该代码段创建了一个高宽 200 像素的 `SizedBox`。

```
SizedBox(
  height: 200,
  width: 200,
  child: Container(
    color: Colors.deepPurple,
  )
),
```

图 7.12 显示了 `SizedBox` 组件。

![](img/ffb84d2e382861a17088a545dbd2b0c6_118_0.png)

**图 7.12** 高和宽为 200 的 SizedBox

有一个便利构造函数 `SizedBox.expand`，它也可以用于创建一个占据父级宽度和高度的框。

```
SizedBox.expand(
  child: Container(
    color: Colors.deepPurple,
  )
)
```

图 7.13 展示了使用 `SizedBox.expand` 构造函数创建 `SizedBox` 组件。通过给 `SizedBox` 的 `width` 和 `height` 属性赋值 `double.infinity` 可以获得相同的结果。

![](img/ffb84d2e382861a17088a545dbd2b0c6_119_0.png)

**图 7.13** 使用 'SizedBox.expand' 构造函数的 SizedBox 组件

在构建界面时，常用没有子组件的 `SizedBox` 来添加组件之间的间距。

## 源码 (Source Code Online)

此示例（构建布局：SizedBox 组件）的源代码可以在 GitHub 上在线获取。

## Row 组件 (Row WIDGET)

`Row`（`Row` 类）组件用于以水平方式排列其子组件。让我们添加三个 `Container` 组件作为子组件。`child(int index)` 方法返回一个宽高密度无关像素的 `Container`。该容器有一个 `Text` 组件作为子组件，显示作为参数传递给方法的数字。

```
Widget childWidget(int index) {
  return Container(
    color: Colors.grey,
    width: 100,
    height: 100,
    child: Center(
      child: Text(
        "$index",
        style: TextStyle(fontSize: 40),
      )
    )
  );
}
```

现在我们有了一个子组件，让我们在 `Row` 组件中如下添加三次：

```
Row(
  children: [
    childWidget(0),
    childWidget(1),
    childWidget(2),
  ]
);
```

图 7.14 显示了用 `Row` 组件构建的多子组件布局。尝试向 `Row` 组件的 `children` 中再添加一个组件 `childWidget(3)` 并观察变化。

```
Row(
  children: [
    childWidget(0),
    childWidget(1),
    childWidget(2),
    childWidget(3),
  ]
);
```

你会注意到有足够的空间让四个组件水平排列。最后一个子组件用黄色和黑色的线条进行渲染。每当一个组件溢出可用空间以渲染自身时，你都会看到那些线条。你将在构建响应式布局的章节中学习创建自适应布局（第 08 章：响应式界面）。

图 7.15 显示了多子组件布局中溢出的组件。

![](img/ffb84d2e382861a17088a545dbd2b0c6_121_0.png)

**图 7.14** Row: 多子组件布局组件

![](img/ffb84d2e382861a17088a545dbd2b0c6_122_0.png)

图 7.15 Row：溢出的子组件

```
Widget childWidget(int index) {
  return Container(
    color: getColor(index),
    width: 100 + index * 20.toDouble(),
    height: 100 + index * 30.toDouble(),
    child: Center(
      child: Text(
        "$index",
        style: TextStyle(fontSize: 40),
      )
    );
  );
}
```

### 构建布局

接下来，将由 `childWidget()` 方法创建的三个子添加到 `Row` 组件中，如下所示：

```
Row(
  children: [
    childWidget(0),
    childWidget(1),
    childWidget(2),
  ],
);
```

上述代码将在水平数组中渲染三个不同大小的 Container 小部件，如图 7.16 所示。

![](img/ffb84d2e382861a17088a545dbd2b0c6_123_0.png)

图 7.16 Row 组件具有不同大小的子组件

目标是将所有子组件拉伸到相同的高度。因此，让我们将 `Row` 组件的 `crossAxisAlignment` 属性设置为 `CrossAxisAlignment.stretch`，使所有子组件等等高。

```
Row(
  crossAxisAlignment: CrossAxisAlignment.stretch,
  children: [
    child(0),
    child(1),
    child(2),
  ]
)
```

然而，问题是它们将占据所有垂直方向的可用空间，导致看起来如图 7.17 所示。

我们希望让所有子组件的高度与最高的子组件相同，同时占据所有的可用垂直空间。这时，`IntrinsicHeight`（`IntrinsicHeight` 类）组件派上用场了。

**图 7.17** Row 组件的 ‘crossAxisAlignment’ 属性设置为 ‘CrossAxisAlignment.stretch’

你只需要将 `Row` 组件封装在 `IntrinsicHeight` 内部，如下所示代码段所示：

```
IntrinsicHeight(
  child: Row(
    crossAxisAlignment: CrossAxisAlignment.stretch,
    children: [
      childWidget(0),
      childWidget(1),
      childWidget(2),
    ]
  )
)
```
