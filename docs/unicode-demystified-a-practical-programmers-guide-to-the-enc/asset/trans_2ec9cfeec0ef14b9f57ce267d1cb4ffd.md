

最后在键盘上打字或接收并阅读电子邮件的时间。在从各种系统文件中提取这些信息后，`finger` 工具会显示用户主目录下名为 `.plan` 和 `.project` 的文件内容。每个用户负责创建和维护这些文件，这些文件通常提供更多关于用户的信息（如电话号码、邮寄地址、日程、兴趣等）。

`finger` 生成的短报告与实用程序提供的类似；它包含了用户的登录名、全名、用户终端的设备号、自上次在终端键盘上打字以来的时间、用户登录的时间以及用户终端的位置。如果用户通过网络登录，则远程系统的名称被识别为用户的位置。

## 注意事项

当你指定网络地址时，`finger` 工具通过查询运行远程系统上的标准网络服务来工作。虽然该服务随 Red Hat Linux 一起提供，但某些站点选择不运行它（以减少其系统的负载，以及潜在的安全风险，或仅仅是为了维护隐私）。如果你尝试使用 `finger` 获取此类站点某人的信息，结果可能是一个错误信息或无所获。远程端决定与你的系统共享多少信息以及以什么格式。因此，任何给定系统显示的报告可能与所示示例不同。另见第 81 页的“finger: Lists Users on the System”。

## 示例

第一个示例显示了当前登录系统上的所有用户的信息：

| finger Name | Tty | Idle | Login Time | Office | Phone |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Alex | Alex Watson | tty1 | 13:29 | Jun 22 21:03 | | |
| hls | Helen Simpson | *pts/1 | 13:29 | Jun 22 21:02 | (:) | |
| jenny | Jenny Chen | pts/2 | Jun 23 07:47 | (bravo.tcorp.com) | | |

在示例中，Helen (TTY) 行名称前的星号 (**) 表示她已阻止他人直接向其终端发送消息（参见 `mesg`，第 87 页）。长报告会为禁用消息的用户显示字符串消息。

接下来的两个示例使 `finger` 通过网络联系名为 `kudos` 的远程系统获取信息：

```
$ finger @kudos
[kudos]
Login Name Tty Idle Login Time Office Phone
alex Alex Watson tty1 23:15 Jun 22 11:22
roy Roy Wong pts/2 Jun 22 11:22

$ finger watson@kudos
[kudos]
Login: alex Name: Alex Watson
Directory: /home/alex Shell: /bin/zsh
On since Sat Jun 22 11:22 (PDT) on tty1, idle /23:22
Last login Sun Jun 23 06:20 (PDT) on ttyp2 from speedy
Mail last read Thu Jun 20 08:10 2002 (PDT)
Plan:
For appointments contact Jenny Chen, x1963.
```

## fmt

非常简单地格式化文本

fmt [option] [file-list]

`fmt` 工具通过尝试让所有非空行的长度几乎相同来执行简单的文本格式化。

## 参数

`fmt` 工具读取 `file-list` 中的所有文件，并将将其内容的格式化版本打印到标准输出。如果你没有提供任何文件名，`fmt` 将读取标准输入。

## 选项

- -uniform-spacing 更改输出，使得单词之间有一个空格（SPACE）；句子之间有两个空格（SPACES）。
- -width=n 将输出行宽改为 n 个字符。如果没有此选项，`fmt` 尝试保持输出行接近 75 个字符。

## 注意事项

`fmt` 工具通过移动换行符来工作。行的缩进以及单词之间的间距保持不变。

此工具通常用于在使用编辑器（如 vi）时格式化文本。例如，你可以在 vi 编辑器的命令模式下，通过将光标置于段落顶部，然后输入 `!fmt -60` 来格式化该段落。这将该段落替换为通过 `fmt` 处理的结果，并指定宽度为 60 个字符。

## 示例

以下示例显示了 `fmt` 如何尝试让所有行相同。`-50` 选项产生的结果：

```
$ fmt -50
One factor that is important to remember while administering the intake of Charchararias that there is, at least from view of the subject, very little differentiating the prepared morsels from your digits.
```

换句话说，不要喂鲨鱼！

## fsck

检查并修复文件系统

fsck [options] [filesystem-list]

`fsck` 工具是一个前端，通过调用其他工具来处理各种类型文件系统。

