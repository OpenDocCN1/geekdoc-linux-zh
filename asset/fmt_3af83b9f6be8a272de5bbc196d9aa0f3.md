
图 13.1 单个项目的 JSON 数据图像

![](img/ffb84d2e382861a17088a545dbd2b0c6_221_0.png)

# CUSTOM WIDGET: BookTile

`BookTile`组件用于显示书籍列表中的每个条目。它由 API 提供的书籍标题、作者和封面信息组成，并带有一个灰色线条作为分隔符（图 13.3）。

# ANATOMY OF CUSTOM LIST ENTRY WIDGET

让我们先了解自定义列表条目的结构。自定义列表条目是使用以下原生 Flutter 组件构建的：

- `Card`组件
- `Padding`组件
- `Row`组件
- `Flexible`组件
- `Column`组件
- `Text`组件
- `Image`组件

![](img/ffb84d2e382861a17088a545dbd2b0c6_225_0.png)

图 13.3 自定义列表条目组件

# ListView Widget

`ListView`组件用于滚动方式布局其子组件。构建`ListView`的一种方法是使用`ListView.builder`。它有两个主要属性：

- `itemCount`：该属性包含要在`ListView`中显示的项目。
- `itemBuilder`：该属性接收一个带有两个参数（`context`, `index`）的匿名函数，用于渲染列表的每一行。`index`跟踪列表中的数量。

`BuildContext`（`BuildContext`类）就像是小部件在树中位置的句柄。

# 数据建模

我们之前看到`booksListing = response["items"];`存储了 API 响应的项。`ListView.builder(...)`创建了一个可以滚动的线性书籍数组。我们将构建一个`BookTile`组件来封装书籍项。`BookTile`组件接收`booksListing`中的当前项并传递书籍信息以便渲染。

```dart
ListView.builder(
  itemCount: booksListing == null ? 0 : booksListing.length,
  itemBuilder: (context, index) {
    // 当前书籍 (book: booksListing[index]) 传递给 BookTile
    return BookTile(book: booksListing[index]);
  }
)
```

# 210

# 实用型 Flutter

自定义组件`BookTile`的结构如图 13.4 所示。由于图像、标题和概览视图是垂直对齐的，我们可以使用`Column`组件。

## BookTile StatelessWidget

`BookTile`可以作为一个`StatelessWidget`组件，因为它创建了界面的一部分并且之后不会改变其状态。创建一个`booktile.dart`来存放无状态的`BookTile`组件类。变量`final book`保存了从`ListView.builder()`构造函数中的当前书籍信息。

```dart
import 'package:flutter/material.dart';

class BookTile extends StatelessWidget {
  final book;

  const BookTile({Key key, this.book}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    //Card
    //Padding
    //Padding's child is Row
    //Row's children are Flexible and Image
    //Column's child is Column
    //Column's children are Two Text widgets
    return Card(
      child: Padding(
        child: Row(
          children: [
            Flexible(
              child: Column(
                children: <Widget>[
                  Text(),
```

![](img/ffb84d2e382861a17088a545dbd2b0c6_226_0.png)

图 13.4 自定义列表项组件的结构分析

```dart
Text (),
],
Image.network()
  ,
};
}
```

让我们逐一查看每个构建块组件

## 数据建模

### CARD 组件

`Card`组件（`Card`类）创建一个 Material Design 卡片（Cards）。它是一个用于一起显示相关信息的有用组件。由于我们需要显示与某本书籍项目相关的标题、作者和图像，因此使用`Card`组件作为列表项是合理的。它具有轻微的圆角和阴影，我们可以对其进行调整。使用`shape`属性的`RoundedRectangleBorder`为`Card`组件分配圆角形状。可以使用`elevation`属性调整投影高度。`margin`属性用于在`Card`组件周围留出隙。添加了`Padding`组件作为其子组件。

```dart
Card(
  shape: RoundedRectangleBorder(
    borderRadius: BorderRadius.circular(10.0),
  ),
  elevation: 5,
  margin: EdgeInsets.all(10),
  child: Padding(...),
)
```

### PADDING 组件

我们希望`Card`组件边缘与`Row`组件之间留有一点空间。我们可以使用`Padding`组件在`Row`组件周围实现这种内边距。`Padding`组件用于在`Row`组件周围提供内边距。

```dart
Padding(
  padding: const EdgeInsets.all(8.0),
  child: Row(),
)
```

### ROW 组件

`Row`组件（`Row`类）在水平方向上对齐其子组件。`Row`组件用于将标题和作者文本放在屏幕左侧，并将书籍图像放在右侧。`mainAxisAlignment`属性告诉`Row`如何在可用空间内放置其子组件。`MainAxisAlignment.spaceBetween`有助于在子组件之间分配剩余空间。`Row`有两个子组件来显示书籍的文本详情和图像。

```dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceBetween,
  children: [
    Flexible(),
    Image.network()
  ]
)
```

### FLEXIBLE 组件

`Flexible`组件（`Flexible`类）用于显示书籍的文本详情。它使用`Column`组件作为子组件，垂直对齐标题和作者信息。`Flexible`组件为`Column`提供了扩展以填充主轴上可用空间的灵活性。如果书籍标题太长，它将垂直扩展而不是溢出。

```dart
Flexible(
  child: Column(
)
)
```

### COLUMN 组件

`Column`组件（`Column`类）垂直对齐其子组件。书籍的标题和作者信息在`Column`组件中垂直对齐。`crossAxisAlignment`属性设置为`CrossAxisAlignment.start`，这有助于将子组件对齐到起始位置。该属性使子组件对齐`Column`组件的左侧。

```dart
Column(
  crossAxisAlignment: CrossAxisAlignment.start,
  children: [
    Text(),
    Text()
  ]
)
```

`Text`组件（`Text`类）用于显示文本。两个`Text`组件放置在`Column`组件中。第一个`Text`组件用于书籍标题。变量`book`是从 API 返回的 JSON 数据：

```json
"volumeInfo": {
  "title": "Learning Python",
  "authors": [
    "Mark Lutz"
  ]
}
```

标题位于`volumeInfo->title`。作者列表位于`volumeInfo->authors`。

```dart
Text(
