
注意，这只会在不使用修饰符时更改这些键的功能。（你需要指定一个键映射来告诉哪些键映射应该受影响。）尽管这两个系统并非 100% 兼容，但这意味着在很多情况下使用 `rmodmap` 已经变得多余了。在很多情况下，使用

```bash
% mykeys
% xmodmap myxmap
```

```
(define-key map "\177" 'isearch-delete-char')
(define-key map "\C-h" 'isearch-mode-help')
```

这意味着使用两个 `global-set-key` 命令可能不是一个好主意。在很多地方，对于 `'H = help` 和 `DEL = delete'` 有内置假设。这并不意味着你必须设置按键让 `Backspace` 生成 `DEL`。但如果它没有这样做，最简单的方法是在 `emacs` 的最低级别对它们进行重映射。

## 6.5 如何告诉 `emacs` 交换 `Delete` 和 `Backspace`

在 `.emacs` 文件中放入以下行：

```
(setq keyboard-translate-table (make-string 128 0))

(let ((i 0))
  (while (< i 128)
    (aset keyboard-translate-table i i)
    (setq i (1+ i))))

(aset keyboard-translate-table "\177" ?\C-?)
(aset keyboard-translate-table "\C-?" ?\C-h)
```

较新版本的 `emacs` 有一个函数 `keyboard-translate`，你可以将上述内容简化为：

```
(keyboard-translate ?\C-h ?\C-?)
(keyboard-translate ?\C-? ?\C-h)
```

注意，`emacs` 可以区分 `Ctrl-h` 和 `Backspace` 键（无论这些在控制台上产生什么代码），并且默认情况下 `emacs` 会将 `Backspace` 键视为 `DEL`（因此执行绑定到该字符的删除操作，而不是绑定到 `'H'` 的帮助操作）。你可以通过以下方式区分 `Backspace` 和 `Delete`：

```
(global-unset-key [backspace])
(global-set-key [backspace] 'delete-backward-char)

(global-unset-key [delete])
(global-set-key [delete] 'delete-char)
```

## 6.6 如何告诉 `kerm` 交换 `Delete` 和 `Backspace`

在 `.kermrc` 文件中放入以下行：

```
set key \127 \8
set key \8 \127
```

## 6.7 如何告诉 `xterm` 你的喜好的 `tty` 模式

普通的 `xterm` 将继承其调用者的 `tty` 模式。在 `xdm` 下，默认的擦除和删除命令是 `#` 和 `_`，就像旧的 `Unix Version 6` 一样。如果你喜欢，可以放入如下内容：

```
XTerm*ttymodes: erase \? kill \U intr \C quit \eof \D \
    tsusp Z start \Q stop \S eol \@
```

## `Delete` 和 `Backspace`

在 `/usr/lib/X11/app-defaults/XTerm` 或 `$HOME/.Resources` 中，假设你有一这一行：

```
xrdb $HOME/.Resources
```

在你的 `$HOME/.xinitrc` 或 `$HOME/.session` 中。

## 6.8 如何告诉 `xmosaic` `Backspace` 键生成一个 `DEL`

将以下内容：

```
*XmText.translations: #override\n\n<Key>osfDelete: delete-previous-character()\n*XmTextField.translations: #override\n\n<Key>osfDelete: delete-previous-character()
```

放入你的 `$HOME/.Resources` 中是有帮助的。

然而，`Netscape FAQ` 提到：

为什么我的 `Backspace` 在文本框中不起作用？
默认情况下，`Linux` 和 `XFree86` 提供的 `Backspace` 和 `Delete` 键配置错误。所有的 `Motif` 程序（包括 `Netscape Navigator`）都会以相同的方式故障。

`Motif` 规范规定 `Backspace` 应该删除上一个字符，而 `Delete` 应该删除后面的字符。`Linux` 和 `XFree86` 的配置是 `Backspace` 和 `Delete` 键均生成 `Delete`。

你可以通过使用 `xmodmap`、`xkeycaps` 或 `loadkeys` 程序中的任何一个，让相关按键生成 `BackSpace` 键码 而不是 `Delete`。

你也可以通过创建一个 `.motifbind` 文件来修复它；参见 `VirtualBindings(3)` 的手册页。

注意：不要使用 `*XmText.translations*` 或 `*XmTextField.translations*` 资源来尝试修补此问题。如果你这样做，将覆盖掉 `Netscape Navigator` 其他的文本框按键绑定。

## 6.9 针对 `Motif` 程序（如 `netscape`）的更好解决方案

`Ted Kandall` (`ted@tcg.net`) 建议如下操作：
在你的配置文件的任何地方添加以下内容：

```
stty erase "H"
```

如果你正在使用 `bash`，请在你的 `.inputrc` 中添加以下行：

```
"\C-?": delete-char
"\C-h": backward-delete-char
```

## 410

# 目录

在你的 `.xinitrc` 文件中添加以下行：

```bash
xmodmap <<EOF
keycode 22 = BackSpace osfBackSpace
keycode 107 = Delete
EOF

#在这里启动你的窗口管理器，例如：
#(fvwm) 2~k1 | tee /dev/tty /dev/console
```

```bash
stty sane
stty erase -H
loadmap <<EOF
keycode 14 = BackSpace
keycode 111 = Delete
EOF
```

这对于带有任何 `Linux`/`FreeBSD` 布局的 `PC 101` 或 `102` 键键盘一定有效。让 `Netscape` 等 `Motif` 程序正常运行的关键在于添加 `BackSpace` 的同时向 `keycode 22` 中添加 `osfBackSpace`。注意 `=` 符号两侧都有空格。

## 6.10 什么是 `Backspace` 键生成一个 `DEL`

# 412

# 目录

当动态分配控制台时，通常运行一个或两个是最简单的。通过 `open -l bash` 可以打开更多控制台。未使用的控制台（无关联进程）使用 `dealloc`（以前为 `disalloc`）释放。但你可能会说，当我正在进行某些活动时突然需要更多控制台，而没有可用的提示符来输入 `open` 命令。幸运的是，只需按一下键即可创建一个新的控制台，无论当前控制台正在发生什么。

如果你有 `kbd-0.95.tar.gz` 中的 `spawn_login` 并将其：

```
loadkeys << EDF
alt keycode 103 = Spawn_Console
EDF

spawn_login &
```

放入 `/etc/rc.local` 中，那么输入 `Alt-UpArrow` 将创建一个运行登录界面的 `VC`（并切换到那里）。使用 `spawn_console &` 代替 `spawn_login &` 你将运行 `bash`。另请参见 `open-1.4.tgz` 和 `dynamic-vc-1.1.tar.gz`。

按下此 `SpawnConsole` 键后应该采取什么操作也可以放在 `/etc/initab.quest` 中，如果你使用的是较新版本的 `init`。请参见 `initab(5)`。

（此操作可以是完全不同的——我只是叫它 `Spawn_Console`，这是我用它的。当用于其他用途时，使用它的同义词 `KeyboardSignal` 会不那么混淆。例如，有些人喜欢将以下行：

```
kb::kquest:sbin/shutdown -h now
```

放在 `/etc/initab` 中，并将

```
control alt keycode 79 = KeyboardSignal
control alt keycode 107 = KeyboardSignal
```
