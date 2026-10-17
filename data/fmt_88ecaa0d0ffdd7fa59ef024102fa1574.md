
# mgetty+sendfax 传真软件配置

`mgetty+sendfax` 是一个软件包，使用 `mgetty` 命令，您可以像前面所示的 `ugetty` 示例一样将其安装在 `/etc/inittab` 中，并使用 `sendfax` 程序发送传真。该软件的安装和配置比设置 `efax` 稍微复杂一些。本节将向您展示如何设置、配置和使用该软件通过调制解调器发送和接收传真文档。

该软件包包含许多文件（太多无法在此列出）。本节中的示例集中在重要的文件上，并向您展示如何配置 `sendfax` 软件并快速发送传真。您的第一步是确保以 `root` 操作员身份登录。您需要将目录更改为 `/etc` 目录下的 `mgetty+sendfax` 目录。那里有许多文件，例如：

```
# ls -A
dialin.config  fax.deny  faxrunq.config  mgetty.config  voice.conf
fax.allow      faxheader  .login.config  sendfax.config
```

## 配置文件准备

您的首要任务是如果不存在则创建 `fax.allow` 和 `fax.deny` 文件。在 `fax.allow` 文件中，输入您希望启用传真服务的用户名称。至少输入两个名称：`root` 和您的用户名。

接下来，编辑 `faxheader` 文件，并在示例页眉行中输入您的姓名和电话，例如：

```
FAX FROM: John H. Doe 1 202 555 1212  TO: @T@  PAGE: @P@ OF @M@
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_239_0.png)

> 您应在对 `sendfax` 配置文件进行更改时使用注释字符 `#`，并在新行上重新输入更改。这可以避免在出现错误需要将文件恢复到原始状态时带来的麻烦。

示例页眉行会出现在接收传真机上传真页面的顶部。接下来，编辑 `sendfax.config` 文件，然后查找 `fax-devices` 部分，并更改调制解调器所连接的设备名称（如 `COM2` 的 `/dev/ttyS1`），例如：

```
# which devices to use for outgoing faxes
#fax-devices tty4c:tty4d
fax-devices ttyS1
```

这告诉 `sendfax` 程序您的传真调制解调器连接到 `/dev/ttyS1`。接下来，输入您的传真号码，该号码将发送到远程传真机，例如：

```
# which fax number to transmit to the receiving station
#fax-id 49 89 xxxxxxx
fax-id 1 317 123-1234
```

这将向远程传真标识您的传真机。您还需要输入发送传真时要使用的拨号类型，例如：

```
# which command is used to dial out? (Could be ATD, ATDP, ATX3DOW...)
#dial-prefix ATD
dial-prefix ATDT
```

这告诉 `sendfax` 软件您希望使用音调拨号拨出。保存文件并退出文本编辑器。此时，您几乎准备好开始发送传真。

## 发送传真

要使用 `sendfax` 程序发送一页传真，您必须先将文本文件转换为 Group 3 传真格式。您可以使用位于 `/usr/bin` 目录下的图形转换程序 `pbm-text` 和 `pbm2g3` 程序来完成此操作，例如：

```
# cat myfile.txt | pbmtext | pbm2g3 > myfile.g3
```

这会将文件 `myfile.txt` 通过 `pbmtext` 命令管道传输，该命令输出便携式位图图形格式到 `pbm2g3` 命令，后者然后将字符管道流转换为传真图形格式。完成此操作后，您可以假设您是 `root` 操作员，使用以下命令发送文件：

```
# /usr/sbin/sendfax -v -l ttyS1 -C cls2 -r 5551212 myfile.g3
Trying fax device '/dev/ttyS1'... OK.
Dialing 5551212... OK.
sending 'myfile.g3'...
```

这运行 `sendfax` 程序。`-v` 命令行选项告诉 `sendfax` 在传真操作期间提供一些反馈。我使用 `-l` 选项指定 `ttyS1` 串行端口，并使用 `-C cls2` 命令行选项通过 Class 2 传真调制解调器发送传真。电话号码 `555-1212` 使用 `-r` 选项指定，文件 `myfile.g3` 是您使用前面命令行管道创建的文件。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_240_0.png)

