
- A. 花括号（{}）语法
- B. ActionScript 表达式
- C. MXML 中的 <mx:binding> 标签。
- D. ActionScript 中的 BindingUtils
- E. 以上所有

7. 以下哪些是项目渲染器的不同类型？
- A. 嵌入式项目渲染器
- B. 内联项目渲染器
- C. 自定义项目渲染器
- D. 以上所有
- E. 以上都不是

8. 以下哪项不是 Flex 中的基本数据存储机制？
- A. Array（数组）
- B. XML
- C. XMLList（XML 列表）
- D. XMLArray（XML 数组）
- E. XMLListCollection（XML 列表集合）

9. 以下哪项不是 Flex 中的滚动控件？
- A. List 控件
- B. HorizontalList 控件
- C. TileList 控件
- D. DataGrid 控件
- E. 以上都不是

10. 以下哪些是 Flex 提供的层级控件？
- A. Menu 控件
- B. Tree 控件
- C. DataGrid 控件
- D. MenuBar 控件
- E. 以上所有

## 第 6 章 - 使用视图状态、过渡和滤镜

在本章中，你将学习如何根据用户正在执行的任务来更改应用程序界面的外观和感觉的基本方法。一个例子是当用户将鼠标悬停在图标上时，更改该图标的图像。通过使用视图状态、过渡和滤镜，可以轻松地构建富互联网应用程序（RIA）。

在本章中，你将了解以下内容：

- 视图状态
- 使用带有状态的组件
- 使用效果
- 使用过渡
- 在效果中使用滤镜

### 6.1 使用视图状态、过渡和滤镜：宏观概览

视图状态允许你根据某些用户操作来更改应用程序的外观。过渡允许你定义这种视图状态变化在屏幕上的呈现方式。过渡是通过效果类来定义的，结合了专门用于处理过渡的不同效果。图 6.1 提供了这些概念之间关系的概览。

![](img/c4119654311ebf24679359ca130a5ee6_114_0.png)

![](img/c4119654311ebf24679359ca130a5ee6_115_0.png)

在图中，*视图状态 1* 是 UI 的初始状态。当定义的*过渡*应用于此视图状态时，UI 会变为*视图状态 2*。过渡是使用不同的效果（*效果 1、效果 2... 效果 N*）定义的。可以使用不同的*滤镜*连同效果来有条件地应用这些效果。滤镜用于仅将定义的效果有条件地应用于*过渡*中定义的子集目标组件。

### 6.2 视图状态

*状态*是对视图变更的集合。假设我们有一个包含许多组件（容器和控件）的视图。那么，如果这些视图组件的任何布局发生变化，它就成为一个视图状态。每个继承 `UIComponent` 类的组件都将拥有视图状态，并且这些组件将继承 states 属性。

#### 6.2.1 创建状态

在 Flex Builder 的设计视图中可以轻松创建状态。让我们通过一个简单的示例来看看如何操作。请遵循以下步骤：

1. 创建一个新的 Flex 项目。

2. 切换到设计视图，并使用布局工具添加两个组件，一个面板和一个按钮，如下面的*图 6.2*所示。这现在成为应用程序的基础状态。

![](img/c4119654311ebf24679359ca130a5ee6_115_1.png)

3. 现在，你可以基于此基础状态创建一个新的状态。选择*窗口 -> 显示视图 -> 状态*以打开状态视图。*图 6.3*显示了状态视图。现在，点击如图下所示的*新建状态*图标。将出现一个弹出窗口。将新状态命名为 *firstState*，然后指定其基于的组件。在此示例中，它基于 `<base state>`。如果希望此状态为起始状态，可以可选地勾选“设为起始状态”选项。暂时不要勾选该选项，因为我们要将基础状态作为起始状态。

![](img/c4119654311ebf24679359ca130a5ee6_116_0.png)

**图 6.3 - 状态视图**

4. 现在，为此新状态添加一个 TextArea，并如下所示定义 TextArea 的一些属性。

```xml
<mx:TextArea id="txt1" x="10" y="10" width="260" height="210"
 text="My First State" fontSize="20" textAlign="center"
 backgroundColor="#FFEA00"/>
```

5. 你可以像之前图 6.3 中展示的那样以相同的方式添加另一个状态，并将其命名为 *secondState*。你可以添加尽可能多的状态。你甚至可以为此每个新状态添加多个你选择的组件。

