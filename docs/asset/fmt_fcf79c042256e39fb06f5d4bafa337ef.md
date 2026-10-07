
## 812 补丁

## patch 更新源代码

语法：`patch [options] 目标文件 补丁文件`
`patch [options]`

## 摘要

`patch` 工具尝试通过由 `diff` 创建的更改信息文件（即补丁）来更新文件。`patch` 工具可以读取许多不同形式的 `diff` 输出，包括上下文差异（context diffs）、`ed` 脚本以及默认的 `diff` 输出。有关这些及其他输出格式的更多信息，请参见 `diff` 页面。

在对大型软件应用（包括 Linux 内核）进行更改时，`patch` 工具非常有用，因为它允许通过简单的应用补丁将一个版本的应用程序源码转换为另一个版本。软件开发者通常假设该工具可用，他们通过电子邮件发送补丁以便用户安装更新。

### 参数

在第一种形式下，`patch` 将补丁文件中的详细列出的更改应用到目标文件上。在进行任何更改之前，程序会通过在原始文件名后添加扩展名 `.orig` 来创建一个目标文件的副本。这允许你在有需要时恢复目标文件。

在第二种形式下，`patch` 从标准输入（通常重定向自文件或管道）中读取信息，并尝试根据更改信息识别要更新的文件名。如果 `patch` 无法确定文件名，它会提示你输入文件名。如果更改信息中有多个文件的更改，`patch` 将更新所有文件。第二种形式更为常用。

### 选项

- `-d directory` 在进一步处理之前，将目录设置为工作目录。
- `-E empty` 如果 `patch` 进行的更改导致文件为空，则删除该文件。
- `-1 loose` 在尝试定位补丁在目标文件中的位置时，执行松散匹配。具体而言，补丁中的任何空白字符序列都会匹配目标文件中的任何空白字符序列。
- `-pn prefixes` 从待补丁的路径中剥离前缀。值 `n` 是从路径名称开始删除的斜杠数量（这些斜杠之间的任何目录名也会被删除）。对 `n` 使用 `0`，或在不带 `n` 的情况下使用 `-p`，将使路径名保持不变。如果你完全省略此选项，则整个补丁名称将被移除，变为简单的文件名。此选项允许你对与构建补丁文件的人所使用的位置不同的位置的文件进行打补丁。
- `-R` 尝试反向应用补丁。参见下文的“讨论”部分。
- `-s` 仅报告错误。通常 `patch` 会显示一些其正在执行的工作信息。

## 讨论

`patch` 工具的设计旨在简化保持大型软件应用源码更新的过程。如果你是软件开发者，这将让你更容易提供更新。如果你是用户，`patch` 将让你更容易获取和安装更新。

## 816 patch

如果你收到了这封邮件，可以将消息保存到文件中并将其移动到存放旧版本 `pi` 的目录，然后运行 `patch` 来升级你的源代码。（某些邮件程序允许你直接将消息管道到 `patch`，而无需将其写入文件。）不需要从邮件文件中提取补丁。运行时 `patch` 会向你显示正在进行的所有处理。共处理了三个块（hunks）。

```
$ cd pi

$ patch <../mail.pi

Hmm... Looks like a new-style context diff to me...

The text leading up to this was:

|

| Hi - Here are the patches you need to upgrade to version 1.1

| of the pi program:

|

|diff --recursive -c Old_pi/Makefile pi/Makefile

|*** Old_pi/Makefilesun Sun Jul 3 14:13:20 1996

|-- pi/Makefilesun Aug 4 08:12:41 1996

```
```
Patching file Makefile using Plan A...

Hunk #1 succeeded at 2.

The next patch leading up to this was:

|diff --recursive -c Old_pi/patchlevel.h pi/patchlevel.h

|*** Old_pi/patchlevel.hSun Aug 4 08:16:08 1996

|-- pi/patchlevel.hSun Aug 4 10:24:29 1996

```
```
Patching file patchlevel.h using Plan A...

Hunk #1 succeeded at 1.

The next patch looks like a new-style context diff to me...

|diff --recursive -c Old_pi/pi.c pi/pi.c

|*** Old_pi/pi.cSun Jul 14 09:43:43 1996

|-- pi/pi.cSun Aug 4 08:09:45 1996

```
```
Patching file pi.c using Plan A...

Hunk #1 succeeded at 17.

Hunk #2 succeeded at 172.

Hmm... Ignoring the trailing garbage.

done

```

