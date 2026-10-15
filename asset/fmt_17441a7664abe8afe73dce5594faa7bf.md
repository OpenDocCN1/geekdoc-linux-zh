
```dart
child: ListView.builder(

  itemCount: booksListing == null ? 0 : booksListing.length,

  itemBuilder: (context, index) {

    return Card(

      Text(

        '${booksListing[index]['title']}'
        //使用自定义文本主题
        style: Theme.of(context).textTheme.headline6,

      )

    );

  }

)
)
);
```

# 扩展父级文本主题

父级主题可以使用 `copyWith`（`copyWith` 方法）扩展以满足你的需求。我们将父级文本主题 `bodyText2` 自定义为斜体字体样式。从作者列表组件的样式中使用 `Theme.of(context).textTheme.bodyText2` 获取 `bodyText2`。

## Flutter 主题

```dart
Theme (
  data: ThemeData(
    ...,
    textTheme: TextTheme(
      body2: Theme.of(context)
      .copyWith(
        textTheme: TextTheme(
          body2: TextStyle(fontStyle: FontStyle.italic),
        ),
      ).textTheme.body2,
    ),
    child: ListView.builder(
      itemCount: booksListing == null ? 0 : booksListing.length,
      itemBuilder: (context, index) {
      return Card(
        ...
        Text(
          'Author(s): ${booksListing[index]['authors'].join(",")}')
        )
        //Using custom text theme
        style: Theme.of(context).textTheme.body2,
        ),
        ...
      );
    ),
  )
)
```

## 在线源代码

此示例（Flutter Themes：本地主题）的源代码可以在 GitHub 上找到。

## 切换主题

目前你已经学习了创建不同类型的主题。在实际应用中，你可能希望为应用提供从一种类型主题切换到另一种主题的功能。在浅色主题和深色主题之间切换以及反之是一个常见的用例。为了实现这一目的，应用需要记住应用的状态。`BooksApp` 组件需要是一个 `StatefulWidget` 以跟踪当前选择的主题。主题使用枚举 `AppThemes` 来表示。

```dart
enum AppThemes { light, dark }
```

`BooksAppState` 持有 `currentTheme`。

### 164 实用型 Flutter

```dart
class _BooksAppState extends State<BooksApp> {
  var currentTheme = AppThemes.light;
}
```

`MaterialApp` 使用 `theme` 属性应用下方当前选择的主题：

```dart
MaterialApp(
  theme: currentTheme == AppThemes.light ? defaultTheme : darkTheme,
)
```

`defaultTheme` 和 `darkTheme` 定义在 `themes.dart` 文件，并通过 `import 'themes.dart'` 导入。

## 切换主题

在 `AppBar` 组件中添加了一个 `IconButton`（`IconButton` 类）组件以方便切换主题。如果选择了浅色主题，则将 `currentTheme` 赋值为 `darkTheme`，反之亦然。`currentTheme` 在 `setState` 方法内部进行更新。更新后的值将强制 `MaterialApp` 重建并应用当前选择的主题。

```dart
appBar: AppBar(
  actions: [
    IconButton(
      icon: Icon(Icons.all_inclusive),
      // 在浅色主题和深色主题之间切换反反之
      onPressed: () {
        setState(() {
          currentTheme = currentTheme == AppThemes.light
          ? AppThemes.dark : AppThemes.light;
        });
      }
    )
  ]
)
```

`BooksApp` 组件如下所示：

```dart
import 'themes.dart';
```

## Flutter 主题

```dart
//BooksApp 的入口点
void main() => runApp(BooksApp());
//StateWidget
class BooksApp extends StatefulWidget {
  @override
  _BooksAppState createState() => _BooksAppState();
}

class _BooksAppState extends State<BooksApp> {
  var currentTheme = AppThemes.light;
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      // 新代码：选择已选主题
      theme: currentTheme == AppThemes.light? defaultTheme : darkTheme,
      home: Scaffold(
        appBar: AppBar(
          leading: Icon(Icons.home),
          title: Text("Books Listing"),
          actions: [
            IconButton(
              icon: Icon(Icons.all_inclusive),
              // 新代码：从浅色主题切换到深色主题
              onPressed: () {
                setState(() {
                  currentTheme = currentTheme == AppThemes.light ? AppThemes.dark : AppThemes.light;
                });
              }
            )
          ]),
        body: BooksListing(),
      ));
  }
```

`BookListing` 组件保持为 `StatelessWidget`，因为不需要更新界面的这部分。

## 浅色主题

默认选择的主题是浅蓝色，如截图图10.6所示。默认主题在 `themes.dart` 文件中定义：

166 实用型 Flutter

![](img/ffb84d2e32861a1708a54db2b0c6_182_0)

图10.6 `BooksApp` 的默认浅色全局主题

```dart
ThemeData(
  // 定义应用的默认亮度和颜色
  brightness: Brightness.light,
  primaryColor: Colors.blue,
  accentColor: Colors.lightBlue,
  appBarTheme: AppBarTheme(
    color: Colors.blue,
    iconTheme: IconThemeData(
      color: Colors.white,
    )
  ),
```

## 深色主题

深色主题如图10.7所示。深色主题的 `ThemeData` 在 `themes.dart` 文件中定义如下：

## Flutter 主题
