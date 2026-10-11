
# 系统配置选项

| `IRCSERVER` | open | 允许您在此处添加喜欢的 irc 服务器地址 |

| `KBD_CAPSLOCK` | yes/no | 询问键盘大写锁定（CapsLock）状态 |

| `KBD_NUMLOCK` | yes/no | 询问键盘数字锁定（NumLock）状态 |

| `KBD_RATE` | open | 提供重复速率；此选项生效时必须输入延迟时间（ms） |

| `KDB_TTY` | open | 指定可以使用 NumLock 和 CapsLock 的 tty（tty1 tty2 或针对所有 tty） |

| `KDM_GREETSTRING` | open | 用于在显示管理器屏幕上显示计算机的主机名 |

| `KDM_SHUTDOWN` | root, all, none, none | 在 KDM 界面上显示可以关闭系统的用户 |

| `KDM_USERS` | open | 修改 KDM 主界面上的用户列表 |

| `KEYTABLE` | <table type> | 允许您指定键盘表类型（如 us.map.gz） |

### 表 10.1 继续

| 系统功能 | 选项 | 注释 |

| --- | --- | --- |

| `LANGUAGE` | open | 允许您指定本地语言。 |

| `MAIL_LEVEL` | warn/all | warn 提供重要消息；all 提供所有邮件和日志。 |

| `MAIL_REPORTS_TO` | open | 将配置更改邮件给 root 或任何指定的用户。 |

| `MAX_DAYS_FOR_LOG_FILES` | open | 告诉日志文件的存储时长。 |

| `MAX_RPMDB_BACKUPS` | open | 指定 rpm 数据库备份文件的最大数量。 |

| `MODEM` | open | 指明用作调制调器的设备 (<TySx>)。 |

| `MOUSE` | open | 指明哪个设备是鼠标 (<TySz>)。 |

| `NAMESERVER` | open | 提供您的 DNS 服务器的 IP 地址。 |

| `NETCONFIG` | open | 指定用网络接口的设备（NIC）。 |

| `NETDEV_0` | automatic | 指明第一个网络设备 eth0。 |

| `NETDEV_1` | automatic | 指明第二个网络设备 eth1。 |

| `NFS_SERVER` | yes/no | 启动 NFS 服务器。 |

| `NNTPERVER` | yes/no | 提供新闻服务器的地址。 |

| `PASSWD_USE_CRACKLIB` | yes/no | 允许您使用 cracklib 检查新密码。 |

| `PATH` | <PATH> |此 PATH 为 SuSEconffig 和 cron 设置。请勿更改此设置。 |

| `PCMCIA` | i82365 or tcic | 指明使用的 PCMCIA 芯片组。 |

| 系统功能 | 选项 | 注释 |

|---|---|---|

| `PCMCIA_CORE_OPTS` | open | 参考 man 页面，选项查看 #man pcmcia-core。 |

| `PCMCIA_PCIC_OPTS` | open | 决定插槽驱动程序定时；详情见 #man 1823S 或 #man。 |

| `PERMISSION_SECURITY` | easy, secure, paranoid | 设置全局文件权限系统。 |

| `POSTFIX_CREATECF` | yes/no | 决定是否由系统创建 Postfix 配置文件。 |

| `POSTFIX_LOCALDOMAINS` | open | 提供 localhost 和系统域名。 |

| `POSTFIX_MAILDROP_MODE` | nosgid/sgid | 是受保护的邮件投递目录还是可写。 |

| `POSTFIX_RELAY` | open | 指明中继（relay）。 |

| `ROOT_LOGIN` | yes/no | 决定 root 是否允许登录。 |

| `SEARCHLIST` | open | 列出域名。 |

| `SMTP` | yes/no | 创建邮件服务器。 |

| `SORT_PASSWD` | yes/no | 对用户排序。 |

| `TIMEZONE` | open | 修改 `/usr/zoneinfo/local-time`。 |

| `USB_DRIVERS` | usb-keyboard,mouse | 启用 USB 设备。 |

| `USE_NIS_FOR_AUTOFS` | yes/no | 使用 NIS 进行 autofofs。 |

| `XNTPD_INITIAL_DATE` | open | 列出服务器地址。 |

## 使用 YaST 配置系统

## 配置互联网服务

