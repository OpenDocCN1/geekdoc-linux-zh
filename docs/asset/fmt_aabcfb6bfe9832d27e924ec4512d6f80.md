
```
myhostname = rhel03.getitcertify.com
mydomain = getitcertify.com
myorigin = $getitcertify.com
inet_interfaces = all
mydestination = rhel03, db03, localhost.getitcertify.com, $getitcertify.com, localhost
mynetworks = 192.168.0.0/24, 127.0.0.0/8
```

### 3. 编辑 `/etc/postfix/access` 文件，并将远程系统、域名或网络的主机或 IP 地址添加，允许或拒绝它们通过此 Postfix 服务器中继邮件：

`192.168.2 RELAY`

`192.168.3 RELAY`

`getitcertify.com RELAY`

`192.168.4 REJECT`

### 4. 执行以下命令以使 Postfix 在每次系统重启时自动启动：

```
# chconfig postfix on
```

### 5. 确保您的 DNS 或 `/etc/hosts` 文件配置正确。

### 6. 允许端口 25 的流量通过防火墙，或者如果不使用防火墙直接将其禁用。参考第 30 章“系统和网络安全”了解如何执行这些任务。

### 7. 启动（或重启）Postfix 守护进程：

```
# service postfix start
Starting postfix:             [ OK ]
```

### 8. 执行以下命令检查 Postfix 的运行状态：

```
# service postfix status
master (pid 1901) is running...
```

所有消息都记录在 `/var/log/maillog` 文件中。对该文件执行 `tail` 操作会产生类似下面的输出：

```
# tail /var/log/maillog
Mar 5 11:20:14 rhel03 postfix/postfix-script: starting the Postfix mail system
Mar 5 11:20:14 rhel03 postfix/master[1901]: daemon started – version 2.2.10, configuration /etc/postfix
```

## 设置默认 MTA

如果系统中同时配置了 `sendmail` 和 `Postfix`，您应该能够使用 `alternatives` 或 `system-switch-mail` 命令激活其中一个作为外发邮件的默认邮件服务器。

以下是使用 `alternatives` 方法。

要列出当前配置为默认的 MTA，请使用命令 `--display` 选项：

```
# alternatives --display mta| current
link currently points to /usr/sbin/sendmail.sendmail
```

您也可以使用 `--config` 选项来显示或更改默认 MTA：

```
# alternatives --config mta
```

有 2 个提供 'mta' 的程序。

| 选择 | 命令 |
| --- | --- |
| * 1 | /usr/sbin/sendmail.sendmail |
| + 2 | /usr/sbin/sendmail.postfix |

按回车保留当前选择，或输入选择数字：

第一个选择旁边的星号字符表示该邮件服务器当前为默认值。如果您想更改设置，只需按回车或输入对应另一个选择的数字并按回车，将该邮件服务器设置为默认值。该选择将更新所有配置为在重启时自动启动该邮件服务器的运行级别。此外，如果选择了替代方案，`alternatives` 命令会停止当前的邮件服务器并启动另一个。使用 `alternatives` 命令检查设置（现在不要做任何更改；只需按回车），或使用 `chkconfig` 命令检查设置为自动启动的运行级别，并使用 `service` 命令检查运行状态：

```
+ # chkconfig --list sendmail
sendmail 0:off 1:off 2:on 3:on 4:on 5:on 6:off
# service sendmail status
sendmail (pid 2393 23833) is running...
```

您还可以按照以下方式使用 `alternatives` 命令设置默认 MTA。以下显示了如何将默认值更改为 Postfix：

```
# alternatives --set mta /usr/sbin/sendmail.postfix
```

或者，可以使用 `system-switch-mail` 工具实现此目的。图 24-2 显示了它的图形界面。

![](img/3f35ec29a294974bc1a4fdae3ae46652_550_0.png)

**图 24-2 邮件服务器选择**

进行适当选择并取消其他选项，点击 OK。您需要使用第 11 章“软件包管理”中解释的包安装方法之一安装 `system-switch-mail` 包，因为它默认没有安装。

## 验证邮件服务器功能

您可以通过发送测试邮件来验证邮件服务器是否配置正确。以下提供了针对 `sendmail` 和 `Postfix` 的常用测试程序。

要测试本地邮件功能，向本地用户（如 `user1`）发送一封主题为“Local Mail Test”的邮件：

```
# date | mail -s "Local Mail Test" user1
```

要测试网络邮件功能，向远程用户（如 `rhel01` 上的 `user2`）发送邮件：

```
# date | mail -s "Remote Mail Test" user2@getitcertify.com
$ mail
```

Mail version 8.1 6/6/93. 输入 ? 获取帮助。

"/var/spool/mail/user2": 1 message 1 new

>N 1 user2@getitcertify.com Wed Mar 5 11:44 18/8/35 "Remote Mail Test"

&

可以使用 `mail` 命令向另一个用户（如 `asghori`）发送普通邮件：

```
$ cal | mail -s "Test Mail from user1" asghori
```

向本地系统的用户 `aghori` 以及远程系统 `rhel01` 上的用户 `aghori` 发送文件 `/etc/group` 的内容：

```
$ cat /etc/group | mail -s "Contents of group" aghori@localhost
$ cat /etc/group | mail -s "Contents of group" aghori@rhel01
```

发送的邮件临时存储在队列目录 `/var/spool/queue` 中。您可以使用 `mailq` 命令配合 `-v` 参数查看：

```
# mailq -v
```

在目标端，邮件由邮件服务器接收。`user1` 可以使用 `mail` 命令读取邮件并回复发送者、删除邮件或将其转发给其他接收者。如果没有删除，邮件将自动保存在 `sendmail` 的 `/var/spool/mail` 文件中或 `Postfix` 的 `/var/spool/postfix` 文件中。

```
$ mail
```

Mail version 8.1 6/6/93. 输入 ? 获取帮助。

"/var/spool/mail/user1": 1 message 1 unread

>U 1 root@getitcertify.com Wed Mar 5 11:35 "Local Mail Test"

&

对 `/var/spool/mail/user1` 文件执行 `cat` 会产生如下：
