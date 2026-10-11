

![](img/f28adb66a7398a382f0505e0ba74a872_169_0.png)

图 4-28 输入 /sleep RETURN 两次后，info coreutils 显示的屏幕

输入 `info coreutils` 命令后，按几次 SPACE 键以滚动查看显示内容。输入 `/sleep` RETURN 以搜索字符串 `sleep`。当你输入 `/` 时，光标移动到窗口的最后一行，并显示 `Search for string [string]`，其中 `string` 是你上次搜索的字符串。按 RETURN 搜索该字符串，或者输入你想搜索的字符串。输入 `sleep` 会在那一行显示 `sleep`，然后按 RETURN 会显示 `sleep` 的下一次出现位置。

现在输入 `/` RETURN（或 `/sleep` RETURN）以搜索 `sleep` 的下一次出现，如图 4-28 所示。行左端的天星号表示此条目是一个菜单项。紧跟在天星号之后是菜单项的名称和该条目的描述。

每个菜单项都是指向描述该条目的 info 页面的链接。要跳转到该页面，请搜索或使用 ARROW 键将光标移动到包含菜单项的行，然后按 RETURN。当时光标位置如图 4-28 所示时，按 RETURN 将显示关于 `sleep` 的信息。或者，你可以在菜单命令中输入菜单项的名称来查看信息：例如，要显示关于 `sleep` 的信息，你可以输入命令 `m sleep`，然后按 RETURN（当你输入 `m`（代表 menu）时，光标像输入 `/` 时一样移动到窗口的最后一行）并显示 `Menu item:`。输入 `sleep` 会在那一行显示 `sleep`，然后按 RETURN 将显示你选择的菜单项的相关信息。

图 4-29（下一页）显示了关于 `sleep` 信息的顶级节点。节点将一组你可以使用 SPACE 键滚动浏览的信息组合在一起。要显示下一个节点，按 `n`；要显示上一个节点，按 `p`。

当你阅读本书并了解新的实用工具时，可以使用 `man` 或 `info` 来了解这些实用工具的更多信息。你可以打印 PostScript 文档，可以使用带有 `-t` 选项（例如，`man -t cat | lp` 打印关于 `cat` 实用工具的信息）的 `man` 实用工具打印手册页。你还可以使用 Web 浏览器显示 www.tldp.org、docs.fedoraproject.org 或 www.redhat.com/docs 上的文档，然后从浏览器中打印所需的信息。

![](img/f28adb66a7398a382f0505e0ba74a872_170_0.png)

图 4-29 关于 `sleep` 实用工具的 info 页面

## `--help` 选项

在文本环境中你可以使用的另一个工具是 `--help` 选项。大多数 GNU 实用工具都提供了一个 `--help` 选项，用于显示关于该实用工具的信息。非 GNU 实用工具可能使用 `-h` 或 `--help` 选项来显示帮助信息。

```
$ cat --help
Usage: cat [OPTION] [FILE]...  Concatenate FILE(s), or standard input, to standard output.
-A, --show-all    equivalent to -vET
-b, --number-nonblank     number nonblank output lines
-e     equivalent to -vE
-E, --show-ends  display $ at end of each line
...
```

如果 `--help` 显示的信息超出了屏幕范围，请使用管道（第 158 页）将输出通过 *less* 分页器（第 125 页）发送：

```
$ ls --help | less
```

## HOWTOs：了解事物如何运作

HOWTO 文档详细解释了与 Linux 相关的某项操作的方法——从设置专用硬件到执行系统管理任务，再到设置特定的网络软件。Mini-HOWTO 提供更简短的说明。与 Linux 软件一样，通常由一个人或少数人负责编写和维护 HOWTO 文档，但许多人可能会为其做出贡献。

Linux 文档项目（LDP，第 132 页）网站托管了大多数 HOWTO 和 mini-HOWTO 文档。使用 Web 浏览器访问 www.tldp.org，点击 HOWTOs，并选择你想用来查找 HOWTO 或 mini-HOWTO 的索引。你还可以使用其主页上的 LDP 搜索功能来查找 HOWTO 和其他文档。

![](img/f28adb66a7398a382f0505e0ba74a872_171_0.png)

图 4-30 Google 报告的一条错误消息

## 获取系统帮助

GNOME 提供了工具提示（第 110 页）、上下文敏感的帮助系统，以及第 125 页讨论的帮助浏览器。

### 在本地查找帮助