最后一个示例展示了你如何将 Linux 操作系统所需的补丁应用到 2.0.10 版本。由于 Linux 内核在分发前使用 `gzip` 压缩，因此 `gunzip` 在将补丁文件交给 `patch` 之前会解压。此外，内核分发假设你的内核源码存储在名为 `linux` 的目录中。`-p0` 允许你从 `linux` 的父目录运行 `patch`；通常是 `/usr/src`。`-d /usr/src` 选项允许 `patch` 在应用补丁之前切换到该目录。你应该超级用户（Superuser）来升级内核源码。（赋予内核源码文件写入权限是一个巨大的安全漏洞。）

```
$ gunzip <patch.2.0.10.gz | patch -d /usr/src -p0
```

## pine 817

`pine` | 发送和接收电子邮件和新闻
Syntax: `pine -i pine [options] [recipient-list]`

## 摘要

你可以使用 `pine` 这种基于屏幕的邮件客户端发送和接收电子消息。`pine` 早期版本的主要设计目标是易用性。为此，`pine` 被赋予了大量的内置文档、防止意外事故的保护措施，以及一个整洁且宽容的用户界面。

自早期版本以来，该邮件客户端添加了许多高级功能，使其对老练用户和新手都具有吸引力。现在 `pine` 中提供的高级功能包括：

- 用于在邮件消息中发送和接收二进制文件的 *MIME*
- 读取和发布网络新闻的能力
- 维护邮件收件人地址簿
- 编写期间的拼写检查
- 在 X Window 系统上使用 `xterm` 的鼠标支持
- 一个高度可配置的环境，可以轻松自定义以适应广泛用户的需求

`pine` 邮件的基本存储单元是消息文件夹（Message Folder）。默认有三个文件夹：`pine` 最初将收到的消息存储在 `INBOX`，将发送的消息副本存储在 `sent-mail`，将显式保存的消息存储在 `saved-messages`。你可以更改这些文件夹的默认值，并根据需要创建任意数量的新文件夹。另见第 57 页的“使用 pine 发送和接收电子邮件”和第 782 页的“邮件”。

### 参数

使用 `-i` 选项（第一种形式），`pine` 会显示文件夹索引（Folder Index）屏幕，跳过主菜单（Main Menu）。在这里你可以查看邮件头并选择你想阅读的收件消息。当你读完消息后，`pine` 会返回 `shell`，再次跳过主菜单。

在 `pine` 命令的第二形式中，`recipient-list` 是你必须编写的邮件的收件人列表。当命令行上存在 `recipient-list` 时，`pine` 会向你展示编写消息（Compose Message）屏幕，跳过主菜单。当你完成编写并发送消息后，将直接返回 `shell`。

`recipient-list` 可能包含电子邮件地址、用户名（针对你系统上的用户）或你在设置地址簿时建立的昵称。你也可以使用昵称来代表一组地址。

## 818 pine

如果你提供 `pine` 命令的第二形式但不提供 `recipient-list`，`pine` 将显示主菜单。在这里，你可以选择任何一个 `pine` 函数，并根据需要多次返回 `pine` 主菜单。在选择选择退出（Quit）命令之前，你不会返回 `shell`。

### 选项

