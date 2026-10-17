
```
backMC.attachMovie("star", "star1", 2 );

border=_root.backMC.star1.getBounds(_root.backMC.star1);

xright=border.yMax;

backMC.attachMovie("star", "star2", 3);

setProperty(_root.backMC.star2, _x, xright);

}
```

![](img/72fce958343eeb5d6d0322213ea85399_168_0.png)

- 4 将每个属性赋值给变量。
- 如果你将变量与动态文本框关联，你就可以向用户显示变量的返回值。
- 5 移动到测试环境。

注意：请参阅第 38 页关于如何测试你的电影的说明。

- 6 点击按钮测试你的电影。
- 当你点击按钮时，`xMin`、`xMax`、`yMin` 和 `yMax` 属性将显示在屏幕上。

153

# Flash Action Script

## 交换深度 SWAP DEPTHS

当你在舞台上放置对象时，Flash 会给它们一个较低的深度并进行堆叠。深度较高的电影剪看起来位于其他对象的前面。例如，如果你在舞台上使用两张照片并用一个电影剪切换全屏视图，你会发现当增加深度时，较低的层级会出现在深度较高的图像后面。当你有多个可拖拽对象时，可能会发生类似的问题。每个对象都有自己的层级。你可能希望用户能够拖动任何对象到顶部。通过使用 `swapDepths` 方法，你可以更改电影剪的堆叠顺序，使图像出现在你所需的层级。

`MovieClip.swapDepths` 的语法为 `movieClipName.swapDepths(depth/target)`。

使用 `movieClipName` 参数指定你想要交换深度的剪辑名称。使用 `target` 参数指定你想要交换深度的电影剪。换句话说，如果你想交换剪辑 A 与电影剪 B 的深度，请使用以下语法：`A.swapDepths(B);`。或者，使用 `target` 参数指定深度而不是使用目标。

使用 `swapDepths` 方法时，两个电影剪必须具有相同的父级。当你调用 `swapDepths` 方法时，如果电影剪正在补间（tween），补间将停止。

![](img/72fce958343eeb5d6d0322213ea85399_169_0.png)

- 1 选择你想添加 ActionScript 的帧、按钮或电影剪。

注意：此示例使用了 `swap.fla`，你可以在随书附带的 CD 中找到它。

注意：脚本与已转换为电影剪的按钮关联。要查看示例文件，请双击电影剪并打开动作面板（Actions panel）。

- 2 点击 `Window`（窗口）-> `Actions` 以打开动作面板。
- 3 将处理器设置为 `on (press )`。
- 4 交换电影剪的深度。
- 5 增大电影剪的大小。

154

# 使用电影剪和数组对象 7

## 练习

你可以使用 `swapDepths` 交换电影剪 A 与电影剪 B 的深度。接下来的脚本与一个按钮关联，并交换 `pictureA` 与 `pictureB` 的深度。

或者，你可以使用深度数字来更改电影剪的深度。接下来的脚本与一个按钮关联。

| 输入内容： |
| :--- |
| `on (release) { pictureA.swapDepths(pictureB); }` |

| 输入内容： |
| :--- |
| `on (release) { pictureA.swapDepths(100); }` |

| 结果： |
| 用户每当点击按钮时，Action 都会交换 `pictureA` 与 `pictureB` 的深度。 |

| 结果： |
| 用户每当释放点击按钮的鼠标时时，`pictureA` 都会移动到深度 100。 |

![](img/72fce958343eeb5d6d0322213ea85399_170_0.png)

- 6 将处理器设置为 `(release)`。
- 8 移动到测试环境。
- 9 当你点击图像时，深度层级切换到顶层且图像会放大。
- 7 将电影剪的大小还原为原始大小。
- 如果你想调整符号的深度，请对每个符号重复第 1 到 7 步。

注意：请参阅第 38 页关于如何测试你的移动的说明。

# Flash Action Script

## 检查电影剪加载 CHECK MOVIECLIP LOAD

