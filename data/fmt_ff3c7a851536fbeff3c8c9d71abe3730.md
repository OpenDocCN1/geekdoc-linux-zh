
或者，你可以右键点击，这将带出一个许多功能的菜单。这些选项包括：

- 重新扫描机器
- 以用户身份扫描
- 编辑机器
- 移除机器
- 显示信息

窗口中你可以双击子目录（以挂载它们），但在下方的窗口中无法这样做。

## 显著特性

`LinNeighborhood` 应用程序提供了这么多功能，几乎不可能列出所有功能。相反，我将只提到几个：

- 异构网络设置。
- 消除了使用 `smb`、`sebi` 和 `smient` 命令的所有复杂性。
- 让你远离命令行界面。
- 提供简单优雅的图形用户界面（GUI）。
- 具有智能设计。
- 与 `Windows` 网络无缝集成。

在这些命令中，你将主要使用“以用户身份扫描”。然而，偶尔你可能更改特定机器的信息或简单获取机器信息。这两个操作都非常简单。获取共享信息只需右键点击图标并选择“显示信息”。你将看到：

- 名称
- 操作系统
- 服务器
- IP 地址

## 结论

一旦挂载了共享并展开其内容，你会看到以文件形式显示的子目录。每个文件代表一个已挂载的共享，你可以使用配置的文件管理器进行浏览。要打开目录，你必须右键点击图标并选择“文件管理器”。配置的文件管理器将打开，你可以像访问本地驱动器一样进行浏览。

如果你使用 `Linux` 并处理 `Linux` 之外的应用程序，我再不能推荐你使用这个应用程序。`LinNeighborhood` 会让你的 `Linux` 计算变得简单得多——你将不知道没有它是如何生存的。

注意屏幕上方窗口的操作与下方窗口不同。在下方窗口中，你会看到显式的目录路径，例如 `/mnt2/TPG`，这显示了当前挂载的所有子目录。对于这些目录路径，右键点击可以访问“挂载”（或卸载）或“文件管理器”命令。虽然在上方窗口中

我的桌面上很少出现能像这个小宝石一样产生如此影响的应用程序。看起来创建者们做到了。
![](img/18a4ef5db1984d10d187_0.png)

网络

169

一旦构建了 `sendmail`，你就需要对其进行配置。`Sendmail` 使用 `m4` 从源配置文件构建所有的 `/etc/sendmail.cf`。这允许你通过定义 `m4` 选项并构建你的 `/etc/sendmail.cf` 来定义一些复杂的邮件行为。另一种方法是手动修改 `/etc/sendmail.cf`，除非你觉得在列表 A 中的操作让你显得非常愚蠢，否则有时这样做是可以接受的，但我不建议你这样做。（当然，如果你是一个 `Perl` 黑客，你可能在想为什么他们选择让这个文件具有如此可读性）。

这些就足够了。让我们聊聊文件中的指令：

- `divert(-1)`: 这意味着忽略后续的所有内容，直到出现 `divert(0)` 命令为止。
- `VERSION`: 这将丢弃生成的配置文件中的版本信息。
- `OPTYPE`: 这非常重要。如果你没有正确定义 `OPTYPE`，在运行程序时会遇到很多问题。
- `DOMAIN`: 你可以在这里输入你的域名名称，或者让 `let-sendmail` 从系统中获取名称。
- `MAILER(local)`: 本地邮件发送器总是会自动包含在内的。
- `MAILER(smtp)`: 应该注意，如果你打算添加 `FEATURE` 指令，那么 `MAILER` 指令应该放在最后。

在 `/etc/sendmail.cf` 顶部的某些选项并非如此。即使在配置文件中进行更改，其缺点是，如果你以后需要从 `m4` 重新生成它，你的更改可能会丢失。

运行新创建的 `sendmail.x.x` 运行你的命令：

这些指令中的每一个都将在生成的文件中生成一行到多行内容，你将使用列表 G 中的命令来构建它：

```
cd /etc
cp generic-linux.m mysite.cf
```