- `-conf` 将有关当前配置的信息发送到标准输出。
- `-feature-list=[no-]{feature-list-option}` 设置功能列表选项。例如，在命令行中包含 `-feature-list-enable-flag-cmd` 会在文件夹索引中提供一个菜单项，允许你更改状态标志。在功能列表选项前加上字符串 `no-` 则表示禁用该选项。请参阅第 821 页的“配置 pine”以讨论功能列表选项。
- `-f folder` 打开由 `folder` 指定的文件夹。若无此选项，`pine` 将打开 `INBOX` 文件夹。
- `-i` 允许你直接进入文件夹索引来阅读邮件。
- `-variable=variable-value` 将 `variable-value` 赋值给命名的变量 `variable`。此值将覆盖 `/usr/local/lib/pine.conf` 文件或家目录下的 `.pine` 文件中的值。例如，给出选项 `-signature-file=/unsig pine` 可以在发送的每条消息中插入 `~/.unsig` 文件的内容。
- `-sort-type[reverse]` 对消息排序。默认情况下，文件夹索引中显示的邮件头按到达时间排序。通过在命令行上提供 `-sort-option` 来对其他字段进行排序。`sort-type` 参数标识排序字段。除了到达，你还可以指定主题（subject）、发件人（from）、日期（date）和大小（size）。要反转排序，在 `sort-type` 后面附加 `/reverse`。
- `-h help` 显示你可以配合 `pine` 命令使用的选项列表，以及每个选项的简要摘要。

## 讨论

所有 `pine` 屏幕的顶部都有一个状态行，包含当前屏幕名称和其他状态信息。每个 `pine` 屏幕的底部是该屏幕定义的双行命令菜单。如果命令太多无法在两行内显示，`pine` 会显示一个允许你循环部分菜单的命令。

每个 `pine` 屏幕允许你利用 `pine` 的某些功能。当你需要决策时，可以使用帮助功能（Help）。

以下项目出现在主菜单中（见第 58 页的图 3-16）：

- *Help*（帮助）
- *Compose Message*（编写消息）
- *Address Book*（地址簿）
- *Folder Index*（文件夹索引）
- *Folder List*（文件夹列表）
- *Setup*（设置）
- *Quit*（退出）

当你选择上述列表一项，`pine` 会向你展示该项目的屏幕。当你选择 `Setup` 时，`pine` 会提示你执行设置任务；你拥有的选择是 `Config`，它会修改 `pine` 的行为（参阅 821 页的“配置 pine”）。选择 `Quit` 将返回 `shell`。

在主菜单中选择 `Help` 会显示 `Help For` 菜单，它提供了 `pine` 的概述。对于新用户来说，这是一个很好的开始。

## 发送消息

拥有地址簿会让发送消息变得简单得多。要初始化地址簿，或在地址簿中添加、删除或编辑项目，请从主菜单选择 `Address Book`。对于你添加到地址簿的每个用户，`pine` 会提示输入姓名、昵称和地址。在地址簿屏幕上，你还可以选择 `Create List` 来定义分发列表——一组你可以用昵称引用的用户。（昵称只是一个别名，可以让你轻松记忆和引用收件人或一组收件人。）

在 `pine` 命令上指定 `recipient-list` 会让你直接进入编写屏幕（见第 59 页的图 3-17）。如果你在命令行上包含了 `recipient-list`，`To:` 字段已填充；否则你需要在字段中输入电子邮件地址，或你在地址簿中显示的全名或昵称。其他字段还有 `Cc;`（用于消息的“抄送”收件人）、`Attmnt;`（用于为消息附加二进制文件）以及 `Subject;`（用于输入消息主题）。在完成头部的字段后，可以使用内置的 `pine` 编辑器编写消息。（可以使用帮助功能学习编辑器命令。）

你也可以通过从 `pine` 主菜单选择 `Compose` 进入消息编写器。访问 `pine` 主菜单允许你在会话期间使用其他 `pine` 功能。

## 820 pine

如果你正在编写消息并想在稍后完成，可以选择“推迟”（Postpone）命令。`pine` 实用会将消息存储在名为 `postponed-msgs` 的文件夹中，并在下次运行 `pine` 时，它将为你提供继续处理该消息的机会。

## 阅读消息

如果你只想读取邮件，最简单的方法是在命令行上使用 `-i` 选项。该选项将直接带你“文件夹索引”（Folder Index）屏幕（见第 61 页图 3-18），那里会显示消息头列表。高亮的消息是当前消息；你可以使用屏幕上显示的控件高亮任何其他消息。

在 `pine` 中读取消息的另一种方法是从 `pine` 主菜单（Main Menu）中选择“文件夹索引”。如果你计划在阅读收到的邮件后对其进行维护，这种方法非常合适。

默认情况下，每个消息头都包含以下字段：

```
flags       message-#      date-sent      from-name      size       [subject]
```
