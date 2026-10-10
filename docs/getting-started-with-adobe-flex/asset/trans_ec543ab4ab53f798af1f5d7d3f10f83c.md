
## 表 4.10 - Flex 中的数据驱动控件

| 控件名称 | 用途/ 描述 |
|---|---|
| List | 包含菜单或级联子菜单的控件。 |
| HorizontalList | 一个水平条，用于承载菜单项。 |
| TileList | PopUpButton 控件的子类，其辅助按钮会弹出一个 Menu 控件。 |
| ComboBox | 一个下拉值列表，可从中选择一个值。 |
| DataGrid | 等价于具有多行多列的表格。这是最常用的一种数据驱动控件。 |
| Tree | 该控件有助于以层级方式处理数据。每个节点可以拥有自己的子树。 |

在下一节中，将向您展示基于菜单的控件和数据提供器控件的一些使用示例。

## 4.5 练习

我们将通过在中部标签页添加更多功能来增强本章一直在开发的应用程序。首先，我们将为该公司提供的不同产品类别创建一个 MenuBar 控件。接下来，我们将使用 TileList 控件显示类别详情。

请按照以下步骤操作：

1. 将 "Tab 2" 重命名为 "Products"
2. 定义一个 XMLListCollection 并创建一个 XMLList 来包含 MenuBar 的数据。使用 menubarXML 初始化 menuBarCollection。所需代码如下，显示在列表 4.6 中。

```actionscript
[Bindable]
public var menuBarCollection:XMLListCollection;
[Bindable]
private var menubarXML:XMLList = <>
<menuItem label="Vehicle">
<menuitem label="Sedan" data="Sedan"/>
<menuitem label="Truck" data="Truck"/>
<menuitem label="Van" data="Van"/>
</menuItem>
<menuItem label="Appliances">
<menuitem label="TV" data="TV"/>
<menuitem label="Freeze" data="Freeze"/>
</menuItem>
<menuItem label="Office Equipment">
<menuItem label="Printer" data="Printer"/>
<menuItem label="Scanner" data="Scanner"/>
<menuItem label="Copier" data="Copier"/>
</menuItem>
<menuItem label="Stationary">
<menuItem label="Pen" data="Pen"/>
<menuItem label="Cartige" data="Cartige"/>
<menuItem label="Scissor" data="Scissor"/>
</menuItem>
</>
private function initMenuBar():void {
menuBarCollection = new XMLListCollection(menubarXML);
}
```

### 列表 4.6 – MenuBar 数据的定义和初始化

3. 在 Canvas 内放置一个 MenuBar。从 menubarXML 的标签中分配 Menu 的标签，将 menuBarCollection 分配为 dataProvider。还要为 itemClick 事件添加一个 itemClickHandler 方法。相应的代码如下所示：

```xml
<mx:MenuBar labelField="@label" dataProvider="{menuBarCollection}"
itemClick="menuClickHandler(event)" />
</mx:MenuBar>
```

4. 暂时将 itemClick 事件处理程序的定义定义为空方法 menuClickHandler：

```actionscript
private function menuClickHandler(event:MenuEvent):void {}
```

现在运行应用程序。您会看到下图（图 4.12）所示的画面。请继续尝试菜单选项。

![](img/c4119654311ebf24679359ca130a5ee6_90_0.png)

### 图 4.12 – 基于菜单的控件示例

5. 添加一个 TileList，并使用以下代码使其最初不可见：

```xml
<mx:TileList id="myTileList" x="10" y="47" width="60%" visible="false" height="95%"> </mx:TileList>
```

6. 为 TileList 控件添加数据以及一些图片。还将 tileListArray 绑定到 ArrayCollection TileListDataProvider。所需代码显示在列表 4.7 中。

```actionscript
[Bindable]
public var TileListDataProvider:ArrayCollection;
[Bindable]
 [Embed(source="vehicle 1.png")]
public var vehicle1:Class;
[Bindable]
 [Embed(source="vehicle 2.png")]
public var vehicle2:Class;
[Bindable]
 [Embed(source="vehicle 3.png")]
public var vehicle3:Class;
[Bindable]
 [Embed(source="vehicle 4.png")]
public var vehicle4:Class;
[Bindable]
 [Embed(source="vehicle 5.png")]
public var vehicle5:Class;
[Bindable]
 [Embed(source="vehicle 6.png")]
public var vehicle6:Class;
[Bindable]
 [Embed(source="vehicle 7.png")]
public var vehicle7:Class;
[Bindable]
 [Embed(source="vehicle 8.png")]
public var vehicle8:Class;
private var tileListArray:Array=[
(label: "Vehicle 1", data: 0, icon: "vehicle1"),
(label: "Vehicle 2", data: 1, icon: "vehicle2"),
(label: "Vehicle 3", data: 2, icon: "vehicle3"),
(label: "Vehicle 4", data: 3, icon: "vehicle4"),
(label: "Vehicle 5", data: 4, icon: "vehicle5"),
(label: "Vehicle 6", data: 5, icon: "vehicle5"),
(label: "Vehicle 7", data: 6, icon: "vehicle7"),
(label: "Vehicle 8", data: 7, icon: "vehicle8"),
];
[Bindable]
public var menuBarCollection:XMLListCollection;
```