这将根据 `generic-linux.m` 文件生成 `mysite.cf` 文件。通过这样做，你可以确保在开始之前拥有一份原始文件的副本。

你最终将得到一个大约 1200 行的文件，与你可以通过随书附带的 CD 光盘访问的示例配置类似。另外请注意上面的输出，如果你手动处理文件为 `.cf`，你需要运行的命令是：

```
/usr/bin/m4 ... /m4/cf.m4 mysite.cf
```

你应该选择一个与你的环境尽可能相似的模板。我是在 `Linux` 系统上构建，所以 `generic-linux` 似乎是合适的。

让我们看看模板文件，它在列表 B 中显示。

这里没什么。记住，这只是一个模板文件。对于许多站点，

最新版本的 `sendmail` 将配置文件保留在 `/etc/mail`，而不仅仅是 `/etc`：

# 列表 A：剥离语法

```
# strip 组：语法（不在括号内！）和结尾的分号
R$: $1 <@  addresses
R* < $ > $* <@  $1 < $2 $3  unmark <addr>
R@ * <@  $1  unmark @host:
nR*: : * <@  $1 : $2  unmark node:addr
R: include:<@  $include: $1  include:
R* [ * ] <@  $1 [ $2 [ 3 ]  IPv6 addrs
R*: : [ ]  $1 : $2 [ 3 ] <@  remark if leading colon
```

## 列表 B：模板文件

```
divert(-1)
# Copyright (c) 1998, 1999 Sendmail, Inc. and its suppliers.
## All rights reserved.
## Copyright (c) 1983 Eric P. Allman. All rights reserved.
# Copyright (c) 1988, 1993
# The Regents of the University of California. All rights reserved.
# 通过使用此文件，你同意在 LICENSE 文件中列出的
# 条款和条件，该文件可以在 sendmail 
# 发行版的根目录中找到。
## 这是一个用于 Linux 的通用配置文件。
# 它仅支持本地和 SMTP 邮件。如果你想
# 自定义它，请将其复制为适合你环境的名称
# 并在此处进行修改。

divert($)dnl
VERSIONID($Id: gen-sendmail.mc.v 8.1 1999/09/24 22:48:05 gshapiro Exp $')
OSTYPE(linux)dnl
DOMAIN(generic)dnl
MAILER(local)dnl
MAILER(smtp)dnl
```

## 列表 C：构建你的 .cf

```
[stew@notebook cf]$ Build mysite.cf
```

```
Using M4 /usr/bin/m4
rm -f mysite.cf
/usr/bin-m4 ...m4/cf.m4 mysite.cf || ( rm -f mysite.cf && exit 1 )
chmod 444 mysite.cf
```

要完成安装，请备份当前的 `sendmail`。运行你的命令：

这些指令每一个都将在生成的文件中生成一行到多行内容。另外请注意上面的输出，如果你手动处理文件为 `.cf`，你需要运行的命令是：

```
/usr/bin/m4 ... /m4/cf.m4 mysite.cf
```

你应该选择一个与你的环境尽可能相似的模板。`generic-linux` 似乎是。

让我们看看模板文件，它在列表 B 中显示。

这里没什么。记住，这只是一个模板文件。对于许多站点，

最新版本的 `sendmail` 将配置文件保留在 `/etc/mail`，而不仅仅是 `/etc`：

# 列表 A：剥离语法

```
# strip 组：语法（不在括号内！）和结尾的分号
R$: $1 <@  addresses
R* < $ > $* <@  $1 < $2 $3  unmark <addr>
R@ * <@  $1  unmark @host:
nR*: : * <@  $1 : $2  unmark node:addr
R: include:<@  $include: $1  include:
R* [ * ] <@  $1 [ $2 [ 3 ]  IPv6 addrs
R*: : [ ]  $1 : $2 [ 3 ] <@  remark if leading colon
```

## 列表 B：模板文件

