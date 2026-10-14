
```
Athena:~ # disable -r "stuck label" Computer_Room_bj200
```

要检查打印机的状态，可以使用 `lpstat` 命令。如果指定 `-t` 选项，将打印打印机环境的所有可用状态信息：

```
Athena:~ # lpstat -t
scheduler is running
system default destination: Computer_Room_bj200
device for Computer_Room_bj200: parallel:/dev/lp0
Computer_Room_bj200 accepting requests since Jan 01 00:00
printer Computer_Room_bj200 disabled since Jan 01 00:00 -
    stuck label)
printer LaserJet is idle.  enabled since Jan 01 00:00
Computer_Room_bj200-4  root 1024  Sun Feb 27 06:14:41 2005
Computer_Room_bj200-5  root 1024  Sun Feb 27 06:15:20 2005
Computer_Room_bj200-6  root 1024  Sun Feb 27 06:15:44 2005
Athena:~#
```

要允许打印恢复，可以使用 `enable` 命令。您需要使用完全限定的路径调用 `enable` 命令，以避免与内置的 `enable` 命令混淆：

```
Athena:~ # /usr/bin/enable Computer_Room_bj200
```

执行上述命令后，该设备的打印将恢复。

> **注意**
>
> 为避免不同 `enable` 命令之间的混淆，建议为打印机 `enable` 功能创建一个别名。这可以使用以下语法完成：

```
Athena:~ # alias penable=/usr/bin/enable
```

这允许您使用别名 `penable` 而不是每次都指定 `enable` 命令的完整路径。此外，您可以将其放在登录 `shell` 中以使其始终可用。如果您希望对所有用户可用，可以将别名定义添加到 `/etc/bash.bashrc`。

### CUPS Web 界面

我们已经看到 SLES 提供了命令行工具和 YaST 来管理打印机、队列和作业。CUPS 内置了从简单 Web 浏览器管理打印环境的能力。通过此 Web 界面，可以解决打印环境的所有方面。使用标准浏览器，可以通过 `http://localhost:631` 访问 CUPS。

默认情况下，Web 界面提供对服务器上类、队列和作业信息的只读访问。在执行管理任务之前，必须在 CUPS 环境中创建用户名/密码对。没有主机系统管理权限的人员也可以轻松成为 CUPS 管理员。您可以使用命令行动词 `lppasswd` 来执行此操作，如以下示例所示：

```
Athena:/etc/cups # lppasswd -g sys -a hart
Enter password:
Enter password again:
Athena:/etc/cups #
```

在此示例中，为管理 CUPS 环境创建了用户名/密码对。这允许名为 Hart 的用户创建新打印机和类并管理打印作业，但仅限于本地服务器节点。这意味着 Hart 需要在服务器上拥有本地账户和 X Windows System 访问权限。要将 CUPS Web 界面的管理功能扩展到本地机器之外，您必须更改 `/etc/cups/cupsd.conf` 配置文件。

`cupsd.conf` 文件使用与 Apache2 服务器配置类似的语法。管理访问基于为 CUPS 网站的 `/admin` 部分定义的访问控制。在 `cupsd.conf` 中，默认配置如下所示：

```
<Location /admin>
#
    AuthType BasicDigest
    AuthClass Group
    AuthGroupName sys

### Restrict access to local domain
    Order Deny,Allow
    Deny From All
    Allow From 127.0.0.1

#Encryption Required
</Location>
```

可以通过插入额外的 `Allow From` 子句来授予单个工作站或子网额外的访问权限。访问便利性必须与 CUPS 环境的暴露程度取得平衡。要添加整个子网，可以简单地将第四个八位组设置为 `*`，如下所示：

```
Allow From 192.168.1.*
```

当用户通过 Web 界面访问 CUPS 时，他或她将看到类似图 9.7 所示的浏览器窗口。

#### 图 9.7

CUPS Web 界面的主页面。

![](img/ae8469257d2662b469f2360b3bbbe322_340_0.png)