你创建了电影剪 A 和 B。电影剪 B 是一个大型电影剪。你不希望剪辑 B 加载到电影剪 A 中。你不希望电影剪 B 在完全加载之前开始播放。使用 `getBytesTotal` 来确定电影剪 B 的字节大小。使用 `getBytesLoaded` 获取电影剪已加载的字节数。当 `getBytesTotal` 等于 `getBytesLoaded` 时，启动电影剪 B。

获取已加载的字节数或总字节数。`getBytesTotal` 和 `getBytesLoaded` 结合让你能够监控电影剪的加载进度。注意，并不总是需要等待电影剪加载。你不希望在电影剪完全加载之前开始播放。获取已加载的字节数或总字节数。

`getBytesTotal` 和 `getBytesLoaded` 结合让你能够监控电影剪的加载进度。注意，并不总是需要等待电影剪加载。

你不希望在电影剪完全加载之前开始播放。获取已加载的字节数或总字节数。

`getBytesTotal` 和 `getBytesLoaded` 结合让你能够监控电影剪的加载进度。注意，并不总是需要等待电影剪加载。

你不希望在电影剪完全加载之前开始播放。

检查电影剪

![](img/72fce958343eeb5d6d0322213ea85399_172_0.png)

## 附加

你可以使用 `hitTest` 来判断两个对象是否重叠。示例中的脚本当用户拖动蓝色点并使其与红色矩形碰撞时，会向变量 `collision` 返回布尔值 `true`。示例将变量 `collision` 赋值给动态文本框。`blueDot` 是一个可拖动的电影剪（movie clip）。`redBox` 是一个电影剪。你将动作分配给 `redBox`。

示例

```
onClipEvent (enterFrame) {

  root.collision = root.redBox.hitTest(root.blueDot);

}
```

你可以使用 `hitTest` 来判断两个对象是否发生碰撞。示例中的脚本当用户拖动蓝色点并使其与红点的 x 坐标和 y 坐标碰撞时，会向变量 `collision` 返回布尔值 `true`。示例将变量 `collision` 赋值给动态文本框。`blueDot` 是一个可拖动的电影剪。`redDot` 是一个在舞台（Stage）上进行补间动画的电影剪。变量 `a` 和 `b` 被赋值给动态框。它们捕获并显示 `redDot` 的 x 坐标和 y 坐标。你将动作分配给 `blueDot`。

示例

```
onClipEvent (enterFrame) {

  root.a = getProperty(_root.redDot, _x);

  root.b = getProperty(_root.redDot, _y);

  root.collision = _root.blueDot.hitTest(_root.a, _root.b, false);

}
```

![](img/72fce958343eeb5d6d0322213ea85399_174_0.png)

- 5 如果电影剪发生碰撞，将 `messageVisible` 属性设置为 `true`。
- 6 如果电影剪没有发生碰撞，将 `messageVisible` 属性设置为 `false`。
- 7 移动到测试环境。
注意：参阅第 38 页查看如何测试你的电影的说明。
- 8 当一辆车碰到另一辆车时，屏幕上会出现一条消息。

## 获取 X 和 Y 坐标

你可以使用 x 坐标和 y 坐标来辅助你在舞台上放置或定位对象。每个时间线都有 x 和 y 坐标。x 坐标标记了距离电影或电影剪左侧的距离。y 坐标标记了从电影或电影剪顶部到电影底部的距离。在主时间线上，x 坐标是电影的左侧，随着向右移动，x 坐标增加。y 坐标位于电影的顶部，随着向下移动，y 坐标增加。

在检索坐标时，使用 `globalToLocal` 方法获取电影剪的局部坐标。使用 `localToGlobal` 方法获取舞台坐标。

`MovieClip.globalToLocal` 和 `MovieClip.localToGlobal` 方法的语法为：

```
movieClipName.globalToLocal(point);

movieClipName.localToGlobal(point);
```