### 列表 4.7 — TileList 数据的定义和初始化

7. 修改 menuClickHandler。添加一些代码，当用户点击“Sedan”选项时显示上述数据。此外，当选择另一个选项时，应清除该区域并重新渲染相应的数据。在此示例中，TileList 被隐藏以使示例更简单。代码显示在列表 4.8 中。

```actionscript
private function menuClickHandler(event:MenuEvent):void {
    initSedanData();
    myTileList.visible = false;
    if ( event.item.@data == "Sedan" ){
        myTileList.visible = true;
        myTileList.dataProvider = TileListDataProvider;
    }
}
```

### 列表 4.8 – 在 TileList 中渲染数据

再次运行应用程序。从菜单选项中选择“Sedan”。您将看到贵公司产品的图片：漂亮的汽车。这不是很酷吗！*图 4.13* 提供了一个示例输出。

![](img/c4119654311ebf24679359ca130a5ee6_92_0.png)

### 图 4.13 – TileList 示例的输出

## 4.6 总结

在本章中，您学习了组件的基础知识，组件是 Flex 应用程序的构建模块。首先，您学习了组件的类层次结构；接下来，您被介绍了容器——其他容器和控件的占位符。Application 容器是任何 Flex 应用程序的第一个组件，它具有一些特定的属性和属性。然后，本章涵盖了其他类型的容器：布局型和导航型。

最后一节涵盖了控件。控件是用户与应用程序交互的手段。控件有不同的类型，例如文本、基本、基于菜单和数据驱动。本章从每个类别中详细展示了一些示例。

至此，您应该更加熟悉构建和操作 Flex 了。在后续章节中，我们将处理更复杂的 Flex 应用程序。

## 4.7 复习题

1. 指出作为大多数 Flex 组件超类的 ActionScript 类名。
2. 默认情况下，Application 容器的尺寸大于所包含的组件——为什么？
3. 您是否可以在控制器的可见区域外放置控件？如何操作？
4. Grid Layout 容器的 HTML 等价物是什么？
5. 可以使用哪个 ActionScript 方法动态设置组件的样式？
6. Flex 应用程序启动后的默认加载时长是多少，超过此时长进度条才会出现：
    - A. 100 毫秒
    - B. 1000 毫秒
    - C. 700 毫秒
    - D. 5 秒
    - E. 以上都不是
7. 以下哪种控件可以仅使用 ActionScript 渲染？
    - A. Label
    - B. Image
    - C. Menu
    - D. 以上全部
    - E. 以上都不是
8. Alert 类中用于显示数据的静态方法名称是什么？
    - A. display()
    - B. show()
    - C. init()
    - D. render()
    - E. 以上都不是
9. 数据提供给 Flex 控件的方式有哪些？
    - A. ArrayCollection 对象
    - B. XMLListCollection 对象
    - C. A 和 B 都是
    - D. XMLText 对象
    - E. 以上都不是
10. 您想要创建一个字段，让用户在地址文件中选择其当前居住地——应该使用以下哪种数据驱动控件？
    - A. DataGrid
    - B. ComboBox
    - C. Tree
    - D. 以上任意一种
    - E. 以上都不是

## 第 5 章 - 在控件之间绑定数据

Flex 框架提供了一个强大的结构，旨在最大程度地促进组件驱动架构。在 MVC（模型-视图-控制器）架构中，视图和控制器与模型的行为绑定。在组件驱动架构中，这种方法不可行。在这种情况下，用户界面（UI）元素在模型之前构建，以提供组件在许多不同应用程序中的重用性。在 Flex 中，我们通过称为数据绑定的机制来实现这一点。

在本章中，您将学习：

- 数据绑定
- 数据绑定的不同方式
- 数据绑定和存储机制
- 数据绑定和 UI 控件

## 5.1 数据绑定 – 大局观

数据绑定是 Flex 中一个非常有趣的概念。它使您能够更高效地在客户端管理数据。图 5.1 提供了数据绑定的概述。

![](img/c4119654311ebf24679359ca130a5ee6_96_0.png)

