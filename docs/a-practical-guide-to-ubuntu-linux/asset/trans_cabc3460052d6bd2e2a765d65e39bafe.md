

## 732 第 20 章 exim4：设置邮件服务器、客户端及其他

### 安装
安装以下软件包：

- squirrelmail
- apache2 (第 902 页；在安装 squirrelmail 时会作为依赖项安装)
- exim4 (第 714 页) 或 sendmail
- php5-cgi
- dovecot-imapad (第 735 页) 或另一个 IMAP 服务器

### 启动
你不需要启动 SquirrelMail，也不需要为它开放任何端口。然而，你需要为 exim4 (第 718 页)、IMAP (第 735 页) 和 Apache (第 903 页) 进行配置、启动并开放端口（如果服务器运行在带有防火墙的系统上）。

### 配置
SquirrelMail 文件位于 `/usr/share/squirrelmail`。创建以下链接以以便通过 Web 访问 SquirrelMail：

```
$ sudo ln -s /usr/share/squirrelmail /var/www/mail
```

执行以下命令来配置 SquirrelMail：

```
$ sudo squirrelmail-configure
SquirrelMail Configuration : Read: config.php (1.4.0)
```

```
+ 主菜单 =
1. 组织偏好
2. 服务器设置
3. 文件夹默认值
4. 普通选项
5. 主题
6. 通讯录
7. 日期消息 (MOTD)
8. 插件
9. 数据库
10. 语言

- D 为特定的 IMAP 服务器设置预定义设置
- D 开启颜色
- S 保存数据
- Q 退出
```

此菜单有多个层次。当你选择一个设置（而不是子菜单）时，`squirrelmail-configure` 会显示有助于帮助决定如何回答其问题的信息。设置服务器的域名（“服务器设置”页面上的第 1 项）以及你正在使用的 IMAP 服务器名称（主菜单上的 D）。SquirrelMail 提供了几个主题；如果你不喜欢 SquirrelMail 的外观，可以从“主题”（第 5 项）中选择另一个主题。完成更改后，退出 `squirrelmail-configure`。每当你想要更改 SquirrelMail 的配置时，运行 `squirrelmail-configure`。

SquirrelMail 提供了一个 Web 页面来测试其配置。将服务器上的浏览器指向 `localhost/src/configtest.php`。将 `localhost` 替换为 IP 地址或

![](img/45ff4cd21497435daa35084a84b95d07_782_0.png)

## 额外的邮件工具 733

![](img/45ff4cd21497435daa35084a84b95d07_783_0.png)

# 图 20-2 正在运行配置测试的 SquirrelMail

从另一个系统查看页面服务器 FQDN。SquirrelMail 会检查其配置并在页面显示结果。图 20-2 显示 SquirrelMail 无法连接到本地系统的 IMAP 服务器，可能是因为尚未安装 IMAP。

在 `localhost/` 或 `localhost/mail/src/login.php` 浏览器中显示 SquirrelMail 登录页面（图 20-3）。将 `localhost` 替换为在服务器系统中拥有账户的用户 IP 地址或密码。

## 邮件列表

如果你定期向同一大群人员发送电子邮件，邮件列表将是一项资产。与在邮件的“收件人”或“抄送”字段中列出大量收件者或向多人发送相同的电子邮件相比，它具有几个优势：

- 匿名性——邮件的任何收件者都看不到其他收件者的地址。

![](img/45ff4cd21497435daa35084a84b95d07_783_1.png)

# 图 20-3 SquirrelMail 登录页面

## 734 第 20 章 exim4：设置邮件服务器、客户端及其他

- 存档——发送到列表的电子邮件存储在中心位置，列表管理员指定的成员或公众可以在其中进行浏览。
- 访问控制——你可以指定谁可以向列表发送电子邮件。
- 一致性——当你使用“收件人”或“抄送”向一组人发送邮件时，很容易忘记谁想加入列表，错误地包含了想离开列表的人。
- 效率——邮件列表应用程序随时间分发邮件传输，不会导致邮件服务器过载。Mailman 列表用 Python 编写，管理邮件讨论和邮件列表。由于它与 Web 集成，使得用户管理账户和管理员管理列表变得非常方便。更多信息请参见 Mailman 页面和 `/usr/share/doc/mailman` 目录下的文件。

