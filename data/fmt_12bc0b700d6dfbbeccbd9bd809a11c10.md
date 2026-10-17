
- 调整窗口大小。将鼠标指针移动到窗口的一个角或边缘，等待指针变为变为双向箭头，然后用鼠标拖动窗口的角或边缘。
- 遮盖/取消遮盖窗口。双击其标题栏。
- 最大化窗口。点击标题栏上的最大化按钮。
- 关闭窗口。点击标题栏上的关闭按钮。在 StarOffice 中，你当然可以选择“文件：退出”（File: Exit）或按照第 2 章所述关闭窗口。

# 切换环境

X 的独特功能之一是在无需重启系统的情况下在窗口管理器之间切换。然而，这些方法都不是 100% 可靠的。有时，从一个窗口管理器切换到另一个会导致运行不同的（备用）窗口管理器，或者在找不到所需的窗口管理器时 X 退出。如果 X 冻结或发生异常，按下 Ctrl+Alt+Backspace。这将把你带回文本模式。在执行之前，请务必尝试保存数据并关闭任何正在运行的应用程序。

# 将 StarOffice 集成到你的环境中

虽然你可以在 `xterm` 窗口的命令行中输入名称来运行 StarOffice，但这样做既快速也不方便。不过，你可以使用任何桌面环境或窗口管理器来打开 StarOffice。本节提供了将最流行的管理器和环境与 StarOffice 集成的指令。

要修改后续章节中提到的系统文件，你必须使用一个可以读取和保存纯文件的文本编辑器。使用 StarWriter 是可以的，但记得将文件保存为纯 ASCII 或文本文件（选择“文件” ▷ “另存为”，并在“另存为”对话框的列表中选择适当的文件格式）。记住使用与原文件相同的名称且不带后缀，否则系统将无法识别修改后的文件。直接使用 `vi` 或 `emacs` 这样的文本编辑器通常更简单。

> 在修改任何系统文件之前，对它们进行备份至关重要，这样你可以在不重新安装系统的情况下回到初始状态。

如果你在查找后续章节中提到的文件时遇到困难，请使用 `find -name "文件名"` 来定位它们：

```
find / -name "name of the file"
```

查找文件可能需要一些时间，但比手动查找要好。

# AfterStep

AfterStep 存储配置信息的方法最为复杂，但一旦你了解了它，它并没有听起来那么糟糕。不过，在开始自定义 AfterStep 之前，你必须确保它已安装在系统上（使用 `find -name "afterstep"`），并且 X 已配置为运行 AfterStep。

> 此处描述的所有更改均适用于 AfterStep 1.7 或更高版本。

## 为 AfterStep 配置 X

确保 AfterStep 启动时至少有一个 `xterm` 窗口。这使得你能够使用任何命令，而无需担心某些应用程序未列在 AfterStep 菜单或其子菜单中。为了方便你设置此选项，我们准备了一个简短的 `xinitrc.afterstep` 文件，你可以按照以下方式使用：

- 将你的个人 `xintrc` 重命名为 `xintrc.original`（这将允许你恢复原始配置）。如果你在家目录中没有 `.xintrc` 副本，可以从 `/etc/X11/xinit/` 目录复制默认版本。如果那里没有，请使用 `find -name "xinitrc"` 查找它。

## 附录 B ★ StarOffice 和你的 X 桌面

2. 将 `xinitrc.afterstep` 文件复制到你的家目录。
3. 将 `xinitrc.afterstep` 重命名为 `xinitrc`。
4. 退出你当前使用的窗口管理器或桌面环境，输入 `startx` 并按回车。如果你的系统中安装了 AfterStep，你应该能看到一个带有单个 `xterm` 窗口和 Wharf 应用程序的空白屏幕。

### 在 CD 盘上

你可以在随书附赠的 CD 盘上找到 `xinitrc.afterstep` 文件。即使 CD 盘已经在驱动器中，Linux 也可能无法看到它，请输入 `mount -t iso0996 /dev/cdrom /mnt/cdrom` 来挂载它。使用命令 `umount /mnt/cdrom` 可以将其卸载。

# 在 AfterStep 中解决键盘冲突

冲突的键盘快捷键是一个非常痛苦的问题，默认的 AfterStep 配置确实非常考验你的耐心。然而，你可以通过相当简单的方法重新获得键盘的控制权。

安装 AfterStep 后，在你的家目录中找到新条目 `GnuStep`，在 `~/.GNU/Library/AfterStep/` 目录下隐藏着许多名为 `0_feel.16bpp`、`0_feel.24bpp` 和 `0_feel.32bpp` 的文件。要决定你需要修改哪一个，需要知道 X 为系统使用哪种颜色模式。如果是 16 位的，你需要编辑 `0_feel.16bpp` 等文件。在编辑这些文件之前，请务必备份它们！

好了吗？现在来看细节。与流行的 Red Hat Linux 分发的默认 AfterStep 配置与 StarOffice 在以下方面存在冲突：

- `Shift+方向键选择`。AfterStep 捕获了这些快捷键和鼠标指针索引。要更改这些，请在相应的“文件”中查找此项：

```
# shift + arrow = move cursor
Key Left            A               CursorMove -1 0
Key Right           A               CursorMove +1 0
Key Up              A               CursorMove +0 -1
Key Down            A               CursorMove +0 +1
```

由于你并不真的需要这些快捷键，可以通过这种方式将它们注释掉：

```
# shift + arrow = move cursor
#Key Left            A               CursorMove -1 0
#Key Right           A               CursorMove +1 0
#Key Up             A               CursorMove +0 -1
#Key Down            A               CursorMove +0 +1
```

## 594 附录

- `Ctrl+方向键移动`。AfterStep 捕获了这些快捷键并切换桌面。为了防止这种情况发生，请在“field”文件中查找此项：

```
# control + arrow = 1 page
Key Left      A C Scroll -100 0
Key Right     A C Scroll +100 +0
Key Up        A C Scroll +0 -100
Key Down      A C Scroll +0 +100
```

你不应该关闭这些，相反，通过这种方式将 Ctrl+方向键快捷键更改为 Alt+Ctrl+方向键（M 表示 Meta 或 Mod，在 Linux 中等同于 Alt）。

- `Shift+方向键选择`。AfterStep 捕获了这些快捷键并切换桌面。为了防止这种情况发生，请在“field”文件中查找此项：

```
# shift + arrow = move cursor
Key Left            A               CursorMove -1 0
Key Right           A               CursorMove +1 0
Key Up              A               CursorMove +0 -1
Key Down            A               CursorMove +0 +1
```

由于你并不真的需要这些快捷键，可以通过这种方式将它们注释掉：

```
# shift + arrow = move cursor
#Key Left            A               CursorMove -1 0
#Key Right           A               CursorMove +1 0
#Key Up             A               CursorMove +0 -1
#Key Down            A               CursorMove +0 +1
```

- `Ctrl+方向键移动`。AfterStep 捕获了这些快捷键并切换桌面。为了防止这种情况发生，请在“field”文件中查找此项：

```
# control + arrow = 1 page
Key Left      A C Scroll -100 0
Key Right     A C Scroll +100 +0
Key Up        A C Scroll +0 -100
Key Down      A C Scroll +0+100
```

你不应该关闭这些，相反，通过这种方式将 Ctrl+方向键快捷键更改为 Alt+Ctrl+方向键（M 表示 Meta 或 Mod，在 Linux 中等同于 Alt）。
