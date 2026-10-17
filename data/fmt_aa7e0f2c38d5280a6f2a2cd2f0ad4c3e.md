
```
[root@hnl]# tail -f /var/log/secure
Mar 13 18:33:20 hnl runuser: pam_unix(runuser:session): opened for user pid by (uid=0)
Mar 13 18:33:20 hnl runuser: pam_unix(runuser:session): closed for user pgid by (uid=0)
Mar 13 18:33:20 hnl runuser: pam_unix(runuser-1:session): opened for user pid by (uid=0)
Mar 13 18:33:21 hnl runuser: pam_unix(runuser-1:session): closed for user pgid by (uid=0)
Mar 13 18:33:28 hnl polkitd(authority-local): Registered Authentication Agent for session /freedesktop/ConsoleKit/Session1 (system name =1.25, [/usr/libexec/polkit-gnome-authentication-agent-1), path object /org/gnome/PolicyKit1/AuthenticationAgent, locale en_US.UTF-8) (disconnected from bus)
Mar 13 14:27:59 hnl gmd-password[28572]: pam_unix(gmd-password:session): opened for user by root (uid=0)
```

# 第 3 章 · 执行日常系统管理任务

Mar 13 15:20:02 sshd[4433]: Accepted password for root from 192.168.1.53 port 55429 ssh2

Mar 13 15:20:02 sshd[4433]: pam_unix(sshd:session): session opened for root (uid=0)

## 设置 logrotate

在非常繁忙的服务器上，你可能会发现日志文件条目的添加速度非常快。这带来了一种风险——你的服务器可能会迅速被日志消息填满，导致普通文件留下的空间很少。解决这个问题有两个方案。首先，`/var/log` 目录应该位于专用分区或逻辑卷上。在第 1 章中，你读过关于如何安装带有多个卷的服务器的内容。如果 `/var/log` 目录位于专用分区或逻辑卷上，即使向日志文件中写入了太多信息，你的服务器文件系统也不会完全填满。

另一个你可以防止服务器被日志文件完全填满的解决方案是使用 `logrotate`。默认情况下，`logrotate` 命令作为 cron 任务每天从 `/etc/cron.daily` 运行一次，它可以帮助你定义一种策略，对增长超过特定年龄或大小的日志文件进行轮转。

`logrotate` 的配置分布在两个不同的位置。主 `logrotate` 文件是 `/etc/logrotate.conf`。在这个文件中，存储了一些通用参数，用以指定如何处理特定文件。

特定服务的 `logrotate` 配置存储在 `/etc/logrotate.d` 目录中。这些脚本通常在你安装服务时就会于那里了，但你可以根据自己的意愿修改它们。`sssd` 服务的 `logrotate` 配置提供了一个很好的示例，如果你想创建自己的 `logrotate` 文件，可以参考它。列表 3.7 显示了其内容

### 列表 3.7: 示例 logrotate 配置文件

```
# # cat /etc/logrotate.d/sssd {
  weekly
  missingok
  notifyempty
  sharedscripts
  rotate 2
  compress
```

## 设置系统日志

```
postrotate
/bin/kill -HUP `cat /var/run/sssd.pid` 2>/dev/null 2>/dev/null || true
endscript
[root@hn1]# 
```

首先，示例文件告诉 `logrotate` 应该轮转哪些文件。在这个示例中，它适用于 `/var/log/sssd` 下所有以 `log` 结尾的文件。该文件中有趣的的参数是 `weekly`、`rotate 2` 和 `compress`。`weekly` 参数告诉 `logrotate` 每周轮转一次文件。接下来 `rotate 2` 告诉 `logrotate` 保留文件的最后两个版本，并删除所有更旧的版本。`compress` 参数告诉 `logrotate` 压缩旧文件，以便它们占用更磁盘空间。练习 3.8 显示了如何配置。

![](img/3a7e027360b64bc83d5cf9a2db902251_126_0.png)

你不需要解压已压缩的日志文件。只需使用 `zcat` 或 `zless` 命令即可立即查看压缩文件的内容。

#### 练习 3.8

#### 配置日志记录

在本次练习中，你将学习如何如何在服务器上配置日志记录。首先，你将设置 `rsyslog`，将所有与认证相关的消息发送到 `/var/log/auth` 文件。接下来，你将设置 `logrotate` 每天对该文件进行轮转，并只保留一个旧版本。

- 1. 打开终端，通过使用 `su -` 打开 root shell 来确保你拥有 root 权限。
- 2. 用编辑器打开 `/etc/rsyslog.conf` 文件，并滚动到 `RULES` 部分。在 `authpriv` 所在的行下方，添加以下行：

`authpriv.* /var/log/auth`

- 3. 关闭日志文件并确保保存更改。现在使用命令 `service rsyslog restart` 以确保 `rsyslog` 使用新配置。
- 4. 使用 `Ctrl+Alt+F4` 键序列登录用户登录。使用哪个用户账户并不重要。
- 5. 使用 `Ctrl+Alt+F1` 回到图形用户界面。在这里，使用 `tail -f /var/log/auth`。这应该显示包含认证消息的新创建文件的内容。使用 `Ctrl+C` 关闭 `tail -f`。

在本章中，你读到了一些最常见的管理任务。你学习了如何管理作业和进程、挂载磁盘设备、设置打印机以及处理日志文件。在下一章中，你将学习如何在你的 Red Hat 企业服务器上管理软件。

# 第 4 章

## 管理软件

本章涵盖的主题：

- 理解 RPM
- 理解元包处理器（Meta Package Handlers）
- 使用 yum 安装软件
- 查询软件
- 从 RPM 包中提取文件

![](img/3a7e027360b64bc83d5cf9a2db902251_128_0.png)

![](img/3a7e027360b64bc83d5cf9a2db902251_129_0.png)

### 理解 RPM

尽管 RPM 是在软件管理方面迈出的一大大步，但仍然有一个必须处理的不便之处——软件依赖性。为了标准化软件，Linux 上的许多程序使用其他包提供的库和其他组件。这意味着要安装包 A，则需要包 B 存在。

**列表 4.1.** 使用 `rpm` 操作时，你将看到依赖消息

```
[root@1 Packages]# rpm -ivh createrpero-0.9.8-4.el16.noarch.rpm
warning: createrpero-0.9.8-4.el16.noarch.rpm: Header V3 RSA/SHA256
signature, key id fd43d1f1: NOKEY
error: Failed dependencies:
  deltarm is needed by createrpero-0.9.8-4.el16.noarch
  python-deltarm is needed by createrpero-0.9.8-4.el16.noarch
[root@1 Packages]#
```

## 理解元包处理器

依赖地狱的解决方案是元包处理器。元包处理器在红帽中被称为 `yum`（Yellowdog Update Manager），配合软件库（repositories），软件库是用户想要安装软件包时查询的安装源。在软件库中，你发行版的所有软件包通常都是可用的。
