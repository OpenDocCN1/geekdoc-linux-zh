
`% xmodmap .xmodmaprc`

其中 `.xmodmaprc` 包含以下行：

```
remove Lock = Caps_Lock
remove Control = Control_L
keysym Control_L = Caps_Lock
keysym Caps_Lock = Control_L
add Lock = Caps_Lock
add Control = Control_L
```

关于键编号是怎么回事？`Backspace` 在 Linux 下是 14，在 X 下是 22？怎么吧，这些编号最好被视为任意的；可以使用 `showkey(1)` 查找 Linux 键码，使用 `xev(1)` 查找 X 编号。通常 X 编号比 Linux 编号大 8 或更多。

此外，人们喜欢更改功能键的绑定。假设你想让 `F12` 变为字符串 `"emacs"`。

```
% loadkeys
keycode 88 = F12
string F12 = "emacs"
%
```

即可实现。更明确地说，步骤如下：(i) 使用 `showkey(1)` 找到要重新映射的按键的键码。(ii) 保存当前键映射，复制一份并进行编辑：

```
% dumpkeys > my_keymap
% cp my_keymap trial_keymap
% emacs trial_keymap
% loadkeys trial_keymap
%
```

表格的格式可以通过查看 `dumpkeys` 的输出来推测，并在 `keytables(5)` 中记录。当新键映射按预期工作时，你可以将一个调用

`loadkeys my_new_keymap`

放入 `/etc/rc.local` 或类似位置，以便在启动时自动执行。注意，修改键位是比较棘手的，新手很容易陷入没有专家可以摆脱的困境。

键映射的默认目录是 `/usr/lib/kbd/keymaps`。`/dev/tty0` 的默认扩展名是 `.map`。因此，`loadkeys` 可能会加载 `/usr/lib/kbd/keymaps/uk.map`。

（在我的机器上）`/dev/console` 是 `/dev/tty0` 的符号链接，但它是当前虚拟终端（VT）的同义词。`XFree861.3` 会更改 `/dev/tty0` 的所有者但在完成后不会重置。因此，`loadkeys` 或 `dumpkeys` 可能会因为其他人拥有 `/dev/tty0` 而失败；在这种情况下你可能需要运行 `root`。注意，当不是控制台且不是 `root` 时，无法更改键盘映射。

## 16.1 “我只能用手指打字”

“可以将 `Shift`、`Ctrl` 和 `Alt` 键制为开关切换模式吗？”

可以，在执行：

```
% loadkeys
keymaps 0-15
keycode 29 = Control_Lock
keycode 42 = Shift_Lock
keycode 56 = Alt_Lock
%
```

后，左侧 `Control`、`Shift` 和 `Alt` 键将充当切换键。涉及的数字可以通过 `showkey` 发现（通常左侧和右侧的 `control`、`shift` 和 `alt` 键数字分别是 29, 27, 42, 54, 56, 100），相应的功能为 `Control_Lock`, `Shift_Lock`, `Alt_Lock`, `AltGr_Lock`。

“‘粘性’（`sticky`）修饰键呢？”

从 1.33 版本开始，内核支持‘粘性’修饰键。这些键作用于下一个按下的键。因此，以前可能需要 3 符号序列 `Shift_Lock a Shift_Lock` 来输入 `‘A’`，现在可以使用 2 符号序列 `Shift_Lock`。早于 0.93 版本的 `kbd` 包尚未包含这些粘性修饰键的代码，需要使用它们的十六进制代码来调用它们。例如：

```
% loadkeys
keymaps 0-15
keycode 54 = 0x0c00
keycode 97 = 0x0c02
keycode 100 = 0x0c03
%
```

将右侧 `Shift`、`Ctrl`、`Alt` 变为左侧对应的粘性版本。> 从 0.93 开始，你可以说：

```
% loadkeys
keymaps 0-15
keycode 54 = SShift
keycode 97 = SCtrl
keycode 100 = SAlt
%
```

来获得相同的结果。这将允许你单手三次按键即可输入 `Ctrl-Alt-Del`。

这些示例中的 `keymaps` 行应该涵盖你正在使用的所有键映射。你可以通过以下命令找到正在使用的键映射：

```
% dumpkeys | head -1
```
