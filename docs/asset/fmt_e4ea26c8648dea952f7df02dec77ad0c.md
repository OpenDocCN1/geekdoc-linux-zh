
3. 点击主工具栏上的`Select and Move`工具。然后点击并拖动`SUN`光变换发生器（`Transform gizmo`）的`Y`轴句柄，将其移动到图 7.2 所示的位置。一旦移动了光，你会看到`Perspective viewport`的光照发生了变化。

4. 点击主工具栏上的`Select by Name`工具。点击列表中的`SUN.Target`并点击选择。或者，在选中灯光的情况下，可以右键点击并从`Tools`菜单中选择`Select Light Target`来选择目标。

5. 在`Select and Move`工具激活状态下，点击并拖动目标位置向上，如图 7.2 所示。你可以使用`Perspective viewport`中的`SUN`光来帮助匹配目标位置。

光源及其目标是独立移动，但它们是相互关联的。如果你需要同时移动两个对象，可以选中并移动连接它们的线。你还会发现使用`Smooth + Highlights`渲染模式的视口会提供光对模型影响的即时反馈。

# 使用`DAYLIGHT`和`SUNLIGHT`系统创建准确的日光环境

日光系统可以用于阴影研究以及创建设计准确的日光表现。它模拟了场景的颜色、强度和表面反射，并考虑了来自天空的“天光”或通用的天空漫射光。日光系统放置了一个名为`IES`（照明工程学会）太阳的特殊光源，它可以根据地理位置、一天中的时间和一年季节更准确地模拟阳光的位置和强度。日光系统旨在与`radiance`配合使用。另一个阳光系统则设计用于像`Default Renderer`一样良好工作，因为它使用的是直接光源而不是`IES`太阳。

为了充分利用日光和阳光系统的功能，你需要设置`North Direction`参数，以在南北方向上准确对齐你的模型。你还需要知道建筑和场址的位置，以及你希望太阳出现的时间。一旦确定了这些标准，就可以相当容易地设置你选择的系统。你将在第 11 章中学习更多关于此功能的内容。

# 编辑聚光灯

你的新聚光灯有许多可用设置。你可以设置强度、颜色，甚至是光的形状，这仅仅是举例。但你将使用的两个设置最像强度和光锥。强度在`Intensity/Color/Attenuation`卷轴中设置，光锥在`Spotlight Parameters`卷轴中设置。

让我们先查看`Hotspot`和`Falloff`设置：

1. 首先，使用`Object`工具选择聚光灯（而不是它的目标）。

2. 点击命令面板中的`Modify`选项卡；向下滚动并打开`Spotlight Parameters`卷轴。

3. 点击并拖动`Falloff/Field`计数器，直到其值达到 12。你会发现光范围缩小了，只在模型的一小部分上照射。注意当你减少`Falloff/Field`值时，`Hotspot/Beam`值也会下降。`Hotspot/Beam`至少比`Falloff/Field`小两个度数。

![](img/7e143440dd5a0ed9683d4f26f3c074f8_360_0.png)

4. 点击并拖动`Hotspot/Beam`计数器，直到其达到 50。光扩散到更大的区域。注意`Falloff/Field`值也增加了，保持了略大的值。

5. 现在，点击并拖动`Hotspot/Beam`计数器到约 20。这会让`Falloff/Field`值保持不变，而热点变小。

6. 将`Hotspot/Beam`值设置为约为 34，`Falloff/Field`值设置为约为 36。

`Hotspot/Beam`和`Falloff/Field`计数器控制聚光灯的扩散。`Hotspot/Beam`控制光最强的区域；`Hotspot`内部的所有区域将接收完全的光强。`Falloff/Field`控制光减至零的地方；`Falloff`之外的任何地方都不接收光照。光内最大强度与边缘的零强度之间存在连续的梯度。`Hotspot`和`Falloff`控制之间的差异越大，到光边缘的过渡就越平滑。这在`Perspective viewport`很难看到，但在渲染视图中会明显；你稍会在本书中看到这一点。`Directional lights`具有相同的`Hotspot`和`Falloff`控制；但它们没有形状限制。现在，尝试通过`Multiplier`输入框设置光强。

1. 在命令面板的`Modify`选项卡上，展开`Intensity/Color/Attenuation`卷轴；然后点击并拖动`Multiplier`输入框。

![](img/7e143440dd5a0ed9683d4f26f3c074f8_361_0.png)

