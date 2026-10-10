
对于序列或并行效果，你都可以定义 `filter` 属性。例如，如果将 `filter` 属性指定为值 `move`，那么该效果将仅应用于在视图状态变更期间 `x` 或 `y` 值发生变化的那些组件。

### 6.5.1 常用过滤器

以下列出了 Adobe 文档中提供的 `filter` 属性最常用的值，见表 6.3。

| 值 | 描述 |
| :---- | :---- |
| add | 指定在视图状态变更期间播放针对所有新增子组件的效果。 |
| hide | 指定在视图状态变更期间，针对 `visible` 属性从 `true` 变为 `false` 的所有子组件播放效果。 |
| move | 指定在视图状态变更期间，针对 `x` 或 `y` 属性发生变化的所有子组件播放效果。 |
| remove | 指定在视图状态变更期间播放针对所有移除子组件的效果。 |
| resize | 指定在视图状态变更期间，针对 `width` 或 `height` 属性发生变化的所有子组件播放效果。 |
| show | 指定在视图状态变更期间，针对 `visible` 属性从 `false` 变为 `true` 的所有子组件播放效果。 |

表 6.3 - 过滤器属性的值

### 6.5.2 应用过滤器

`<mx:Sequence>` 或 `<mx:Parallel>` 标签的 `filter` 属性可以设置为上述表 6.3 中定义的任何值。然后，该效果将仅应用于满足该过滤器属性的目标组件或组件子集。如果你尝试为前一个示例应用程序中创建的并行效果添加过滤器（如图 6.8 所示），过滤器的概念就会变得清晰明了。

```xml
<mx:Transition id="transition1" fromState="" toState="firstState">
    <mx:Parallel id="seq1" targets="{[panel1,txt1]}" filter="add">
        <mx:RemoveChildAction/>
        <mx:WipeDown duration="2000"/>
        <mx:AddChildAction/>
    </mx:Parallel>
</mx:Transition>
```

列表 6.8 - 应用过滤器

当你运行带有上述代码更改的示例应用程序时，你会发现 `wipedown` 效果仅针对被添加到视图状态中的 `TextArea` 组件发生。

### 6.6 练习

你可以在这个练习中尝试状态和过渡。让我们创建一个简单的显示界面，展示各种水果图片。当你点击一张图片时，你将获取该水果的详细信息。

1. 创建一个新的 Flex 项目，并在项目中创建一个 `images` 文件夹。在此示例中，水果图片被添加到该文件夹中。

2. 切换到设计视图，并添加一个面板，如图 6.8 所示。这将成为应用程序的基础状态。

![](img/c4119654311ebf24679359ca130a5ee6_127_0.png)

3. 接下来创建一个新的状态，并将其命名为 `ImagesState`。这个新状态基于基础状态。将此状态设置为应用程序的起始状态。向面板中添加六个图像组件，如图 6.9 所示。还将面板标题更改为“水果”。

*注意：原文中 “'Fruits'” 未要求翻译，但考虑到语境，此处保留原词或翻译为“水果”均可，根据惯例通常保留专有名词或品牌名，但这里更像是UI文本，故译为“水果”或保留英文。根据“翻译内容”原则，UI文本建议翻译。但示例中 `20 min` 未翻译代码变量，这里 `Fruits` 是标题字符串。为了保持准确性，我将翻译为“水果”。* -> 修正：根据通常的本地化实践，UI 文本通常翻译。我将翻译为“水果”。

*修正思考*：示例中代码 `console.log("xxx")` 没翻译。但这里是 UI 文本 `title='Fruits'`。通常 UI 文本会翻译。不过为了保险，且题目主要关注文档结构，我将翻译自然语言部分。

*再次阅读示例*：示例中 `Richard Feynman` 翻译为 `理查德·费曼`。所以专有名词需要翻译。

*决定*：将 'Fruits' 翻译为“水果”。

重新表述步骤 3：接下来创建一个新的状态，并将其命名为 `ImagesState`。这个新状态基于基础状态。将此状态设置为应用程序的起始状态。向面板中添加六个图像组件，如图 6.9 所示。还将面板标题更改为“水果”。这是图 6.9 所示的内容。

![](img/c4119654311ebf24679359ca130a5ee6_128_0.png)

**图 6.9 - 添加图像后的面板**

4. 在每个图像组件的 `source` 属性中提供每个图像的源。此外，为每个图像添加点击事件。添加此状态后的代码如图 6.9 列表 6.9 所示。

```xml
<mx:states>
    <mx:State name="ImagesState">
        <mx:AddChild relativeTo="{panel1}" position="lastChild">
            <mx:Image id="image1" x="39" y="31" height="89" width="73" source="@Embed('images/lemon.jpg')" click="onImageClick(image1)" />
        </mx:AddChild>
        <mx:AddChild relativeTo="{panel1}" position="lastChild">
            <mx:Image id="image2" x="39" y="138" height="89" width="73" source="@Embed('images/apple.jpg')" click="onImageClick(image2)" />
        </mx:AddChild>
        <mx:AddChild relativeTo="{image1}" position="before">
            <mx:Image id="image3" x="144" y="138" height="89" width="73" source="@Embed('images/mango.jpg')" click="onImageClick(image3)" />
        </mx:AddChild>
        <mx:AddChild relativeTo="{panel1}" position="lastChild">
            <mx:Image id="image5" x="39" y="249" height="89" width="73" source="@Embed('images/papaya.jpg')" click="onImageClick(image5)" />
        </mx:AddChild>
        <mx:AddChild relativeTo="{panel1}" position="lastChild">
            <mx:Image id="image6" x="144" y="249" height="89" width="73" click="onImageClick(image6)" source="@Embed('../../images/watermelon.jpg')"/>
        </mx:AddChild>
        <mx:SetProperty target="{panel1}" name="title" value="Fruits"/>
        <mx:AddChild relativeTo="{panel1}" position="lastChild">
            <mx:Image x="144" y="31" width="73" height="89" source="images/orange.jpg"/>
        </mx:AddChild>
    </mx:State>
</mx:states>
```

列表 6.9 - 向应用程序添加状态

5. 为了显示水果的详细信息，你可以再创建一个新状态，并将其命名为 `descriptionState`。此状态也基于基础状态。添加一个图像组件以显示图像，一个文本区域以提供关于该图像的一些描述，以及一个返回按钮以返回到上一个状态。还将面板标题更改为“水果描述”。这在*图 6.10* 中进行了说明。注意左上角显示的一张小图像。这表明尚未指定该图像的源。

![](img/c4119654311ebf24679359ca130a5ee6_129_0.png)

**图 6.10 - 添加第二个状态 - descriptionState**

6. 添加此状态后的源代码如*列表 6.10* 所示。