`/usr/src/linux/Documentation`（仅在安装内核源代码时存在，如第 15 章所述）和 `/usr/share/doc` 目录通常包含关于实用工具比 `man` 或 `info` 提供的更详细且不同的信息。这些信息通常是针对将编译和修改该实用工具的人，而不仅仅是使用者。这些目录包含数千个文件，每个文件都包含关于单独主题的信息。

### 使用互联网获取帮助

互联网提供了许多与 Linux 相关的有用网站。除了提供各种形式文档的网站外，你还可以在搜索引擎（如 Google（www.google.com）或其 Linux 专用版本 www.google.com/linux）中输入你遇到问题的程序的错误消息。将错误消息用双引号括起来以提高结果的质量。搜索很可能会产生一条关于你问题的帖子以及关于如何解决它的建议。参见图 4-30。

- Fedora 文档可在 docs.fedoraproject.org 上获取。

![](img/f28adb66a7398a382f0505e0ba74a872_172_0.png)

- 从 Red Hat Linux 到 Linux 9 和 RHEL 的手册可在 www.redhat.com/docs 上获取。
- 各种类型的支持文档和支持可在 www.redhat.com/apps/support 上获取（需要免费注册）。
- 你可以在 kbase.redhat.com 上查询 Red Hat 知识库。
- Fedora（fedoraproject.org）和 RHEL（www.redhat.com）的主页拥有大量的信息。
- Fedora/RHEL 支持论坛是关于人们想要提出的任何 Red Hat 相关问题的在线讨论。一个论坛专门面向新用户；其他论坛面向 Apache、X 窗口系统等。请访问 www.redhat.com/mailman/listinfo 浏览列表列表。另一个具有类似有用信息的网站是 fedorafa.org。
- Fedora/RHEL 错误数据库可在 bugzilla.redhat.com 上获取。任何人都可以搜索该数据库。要提交新错误或追加到现有错误，你需要注册一个免费帐户。
- Fedora 每周新闻可在 fedoraproject.org/wiki/FWN 上获取。
- RHEL 硬件帮助可从 Red Hat 硬件目录 hardware.redhat.com 获取。Fedora 支持的硬件大多是 RHEL 所支持硬件的超集。

**GNU** GNU 手册可在 www.gnu.org/manual 上获取。此外，你可以访问 GNU 主页（www.gnu.org）以获取额外的文档和其他 GNU 资源。许多 GNU 页面和资源可用多种语言获取。

**Linux 文档项目** Linux 文档项目（www.tldp.org；图 4-31），其存在时间几乎与 Linux 一样长，托管了完整的指南、HOW-TOs、FAQs、man 页面和 Linux 杂志的集合。主页可用英语、葡萄牙语、西班牙语、意大利语、韩语和法语获取。它易于使用，并支持本地文本搜索。它还提供了完整的链接集，你可以用它来查找几乎任何与 Linux 相关的内容（点击搜索框中的**Links**或访问 www.tldp.org/links）。链接页面包含关于通用信息、事件、入门、用户组、邮件列表和新闻组的章节，每个章节包含许多子章节。

## 更多关于登录

有关登录信息，请参考第 91 页的“Logging In on the System”。本节涵盖你可以从登录屏幕选择的选项以及常见登录问题的解决方案。它还描述了如何从终端和远程系统登录。

![](img/f28adb66a7398a382f0505e0ba74a872_173_0.png)

图 4-31 Linux 文档项目主页

### security

#### 始终使用密码

除非你是系统唯一的用户，系统没有连接到其他系统、互联网或调制解调器，并且你是唯一拥有该系统物理访问权限的人，否则维护一个没有密码的用户帐户是一种糟糕的做法。

#### fedora

#### 登录屏幕

登录屏幕（图 4-1，第 91 页）显示了一个允许在系统上登录的用户列表。在屏幕底部的面板上有三个按钮。点击描绘人物的圆形蓝色按钮，以从访问首选项中选择一个列表，这可能会让某些人更容易使用系统。点击包含感叹号的三角形黄色按钮以显示启动消息列表。点击面板右端的灰色圆形按钮以重启或关闭系统。点击用户列表中的你的名字以登录。

一旦你点击了你的名字，登录屏幕会显示一个标记为 `Password` 的文本框。除了屏幕底部的面板外，它还添加了标记为 `Language` 和 `Keyboard` 的按钮。如果安装了多个窗口管理器或桌面，还会出现一个标记为 `Sessions` 的按钮。在文本框中输入你的密码并按 RETURN 以登录。

在登录之前，标记为 `Language` 的按钮显示即将使用的会话的语言名称。要更改即将使用的会话的语言，请点击此按钮并从下拉列表中选择一种语言。如果你