当你减少`Multiplier`时，`Perspective viewport`中的值变暗。记住，这是因为`SUN.Target`是唯一照明场景的光。如果你将光的`Multiplier`设置为零，将没有任何光。

2. 点击主工具栏上的`Undo`工具将`Multiplier`恢复为 1。

# 在调整现有光后创建新光

请注意，当你在调整现有光的`Multiplier`后创建新灯光时，新光的默认值将与上一个光的修改值匹配。

`Multiplier`计数器控制光源的整体强度。从技术上讲，它乘以颜色值得到总强度。你可以使用`RGB`（红、绿、蓝）或`HSV`（色相、饱和度和值）来更改光源的颜色。你使用图 7.3 所示的`Color Selector`选择颜色。

要打开颜色选择器对话框，点击`Intensity/Color/Attenuation`卷轴中`Multiplier`计数器旁边的颜色块。

![](img/7e143440dd5a0ed9683d4f26f3c074f8_361_1.png)

## 图 7.3

颜色选择器对话框

![](img/7c74f8_361_2.png)

颜色选择器对话框让你在对话框的右下角作为样本查看所选的颜色。在它左侧相邻的是打开颜色选择器时块中的原始颜色。当你想要对比新旧颜色时，此功能非常有用。如果你选择的光不合适且尚未退出颜色选择器，请使用`Reset`按钮将光恢复到进行任何修改之前的颜色。

最后，如果你认为选定的光不适合当前任务，可以使用`General Parameters`卷轴中的`Light Type`下拉列表来更改使用的光类型。

![](img/7e143440dd5a0ed9683d4f26f3c074f8_362_0.png)

此工具带有同一组中的`Targeted`选项提供了一种方便的方法来更改光类型，而无需删除光并创建一个新的。

# 光类型

正如我在上一节中提到的，一旦你在模型中放置了灯光，就不受限于所选择的光类型。你可以在命令面板的`Modify`选项卡中进行更改。

你被要求使用`Target Spot`创建阳光源。用灯光代表太阳并没有错，但`Target Direct`实际上是太阳更合适的标准光源。

> 将太阳视为直接光

来自`VIZ`目标或`Free Direct`的光线是平行的，就像真实太阳的光线相对于地球基本上是平行的一样。由于太阳的相对以及它们之间巨大的距离，太阳的光线几乎是平行的。尽管太阳实际上是一个`Omni light source`，它距离地球约 9300 万英里，因此从我们的角度来看，照射地球的光线基本上是平行的。

以下是如何从`Target Spot`更改为`Target Direct`：

1. 点击`General Parameters`卷轴中的`Light Type`下拉列表并选择`Directional`。同时确保勾选了`Targeted`选项。由聚光灯创建的定向光产生的光与原始聚光灯的范围相比，可能非常小。

![](img/7e143440dd5a0ed9683d4f26f3c074f8_362_1.png)

注意，灯光在视口中更改了图标以表示`Target Direct`对象。你可能还会注意到，灯光没有显示锥体，而是显示一个窄圆柱体，以指示光线的方向和平行扩散范围。你可以在`Left`视口中最清晰地看到这个柱体。

![](img/7e143440dd5a0ed9683d4f26f3c074f8_363_0.png)

2. 向下滚动`Modify`面板并打开`Directional Parameters`展开列表。

| 方向参数 | | |
| :--- | :--- | :--- |
| `Light Cone` | `Show Cone: Overshoot` | |
| `Hotspot/Beam`: 34.0m | `Falloff/Field`: 36.0m | |
| `Circle` | `Rectangle` | |
| `Aspect`: 1.0 | `Bitmap Fit` | |

3. 点击并拖动`Hotspot/Beam`调节器，直到其值显示为800左右，点击并拖动`Falloff/Field`调节器，直到其值显示为850m。你会看到光扩大形成一个大圆柱体，如图 7.4 所示。

## 图 7.4

光照和衰减的增加

![](img/7e143440dd5a0ed9683d4f26f3c074f8_363_1.png)

如前所述，`Target Direct`光源产生的光是平行的，因此光表现为圆柱体。`Target Spot`的光线是发散的，光形成锥体。两种光源都提供`Falloff`来柔化光的边缘。许多其他参数与灯光对象相关，你将在后面的章节中学习更多用法。现在，让我们来看看光照和相机位置如何影响你的渲染。
