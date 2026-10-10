
```javascript
if (retain) {
  index = text.indexOf(search, start);
  if (index != -1) {
    Selection.setSelected(text);
    Selection.setSelected(index, index + length(search));
    start = index + 1;
  } else {
  start = 0;
    message = "文本结束。未找到。再次点击以从开头开始";
  }
}
```

![](img/72fce958343eeb5d6d0322213ea85399_264_0.png)

## 使用创意技巧 12

## 额外内容

`String.lastIndexOf` 方法在字符串中搜索指定的值，并返回该值最后一次出现的索引位置。你可以使用 `lastIndexOf` 方法从底部开始搜索文本框，如下所示。

```javascript
if (text.lastIndexOf(searchV, startV) != -1) {
Selection.setFocus("text");
```

```javascript
Selection.setSelection(text.lastIndexOf(searchV, startV), text.lastIndexOf(searchV, startV) + length(searchV));
startV = text.lastIndexOf(searchV, startV) - 1;
messageV = "\*";
} else {
startV = 0;
startV = length(text);
messageV = "文本开头。未找到条目。点击按钮重新开始。
}
```

![](img/72fce958343eeb5d6d0322213ea85399_266_0.png)

![](img/72fce958343eeb5d6d0322213ea85399_266_1.png)

| 搜索 | Bill |

|---|---|

| Peter Bill George |

| Allen Bill Fred |

| Peter George Tom |

| Allen Tom Peter |

- 10 向用户发送消息。
- 17 到测试环境。

注意：查看第 38 页有关如何测试你的电影的说明。

- 18 先输入一个名称来测试你的电影。
- 19 点击搜索按钮。
- ActionScript 搜索你输入的值。

## FLASH ACTIONSCRIPT

### 转换符号

但按钮有几个你可以用来触发动作的处理器。电影剪辑（Movie clips）也有许多你可以用来触发动作的处理器。有时你可能同时使用电影剪辑和按钮处理器。在这种情况下，你必须将按钮转换为电影剪辑，或反之。

创建一个执行连续动作的按钮，是你需要将按钮转换为电影剪辑的一个良好示例。如果你转换一个执行连续动作的按钮（例如当用户点击对象时旋转对象，并在用户按住按钮时旋转对象），你需要使用按钮的 `on(press)` 和 `(release)` 处理器以及电影剪辑的 `onClipEvent(enterFrame)` 处理器。

`on(press)` 处理器在用户点击对象时触发动作。`on(release)` 处理器在用户释放鼠标时触发动作。使用 `on(press)` 启动连续动作，使用 `on(release)` 停止连续动作。

创建连续动作的方便技巧是创建一个带带有 `onClipEvent(enterFrame)` 处理器的单帧电影或电影剪辑。当你对单帧电影使用 `onClipEvent(enterFrame)` 处理器时，帧中的动作会连续执行，从而创建出连续动作。

要让这些动作相互配合，你必须创建一个用于启动和停止该动作的按钮，然后将按钮转换为电影剪辑。使用属性（Properties）对话框将按钮转换为电影剪辑。

创建一个用户可以点击并拖拽的对象是另一个需要将按钮转换为电影剪辑的常见示例。更多关于创建可拖动对象的信息，请参阅第 2 章。

![](img/72fce958343eeb5d6d0322213ea85399_267_0.png)

![](img/72fce958343eeb5d6d0322213ea85399_267_1.png)

| Flash [1204cha.flc] | Flash [1204cha.flc] | | | | | | | |

|---|---|---|---|---|---|---|---|---|

| 工具 | 场景 | 修改 | 测试 | 控制 | 窗口 | 帮助 | | |

| | | | | | | | | | |

| 动作 | | | | | | | | | |

| on(press, release) | | | | | | | | | |

| on (release, rollout) | | | | | | | | | |

| press = false; | | | | | | | | | |

| | | | | | | | | | |

| 运动引导 | | | | | | | | | |

| | 帧 | | | | | | | | |

| 关键帧 | | | | | | | | | |

| 黑色关键帧 | | | | | | | | | |

| 笼形关键帧 | | | | | | | | | | |

| 创建运动 | | | | | | | | | | |

| 补间 | | | | | | | | | | |

| 得分 | | | | | | | | | | |

- 1 创建一个按钮。
- 2 添加 ActionScript。
- 3 点击“插入：转换为符号”以打开符号属性对话框。

注意：此示例使用了文件点击，你可以在随书的 CD-ROM 上找到它。

注意：查看第 12 页有关创建按钮的信息。

## 额外内容

将按钮转换为电影剪辑后，你必须选择该电影剪辑，点击“编辑 ✎ 符号”，并打开动作（Actions）面板来编辑与按钮关联的脚本。编辑脚本后，点击“编辑 ↩ 符号”返回主时间轴。你也可以通过双击电影剪辑然后打开动作面板来编辑脚本。

![](img/72fce958343eeb5d6d0322213ea85399_268_0.png)

|  own | checkMC | |

|---|---|---|

| 行为 | 电影剪辑 | 取消 |

| 返回 | | |

- 输入符号名称。
- 点击电影剪辑。
- 点击确定。
- 按钮现在是电影剪辑。
- 选择电影剪辑。
- 添加 ActionScript。

## FLASH SCRIPTING

### 创建特效

显而易见，你可以使用电影剪辑来创建特效。可能不明显的是如何创建它们。例如，你可以使用 `rotation` 属性设置对象的值。当你将对象放在舞台上时，它的旋转值为 0。要让对象顺时针旋转，增加该值；要让对象逆时针旋转，减小该值。你应该在每个电影剪辑上尝试一下。

如果你添加了一些额外的脚本 `rotation += x`，你就可以创建一个在点击时旋转、释放鼠标时停止的对象。你可以使用表达式 `rotation += x` 制作许多有趣的特效，其中 `x` 的值越大，对象旋转越快。负的 `x` 会让对象逆时针旋转。

如果你使用 `rotation += y` 属性或 `y` 值，可以同时旋转对象。然而，你必须添加一些额外的代码来限制对象移动的区域，否则对象可能会移出舞台。你也可以使用表达式 `rotation = _mouse` 来创建特效。你可以通过点击让对象绕其注册点（registration point）旋转。你可以更改注册点来改变角度。

使用 `rotation += x` 配合 `onClick(enterFrame)` 可以创建一个持续旋转的对象。

![](img/72fce958343eeb5d6d0322213ea85399_269_0.png)

- 1 选择想要添加 ActionScript 的帧、按钮或电影剪辑。
- 2 点击窗口打开面板。
- 3 选择事件处理器。

注意：此示例使用了 `rotate.fla`，你可以在随书的 CD-ROM 上找到它。

## 额外内容

要让按钮持续旋转，你可以向它附加这里的脚本。当鼠标悬停在对象上时，它会持续旋转直到鼠标移出。

```javascript
on (rollOver) {
press = true;
}
on (rollout) {
press = false;
}
```

然后将按钮转换为电影剪辑，并将这里的脚本附加到它上。变量是文本框的名称。在这个示例中，`frogMC` 是电影剪辑。

```javascript
onClipEvent(enterFrame) {
if (press == true) {
root.frogMC.rotation = root.frogMC.rotation + 10;
}
}
```

![](img/72fce958343eeb5d6d0322213ea85399_270_0.png)