```
divert(-1)
# Copyright (c) 1998, 1999 Sendmail, Inc. and its suppliers.
## All rights reserved.
## Copyright (c) 1983 Eric P. Allman. All rights reserved.
# Copyright (c) 1988, 1993
# The Regents of the University of California. All rights reserved.
# 通过使用此文件，你同意在 LICENSE 文件中列出的
# 条款和条件，该文件可以在 sendmail 
# 发行版的根目录中找到。
## 这是一个用于 Linux 的通用配置文件。
# 它仅支持本地和 SMTP 邮件。如果你想
# 自定义它，请将其复制为适合你环境的名称
# 并在此处进行修改。

divert($)dnl
VERSIONID($Id: gen-sendmail.mc.v 8.1 1999/09/24 22:48:05 gshapiro Exp $')
OSTYPE(linux)dnl
DOMAIN(generic)dnl
MAILER(local)dnl
MAILER(smtp)dnl
```

## 列表 C：构建你的 .cf

```
[stew@notebook cf]$ Build mysite.cf
```

```
Using M4 /usr/bin/m4
rm -f mysite.cf
/usr/bin-m4 ...m4/cf.m4 mysite.cf || ( rm -f mysite.cf && exit 1 )
chmod 444 mysite.cf
```

要完成安装，请备份当前的 `sendmail`。运行你的命令：

这些指令每一个都将在生成的文件中生成一行到多行内容。另外请注意上面的输出，如果你手动处理文件为 `.cf`，你需要运行的命令是：

```
/usr/bin/m4 ... /m4/cf.m4 mysite.cf
```

你应该选择一个与你的环境尽可能相似的模板。`generic-linux` 似乎是。

让我们看看模板文件，它在列表 B 中显示。

这里没什么。记住，这只是一个模板文件。对于许多站点，

最新版本的 `sendmail` 将配置文件保留在 `/etc/mail`，而不仅仅是 `/etc`：

# 列表 A：剥离语法

```
# strip 组：语法（不在括号内！）和结尾的分号
R$: $1 <@  addresses
R* < $ > $* <@  $1 < $2 $3  unmark <addr>
R@ * <@  $1  unmark @host:
nR*: : * <@  $1 : $2  unmark node:addr
R: include:<@  $include: $1  include:
R* [ * ] <@  $1 [ $2 [ 3 ]  IPv6 addrs
R*: : [ ]  $1 : $2 [ 3 ] <@  remark if leading colon
```

## 列表 B：模板文件

```
divert(-1)
# Copyright (c) 1998, 1999 Sendmail, Inc. and its suppliers.
## All rights reserved.
## Copyright (c) 1983 Eric P. Allman. All rights reserved.
# Copyright (c) 1988, 1993
# The Regents of the University of California. All rights reserved.
# 通过使用此文件，你同意在 LICENSE 文件中列出的
# 条款和条件，该文件可以在 sendmail 
# 发行版的根目录中找到。
## 这是一个用于 Linux 的通用配置文件。
# 它仅支持本地和 SMTP 邮件。如果你想
# 自定义它，请将其复制为适合你环境的名称
# 并在此处进行修改。

divert($)dnl
VERSIONID($Id: gen-sendmail.mc.v 8.1 1999/09/24 22:48:05 gshapiro Exp $')
OSTYPE(linux)dnl
DOMAIN(generic)dnl
MAILER(local)dnl
MAILER(smtp)dnl
```

## 列表 C：构建你的 .cf

```
[stew@notebook cf]$ Build mysite.cf
```

```
Using M4 /usr/bin/m4
rm -f mysite.cf
/usr/bin-m4 ...m4/cf.m4 mysite.cf || ( rm -f mysite.cf && exit 1 )
chmod 444 mysite.cf
```

要完成安装，请备份当前的 `sendmail`。运行你的命令：

这些指令每一个都将在生成的文件中生成一行到多行内容。另外请注意上面的输出，如果你手动处理文件为 `.cf`，你需要运行的命令是：

```
/usr/bin/m4 ... /m4/cf.m4 mysite.cf
```

你应该选择一个与你的环境尽可能相似的模板。`generic-linux` 似乎是。

