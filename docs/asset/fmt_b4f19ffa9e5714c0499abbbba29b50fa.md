
```
onOff = "Click to Stop";
} else {
    beat.stop();
    status = false;
    onOff = "Click for Music";
}
```

![](img/72fce958343eeb5d6d0322213ea85399_218_0.png)

## 添加声音

- 1 选择你想添加 ActionScript 的帧、按钮或电影剪。
- 2 点击 Window Actions 打开 Actions 面板。
- 3 将变量设置为 `false`。你正在初始化该变量；通常在第 1 帧初始化变量。在这种情况下，`false` 表示没有声音在播放。

## 使用声音对象（续）

你使用 `start` 方法来播放声音。`Sound.start` 方法的语法为：

```
soundName.start(secondoffset, offset);
```

使用 `idName` 参数来指定声音对象的名称。`secondOffset` 参数用于指定你希望从哪里开始播放。如果你有一个 20 秒的声音，并且使用的 `secondOffset` 为 10，那么声音将从声音的中间开始播放。注意，播放并没有删除前 10 秒，而是从第 10 秒处开始播放声音。`secondOffset` 参数是可选的。使用 `loop` 参数来指定声音循环的次数。

使用 `stop` 方法来停止声音。使用 `idName` 参数来指定你停止的的名称。将 `idName` 包含在引号中。`idName` 参数是可选的。如果你不指定 `idName`，所有声音都将停止。

你也可以使用 `stopAllSounds` 动作来停止声音。设置 `streaming` 在播放头移动过时恢复。`stopAllSounds` 动作的语法为：

```
stopAllSounds();
```

`stopAllSounds` 动作不接受任何参数。

在 Flash 中，你可以同时播放多个声音。你可以在旁白解说你的视频时播放背景音乐。你可以在帧中或使用按钮或电影剪辑来启动声音。这意味着你可以通过按钮、当用户悬停或进入某一帧时停止声音。

一旦你启动了声音，你就可以使用 `stop` 参数来停止。`stop` 参数的语法为：

```
soundName.stop("idName");
```

![](img/72fce958343eeb5d6d0322213ea85399_219_0.png)

- 选择你想要添加 ActionScript 的帧、按钮或电影剪辑。
- 使用 `if` 语句测试你在第 1 帧中设置的变量。
- 如果变量等于 `false`，则执行该语句。
- 创建一个 `Sound` 对象。
- 使用你在“符号链接属性”（Symbol Linkage Properties）对话框中赋予声音的实例名称。
- 启动声音。

## 额外

你可以使用类似下面这样的脚本来增加声音的音量。在这个脚本中，如果音量小于 95，则每当用户点击按钮后释放鼠标时，脚本会将音量增加 5。如果音量大于或等于 95，脚本会将音量设置为 100。你可以以相同的方法创建一个单独的按钮来减少音量。

### 按钮

```
on (release) {
  vol = beat.getVolume();
  if (vol < 95) {
    beat.setVolume(vol + 5);
  } else {
    beat.setVolume(100);
  }
  vol = beat.getVolume();
}
```

![](img/72fce958343eeb5d6d0322213ea85399_220_0.png)

![](img/72fce958343eeb5d6d0322213ea85399_220_1.png)

- 9 重置变量的值。
- 声音正在播放，因此你将 `status` 设置为 `true`。
- 10 创建一个 `else` 语句。
- 如果 `status` 不等于 `false`，这些语句将执行。
- 11 移动到测试环境。
- 12 重置变量的值。
- 声音不再执行，因此你将 `status` 设置为 `false`。
- 14 点击按钮测试你的电影。
- 点击按钮切换声音的开启和关闭。

## 设置音量和声平衡

ActionScript 提供了允许你调整音量和声平衡的方法，或者赋予你调整音量和声平衡的能力。你使用 `setVolume` 方法来调整声音音量。`setVolume` 方法的语法为：

```
soundName.setVolume(volume);
```

使用 `soundName` 参数指定声音对象的名称。使用 `pan` 参数指定一个在 -100 到 100 之间的整数。`pan` 为 -100 只使用左扬声器。`pan` 为 0 等于两个扬声器之间的中心。你可以使用 `setPan` 将声音从一个扬声器淡入到另一个。

使用 `soundName` 参数指定声音对象的名称。使用 `volume` 参数指定一个在 0 到 100 之间的整数，代表音量级。值 100 代表全音量。值 0 代表无声音。默认值为 100。

要获取当前音量级，使用 `getVolume` 方法。`getVolume` 方法的语法为：

```
soundName.getVolume();
```

使用 `getPan` 方法获取当前的声平衡值。`getPan` 方法的语法为：

```
soundName.getPan();
```

`getVolume` 方法返回 1 到 100 之间的值，代表当前音量。

ActionScript 包含一个 `soundbuffer` 动作。`soundbuffer` 动作建立缓冲的秒数。默认是 5 秒。`soundbuffer` 动作的语法为：

你使用 `setPan` 方法控制声音在每个扬声器中的播放方式。`setPan` 方法的语法为：

```
soundbuffer = integer;
```

## 设置音量和声平衡

![](img/72fce958343eeb5d6d0322213ea85399_221_0.png)

![](img/72fce958343eeb5d6d0322213ea85399_221_1.png)

- 1 选择你想要添加 ActionScript 的帧、按钮或电影剪辑。
- 2 点击 Window Actions 打开 Actions 面板。
- 3 创建一个 `Sound` 对象。
- 4 获取音量。
- 5 使用 `setPan` 方法。
- 6 使用 `getPan` 方法。
- 7 使用 `getVolume` 方法。
- 8 `soundbuffer` 动作
- 9 重置变量的值。
- 声音正在播放，因此你将 `status` 设置为 `true`。
- 10 创建一个 `else` 语句。
- 如果 `status` 不等于 `false`，这些语句将执行。
- 11 移动到测试环境。
- 12 重置变量的值。
- 声音不再执行，因此你将 `status` 设置为 `false`。
- 14 点击按钮测试你的电影。
- 点击按钮切换声音的开启和关闭。

## 额外

你可以使用类似于这个的脚本来增加声音的音量。在这个脚本中，如果音量小于 95，则每当用户点击按钮后释放鼠标时，脚本会将音量增加 5。如果音量大于或等于 95，脚本会将音量设置为 100。你可以以相同的方法创建一个单独的按钮来减少音量。

### 按钮

```
on (release) {
  vol = beat.getVolume();
  if (vol < 95) {
    beat.setVolume(vol + 5);
  } else {
    beat.setVolume(100);
  }
  vol = beat.getVolume();
}
```

## 设置音量和声平衡

ActionScript 提供了允许你调整音量和声平衡的方法，或者赋予你调整音量和声平衡的能力。你使用 `setVolume` 方法来调整声音音量。`setVolume` 方法的语法为：

```
soundName.setVolume(volume);
```

使用 `soundName` 参数指定声音对象的名称。使用 `pan` 参数指定一个在 -100 到 100 之间的整数。`pan` 为 -100 只使用左扬声器。`pan` 为 0 等于两个扬声器之间的中心。你可以使用 `setPan` 将声音从一个扬声器淡入到另一个。

使用 `soundName` 参数指定声音对象的名称。使用 `volume` 参数指定一个在 0 到 100 之间的整数，代表音量级。值 100 代表全音量。值 0 代表无声音。默认值为 100。

要获取当前音量级，使用 `getVolume` 方法。`getVolume` 方法的语法为：

```
soundName.getVolume();
```

使用 `getPan` 方法获取当前的声平衡值。`getPan` 方法的语法为：

```
soundName.getPan();
```
