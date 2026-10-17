
`+ sunFunctionKeys` (`class SunFunctionKeys`)

`+ waitWaitMap` (`class WaitMap`)

指定 `xterm` 是否应该在启动子进程之前等待初始窗口映射（map）。默认是 `false`。

# 第一部分：用户命令

以下资源作为 `vt100` 控件（`class VT100`）的一部分指定：

`allowSendEvents` (`class allowSendEvents`)

指定是否解释或丢弃合成按键和按钮事件（使用 `x` 协议的 `SendEvent` 请求生成的事件）。默认是 `False`，意味着它们被丢弃了。注意，允许此类事件会产生巨大的资源漏洞。

`alwaysHighlight` (`class AlwaysHighlight`)

指定 `xterm` 是否始终显示高亮光标。默认情况下，当指针移动过窗口并失去焦点时，会显示文本光标。

`cursorDefault` (`class AppcursorDefault`)

如果为 `true`，方向键初始为应用程序模式。默认是 `False`。

`keypadDefault` (`class AppkeypadDefault`)

如果为 `true`，小键盘初始为应用程序模式。默认是 `False`。

`autoWrap` (`class AutoWrap`)

指定是否启用自动换行。默认是 `true`。

`bellSuppressTime` (`class BellSuppressTime`)

在发送铃声命令后的毫秒数内将抑制额外的铃声。默认是 `208`。如果设置为非零，则在服务器报告第一个铃声处理完成之前将抑制额外的铃声，此功能在具有可见铃声时最有用。

指定用于覆盖（overstriking）的字体名称。

`boldFont` (`class BoldFont`)

指定是否尊重 `VT102` `DE`。默认是 `false`。

`c132` (`class C132`)

如果为 `false`，三击选择行不包含行尾的换行符。如果为 `true`，则选择换行符。默认是 `true`。

`cutLine` (`class CutLine`)

如果为 `false`，三击选择行仅选择当前单词。如果为 `true`，则选择整行。

`cutToBeBeginningOfLine` (`class CutToBeBeginningOfLine`)

指定字符类绑定的逗号列表 `[low--high]:values`，用于确定字符集在剪切和粘贴时是否被相同的处理。参见指定字符类的章节。

`charClass` (`class CharClass`)

指定是否对最后一列进行回绕。详情见 `-cu` 选项。默认是 `false`。

`background` (`class Background`)

指定窗口背景使用的颜色。默认为白色。

`foreground` (`class Foreground`)

指定用于显示文本的颜色。设置类名而不是实例名是一种简单的方法，可以让所有通常显示在文本颜色中的内容都变为默认值。默认为黑色。

`cursorColor` (`class Foreground`)

指定用于文本光标的颜色。默认为黑色。

`eightBitInput` (`class EightBitInput`)

如果为 `true`，输入的元字符将作为开启第 8 的单字符呈现。如果为 `false`，元字符将转换为两个字符的序列，在字符本身前加上 `ESC`。默认是 `true`。

# xterm

## `eightBitOutput` (`class EightBitOutput`)

指定从主机发送的 8 位字符在打印时是按原样接受还是被剔除。默认值为 `true`。

- `font` (`class Font`)
- `font1` (`class Font1`)
- `font2` (`class Font2`)
- `font3` (`class Font3`)
- `font4` (`class Font4`)
- `font5` (`class Font5`)
- `font6` (`class Font6`)
- `geometry` (`class Geometry`)

指定普通字体的名称。默认为等宽（`fixed`）。

指定第一个备用字体名称。

指定第二个备用字体名称。

指定第三个备用字体名称。

指定第四个备用字体名称。

指定第五个备用字体名称。

指定 `VT102` 窗口的首选大小和位置。

## `hpLowerleftBugCompat` (`class hpLowerleftBugCompat`)

指定是否绕过 `HP` `xdb` 中的 bug，忽略 `term` 并发送 `ESC F` 以移动到左下角，这会导致 `xtierm` 将 `ESC F` 解释为移动到屏幕左下角的请求。`false`。

