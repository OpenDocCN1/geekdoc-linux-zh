
这将在每次加载 `cdrom` 内核模块时都启用该参数。

## 升级 Linux 内核

你经常需要升级 Linux 内核。当你升级 Linux 内核时，会安装一个新版本的内核并将其设置为默认内核。不过，旧版本的内核文件仍然可用。这确保了如果新内核包含了某些你的硬件不支持的功能，你的计算机仍然可以启动。要安装新版本的内核，你可以使用 `yum upgrade kernel`。`yum install kernel` 命令同样有效。这两个命令都会在旧内核旁边安装新内核。

你在服务器上安装的最后四个内核的内核文件将保留在 `/boot` 目录中。`GRUB 2` 引导程序会自动识别此目录中找到的所有内核。

## 总结

在本章中，你学习了如何使用 Linux 内核。你了解到 Linux 内核是模块化的，并且与内核模块一起是非常重要的。你还学习了如何管理内核模块，以及在处理新硬件时内核模块是如何自动管理的。

## 考试准备任务

回顾所有关键主题

回顾章节中最重要的主题，这些主题在页面外边缘用“关键主题”（Key Topic）图标标记。表 16.3 列出了这些关键主题的参考及其所在的页码。

| 关键主题元素 | 描述 | 页码 |
| --- | --- | --- |
| 列表 | 内核相关工具概述 | 374 |
| 表 16.2 | 内核模块管理概述 | 379 |

## 定义关键术语

定义本章中的以下关键术语并在词表中检查你的答案：

`kernel`（内核）, `module`（模块）, `dmesg`, `udev`, `sysfs`, `proc`, `tainted kernel`（受污染内核）

## 复习题

+ 1. 哪个命令显示你计算机当前使用的内核版本？
2. 在哪里可以找到 RHEL 7 安装的当前版本信息？
3. 哪个命令显示当前已加载的内核模块列表？
4. 哪个命令允许你发现内核模块参数？
5. 如何卸载内核模块？
6. 如果在尝试卸载内核模块时收到错误消息，你可以做什么？
7. 如何找到支持哪些内核模块参数？
8. 在何处指定应该持久使用的内核模块参数？
9. 假设 `cdrom` 模块有一个参数“debug”，且该参数必须设置为 1 才能启用调试模式，你会在自动加载该模块的文件中包含哪一行？
10. 你如何安装新版本的内核？

## 章节末实验

在章节末实验中，你将安装新版本的内核并与内核模块一起工作。

## 实验 16.1

+ 1. 检查是否有可用的新版本内核。如果有，安装它并重启计算机以使用。
2. 使用适当的命令显示内核记录的最近事件。
3. 找到你的网卡所使用的内核模块。找出它是否有选项（options）。尝试手动加载这些内核模块选项之一；如果加载成功，则采取必要措施持久地加载此选项。

本页特意留白

本章涵盖了以下主题：

+ - 配置基础 Apache 服务器
- 理解 Apache 配置文件
- 创建 Apache 虚拟主机

本章涵盖了以下 RHCSA 考试目标：

+ - 没有 RHCSA 考试目标与 Apache 直接相关

## 配置基础 Apache 服务器

这是书中唯一一个讨论了甚至未在 RHCSA 目标中列出的主题的章节。然而，对于红帽服务器管理员来说，如何处理 Apache Web 服务器是非常重要的。在随后的章节中，你将学习如何配置 SELinux 和安装服务器。这些主题在不知道如何处理 Apache Web 的情况下是很难理解的。在第 18 章“管理和理解引导过程”中，你将学习如何在 RHEL 7 环境中使用服务。了解如何配置像 Apache Web 服务这样的通用服务对这样做非常有帮助。这就是为什么本章解释了 Apache Web 服务的基础。有关 Apache Web 服务的更深入的信息，你可以阅读第 33 章“管理高级 Apache 服务”。

## 我已经掌握了吗？测验

