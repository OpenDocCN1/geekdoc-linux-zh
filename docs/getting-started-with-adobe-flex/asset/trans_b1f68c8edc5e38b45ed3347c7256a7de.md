

但是，如果使用 *handlerFunction* 属性，事件监听函数将只接受一个事件对象作为参数，如下所示。

```xml
<mx:SetEventHandler target="(Button)" name="ButtonClick"
     handlerFunction="buttonHandler"/>
```

### 6.2.2.2 <mx:setProperty> 标签

<mx:setProperty> 标签用于设置将在特定视图状态下生效的某些属性值：

```xml
<mx:SetProperty target="(container)" name="alpha" value="0.5"/>
```

在此处，*target* 指定包含要更改属性的对象，*name* 是值需要更改的属性，*value* 是属性的新值。

### 6.2.2.3 <mx:setStyle> 标签

<mx:setStyle> 标签用于设置将在特定视图状态下生效的某些样式值：

```xml
<mx:SetStyle target="(this)" name="backgroundColor" value="#ffcccc"/>
```

在此处，*target* 指定要更改样式的对象，*name* 是需要更改的样式，*value* 是样式的新值。

## 6.2.3 添加组件

不仅可以在状态期间更改现有组件的行为或外观，还可以添加新组件或移除现有组件。其定义方法如下。

### 6.2.3.1 <mx:AddChild> 标签

此标签告知 Flex，当应用程序处于此状态时，需要添加一个子元素。该子元素可以是任何组件，例如按钮或文本区域。*列表 6.3* 展示了使用该标签的示例。

```xml
<mx:AddChild relativeTo="(panel1)" position="lastChild"
          creationPolicy="all">
      <mx:TextArea id="t1" text="New State"/>
</mx:AddChild>
```

而 `none` 值意味着子元素不会被创建，直到调用 `createInstance()` 方法来创建它。

### 6.2.3.2 <mx:RemoveChild> 标签

此标签告知 Flex，当应用程序处于此状态时，需要移除一个子元素。
该子元素可以是任何组件，例如按钮或 TextArea。

```xml
<mx:RemoveChild target="{linkButton1}"/>
```

# 6.3 行为

*效果* 是组件在预定持续时间（以毫秒计）内发生的一种可见变化。Flex 效果的示例包括 `wipedown` 效果、`blur` 效果和 `dissolve` 效果等。*触发器* 是一种动作，例如鼠标点击。
但是，不应将其与事件混淆。触发器导致效果发生，而事件则调用 Actionscript 函数或对象。例如，一个组件可以拥有 `focusOut` 事件和 `FocusOutEffect` 触发器。当效果与触发器关联注册时，就创建了一个*行为*。行为允许你为应用程序添加运动、声音和动画。

## 6.3.1 常用效果

*表 6.7* 列出了 Flex 支持的效果。

| 效果 | 描述 |
|---|---|
| AnimateProperty | 用于对组件的数值属性（如高度、宽度、scaleX 或 scaleY）进行动画处理。 |
| Blur | 用于对组件应用模糊视觉效果。 |
| Dissolve | 用于修改叠加层的 alpha 属性，使目标组件逐渐出现或消失。 |
| Fade | 用于对组件进行从透明到不透明，或从不透明到透明的动画处理。 |
| Glow | 用于对组件应用发光视觉效果。 |
| Iris | 通过扩展或收缩以目标为中心的矩形蒙版，对效果目标进行动画处理。 |
| Move | 用于在指定时间间隔内更改组件的位置。 |
| Pause | 在给定时间段内不做任何操作。 |
| Resize | 在指定时间框架内更改组件的宽度和高度。 |
| Rotate | 围绕特定点旋转组件。 |
| SoundEffect | 用于播放 MP3 音频文件。 |
| WipeLeft, WipeRight, WipeUp, WipeDown | 用于定义条形清除（Wipe）效果。 |
| Zoom | 用于从中心点放大或缩小组件。 |

表 6.7 - 常用效果

## 6.3.2 使用效果

你可以通过调用 pause()、resume() 或 end() 方法来改变效果的播放方式。pause() 方法暂停效果，resume() 方法允许你恢复暂停的效果，end() 方法结束正在播放的效果。

当效果开始时，会分发 startEffect 事件；当效果结束时，会分发 endEffect 事件。你可以根据需要使用这些事件并执行特定功能。

可以使用 <mx:sequence> 和 <mx:parallel> 标签分别顺序或并行播放效果。序列中定义的效果按顺序逐个播放，而并行中定义的效果则同时播放。

通过一个示例，你可以更好地了解如何使用效果。因此，让我们创建一个在用户点击图片时变模糊的图像。请遵循以下步骤：

