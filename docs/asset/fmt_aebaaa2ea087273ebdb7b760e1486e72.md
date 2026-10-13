
[root@server /root]# rpm yp-tools-2.2-1.1386.rpm bind3-3.3-20.1386.rpm and

使用以下命令安装 RPMS `yp-tools-2.2-1.1386.rpm` 和 `ypserv-1.3.6.91-1.1386.rpm`：

```
[root@server RPMS]# rpm -i yp-tools-2.2-1.1386.rpm
[root@server RPMS]# rpm -i bind3-3.3-20.1386.rpm
[root@server RPMS]# rpm -i ypserv-1.36.91-1.1386.rpm
```

软件安装完成后，下一步是配置 NIS 服务器。

## 配置主 NIS 服务器

在配置服务器软件之前，你需要决定是否要设置从服务器。如果是的话，你需要在继续之前知道它们的主机名。在确定 NIS 服务器名称的同时，你此时还需要决定一个 NIS 域名。请记住，这个域名与你的 DNS 域名不同，为了清晰起见，它们将设置得不同。此外，该名称必须存在于 `/etc/hosts` 文件中。

有了这些信息，你就可以准备开始了。首先，你需要使用 `domainname` 命令设置域名：

```
[root@vestax /etc]# hostname audionet.domain.com
```

虽然这目前可以运行，但你确实需要更改启动配置文件，以便在系统每次重启时都发生这种情况。作为 RPM 部分安装的 `/etc/rc.d/init.d/ypserv` 脚本会查找 `/etc/sysconfig/network` 文件中设置的域名。只需添加以下行：

```
NIS_DOMAIN=audionet.domain.com
```

设置域名后，你可以决定想通过 NIS 共享哪些文件以及它们的文件名。通过编辑 `/var/yp/Makefile` 来执行此操作。正如名称所示，NIS 使用 `map` 工具来维护其映射（maps）。虽然熟悉该工具的工作原理很有帮助，但配置 NIS 并非强制要求。

从将 `/var/yp/Makefile` 加载到你喜喜欢的编辑器中开始。跳过显示如下内容的行：

+   # 这些是用于构建 NIS 数据库的文件。你可能根据喜好对这些 
#   # 文件进行编辑，以防你希望将你的 NIS 源文件
#   # 与 NIS 服务器的实际配置文件分开。

在这一段文本下方，你将看到类似下面的行：

```
GROUP = $(YPPWDDIR)/group
PASSWD = $(YPPWDDIR)/passwd
et...
```

当你向下滚动文件时，你会注意到有几个可以设置的参数，这些参数可以用来更改 NIS 服务器的行为。目前，你可能不应该修改本节中讨论的项之外的任何内容。如果你觉得想冒险，可以阅读与每行相关的注释并尽情尝试。

这一节告诉 NIS 你的数据库文件所在地。`$(YPPWDDIR)` 字符串是一个变量，在 Makefile 顶部被设置为 `/etc`。虽然可以将其更改另一个目录，但为了一致性，你可能应该保持在那里。`$(YPPWDDIR)` 之后的字符串是 `/etc` 中的文件名，它将通过 NIS 传输。大多数条目可以保持不变。你想更改的少数项是 `GROUP`、`PASSWD`、`SHADOW`、`ALIASES` 以及可能还有 `HOST`。

`GROUP` 行显示控制组信息位于 `/etc/group`。你可能希望将服务器上的本地组文件与其他文件分开。

设置好域名后，你可以决定想通过 NIS 共享哪些文件以及它们的文件名。你通过编辑 `/var/yp/Makefile` 来执行此操作。正如名称所示，NIS 使用 `map` 工具来维护其映射。虽然熟悉该工具的工作原理有用，但配置 NIS 并非强制要求。

对于其他 行也是如此，一个简单的约定是后缀加上 `.yp`。结果看起来如下：

```
PASSWD = $(YPPWDDIR)/passwd
```

默认情况下，NIS 不分发 UID 低于 500 的任何密码项。要更改此项，请查找读取 `MINUID=500`。紧随其后的是 `MINGID=500`。如果你已经包含 500 以下值的 UID/GID 系统，你可能希望保持此设置不变。

## 配置服务

第二部分

确定了想要设置的文件后，你现在可以决定分发哪些。向下滚动 Makefile 直到以下块：

```
# 如果你不想构建其中的某些映射，可以随时在列表中 
# 将它们注释掉。
```

你的光标应该位于以下行：

```
all: ypsvers passwd group hosts rpc services netid mail \
  # shadow publicickey # netgrp ethers bootparams \
  # # amd.home auto.master
```

这一行指定了哪些映射可用。`#` 符号是注释符号。第二和第三行被注释掉了。

在对此行进行任何更改之前，你应该为它创建一个备份并将备份注释掉。结果看起来如下：

```
#all: ypsvers passwd group hosts rpc services netid mail \
  # shadow publicickey # netgrp ethers bootparams \
  # # amd.home auto.master

all: ypsvers passwd group hosts rpc services netid mail \
  # shadow publicickey # netgrp ethers bootparams \
  # # amd.home auto.master
```

通过注释掉该行，你可以保留一个副本，以防出现问题。你可以随时参考副本并查看更改前的行内容。在有了副本后，可以开始你的更改。

你的网络需要分发的文件只有 `ypsvers`, `passwd`, `group`, `hosts`, `rpc`, `services`, `netid`, `protocols` 和 `mail`。这种分发已经设置好，你不需要更改任何内容。

> 注意

其他行有什么用吗？好问题！它们是某些站点使用的其他数据库。当你需要特定的条目时，只需取消注释并将其分发给你的客户端。在某些站点，NIS 被用于分发其他类型的信息，因此你甚至可以使用 NIS 制作公司电话录。

除非你熟悉 Makefile，否则你应该保持文件的其余部分不动。保存 Makefile 并退出编辑器。

# NIS: 网络信息服务

第 12 章

至此，我们已经通过 `/usr/lib/yp/ypinit` 命令调用了你的 NIS 数据库。调用该命令时，它会提示你想要启动的任何 NIS 从服务器的名称。例如，选择 `denon` 作为 NIS 从服务器。

请记住，你并不需要设置 NIS 从服务器。如果你有大量的 NIS 客户端并且需要分担它们产生的负载，那么设置从服务器是有用的。

如果你尚未设置域名，接下来的初始化将报错，并显示信息“The local host's domain name has not been seen. Please set it.”（未看到本地主机的域名。请设置）。要初始化主服务器，请使用以下命令：

```
[root@vestax /root]# /usr/lib/yp/ypinit
我们必须构建一个运行 NIS 服务器的主机列表。vestax 已在 NIS 服务器主机列表中。请继续添加其他主机的主机名，每行一个。列表完成后，输入 <CTRL-D>
```

```
next host to add: vestax
next host to add: denon
next host to add: <CTRL-D>
当前的 NIS 服务器列表如下：
```
