
参考图 8.6 查看使用 `FlexFit.loose` 属性的 `Flexible` 组件。

## 在线源码

此示例的源代码（响应式界面：`Flexible` 组件）可以在 GitHub 上查看。

## LayoutBuilder 组件

`LayoutBuilder`（`LayoutBuilder` 类）支持多子布局。它根据父组件传递的约束动态构建组件。`LayoutBuilder` 布局在创建响应式布局时效果良好。它可以根据约束的最大宽度 `maxWidth` 或最大高度 `maxHeight` 构建合适的布局。`LayoutBuilder` 在此时调用 `builder` 函数。

在这个示例中，`LayoutBuilder` 在布局期间根据屏幕的最大宽度渲染不同的组件。对于宽度大于 400 的屏幕渲染 `largeScreen()` 布局，对于宽度小于 400 的屏幕渲染 `smallScreen()`。

```
LayoutBuilder(
  builder: (context, constraints) {
    if (constraints.maxWidth > 400) {
      return largeScreen();
    } else {
      return smallScreen();
    }
  }
);
```

在小屏幕上渲染的 `LayoutBuilder` 组件见图 8.8。在大屏幕上渲染的 `LayoutBuilder` 组件见图 8.9。

## 在线源码

此示例的源代码（响应式界面：`LayoutBuilder` 组件）可以在 GitHub 上在线查看。

## FractionallySizedBox 组件

`FractionallySizedBox`（`FractionallySizedBox` 类）是一个单子节点布局组件。它将子组件的大小设置为总可用空间的比例。它的属性 `widthFactor` 和 `heightFactor` 提供了组件可以占据的区域比例。`alignment` 属性定位其子组件。这个没有子组件的组件作为占位符。在 `Row` 和 `Column` 组件中添加子组件时，建议将 `FractionallySizedBox` 包裹在 `Flexible` 组件中。

在下面的示例中，使用 `Center` 组件将 `Container` 组件放置在屏幕中心。`FractionallySizedBox` 被包裹在 `Padding` 组件中以保持视觉上的可区分。`ElevatedButton`（`ElevatedButton` 类）组件作为子组件添加到 `FractionallySizedBox` 中。`FractionallySizedBox` 通过 `alignment` 属性控制 `ElevatedButton` 组件的宽高以及它在 `Container` 组件内部的位置。在这种情况下，`FractionallySizedBox` 对齐到 `Container` 组件的底部。

```
Center(
  child: Container(
    width: 200,
    height: 200,
    decoration: BoxDecoration(
      border: Border.all(),
    ),
    child: Padding(
      padding: const EdgeInsets.all(8.0),
      child: FractionallySizedBox(
        alignment: Alignment.bottomCenter,
        widthFactor: 0.8,
        heightFactor: 0.2,
        child: ElevatedButton(
          child: Text(
            "Tap",
            style: TextStyle(
              fontSize: 20,
            ),
          ),
          onPressed: () {},
        ),
      ),
    ),
  ),
)
```

参考图 8.7 查看作为 `Container` 组件子组件的 `FractionallySizedBox`。

![](img/ffb84d2e382861a17088a545dbd2b0c6_151_0.png)

**图 8.6** 使用 'fit' 属性为 `FlexFit.loose` 的 `Flexible` 组件

## 在线源码

此示例的源代码（响应式界面：`FractionallySizedBox` 组件）可以在 GitHub 上在线查看。

![](img/ffb84d2e382861a17088a545dbd2b0c6_152_0.png)

**图 8.7** 作为 `Container` 组件子组件的 `FractionallySizedBox`

![](img/ffb84d2e382861a17088a545dbd2b0c6_154_0.png)

图 8.8 `LayoutBuilder` 组件在小屏幕上的渲染

当垂直对齐时位于下一列。`runSpacing` 属性提供了这些行之间的间隙。

```
child: Wrap(
  direction: Axis.horizontal,
  spacing: 20.0,
  runSpacing: 40.0,
  children: [
    childWidget("1"),
    childWidget("2"),
    childWidget("3"),
    childWidget("4"),
    childWidget("5"),
    childWidget("6"),
  ]
)
```