让我们看看模板文件，它在列表 B 中显示。

这里没什么。记住，这只是一个模板文件。对于许多站点，

最新版本的 `sendmail` 将配置文件保留在 `/etc/mail`，而不仅仅是 `/etc`：

# 列表 A：剥离语法

```
# strip 组：语法（不在括号内！）和结尾的分号
R$: $1 <@  addresses
R* < $ > $* <@  $1 < $2 $3  unmark <addr>
R@ * <@  $1  unmark @host:
nR*: : * <@  $1 : $2  unmark node:addr
R: include:<@  $include: $1  include:
R* [ * ] <@  $1 [ $2 [ 3 ]  IPv6 addrs
R*: : [ ]  $1 : $2 [ 3 ] <@  remark if leading colon
```

## 列表 B：模板文件

```
divert(-1)
# Copyright (c) 1998, 1999 Sendmail, Inc. and its suppliers.
## All rights reserved.
## Copyright (c) 1983 Eric P. Allman. All rights reserved.
# Copyright (c) 1988, 1993
# The Regents of the University of California. All rights reserved.
# 通过使用此文件，你同意在 LICENSE 文件中列出的
# 条款和条件，该文件可以在 sendmail 
# 发行版的根目录中找到。
## 这是一个用于 Linux 的通用配置文件。
# 它仅支持本地和 SMTP 邮件。如果你想
# 自定义它，请将其复制为适合你环境的名称
# 并在此处进行修改。

divert($)dnl
VERSIONID($Id: gen-sendmail.mc.v 8.1 1999/09/24 22:48:05 gshapiro Exp $')
OSTYPE(linux)dnl
DOMAIN(generic)dnl
MAILER(local)dnl
MAILER(smtp)dnl
```

## 列表 C：构建你的 .cf

```
[stew@notebook cf]$ Build mysite.cf
```

```
Using M4 /usr/bin/m4
rm -f mysite.cf
/usr/bin-m4 ...m4/cf.m4 mysite.cf || ( rm -f mysite.cf && exit 1 )
chmod 444 mysite.cf
```

我们要求的是将 `sendmail.cf` 中的 `HOLD_EXPENSE` 标记设置为 `true`，并将所有 `SMTP` 邮件发送器标记为高昂（expensive）。我们还将所有出站邮件传递到我们 `ISP` 的 `SMART_HOST` 服务器——`smtp.mysyip.com`。

拒绝来自你域名之外主机或某些“信任”主机的中继。在下一篇文章中，我们将介绍如何微调此行为，以及如何控制系统内部和外部对邮件系统的使用。

对生成的 `sendmail.cf` 的影响将类似于列表 所示。

最后，如果你查看 `sendmail.cf` 文件末尾附近的 `SMTP` 邮件发送器定义，你会注意到添加了表示高昂的 `e` 标记：

```
Msmtp P=[IPC] F=MDFMuxe
```

本地邮件发送器将没有 `e` 标记。现在，所有出站邮件将被暂留，直到你运行以下命令：

```
/usr/sbin/sendmail -q -v
```

默认情况下，依赖于 `sendmail` 的中继并没有被禁用。在互联网爆炸以及我们收到的相应的垃圾邮件出现之前，从/到任何主机进行中继曾相当常见。大多数邮件服务器现在

## 结论

我们触及了一些可以在 `.mc` 文件中启用的功能，并简单介绍了 `sendmail` 使用的一些数据库功能。作为一个极其灵活、可配置的程序，`sendmail` 具有许多功能和可以启用的“黑科技”（hacks）。O'Reilly 的那本蝙壳书有 1000 页关于 `sendmail` 及相关的文档，这可能让你了解这个主题可以有多深。有些人已经将 `sendmail` 视为过恐龙，并推崇其他邮件发送器（如 `qmail`）的优点。这些发送器也很好，但 `sendmail` 仍然满意地运行着许多高流量邮件站点。

## 列表 G：智能中继

```
## “智能”中继主机（可能为空）
DSsmtp.mysyip.com
```