在配置互联网服务时，问题在于要在机器上运行哪些服务和功能。例如，您的独立机器每天连接时间很短，没有理由使用调制调器以外配置浏览器以外。有些人可能考虑过构建家庭网络，如果是这样，您需要多台机器连接到同一个连接。让我们从处理浏览器配置开始。

### Web 浏览器配置

自从 Linux 在互联网剧图中占据中心地位以来已经过了很多时间。互联网使用的增加需要比 Linux 创建时更先进的技术。SuSE Linux 提供了两种 Web 浏览器选择：Lynx 和 Netscape Communicator。让我们来看看它们的特征。

## 第 10 章：管理网络设置

### Lynx 浏览器

通常，大多数 Linux 发行版在软件包中都包含了几个 浏览器。SuSE 也不例外；资深 Linux 用户喜欢的浏览器之一就是 Lynx。这是一个基于文本的浏览器，可能会吸引硬核 Linux 用户。该浏览器的速度惊人，因为它不需要解析图形。尽管它是一个文本类型的浏览器，但它具有其他 浏览器不具备的配置功能。列表显示了 Lynx 的某些选项。

通过按 `O` 键可以访问 Lynx 选项。

- `E`—显示选定的编辑器
- `D`—显示显示变量
- `B`—访问书签文件
- `F`—指定 ftp 排序标准
- `P`—输入个人邮箱地址
- `S`—选择类型
- `C`—选择字符集
- `V`—显示 vi 键
- `*e`—显示 emacs 键
- `K`—使用数字键盘作为方向键
- `U`—访问用户模式
- `L`—显示执行链接

在命令行输入 `Lynx` 时，可以访问 Lynx 帮助屏幕。图 10.2 显示了 Lynx 帮助页面。

![](img/e140cb30051378468280d532cc3eccef_128_0.png)

`图 10.2` 从 Lynx 获取帮助。

配置完成后，Lynx 证明是一个强大的 Web 浏览器应用程序。对于任何关注文本应用和在线阅读文档的人来说，Lynx 都是理想的浏览器。Lynx 支持一些最新的 HTML 技术（图形除外），在使用网页提供的链接时不会遇到困难。如果你的机器较旧，或者内存小于 24–32MB，这个浏览器会让生活变得可以忍受。HTML 页面的加载时间会缩短，因为 Lynx 只查看文本。

堪萨斯大学是获取有关新发布版本和用户信息的最佳来源。你们的网站位于 http://cc.ukans.edu/lynx_help/Lynx_users_guide.html 了。Lynx 的当前版本为 2.8.2。

另一个网站可能对熟悉 Lynx 有帮助。该网站提供了关于 Lynx 快速配置的额外见解：http://reality.sgi.com/raju/lynx.txt。

### Netscape 浏览器

Netscape Web 浏览器因其可携性和成本（为零）而成为 Lynx 爆发增长的一部分。Netscape 与此发行版中包含的其他软件完美融合。

Netscape 是一个完全可配置的浏览器，内置了支持 POP、IMAP 和 Movemail 协议的邮件程序。你可以设置 Netscape 以便从新闻组接收帖子。你还可以使用其他几个功能来增强你的日常上网任务。

如果你启动 Netscape 时它似乎长时间卡住并给你显示图 10.3 所示的错误，你可能存在网络连接问题。

![](img/e140cb30051378468280d532cc3eccef_129_0.png)

图 10.3 识别 Netscape 错误。

在前面的图中，你看到注释“警告，以下主机未知”。这表明你可能漏掉了 `resolv.conf` (DNS 域名服务器) 的条目。另一方面，你可能没有物理连接到网络或互联网。检查你的所有连接，然后查看 `/etc/resolv.conf` 文件（使用系统配置工具中的 `NAMESERVER`）。如果 `/etc/resolv.conf` 文件中没有列出 IP 地址，添加域名服务器 IP 地址应该可以解决你的问题。

此版本包含的 Netscape 浏览器可以像之前的版本一样进行配置。工具栏选择（位于浏览器区域顶部）执行功能。虽然这是一个较新的版本，但你不应该在操作上遇到困难。

Netscape 的巧妙功能之一是新闻组功能。目前订阅邮件列表的人会发现，设置新闻组是一项简单的任务。为了方便起见，Netscape Communicator 集成了一个新闻组客户端。图 10.4 显示了新闻组的设置。