## `internalBorder` (`class BorderWidth`)

## `jumpScroll` (`class JumpScroll`)

## `loginShell` (`class LoginShell`)

## `marginBell` (`class MarginBell`)

## `multiClickTime` (`class MultiClickTime`)

## `multiScroll` (`class MultiScroll`)

## `MarginBell` (`class Column`)

指定字符与底部边界之间的像素数。默认值为 `2`。

指定是否使用跳跃滚动（`jump scroll`）。默认值为 `true`。

指定是否应在作为登录 shell 启动的窗口中运行 shell。默认值为 `false`。

指定当用户输入右侧边距时是否运行响铃（bell）。默认值为 `false`。

指定多次点击事件之间的最大时间（单位毫秒）。默认值为 `250` 毫秒。

指定是否应异步执行滚动。默认值为 `true`。

当启用时，指定在触发响铃时距离右侧边距的字符数。

## `pointerColor` (`class Foreground`)

## `pointerColorBackground` (`class Background`)

## `pointerShape` (`class Cursor`)

## `resizeGravity` (`class ResizeGravity`)

指定指针的前景色。默认值为 `DefaultForeground`。

指定指针的背景颜色。默认值为 `XtDefaultBackground`。

指定指针的名称。默认是 `xterm`。

影响窗口调整大小为更高或更矮时的行为。`Northwest`（西北）指定屏幕上的第一行文本保持在底部；如果窗口变高，则在底部添加空行；这与 `R4` 的行为兼容。`Southwest`（默认值）指定屏幕上的文本行固定。如果窗口变短，额外的保存行将向下滚动到屏幕；如果窗口变短，顶部的保存行将被丢弃。

## `reverseVideo` (`class ReverseVideo`)

指定是否模拟反色视频显示（reverse video）。默认值为 `false`。

# 第一部分：用户命令

## `reverseWrap` (`class ReverseWrap`)

指定是否启用反向回绕（`reversewraparound`）。默认值为 `false`。

## `saveLines` (`class SaveLines`)

指定开启滚动条时，屏幕顶部之外保存的行数。默认值为 `64`。

## `scrollBar` (`class ScrollBar`)

指定是否显示滚动条。默认值为 `false`。

## `scrollTTY` (`class ScrollCond`)

指定输出到终端的内容是否自动导致滚动到滚动区域的底部。默认值为 `true`。

## `scrollKey` (`class ScrollCond`)

指定按键是否自动导致滚动条到达滚动区域的底部。默认值为 `false`。

## `scrollLines` (`class ScrollLines`)

指定滚动行数。

## `scrollLines` (`class ScrollIn`)

指定在启用时，滚动时距离右侧边距的字符数。

`class` (`class ScrollLines`)

指定是否在 `Tek` 窗口滚动时禁用某些功能。默认值为 `false`。

## `tekGeometry` (`class Geometry`)

指定 `Tek` 窗口的大小和位置。

## `tekInhibit` (`class TekInhibit`)

指定是否禁用 `Tek` 窗口。默认值为 `false`。

## `tekSmall` (`class Small`)

指定是否以最小化模式启动。

## `tekStartup` (`class TekStartup`)

指定是否应以登录 shell 启动窗口。默认值为 `false`。

## `titleInhibit` (`class TitleInhibit`)

指定是否禁用显示标题。默认值为 `false`。

## `translations` (`class Translations`)

指定输出到终端的内容是否自动导致滚动到滚动区域的底部（此处与 `scrollTTY` 类似）。

## `visualBell` (`class VisualBell`)

指定在响铃时是否运行视觉响铃。默认值为 `false`。

## `width` (`class Width`)

指定 `Tek` 窗口的宽度。

## `height` (`class Height`)

指定窗口的高度。

## `fontLarge` (`class Font`)

指定用于 `Tek` 窗口的大字体。