在图 9.7 中，主菜单将管理任务分解为以下主要部分：

- Administration，面向授权用户
- Classes
- Jobs
- Printers
- Help
- Software — 访问 CUPS 网站

Administration 菜单选项显示类似图 9.8 所示的窗口。如果需要定义新打印机或打印机类，则必须选择此菜单选项。Add 功能不在其他各种 CUPS 菜单上找到。再次说明，管理页面仅对能够使用通过 `lppasswd` 命令建立的凭据进行身份验证的用户可用。

#### 图 9.8

CUPS Web 界面的管理菜单。

![](img/ae8469257d2662b469f2360b3bbbe322_341_0.png)

类页面显示在图 9.9 中。与后续的管理页面一样，显示了“删除”和“修改”选项。访问这些选项需要适当的身份验证。未经授权的用户只会收到授权失败提示（HTTP 403 错误）。

#### 图 9.9

CUPS 类页面。

![](img/ae8469257d2662b469f2360b3bbbe322_341_1.png)

图 9.10 和 9.11 完成了 CUPS Web 界面下可用菜单选项的系列。在图 9.10 所示的作业页面中，您可以看到有关待打印作业的信息。同样，图 9.11 所示的打印机页面提供了每个打印机的配置信息、状态信息以及一系列管理选项。

#### 图 9.10

CUPS 作业管理页面。

![](img/ae8469257d2662b469f2360b3bbbe322_342_0.png)

#### 图 9.11

CUPS 打印机管理页面。

![](img/ae8469257d2662b469f2360b3bbbe322_342_1.png)

CUPS Web 界面对打印机配置管理的集成是简化分布式打印环境支持的重要一步。CUPS 环境包含其自身的管理模型。这允许将管理权限授予主机服务器身份验证方案之外的个人。因此，不拥有主机服务器任何权限的用户可以直接在 CUPS 中获得管理权限。在实施账户管理策略时，这增加了额外的管理负担。然而，它确实允许将队列管理委托给帮助台工作人员等个人，而无需在服务器上拥有提升的用户权限。

### 摘要

本章中，我们检查了打印的各个方面。SLES 提供了多种创建和维护队列的方法。

使用 YaST，我们创建了本地和网络打印队列。我们使用命令行工具来微调这些队列的特性并提交作业。

在本章中，我们看到了 CUPS 打印环境如何使队列管理变得更简单。此外，我们研究了如何使用 CUPS Web 界面远程管理打印环境，而无需本地访问打印服务器本身。

## 数据备份与灾难恢复

无论服务器硬件有多么容错，或者您是否实施了最佳的安全措施，都不能保证数据永远不会丢失。有时原因完全超出您的控制——例如由燃气泄漏引起的火灾，甚至大自然（还记得洛杉矶地震吗？）。此外，人皆会犯错；即使是最有经验的用户和系统管理员也会犯错误。删除错误的文件或在文件中输入错误信息（例如 `/etc/passwd`）可能会导致不必要的头痛，并为需要访问数据的您或同事带来额外的工作，在最坏的情况下，删除会导致整个系统无法使用。此外，心怀不满的用户或恶意的黑客可能会故意删除或损坏基本数据或系统文件；事实上，大多数攻击来自公司内部而不是外部。在所有情况下，拥有最新的备份都是救命稻草。

从黑客入侵中恢复可能是一项繁琐的工作。问题在于，一旦系统被入侵，就几乎不可能确定发生了一切，特别是如果系统的 `root` 账户已被入侵。日志文件和审计跟踪有所帮助，但如果黑客很好地掩盖了自己的痕迹，就找不到任何迹象。因此，快速从任何入侵中恢复的最佳方法是使用一个干净的备份。

为了能够使用此类备份，至关重要的是您已开发并实施了可靠的数据备份和灾难恢复策略。本章中，您将学习如何制定备份计划以及如何何时使用标准 Linux 备份工具，如 `tar` 和 `cpio`。您还将了解如何使用 YaST 创建和使用 SLES 救援软盘。

#### 提示
