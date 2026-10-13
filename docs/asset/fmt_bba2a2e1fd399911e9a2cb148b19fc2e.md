
- `imlib`
- `gntop`
- `fnlib`
- `extace`
- `gnome-audio`
- `gnome-media`
- `gnome-libs`
- `gnome-pim`
- `lib-gtop`
- `libhttp`
- `gnome-games`
- `enlightenment`
- `gnome-users-guide`
- `xloadimage`
- `gnumeric`
- `xscreensaver`

你可以通过打开 X 并使用 Netscape 或通过命令行界面下载 GNOME，这样安装包会更简单，因为依赖错误可能会令人困惑。如果你是第一次安装 GNOME，你可能会发现一个一个安装包更简单。（注：此处原文后续存在大量重复文本，已根据逻辑流处理）

## 解决依赖错误

从二进制包安装时最常见的错误是依赖错误。当你尝试安装的包需要某些文件工作时，就会发生依赖错误。例如，在所示的依赖消息中，我们尝试安装 `guile`。我们收到一个错误消息，说我们必须安装 `um-scheme`。

```
[root@localhost i386#] rpm -Uvh guile*
error: failed dependencies:
umb-scheme is needed by guile-1.3.7
[root@localhost i386#]
```

清除错误，下载 `um-scheme` 包并使用命令 `rpm -Uvh` 安装。再次安装 `guile`，安装就成功了。

### 图 2.4 显示了 wget 的用法

![](img/56ffc05f2012b0375f0809ea492838b_46_0.png)

```bash
[root@localhost i386]#
[root@localhost i386]# rpm -Uvh xscreensaver*
error: failed dependencies:
xloadimage is needed by xscreensaver-3.17.14
[root@localhost i386]#
```

## 解决版本依赖错误

另一种常见的依赖错误发生在我们在计算机上安装包时：你正尝试安装的包需要一个更高版本的该包。正如列表 2.4 所示，我们已经安装了 `imlib-1.9.7-1`。当我们尝试安装 `enlightenment-0.16.3-1` 时，我们得到了依赖错误，因为 `enlightenment-0.16.3-1` 需要 `imlib-1.9.8` ——这比我们已经拥有的版本更高。

列表 2.4 需要更高版本包的依赖错误

```bash
[root@localhost i386]# ls
ImageMagick-4.2.9-1.1386.rpm gtk+-1.2.6-1.1386.rpm
core guile-1.3.7-1.1386.rpm
enlightenment-0.2.14-1.1386.rpm imlib-1.9.7-1.1386.rpm
esound-0.2.14-1.1386.rpm libhttp2-1.0.4-1.1386.rpm
flib-0.5.1-1.1386.rpm libgr2-2.0.13-20.1386.rpm
glib-1.2.5-1.1386.rpm libgtop-1.0.5-1.1386.rpm
gnome-audio-1.0.0-7.noarch.rpm umb-scheme-3.2-9.1386.rpm
gnome-core-1.0.53-2.1386.rpm wvdial-1.20-1.1386.rpm
gnome-libs-0.53-1.1386.rpm : 0.0
[root@localhost i386]# rpm -Uvh enlightenment*
error: failed dependencies:
imlib > 1.9.8 is needed by enlightenment-0.16.3-1
[root@localhost i386]#
```

要解决此错误，只需下载必须升级的包的更高版本，并使用与安装包时相同的命令进行升级即可：

`rpm -Uvh [package_name].rpm`

## 总结

在这一小时中，你学习了如何从光盘分发版通过下载和安装单个包来安装 GNOME。你还学习了如何解决一些安装错误。

## 问答

**Q：我想安装 GNOME，但我的电脑上是 Windows 而不是 Linux。我可以在 Windows 中运行 GNOME 吗？**

**A：** 在编写本文时，你必须拥有 Linux/UNIX 操作系统（包括 FreeBSD）才能运行 GNOME。有一个将 GNOME 移植到 Windows 的项目，但该项目还处于起步阶段。红帽 Linux 是最容易安装的 Linux 之一，包含在本本书的光盘中。祝你玩得开心！

**Q：我的电脑上安装了 KDE。安装 GNOME 之后我还能使用 KDE 吗？**