- 1. 创建一个新的 Flex 项目。
- 2. 在 src 文件夹中添加一个 images 文件夹，并在此文件夹中添加一张图片。在本例中，我们有一张名为 rambutan.jpg 的图片，它包含在随附的 zip 文件（Exercise_Files_AdobeFlex.zip）中的 Chapter 6 子目录下。
- 3. 转到设计视图。拖放一个面板并在面板上添加一张图片。你可以选择面板的属性，或使用以下列表 6.4 中显示的属性。

```xml
<mx:Panel title="Blur Effect" layout="vertical" color="0xffffff"
borderAlpha="0.15" width="500" paddingTop="10" paddingRight="10"
paddingBottom="10" paddingLeft="10" horizontalAlign="center">
<mx:Image id="fruit"
source="@Embed(\"/assets/images/fruit.jpg\")"/>
</mx:Panel>
```

列表 6.4：向应用程序添加面板

- 4. 现在，你可以如下列表 6.5 所示定义模糊效果及其属性。

```xml
<mx:Blur id="blurImage" duration="1000"
blurXFrom="0.0" blurXTo="10.0"
blurYFrom="0.0" blurYTo="10.0"/>
<mx:Blur id="unblurImage" duration="1000"
blurXFrom="10.0" blurXTo="0.0"
blurYFrom="10.0" blurYTo="0.0"/>
```

列表 6.5 - 定义模糊效果

- 5. 现在你需要定义启动该效果的 `trigger`。效果的 `id` 属性指定当触发器发生时播放哪个效果。

```xml
<mx:Image id="fruit" source="@Embed('images/fruit.jpg')"
mouseDownEffect="{blurImage}" mouseUpEffect="{unblurImage}"/>
```

- 6. 继续运行此应用程序。你可以在 *图 6.7* 中看到，图片在点击时优雅地模糊，然后恢复初始状态。

![](img/c4119654311ebf24679359ca130a5ee6_123_0.png)

## 6.3.3 自定义效果

通过在代码中指定效果属性来自定义效果。例如，在上面的示例应用程序中，`duration` 属性定义了模糊持续的时间（以毫秒计）。

```xml
<mx:Blur id="blurImage" duration="1000" blurXFrom="0.0" blurXTo="10.0"
blurYFrom="0.0" blurYTo="10.0"/>
```

## 6.4 过渡

过渡是一种优雅地开启或关闭状态的方式。过渡实际上是分组在一起并在状态变化发生时播放的效果。过渡将其效果应用到一个或多个组件。与组件的 `states` 属性一样，`transitions` 属性也是继承自 `UIComponent` 类。

### 6.4.1 使状态更有趣

过渡和状态密切相关。State 类定义了所有将从基础状态变更的动作。这包括从基础视图状态添加或移除组件、设置属性、设置样式或设置事件处理程序。在 transitions 类中，你定义了所有这些动作的顺序。在状态中发生的更改在过渡定义中再次声明。如果你没有将过渡应用于某个状态，则该状态的更改将立即应用，不会发生过渡。

你可以拥有来自不同状态的不同过渡。<mx:transitions> 标签定义了一个过渡对象数组。<mx:Transition> 标签定义了一个过渡。它具有 toState 和 fromState 属性，指定需要应用过渡的状态。默认情况下，fromState 和 toState 属性都设置为 "*"，即从任意状态到任意状态应用过渡。fromState 属性指定你正在从中更改的视图状态，而 toState 属性指定你正在更改到的视图状态。使用过渡，你可以指定以并行或序列顺序应用更改。语法如下：

```xml
<mx:Transition id="ID" fromState="*" toState="*" />
```

### 6.4.2 使用动作效果

Flex 定义了几种动作效果，以控制过渡发生时视图状态更改的顺序。当创建视图状态时，有四个类用于定义视图状态。这些类中的每一个都有一个对应的动作效果，用于控制由视图状态属性定义的更改在过渡中何时发生。

表 6.2 描述了动作效果

| 动作效果 | 对应的视图状态类 | 用途 |
| :--- | :--- | :--- |
| SetPropertyAction | SetProperty | 用于作为过渡的一部分设置属性值。 |
| SetStyleAction | SetStyle | 用于作为过渡的一部分将样式设置为某个值。 |
| AddChildAction | AddChild | 用于作为过渡的一部分添加子元素。 |
| RemoveChildAction | RemoveChild | 用于作为过渡的一部分移除子元素。 |

表 6.2 - 动作效果

现在，让我们在之前关于状态的示例中添加一些过渡，看看它是如何工作的。