“我已经掌握了吗？”测验可以让你评估应该从彻读本章，还是跳到“考试准备任务”部分。如果你对这些问题的答案或你对主题知识的自我评估有疑问，请阅读整个章节。表 17.1 列出了本章的主要标题及其对应的“我已经掌握了吗？”问题。你可以在附录 A“‘我已经掌握了吗？’测验和复习题的答案”中找到答案。

表 17.1 “我已经掌握了吗？”章节与问题映射
| 基础主题 | 问题 |
| --- | --- |
| 配置基础 Apache 服务器 | 1–4 |
| 理解 Apache 配置文件 | 5–7 |
| 创建 Apache 虚拟主机 | 8–10 |

+ 1. 哪个命令安装软件？
- a. `yum install`
- b. `yum install`
- c. `yum install`
- d. `yum install`
+ 2. 配置文件的名称是什么？
- a. `/etc/httpd/conf`
- b. `/etc/httpd/conf`
- c. `/etc/httpd/conf`
- d. `/etc/httpd/conf`
+ 3. 配置文件中的哪个参数定义了位置？
- a. `ServerRoot`
- b. `ServerDocuments`
- c. `DocumentRoot`
- d. `DocumentIndex`
+ 4. 配置文件中的哪个参数指定了查找位置？
- a. `ServerRoot`
- b. `ServerDocuments`
- c. `DocumentRoot`
- d. `DocumentIndex`
+ 5. 哪个目录包含配置文件？
- a. `/etc/httpd`
- b. `/etc/httpd/conf`
- c. `/etc/httpd/conf`
- d. `/etc/httpd/conf`
+ 6. 哪个目录包含配置模块？
- a. `/etc/httpd`
- b. `/etc/httpd/conf`
- c. `/etc/httpd/conf`
- d. `/etc/httpd/conf`
+ 7. 哪个目录用于放置配置？
- a. `/etc/httpd`
- b. `/etc/httpd/conf`
- c. `/etc/httpd/conf`
- d. `/etc/httpd/conf`
+ 8. 哪种类型允许多个虚拟主机？
- a. `NameBased`
- b. `IPBased`
- c. `ConfigurationBased`
- d. `Default`
+ 9. 哪一行用于启动虚拟主机？
- a. `<VirtualHost *:80>`
- b. `<VirtualHost *>`
- c. `<NameHost *:80>`
- d. `<NameHost *>`
+ 10. 关于虚拟主机的陈述中哪个是不正确的？
- a. 当通过 `httpd` 提供虚拟主机时，默认配置不再生效。
- b. 虚拟主机的名称必须通过 `/etc/hosts` 解析。
- c. 要使用虚拟主机，必须安装 `mod_virt` 包。
- d. 虚拟主机配置可以在 `httpd` 中指定。

to. 使用额外的配置文件使得应用程序可以通过 RPM 包轻松安装由 Apache 服务器包含的文件。这些配置文件的名称均相对于相对于 `ServerRoot` `/etc/httpd`。列表 17.1 显示了 `httpd` 配置文件的部分内容。

### 列表 17.1 `/etc/httpd/conf/httpd.conf` 配置文件的部分内容

```
[root@server1 ~]# cat /etc/httpd/conf/httpd.conf | grep -v '#*'

ServerRoot "/etc/httpd"

Listen 80

Include conf.modules.d/*.conf

User apache

Group apache

ServerAdmin root@localhost

<Directory />

AllowOverride none

Require all denied

</Directory>

DocumentRoot "/web"

<Directory "/var/www">

AllowOverride None

Require all granted

</Directory>

<Directory "/web">

Options Indexes FollowSymLinks

AllowOverride None

Require all granted

</Directory>

<IfModule dir_module>

  DirectoryIndex index.html

</IfModule>
```

```
<Files ".ht*>

Require all denied combined

</Files>

ErrorLog "logs/error_log"

LogLevel warn

<IfModule log_config_module>

  LogFormat %h %l %u \%r\" >%s \%{Referer\i} \%{User-Agent\i}\" combined

  LogFormat %h %l %u \%r\" >%s "%b" common

  <IfModule module_module>

    LogFormat %h %l %u \%r\" >%s \%{Referer\i} \%{User-Agent\i}\" %I%nio
```
