
`CFLAGS = -O3 -m486 -fomit-frame-pointer -ffast-math -fwritable-strings`

`all: pi`

`pi.c`

`$(CC) $(CFLAGS) -o pi $ -lm`

```
# patch 815
```

+ clean

+rm -f *.o

`diff --recursive -c Old_pi/patchlevel.h pi/patchlevel.h`

*** Old_pi/patchlevel.h Sun Aug 4 08:16:08 1996

---

pi/patchlevel.h Aug 4 10:24:29 1996

*******************************

+*** 0 ***

+--- 1,4 ---

+ #define VERSION

+ #define PATCHLEVEL

+

`diff --recursive -c Old_pi/pi.c pi/pi.c`

*** Old_pi/pi.c Sun Jul 14 09:43 1996

---

pi/pi.c Aug 4 08:09:45 1996

*******************************

*** 17,22 ***

--- 17,23 ---

{

 int i;

 char *s = "";

+ sprintf(s,"%s.");

+ printf(s,(int)a[0]);

+ sprintf(s,"%s ",

+ for (i = 1; i < n; i++) {

+ printf(s,(int)a[i]);

}

```

然后将此补丁文件通过邮件发送给所有用户。

`$ mail pi-users`
To: pi_users
Subject: New version of pi available

Hi Here are the patches you need to upgrade to version 1.1
of the pi program:

```

~ patch.1.1

patch.1.1: 61 lines

(continue editing letter)

CONTROL-D

```

# patch 816

如果您收到此邮件，可以将消息保存到存放旧版本 pi 的目录并运行 `patch` 来升级您的源代码。（某些邮件程序允许将消息管道到 `patch`，而无需保存为文件。）不需要从邮件文件中提取补丁。运行期间，`patch` 会显示正在发生的过程。三个差异块已完全处理。

```
$ cd pi

$ patch ../mail.pi
```
Hmm... 对我来说这是一个新式的上下文 diff...

之前的文本是：

---

|Hi Here are the patches you need to upgrade to version 1.1

| of the pi program:

---

|diff --recursive c Old_pi/Makefile

|*** Old_pi/Makefile Sun Jul 3 14:13:20 1996

|--- pi/Makefile Aug 4 08:12:41 1996

```

使用 Plan A 修复 Makefile...
Hunk #1 成功于 2。
Hmm... 下一个补丁对我来说看起来是一个新式的上下文 diff...
之前的文本是：
---
|diff --recursive c Old_pi/patchlevel.h pi/patchlevel.h
|*** Old_pi/patchlevel.h Sun Aug 4 08:16:08 1996
|--- pi/patchlevel.h Aug 4 10:24:29 1996

使用 Plan A 修复 file.c...
Hunk #1 成功于 17。
Hunk #2 成功于 172。
Hmm... 忽略末尾的垃圾。

最后一个示例显示了如何应用将 Linux 操作系统 2.0.9 版本升级到 2.0.10 所需补丁。由于内核补丁在分发前使用 `gzip` 压缩，`gzip` 在传递给 `patch` 之前会解压补丁文件。此外，内核补丁的分发假设您的内核源码存储在名为 `linux` 的目录中。`-p0` 选项允许您从 linux 的父目录运行 `patch`；通常是 `/usr/src`。`-d /usr/src` 选项导致 `patch` 在应用补丁之前切换到目录。您应该是超级用户以升级内核源码。（允许其他用户写入内核源码权限是一个巨大的安全漏洞。）

```
$ gunzip <patch.2.0.10.gz | patch -d /usr/src -p0
```

# pine 发送接收邮件和新闻

语法：`pine -i`
`pine [options] [recipient-list]`

## 总结

可以使用 `pine` 发送和接收邮件。早期版本的主要设计目标是自由使用。为了这一目标，`pine` 被赋予了丰富的内置文档、防止误操作的安全措施以及简洁易用的用户界面。

自早期发布以来，`pine` 添加了许多高级功能，使其对高级用户和新手都具有吸引力。现在提供的高级功能包括

字体 支持发送接收二进制文件的 MIME
- 读取和发布网络新闻
- 维护邮件接收者地址簿
- 消息期间的拼写检查
- 在 X Window 系统使用时的鼠标支持
- 高配置的环境，可根据需要定制

`pine` 存储的基本单位是邮件文件夹（Message Folder）。默认有三个邮件文件夹：`pine` 最初将收到的消息存储在 INBOX，将发送的消息副本存储在 sent-mail 中，将显式保存的消息存储在 saved-messages 中。您可以更改这些默认值，也可以创建任意数量的新文件夹。另见第 57 页的“使用 pine 发送和接收邮件”以及第 782 页的 mail。

## 参数

使用 `-o` 选项（第一种形式），`pine` 显示文件夹索引屏幕，跳过主菜单。在这里您可以查看邮件头并选择想要读取的消息。阅读完消息后，`pine` 返回 shell，跳过主菜单。

在 `pine` 命令的第二种形式中，`recipient-list` 是您要编写的消息的接收者列表。接收者列表出现在命令行中，`pine` 向您呈现编写消息界面。完成编写并发送消息后，您将直接返回 shell。

# 818 pine

如果你在不提供收件列表的情况下提供 `pine` 命令的第二形式，`pine` 将显示主菜单（Main Menu）。在这里，你可以选择 `pine` 的任何一个功能，并根据需要多次返回 `pine` 主菜单。在选择选择 Quit（退出）命令之前，你将不会返回到 shell。

## 选项

- `-conf` 将当前配置的信息发送到标准输出。
- `-feature-list=[no-|]|feature-list-option` 设置功能列表选项。例如，在命令行中包含 `-feature-list=enable-flag-cmd` 可以在文件夹索引（Folder Index）屏幕中为你提供一个菜单项，允许你更改消息状态标志。在 `feature-list-option` 前加字符串 `no-` 可以重置该选项。关于功能列表选项（feature-list options）的讨论，请参阅第 821 页的“配置 pine”。
- `-f folder` 打开由 `folder` 指定的文件夹。如果没有此选项，`pine` 将打开收件箱（Inbox）文件夹。
- `-i` 允许你直接进入文件夹索引屏幕以阅读邮件。
- `-variable=variable-value` 将 `variable-value` 分配给指定的变量。此值将覆盖你主目录下 `/usr/local/lib/pine.conf` 文件中给出的。例如，提供选项 `-sig-nature-file=/.fusig` 会导致 `pine` 在发送的每条消息中插入 `~/.fusig`文件的内容。
- `-sort sort-type[/reverse]` 对消息头进行排序。默认情况下，文件夹索引屏幕显示的消息头按到达时间排序。你可以使用命令行上的 `-sort` 选项让 `pine` 按其他字段排序。参数 `sort-type` 标识排序字段。除了到达时间外，你还可以指定主题（subject）、发件人（from）、日期（date）和大小（size）。要反转排序顺序，在 `sort-type` 后追加 `/reverse`。
- `-h help` 显示你可以配合 `pine` 命令使用的选项列表，以及每个选项的简要说明。

## 讨论

所有 `pine` 屏幕的顶部都有状态行，包含当前屏幕名称和其他状态信息。每个 `pine` 屏幕的底部是该屏幕定义的双行命令菜单。如果命令太多，无法在两行内显示，`pine` 将显示一个命令，允许你在两个或多个部分菜单之间循环切换。

每个 `pine` 屏幕都允许你利用 `pine` 的某些功能。当你需要做决定时，可以获取帮助。

以下项目出现在主菜单中（见第 58 页的图 3-16）：

- 帮助（Help）
- 编写消息（Compose Message）
- 通讯录（Address Book）
- 文件夹列表（Folder List）
- 设置（Setup）
- 退出（Quit）

除了 Setup 和 Quit 外，当你选择上述列表中的某项时，`pine` 会为你显示该项的屏幕。当你选择 Setup 时，`pine` 会先提示你执行一个设置任务；你的一个选择是 Config（配置），它会修改 `pine` 的行为（见第 821 页的“配置 pine”）。选择 Quit 将返回到 shell。

在主菜单中选择 Help 将显示“主菜单帮助”屏幕，该屏幕提供了 `pine` 邮件程序的概述。这是新 `pine` 用户的很好的入门点。

## 发送消息

拥有 `pine` 通讯录会让发送邮件变得简单得多。要初始化你的通讯录，或在通讯录中添加、删除或编辑条目，请从 `pine` 主菜单中选择 Address Book。对于你向通讯录添加的每个用户，`pine` 都会提示用户的全名、昵称和电子邮件地址。在通讯录屏幕中，你还可以选择 List 来定义一个分配列表（distribution list）——一组你可以通过单个昵称引用的用户（昵称只是一个别名，可以方便你记忆和引用收件人或一组收件人）。

在 `pine` 命令行上指定收件列表将直接带带到“编写消息”（Compose Message）屏幕（见第 59 页的图 3-17）。如果你使用全名或昵称作为地址，`pine` 将尝试使用你的通讯录将名称映射到正确的电子邮件地址（或电子邮件地址列表）。如果你提供的名称不在你的通讯录中，`pine` 会假设该名称是你机器上的用户。当然，你可以在命令行上指定任何地址；收件人不需要在你的通讯录中也不要在你的机器上。

你也可以通过从 `pine` 主菜单中选择 Compose 进入消息编写器。访问 `pine` 主菜单允许你在会话期间使用其他 `pine` 功能。

消息头的字段显示在编写消息屏幕的顶部。如果你在命令行中包含了收件列表，To: 字段已填充；否则，你需要在该字段输入电子邮件地址，或在通讯录中显示的全名或昵称。其他字段包括：Cc:（用于消息抄送收件人）；用于为消息附加二进制文件；以及 Subject:（用于输入消息主题）。完成头部的字段后，你可以使用内置编辑器编写邮件消息（可以查看帮助来学习）。

如果你在编写消息的过程中想稍后再完成，可以选择 Post（发送）。`pine` 工具程序会将消息存储在名为 postponed 的文件夹中，下次你运行 `pine` 时，它将给你继续处理延迟消息的机会。

## 阅读消息

如果你想阅读邮件，最简单的方法是在命令行上使用 `-i` 选项。此选项将直接带进入文件夹索引屏幕（见第 6 页的图 3-18），其中显示了消息头列表。高亮的消息是当前消息；你可以使用屏幕定义的控制键高亮任何其他消息。

阅读消息的另一种方法是从主菜单中选择 Folder Index。这适用于你计划在阅读消息后进行操作。默认情况下，消息头包含以下字段：

| 标记 | 日期 | 发件人 | 大小 |
| :--- | :--- | :--- | :--- |
| A | 你回复了消息 | | |
| D | 消息是新的 | | |
| N | 转发消息 | | |
| * | 你标记了消息 | | |
| + | 你标记了消息为抄送 | | |

一旦你查看了消息，可以通过设置 `nntp-server` 访问新闻组。一旦服务器名称分配给 `nntp-server`，`pine` 将创建一个独立的目录或集合来存储新闻组。你订阅的每个组都会成为集合中的一个文件夹。此时你可能至少有两个集合，包括 INBOX、sent-mail 和 saved-messages。当你有多个集合时，Folder List 显示集合列表而不是文件夹列表；你需要高亮新闻组集合才能查看其中的文件夹。

在大多数情况下，`pine` 这样管理新闻。你可以删除消息、回复消息等。

要使用 `pine` 向新闻组发布消息，请在编写消息菜单中选择 Rich Hdr（丰富头）。这会显示通常隐藏的字段，包括 Newsgroups（新闻组）：这是输入要发布消息的新组名称的地方

## 配置 pine

更改 `pine` 的默认配置会改变工具的行为。某些 `pine` 变量取字符串值，而另一些则是设置或未设置。后者被称为功能列表选项。

超级用户可以在`usr/local/lib/pine.conf` 文件中建立某些 `pine` 变量的值。要显示这些值，请在 `pine` 命令行上提供 `-conf` 选项。如果你有想要覆盖的值，可以在你主目录 `pine` 启动文件 `pinerc` 中设置变量，或者从 `pine` 主菜单选择 Setup 进入设置配置屏幕。

以下是一些重要的字符串值 `pine` 变量：

- `editor` - 指定在消息编写器中编辑器。如果未设置，此变量默认为 `pine` 内置编辑器 `pico`。
- `personal-name` 出现在你发送的消息的 From: 行中。如果此变量未设置，`pine` 将使用存储在 `/etc/passwd` 文件中的全名。
- `signature-file` - 指定插入到你回复或编写的消息中的文件路径。此文件通常至少包含你的姓名和电子邮件地址。此变量的默认值为 `signature`（在你的主目录下）。
- `nntp-server` - 如果你有访问新闻服务器，如果你想阅读和发布 USENET 新闻，应将此变量设置为服务器的地址。

## 822 pine

以下是 `pine` 功能列表的部分选项：

- `enable-flag-cmd`
设置此选项允许你为邮件文件夹中的邮件消息指定标记（flags）。当设置此选项时，文件夹索引菜单中将包含“标记 (Flag)”菜单项。

- `enable-unix--pipe-cmd`
如果设置了此选项，`pine` 的文本屏幕上将出现“管道 (Pipe)”菜单项。选择此菜单项将使 `pine` 将消息文本通过管道传输到你输入的命令。

- `expunge-without-confirm`
如果设置了此选项，`pine` 在删除（expunge）消息之前不会请求确认。

- `quit-without-confirm`
通常情况下，当你选择“退出 (Quit)”退出 `pine` 时，它会提示确认。如果设置了此选项，`pine` 将不再询问确认。

- `save-will-not-delete`
通常，当你使用文件夹索引中的“保存 (Save)”命令将消息复制到文件夹时，该消息会被标记为待删除。此选项会抑制此行为。

- `signature-at-bottom`
如果你在回复邮件时包含了原始邮件，`pine` 会将你的签名（默认位于你的主目录下）放在原始消息上方。设置此选项会导致 `pine` 将你的签名放在原始消息文本下方。

- `use-current-dir`
当你在邮件程序中输入相对路径以导出邮件消息或将文件内容读取到邮件消息时，`pine` 该路径是相对于主目录的。此选项告诉 `pine` 使用工作目录。

## 示例

通常启动 `pine` 时会打开邮件文件夹 INBOX。在下面的示例中，`-f project_may97` 替换了它：

```
$ pine -f project_may97
```

在下一个示例中，Alex 给出了命令使用 `-i` 选项运行 `pine`：

```
$ pine -i
```