### 前提条件
安装邮件包和 MTA，如 exim4 (第 715 页)。要使用 Web 接口，必须安装 Apache (第 902 页)。

### 安装
当你安装 mailman 包时，`dpkg postinst` 脚本会描述一个图形界面，要求你指定 Mailman 显示的语言并告诉你必须创建一个列表。执行以下请求：

```
$ sudo newlist
输入运行列表的电子邮件：helen@example.com
初始列表密码：
```



要完成创建邮件列表，你必须通过添加以下行来编辑 `/etc/aliases`（或等效）文件并运行 `newaliases`：

```
## list
list: "/var/lib/mailman/mailman"
admin: "/var/lib/mailman/mailman admin"
bounces: "/var/lib/mailman/mailman bounces"
confirm: "/var/lib/mailman/mailman confirm"
join: "/var/lib/mailman/mailman join"
leave: "/var/lib/mailman/mailman leave"
owner: "/var/lib/mailman/mailman owner"
request: "/var/lib/mailman/mailman request"
subscribe: "/var/lib/mailman/mailman subscribe"
unsubscribe: "/var/lib/mailman/mailman unsubscribe"
```

按回车键通知所有者...

在列表上的用户接收电子邮件之前，你需要将 `newlist`（以你的邮件列表名称开头的）复制到 `/etc/aliases` (第 722 页) 的末尾并运行 `newaliases`。

### 站点列表
在启动 Mailman 之前，你必须创建一个名为 mailman 的站点列表。执行命令 `sudo newlist mailman`，将行复制到 aliases 文件并运行 newaliases。

## 额外的邮件工具 735

### mailman init 脚本
设置好 mailman 站点列表和你选择的列表后，使用以下命令启动 Mailman 守护进程：

```
$ sudo service mailman start
* Starting Mailman master mailmanctl [ OK ]
```

在修改任何 Mailman 配置文件或添加新的站点列表后，使用相同的命令将 `start` 替换为 `reload`，让 Mailman 重新读取其配置文件。
Mailman 的主配置文件是 `/etc/mailman/mm_cfg.py`。当你安装 Mailman 时，它会自动为 `DEFAULT_EMAIL_HOST`（邮件列表默认域名）和 `DEFAULT_URL_HOST`（邮件默认 Web 服务器）赋值。更改这些变量的值并重启 Mailman。

```
$ cat /etc/mailman/mm_cfg.py
...
# 新创建邮件地址默认域名
DEFAULT_EMAIL_HOST = 'example.com'

# 新创建 Web 接口默认主机
DEFAULT_URL_HOST = 'example.com'
```

假设 Web 接口位于 example.com，任何人都可以将浏览器指向 example.com/cgi-bin/mailman/listinfo 显示邮件列表。点击邮件列表将显示允许你查看列表存档、发送或订阅列表的页面。页面底部是该列表管理界面的链接。

## 设置 IMAP 或 POP3 邮件服务器

Dovecot IMAP（互联网消息访问协议）和 POP（邮局协议）允许用户远程检索和处理电子邮件。本说明介绍了如何为这些协议设置服务器。Dovecot (dovecot.org 和 wiki.dovecot.org) 实现了这些协议的 imap-login 和 pop3-login 守护进程。

### 前提条件
安装 dovecot-pop3（用于 POP3 服务器）和/或 dovecot-imap（用于 IMAP 服务器）软件包。安装其中一个包时，APT 会自动安装 dovecot-common 包。当你安装任何一个包时，dovecot-common 包的 `dpkg postinst` 脚本会在证书不存在时生成自签名 SSL 证书。

### 配置
在你在 `/etc/dovecot/dovecot.conf` 文件中指定要运行的服务器之前，Dovecot 将不会启动。在这个长文件的开头有一个以 `protocols =` 开头的行。在这一行的末尾写你想要运行的服务器名称。根据你安装的软件包，可能的服务器有：imap（端口 143 上的 IMAP）、imaps（端口 993 上的 SSL IMAP）、pop3（端口 110 上的 POP3）和 pop3s（端口 995 上的 SSL POP3）。

