
为了防止这种情况发生，你需要从 ypservers 数据库中移除已停用的从服务器的条目。

本章前面已经详细介绍了编辑 ypservers 映射的方法。

## 编辑 ypservers 的另一种方法

编辑 ypservers 文件的四步方法灵活且通用。它可以用于删除条目、添加条目和编辑条目。但是，也可以用一条命令删除服务器。例如，如果要为 NIS 主域从 ypservers 数据库中删除名为 foo 的服务器，请将当前工作目录更改为 `/var/yp/mydomain/`，然后在 NIS 主服务器上使用以下命令：

```
ypcat -k ypservers | grep -v '^foo$' | /usr/lib/yp/makedbm - ypservers; yppush ypservers
```

此命令实际上是由分号分隔的两个命令。这两个命令将按顺序执行。第一个命令是一个复合命令，通过管道将数据传递给三个命令。`ypcat -k ypservers` 的输出（即 ypservers 数据库的内容）通过管道传递给 `grep`，`grep` 使用 `-v` 选项显示任何不包含 foo 的行。插入符号（^）和美元符号（$）是元字符，分别匹配一行的开头和结尾。然后，这个 grep 命令的输出传递给 `makedbm`，以重新生成 ypservers。第二个命令将新的数据库推送到网络上的从服务器。

> **警告**
>
> 不要使用 `grep -v foo` 替代，因为它会匹配所有包含字符串 foo 的服务器名称，并将其从 ypservers 数据库中删除。

## 维护 NIS 映射

NIS 映射通常几乎不需要维护或关注。但是，仍需要做一些工作来使一切保持完美的运行状态。特别是，对 NIS 映射的任何更改都必须在主服务器上进行，并在更改之后重新构建 NIS 映射。此外，还应安排多个脚本自动运行，以确保所有 NIS 服务器上的 NIS 映射保持同步。

## 编辑 NIS 映射

通常，如果要更改 NIS 映射，你应当修改主服务器上 `/etc` 中的源文件，然后重建 NIS 映射。例如，要添加用户，应将其添加到主服务器上的 `/etc/passwd` 文件中。类似地，应将新主机添加到 NIS 主服务器上的 hosts 表 `/etc/hosts` 中。

完成此类更改后，你需要重新生成 NIS 映射。为此，将当前目录更改为 `/var/yp`，然后执行以下命令：

```
# make
```

NIS 映射将被重新构建并推送到从服务器。你可以参阅 `/var/yp/Makefile` 的内容，以便更详细地了解这些映射是如何构建并推送到从服务器的。

## 按计划同步 NIS 映射

NIS 服务器软件包提供了三个脚本，以确保所有服务器上的 NIS 映射保持同步。这些脚本如下：

- `/usr/lib/yp/ypxfr_1perday`：此脚本需要每天自动运行一次。
- `/usr/lib/yp/ypxfr_1perhour`：此脚本需要每小时自动运行一次。
- `/usr/lib/yp/ypxfr_2perday`：此脚本需要每天自动运行两次。

确定你要在何时运行这些脚本，然后按照第 7 章“计划任务”中的说明，将它们添加到 root 用户的 crontab 文件中。

## 其他 NIS 程序

以下三个 NIS 程序对于管理与使用 NIS 映射非常有用：

- `ypwhich`：此命令返回为使用该命令的 NIS 客户端提供服务的 NIS 服务器的名称。
- `ypcat`：此命令显示特定 NIS 映射中所有键的值。
- `ypmatch`：此命令显示特定 NIS 映射中一个或多个指定键的值。

### ypwhich 命令

ypwhich 命令用于显示当前客户端正在用来处理其 NIS 请求的 NIS 服务器名称。其最简单的形式是直接不带参数使用该命令，如下所示：

```
# ypwhich
```

你也可以使用 `-m` 参数运行 ypwhich，以显示特定 NIS 映射的主服务器。例如，要显示 ypservers 映射的主服务器，请使用以下命令：

