
重启已加载配置文件之一的进程会改变 `rcapparmor status` 的输出：

```
dal10:- # rcs nsc restart
Shutting down Name Service Cache Daemon        done
Starting Name Service Cache Daemon             done
dal10:- # rcapparmor status
apparmor module is loaded.
50 profiles are loaded.
49 profiles are in enforce mode.
1 profiles are in complain mode.
Out of 62 processes running:
1 processes have profiles defined.
1 processes have profiles in enforce mode.
0 processes have profiles in complain mode.
```

AppArmor 的输出不包含关于已加载配置文件或被限制进程的具体数据。

已加载配置文件列表保存在 `/sys/kernel/security/apparmor/profiles` 中。它可能如下所示：

```
dal10:- # cat /sys/kernel/security/apparmor/profiles
/usr/sbin/traceroute (enforce)
/usr/sbin/squid (enforce)
/usr/sbin/sendmail (enforce)
/usr/sbin/postqueue (enforce)
...
/usr/lib/postfix/bounce (enforce)
/usr/lib/firefox/firefox.sh (complain)
/usr/bin/ldd (enforce)
...
```

命令 **unconfined** 列出了具有绑定套接字但未加载任何配置文件的进程：

```
da10:~ # unconfined
2659 /sbin/portmap not confined
2659 /sbin/portmap not confined
2694 /usr/lib/zmd/zmd not confined
2756 /usr/sbin/slpd not confined
2756 /usr/sbin/slpd not confined
2756 /usr/sbin/slpd not confined
2756 /usr/sbin/slpd not confined
2756 /usr/sbin/slpd not confined
2756 /usr/sbin/slpd not confined
2831 /usr/sbin/cupsd not confined
2831 /usr/sbin/cupsd not confined
2874 /usr/sbin/sshd not confined
2905 /usr/sbin/sshd not confined
2905 /usr/sbin/sshd not confined
3040 /usr/lib/postfix/master not confined
3040 /usr/lib/postfix/master not confined
```

此命令不会提供有关因在启用 AppArmor 时已经在运行而未受限的已加载配置文件的进程的信息。为了找出这些进程，请查看 `ps -Z` 并将其输出与 `/sys/kernel/security/profiles` 的内容进行比较；重启那些本应受限的进程。

## 重新加载配置文件

如果您使用编辑器手动修改了 `/etc/apparmor.d/` 中的配置文件（而不是使用 `logprof` 等 AppArmor 工具），则必须重新加载相关的配置文件。应使用的命令是 **rcapparmor reload**。**rcapparmor restart** 等效于重新加载；它不会停止然后启动 AppArmor，但会重新加载配置文件。在发出 **rcapparmor reload** 之前已受限的进程将保持受限状态（除非您删除了它们的配置文件或将它们的模式从 enforce 更改为 complain）。

命令 **enforce** 和 **complain** 在 enforce 和 complain 模式之间切换，并重新加载相关的配置文件。

## 目标 4 监控 AppArmor

监控 AppArmor 有两种方法：

-   安全事件报告
-   安全事件通知

## 安全事件报告

用于配置和查看 AppArmor 安全事件报告的 YaST 模块可以通过启动 YaST 并选择 **Novell AppArmor > AppArmor Reports** 来启动。也可以在控制台窗口中以 root 身份直接输入 `yast2 SD_Report` 启动。

打开的对话框显示了生成安全事件报告的时间：

![](img/63e88022bf135307e3eac051ad238b5b_362_0.png)

默认情况下，这些报告每天午夜生成一次。

使用按钮 **Add**、**Edit** 或 **Delete**，您可以计划新的安全事件报告，编辑现有报告（例如，设置接收报告的电子邮件地址），或删除事件报告。

选择一个报告，然后选择 **Run Now**，将直接显示结果，或者在安全事件报告的情况下，首先打开一个对话框，您可以在其中微调结果报告的内容：

![](img/63e88022bf135307e3eac051ad238b5b_363_0.png)

