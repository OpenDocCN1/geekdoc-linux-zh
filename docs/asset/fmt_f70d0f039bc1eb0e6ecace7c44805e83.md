
在该页面上，我们在搜索栏中使用 `git` 并选择它。然后，向下滚动直到到达 `Sudo` 节。在我们尝试利用这一发现进行权限提升之前，让我们先找到 `linPEAS` 的结果。我们可能会漏掉一些关键的发现。下一个有趣点是分析 `WordPress` 文件，其中包含一个用于数据库访问的明文密码。

## 821 - 当 git 等二进制文件允许通过 sudo 运行时寻找潜在的滥用

在该页面上，我们在搜索栏中使用 `git` 并选择它。然后，向下滚动直到到达 `Sudo` 节。在我们尝试利用这一发现进行权限提升之前，让我们先找到 `linPEAS` 的结果。我们可能会漏掉一些关键的发现。下一个有趣点是分析 `WordPress` 文件，其中包含一个用于数据库访问的明文密码。

# OffSec

使用 Kali Linux 进行渗透测试

```diff
diff --git a/fetch_current.sh b/fetch_current.sh
deleted file mode 100644
index 25667c..0000000
--- a/fetch_current.sh
+++ /dev/null
@@ -1,6 +0,0 @@
-#!/bin/bash
```

列表 893 - 显示提交之间的差异

太棒了！通过显示提交之间的差异，我们又识别出了另一组凭据。使用 `sshpass`¹¹⁵ 自动化任务的方法通常用于为脚本以非交互方式提供密码。

在结束此之前，让我们将用户名和密码添加到我们 Kali 机器上的 `creds.txt` 中。

> 在实际评估中，一旦我们获得了系统的权限访问，就应该再次运行 `LinPEAS`。因为该工具现在可以访问用户和系统文件，它可能会发现在运行 `daniela` 时无法访问的敏感信息和数据。

让我们总结一下在本节中我们取得的成就。我们使用 `LinPEAS` 自动枚举脚本识别了潜在的敏感信息和权限提升向量。脚本识别出可以以用户 `daniela` 通过 `sudo` 运行 `/usr/bin/git`、`WordPress` 目录是一个 Git 仓库，且 `WordPress` 数据库设置中有明文密码。通过执行 `sudo` 命令，我们成功提升了权限。然后，我们在 Git 仓库中识别了一个之前被删除的 bash 脚本并显示了它。该脚本包含一个新的用户名和密码。

在下一个学习单元中，我们将结构化并利用获得的信息进行攻击，这将提供对内部网络的访问权限。

# 24.3 获取内部网络的访问权限

本学习单元涵盖以下目标：

- 从非域联机器上验证域凭据
- 执行网络钓鱼以获取对内部网络的访问权限

在上一个学习单元中，我们获得了 `WEBSRV1` 的权限访问。此外，我们还识别了几个密码和用户名。

¹¹⁵ (Linux Die.Net, 2022), https://linux.die.net/man/1/sshpass

PWK - © 2023 OffSec Services Limited. 版权所有。

824

# OffSec 使用 Kali Linux 进行渗透测试

在本学习单元中，我们将共同尝试验证一组有效的凭据，并利用它们通过准备和发送电子邮件来获取内部网络的访问权限。

## 24.3.1 域凭据

在本节中，我们将尝试识别 `MAILSRV1` 上的用户名和密码组合。让我们开始使用 `creds.txt` 文件中的当前信息创建一个用户名和密码列表。让我们先查看 `creds.txt` 中的当前信息。

```
kali@kali:~/$ creds.txt
daniela:tequieromucho (SSH 私钥密码)
wordpress:DanielKeyboard3311 (WordPress 数据库连接设置)
john:dqsTwTpZpn# (fetch-current.sh)
```

其他识别出的用户：`marcus`

> 列表 894 - 显示 `creds.txt` 的内容

根据列表 894，我们将为 `marcus`、`john` 和 `daniela` 创建一个用户名列表。由于 `wordpress` 不是一个真实用户，而是用于 `WEBSERV1` 上 `WordPress` 实例的数据库连接，我们将为 `tequieromucho`、`DanielKeyboard3311` 和 `dqsTwTpZpn#nl` 创建一个密码列表。两个列表及其内容显示在如下列表中：

```
kali@kali:~/$ usernames.txt
marcus
john
daniela
```

```
kali@kali:~/$ passwords.txt
tequieromucho
danielKeyboard3311
dqsTwTpZpn#nl
```

> 列表 895 - 显示包含识别出的用户名和密码的列表