> 与 `efax` 不同，`sendfax` 命令仅支持 Class 2 传真调制解调器。如果您有 Class 1 调制解调器，请使用 `fax` shell 脚本。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_240_1.png)

## 接收传真

您还可以使用 `mgetty` 程序设置 Linux 系统以自动接收传入传真。与 `ugetty` 程序类似使用，`mgetty` 也需要在 `/etc/mgetty+sendfax` 目录中的配置文件进行至少一次更改。您可以进行的更改（作为 `root` 操作员）是编辑文件 `mgetty.config` 中的电话识别条目，例如：

```
# set the local fax station id
#fax-id 49 89 xxxxxxx
fax-id 1 317 123 1234
```

这设置了本地传真机的电话号码。完成此操作后，如前所述编辑 `/etc/inittab` 文件，并使用 `mgetty` 监听串行端口，例如：

```
3:2345:respawn:/usr/sbin/mgetty -s 38400 ttyS1
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_241_0.png)

> 如前所述，对 `/etc/inittab` 文件的任何编辑都可能存在危险。始终准备一个备用启动盘并先备份该文件。

做出此更改后，保存文件并重新启动计算机。现在，您不仅能够接收传真，还可以从外线拨入并运行 Linux 程序。要查看是否有传真到达，您必须显式查看 `/var/spool/fax/incoming` 目录，例如：

```
# ls -A /var/spool/fax/incoming
fn4878f9aS1..._IBM-APTIVA-M61_..01  fn4878f9aS1..._IBM-APTIVA-M61_..02
```

这显示有一份两页的传真等待阅读。您可以通过先将它们转换为便携式位图文件格式来阅读传真，例如：

```
# cat /var/spool/fax/incoming/*.01 | g32pbm > faxpage1.pbm
```

将这些传真文件转换为便携式位图格式后，您就可以使用 X11 `xv` 客户端或 ImageMagick 显示 X11 程序来阅读或打印您的传真。

如您所见，使用 OpenLinux 传真文档时您有几种软件选择。`sendfax` 程序还有许多其他选项。请阅读其手册页和 `/usr/doc/mgetty+sendfax` 目录下的文档以了解详细信息。

## 摘要

本小时向您展示了如何配置 OpenLinux 系统以与计算机的调制解调器配合使用。您还学习了如何设置 OpenLinux 应答来电以及如何发送和接收传真文档。

### 问答

Q 我想了解更多关于调制解调器和传真的信息。有没有资源？

A 首先，阅读 `efax` 和 `mgetty+sendfax` 程序的文档，以了解更多关于使用这些程序与 OpenLinux 的信息。如果您想阅读一篇关于使用调制解调器和调制解调器软件的非特定操作系统概述，请阅读 Peter Chen 的《What You Need to Know about Modems》，网址为 http://www.vix.com/flexfax/Modems-PeterChen。

Q 我想关闭调制解调器连接时发出的高 pitched 尖叫声。如何操作？

A 请阅读调制解调器文档了解具体细节，但通常情况下，`ATM0` 命令会关闭您的调制解调器。

Q 我想听到调制解调器拨号和连接，但不想声音太大！

A 尝试使用 `ATM1` 命令启用声音，然后尝试使用 `ATLx` 命令，其中 `x` 代表 0（低）到 3（高）的扬声器音量。此功能并非所有调制解调器都支持。

Q 我的调制解调器在在线会话期间有时会断开连接！

A 如果您有呼叫等待，传入呼叫可能会干扰您的调制解调器。尝试在任何拨号字符串前面加上 `*70`（例如 `ATDT*70`）以禁用呼叫等待。

### 练习

- 1. 尝试拨打本地公告板服务（BBS）并使用 `seyon` 或 `minicom` 程序连接。
- 2. 创建一个图形，然后以 PostScript 格式保存它，并尝试将其作为传真发送。有关在 OpenLinux 会话期间创建图形的更多信息，请参阅第 16 小时。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_244_0.png)

# 第10小时

## 连接到互联网