```
# ypwhich -m ypservers
```

类似地，你可以通过指定主机名，使用 ypwhich 显示为另一台主机处理请求的 NIS 服务器。例如，要显示为主机 foo 提供服务的服务器，请使用以下命令：

```
# ypwhich foo
```

### ypcat 命令

ypcat 命令允许你显示指定 NIS 映射中所有键的值。例如，要显示 ypservers 映射中的值，请使用以下命令：

```
# ypcat ypservers
```

此外，你可以使用 ypcat 的 -k 参数来同时显示键和值，每个键值对单独占一行：

```
# ypcat -k ypservers
```

### ypmatch 命令

ypmatch 命令允许你显示指定 NIS 映射中一个或多个特定键的值。该命令的基本形式如下：

```
ypmatch <key list> <map name>
```

键列表是以空格分隔的键名列表。例如，要显示 passwd.byname 映射中 user1 条目的值，请使用以下命令：

```
# ypmatch user1 passwd.byname
```

要显示多个用户（例如 user1 和 user2）的值，请在以下命令中将它们全部列出：

```
# ypmatch user1 user2 passwd.byname
```

如果希望在显示每个值的同时显示键名，请添加 -k 参数，如下所示：

```
# ypmatch -k user1 user2 passwd.byname
```

## 了解名称服务器切换

使用 NIS 可能会带来潜在的混淆。考虑一个简单的例子：在一台 NIS 客户端上，你还在 /etc/passwd 中维护着本地用户数据库，以允许有限的本地登录。系统如何知道应该尝试对本地用户数据库还是对 NIS 用户数据库进行身份验证？

这是通过存储在 /etc/nsswitch.conf 的名称服务器切换文件来完成的。该文件指定了应该从以下三种可能来源中获取数据的顺序：

- 本地 /etc 文件
- NIS 映射
- 用于主机特定数据的 DNS 服务器

请考虑以下示例 nsswitch.conf 文件：

```
passwd:      files nis
group:       files nis
shadow:      files nis
hosts:       nis files dns

services:    nis [NOTFOUND=return] files
networks:    nis [NOTFOUND=return] files
protocols:   nis [NOTFOUND=return] files
rpc:         nis [NOTFOUND=return] files
ethers:      nis [NOTFOUND=return] files
netmasks:    nis [NOTFOUND=return] files
netgroup:    nis [NOTFOUND=return] files
bootparams:  nis [NOTFOUND=return] files
publickey:   nis [NOTFOUND=return] files
automount:   files nis
aliases:     nis [NOTFOUND=return] files
```

在这个文件中，有几个条目值得注意，以突出说明该文件的工作方式。请考虑以下条目：

```
passwd:   files nis
```

此条目表明，用户查找应首先针对本地 `/etc/passwd` 文件执行；如果未找到该用户，再针对 NIS 用户数据库执行用户查找。相比之下，请考虑以下条目：

```
hosts:    nis files dns
```

此条目表明，主机名查找应首先针对 NIS 主机数据库执行。如果未找到匹配的条目，则应查阅本地 `/etc/hosts` 文件。如果仍然找不到主机，则应尝试 DNS 查询，以将主机名解析为地址。

以下条目

```
services:  nis [NOTFOUND=return] files
```

是几个包含 `[NOTFOUND=return]` 的条目的示例。这表示，仅当 NIS 查找因“数据库中无匹配项”以外的原因失败时，查找才会从相关的 NIS 数据库映射继续到 `/etc` 中的相关文件。

例如，如果你尝试进行查找，但在 NIS 数据库中没有找到匹配的条目，则查找失败并停止。但如果你尝试进行查找，而对 NIS 服务器的请求超时，则查找将继续，并使用 `/etc` 中的本地文件。

## 有用的脚本

创建一些管理脚本可以简化 NIS 管理。特别是，使用脚本来添加和删除 NIS 域中的服务器非常有用。下面的脚本 `add-rm-ypservers` 可让这一管理任务变得更轻松。