**A：** 可以，事实上，KDE 和 GNOME 应用程序是可以交换的。你可以在 GNOME 中运行 KDE 应用程序，反之亦然。你可以设置系统启动一个桌面作为默认，并将另一个桌面作为备用，或者你可以使用某些允许你切换桌面的实用程序。我们将在第 3 小时“启动 GNOME”中学习更多关于在 GNOME 和 KDE 之间切换的内容。

## 工作坊

提供的测试和练习旨在帮助测试你的知识并提高你的理解。答案可以在附录 B“答案”。

## 测试

1. 哪种 GNOME 安装方法是由 GNOME 项目监控并官方认可的？
2. “依赖错误”是什么意思？
3. 如果在安装 GNOME 时遇到依赖错误，你应该怎么办？

## 练习

1. 在提示符处输入 `rpm` 命令并研究输出。`rpm -Uvh [package_name].rpm` 中的 `-Uvh` 是什么意思？
2. 按照本章的说明安装 GNOME，并使用你喜欢的文本编辑器创建一个名为 `.Xclients` 的文件。（如果 `.Xclients` 已存在，请将其另存为，，然后在完成此练习后恢复其原始状态。）在文件中输入一行：

   `exec gnome-session`

退出 X 并重启 X。GNOME 出现了吗？如果没有，不要担心。我们将在下一小时介绍启动问题。如果它启动了，恭喜你！

# 第 3 小时

# 启动和退出 GNOME

通常，处理新软件时最令人感到沮丧和痛苦的部分是在安装完软件后让它运行起来。幸运的是，GNOME 不需要许多特殊的配置步骤。在安装完所需的组件后，在实际启动 GNOME 会话之前，只有几件事需要完成。

在这一小时中，你将：

- 在你的计算机上启动 GNOME 会话。
- 将 GNOME 设置为一个用户账户的默认桌面。
- 将 GNOME 设置为系统中所有账户的默认桌面。
- 使用 Switchdesk 在 GNOME 和其他桌面（如 KDE）之间切换。

## 准备启动 GNOME

GNOME 是作为启动脚本的一部分启动的。在安装完所需的组件后，在实际启动 GNOME 会话之前，只有几件事需要完成。

在这一小时中，你将：

- 在你的计算机上启动 GNOME 会话。
- 将 GNOME 设置为一个用户账户的默认桌面。
- 将 GNOME 设置为系统中所有账户的默认桌面。
- 使用 Switchdesk 在 GNOME 和其他桌面（如 KDE）之间切换。

GNOME 是作为启动脚本的一部分启动的。在安装完所需的组件后，在实际启动 GNOME 会话之前，只有几件事需要完成。

在这一小时中，你将：

- 在你的计算机上启动 GNOME 会话。
- 将 GNOME 设置为一个用户账户的默认桌面。
- 将 GNOME 设置为系统中所有账户的默认桌面。
- 使用 Switchdesk 在 GNOME 和其他桌面（如 KDE）之间切换。

GNOME 是作为启动脚本的一部分启动的。在安装完所需的组件后，在实际启动 GNOME 会话之前，只有几件事需要完成。

命令是：

```bash
exec gnome-session
```

在安装完所需的组件后，在实际启动 GNOME 会话之前，有几件事需要考虑：

1. X 如何启动。
2. 你是否希望将一个桌面作为默认，另一个作为备用。
3. 或者是使用某些允许你切换桌面的实用程序。

如果你使用 `startx` 或 `x11` 启动 X，那么系统可能使用 `xinit`。

如果你使用 `startx` 或 `x11` 启动 X，那么系统可能使用 `xinit`。

如果你使用 `startx` 或 `x11` 启动 X，你可以使用 `xdm`（显示管理器）或 `kdm`（显示管理器）来启动它。

你可以设置系统启动一个桌面作为默认，另一个作为备用，或者你可以使用某些允许你切换桌面的实用程序。

如果你使用 `startx` 或 `x11` 启动 X，那么系统可能使用 `xinit`。

查看以下帮助页：

- `man X`
- `man xdm`
- `man xinit`
- `man xterm`

## 启动并退出 GNOME

查看以下帮助页了解：

- `man X`
- `man xdm`
- `man xinit`
- `man xterm`