6. 你可以检查源代码视图，以查看我们在创建这些新状态并向其添加组件时后台发生了什么。清单 6.1 展示了生成的代码。

```xml
<mx:Panel id="panel1" x="0" y="0" width="300" height="300"
 layout="absolute" title="Learn how to change states">
 <mx:Button x="99" y="228" label="Change"
 click="onClick(event)"/>
</mx:Panel>
<mx:states>
 <mx:State name="firstState">
 <mx:AddChild relativeTo="[panel1]" position="lastChild">
 <mx:TextArea id="txt1" x="10" y="10" width="260"
 height="210"
 text="My First State" fontSize="20" textAlign="center"
 backgroundColor="#FFEA00"/>
 </mx:AddChild>
 </mx:State>
 <mx:State name="secondState">
 <mx:AddChild relativeTo="[panel1]" position="lastChild">
 <mx:TextArea id="txt2" x="10" y="10" width="260"
 height="210"
 text="My Second State" fontSize="20" textAlign="center"
 backgroundColor="#0036FF"/>
 </mx:AddChild>
 </mx:State>
</mx:states>
```

**清单 6.1 - 定义状态**

7. 现在，在源代码视图中为按钮添加一个事件处理程序，以便在当前状态之间切换。ActionScript 代码如下面的清单 6.2 所示。

```actionscript
<mx:Script>
    <![CDATA[
    private function onClick(e:MouseEvent):void{
        if (currentState=='firstState')
            currentState='secondState';
        else if(currentState=='secondState')
            currentState='firstState';
        else
            currentState='firstState';
    }
    ]]>
</mx:Script>
```

**清单 6.2 - 在状态之间切换的代码**

8. 运行应用程序，你可以看到如图 6.4 所示的输出。这是应用程序的基础状态。

![](img/c4119654311ebf24679359ca130a5ee6_117_0.png)

9. 现在点击*change* 按钮，你可以看到如图*图 6.5*所示的你创建的第一个状态。

![](img/c4119654311ebf24679359ca130a5ee6_118_0.png)

**图 6.5 - 用户第一次点击 *change* 按钮时的状态**

10. 再次点击 *Change* 按钮，你可以查看如图 *图 6.6* 所示的第二个状态。

![](img/c4119654311ebf24679359ca130a5ee6_118_1.png)

**图 6.6 - 用户第二次点击 *Change* 按钮时的状态**

11. 使用设计视图创建不同的状态很简单，但你需要了解后台创建的所有代码。因此，让我们来看看这些新标签。

##### 6.2.1.1 <mx:states> 标签

states 属性为视图组件定义了一个视图状态数组。每个视图组件都将有一个基础状态，即第一个状态。基础状态是任何 Flex 应用程序的默认状态。states 属性不能在子控件上指定。它只能在自定义控件或应用程序的根上指定。

##### 6.2.1.2 <mx:State> 标签

可以将 State 对象添加到组件的 state 属性中。这样做会为该组件创建新的视图状态。

<mx:State> 标签的语法：

```xml
<mx:State basedOn="null" name="null" overrides="null"/>
```

basedOn 属性指定其基于的视图状态，name 属性指定当前 State 对象的名称。状态的目的是响应用户或系统发起的事件（例如，按钮的点击）来改变组件的外观。改变组件的外观涉及通过状态使用覆盖（overrides）。有效的覆盖包括：

- AddChild
- RemoveChild
- SetEventHandler
- SetProperty
- SetStyle

#### 6.2.2 状态属性、样式和事件

为了进一步在外观、感觉和行为方面定制状态，可以使用以下标签。

##### 6.2.2.1 <mx:SetEventHandler> 标签

<mx:SetEventHandler> 标签允许你创建仅在特定状态期间有效的事件监听器。这是通过使用处理程序事件类型或 handlerFunction 属性实现的。

在处理程序事件类型中，你可以为事件监听器函数指定多个参数。你甚至可以添加 ActionScript 代码在标签内部，而不是提供事件监听器函数。这在下方的示例中展示：

```xml
<mx:SetEventHandler target="(Button)" name="ButtonClick"
    handler = "buttonHandler(event, linkButtonID)"/>
```