左侧的帮助文本解释了可用选项。配置完您希望在报告中包含的内容后，选择 **Next**。报告显示了安全事件：

![](img/63e88022bf135307e3eac051ad238b5b_364_0.png)

根据您在前面对话框中的配置，报告也会保存到磁盘，默认情况下保存在目录 `/var/log/apparmor/reports-exported/` 中。

## 安全事件通知

要配置安全事件通知，请启动 YaST 并选择 **Novell AppArmor > AppArmor Control Panel**，或者在控制台窗口中以 root 身份直接输入 **yast2 subdomain** 启动该模块。

打开以下对话框：

![](img/63e88022bf135307e3eac051ad238b5b_365_0.png)

在 **Enable Security Event Notification** 框中选择 **Configure**。将打开一个对话框，您可以在其中配置通知频率、电子邮件地址以及报告应涵盖的严重级别：

### 图 7-11

![](img/63e88022bf135307e3eac051ad238b5b_366_0.png)

选择 **Ok** 以保存您的配置。选择 **Done** 以关闭 **AppArmor** 配置窗口。

## 摘要

| 目标 | 摘要 |
| :--- | :--- |
| 1. 理解 SELinux 和 AppArmor 之间的区别 | SELinux 和 AppArmor 根据策略和配置文件中设置的规则对进程施加限制。<br><br>即使被入侵，程序在允许其读取、写入和执行的操作方面也受到限制。即使对于以 root 权限运行的程序也是如此。<br><br>虽然 SELinux 和 AppArmor 具有共同的目标，但技术实现完全不同。 |
| 2. 创建和管理 AppArmor 配置文件 | 有 YaST 模块和命令行工具用于创建和管理 AppArmor 配置文件。<br><br>主要的 YaST 模块是“添加配置文件向导”和“更新配置文件向导”。<br><br>相应的命令行工具是 autodep、genprof 和 logprof。<br><br>配置文件是位于 /etc/apparmor.d/ 中的文本文件，可以使用任何文本编辑器进行维护。 |
| 3. 控制 AppArmor | AppArmor 在启动过程早期启动。<br><br>`/etc/init.d/boot.apparmor` 是用于控制 AppArmor 的脚本。<br><br>`/sbin/rcapparmor` 是到它的链接。<br><br>参数 **stop** 和 **kill** 结束 AppArmor 对进程的限制。**start** 用于激活进程限制——但只有 AppArmor 激活后启动的具有配置文件的进程才会被限制。**reload** 或 **restart** 重新加载配置文件。<br><br>**enforce** 和 **complain** 切换 enforce 和 complain 模式。<br><br>**unconfined** 列出具有绑定套接字但没有配置文件的进程。<br><br>**ps -Z** 列出与相关的安全信息。 |
| 4. 监控 AppArmor | 可以通过 YaST 配置 AppArmor 以创建安全事件报告并发送电子邮件消息以通知安全事件。 |

## 第 8 章 使用 Xen 管理虚拟化

虚拟化目前是业界最热门的话题之一。然而，虚拟化的想法并不新。像 IBM 的 pSeries 或 zSeries 这样的硬件平台长期以来就支持虚拟化，而像 VMware Workstation 这样适用于基于 x86 系统的软件已经存在多年。

现在虚拟化正在走向主流，因为可负担得起的基于 Intel 或 AMD 的 x86 系统提供了足够的资源来同时运行多台虚拟机。

SUSE Linux Enterprise Server 10 是第一个通过 Xen 虚拟机监视器提供内置虚拟化支持的企业级 Linux 产品。在接下来的部分中，您将学习如何使用这一强大功能。

### 目标

-   1. 理解虚拟化概念
-   2. 理解 Xen 的工作原理
-   3. 安装 Xen
-   4. 使用 YaST 管理 Xen 域
-   5. 在命令行管理 Xen 域
-   6. 理解 Xen 网络
-   7. 迁移来宾域

*严禁复制本手册的全部或部分，或分发此类副本。如怀疑有复制行为，请致电 1-800-PIRATES。*

