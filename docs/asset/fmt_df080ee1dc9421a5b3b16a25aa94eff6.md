
# 步骤 4. 你还需要防止它在系统启动时启动：

```bash
# chconfig sendmail off
```

# 步骤 5. 验证：

```bash
# chconfig sendmail --list

sendmail      0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

# 步骤 6. 将默认邮件程序更改为 Postfix：

```bash
# alternatives --config mta
```

有 2 个提供 'mta' 的程序：

| 选择 | 命令 |
|---|---|
| *+ 1 | /usr/sbin/sendmail.sendmail |
| 2 | /usr/sbin/sendmail.postfix |

按回车保留当前选择，或输入选择数字：2

# 步骤 7. 验证当前邮件默认设置是否为 Postfix：

```bash
# alternatives --display mta | grep current
```

link currently points to `/usr/sbin/sendmail.postfix`

# 配置 Postfix

Postfix 实际上启动了一个名为 `master` 的服务，它是它的主服务。该 `master` 服务本身会启动另外三个服务：`nmgr`、`pickup` 和 `smtpd`。`nmgr` 服务负责邮件的传输、中继和投递。`pickup` 服务负责传输消息，而 `smtpd` 服务负责处理入站邮件。在处理 Postfix 时有许多需要了解的内容，让我们来看一下吧。

以下是 Postfix 的管理命令：

- `mailq` 允许你查看邮件队列（* 号表示活跃，'!' 表示挂起*）
- `postmap` Postfix 查找表管理
- `postsuper` 允许你对 Postfix 队列执行维护作业
- `postconf` Postfix 配置工具

Postfix 的主配置文件位于 `/etc/postfix` 目录：

- `master.cf` 包含控制 `master` 服务的设置
- `main.cf` 打开 Postfix 的主配置文件
- `access` 提供访问控制
- `transport` 将电子邮件地址映射到中继主机

`master.cf` 文件被分为八列：

- `service` 标识服务的名称
- `type` 命名所使用的传输机制
- `private` 仅供 Postfix 使用的服务
- `unpriv` 命名由非 root 用户运行的服务
- `chroot` 指明邮件队列是否在 chroot 环境中运行
- `wakeup` 指定服务的唤醒间隔
- `maxproc` 指明服务可以执行的最大进程数
- `command` 命名要执行的命令加参数

在 `master.cf` 文件中，列按以下顺序排列：

`<service> <type> <private> <unpriv> <chroot> <wakeup> <maxproc> <cmd>`

# 考试提示

> `/etc/postfix/main.cf` 文件不允许 Postfix 接受来自本地系统以外的任何主机的网络连接。

在更改配置文件中的任何选项之前，请确保 Postfix 服务没有运行。现在我们来看 Postfix 的默认选项：

```bash
# head -n 35 /etc/postfix/master.cf
#
# Postfix master 进程配置文件。有关文件格式
# 的详情，请参见 master(5) 手册页（命令: "man 5 master"）
#
#=================================================================
# service type private unpriv chroot maxproc command + args
#               (yes)      (yes) (never) (100)
# ==================================================================
smtp     inet n       n                 smtpd
```

# 第 20 章：邮件服务

| pickup | fifo | n | | n | 60 | 1 | pickup |
| cleanup | unix | n | | n | 0 | | cleanup |
| qmgr | fifo | n | | n | 300 | 1 | qmgr |

你可以对想要编辑的子服务进行调整，但为了本示例，目前请保持默认值。

接下来，让我们来看主配置文件，在使用 Postfix 之前需要对其进行编辑。由于配置文件有 667 行，因此没有显示整个文件。相反，我们查看关键部分。为了让 Postfix 服务器正常工作，需要设置以下变量：

- `myhostname` 定义 Postfix 服务器的完整主机名
- `mydomain` 定义域名
- `myorigin` 定义发出邮件的源名称
- `inet_interfaces` 识别接收邮件的接口
- `mydestination` 定义 Postfix 接受邮件的域名
- `mynetworks` 列出受信任的网络
- `virtual_alias_maps` 定义入站邮件的虚拟别名

你可以按照以下步骤操作：

- **步骤 1.** 使用任何文本编辑器打开 `master.cf` 文件并设置前面的变量：`# nano /etc/postfix/master.cf`

- **步骤 2.** 更改以下选项以反映实验室环境：
`myhostname = rhel01.example.com`
`mydomain = example.com`
`myorigin = $mydomain`
`inet_interfaces = all`
`ydestination = $hostname, localhost.$mydomain, localhost`
`mynetworks = 172.168.1.0/24, 127.0.0.0/8`
当你对设置有信心时，继续。

# Red Hat® 考试450 实战指南：RHCSA® 和 RHCE® 认证指南与实验手册

第 1 ：查询你需要更改的布尔值：

```bash
# getseboolean -a | grep postfix_disable_trans

postfix_disable_trans -> off
```

第 2 ：禁用 SELinux 保护：

```bash
# setseboolean -P postfix_disable_trans=1
```

第 3 步：验证布尔值已更改：

```bash
# getseboolean -a | grep postfix_disable_trans

postfix_disable_trans -> on
```

## Postfix 安全

由于邮件服务器无处不在，了解如何锁定其特定功能至关重要。对于像 Postfix 这样处理 SMTP 协议的传发邮件服务器，你应该确保它不会处于开放状态被用作邮件中继。这将允许外部人员免费使用你的服务器。要实现这一点，你可以打开 `/etc/postfix/access` 文件，并允许任何想要通过你的发送邮件服务器进行中继的服务器的主名或 IP 地址。

如果你想让 RHEL02 中继邮件，但不是这些客户端系统，可以执行以下操作：

```bash
# nano /etc/postfix/access
172.168.1.2                               RELAY

172.168.1.10                           REJECT

Client                               REJECT
```

为了额外的安全性，你可以在 `/etc/postfix/main.cf` 中使用以下选项：

```conf
smtpd_helo_required = yes

smtpd_recipient_limit = 500

smtpd_recipient_restrictions = mynetworks

smtpd_sender_restrictions = reject
```

这些设置限制了网络内部访问邮件服务器，同时也限制了单封邮件的收件人数量。除了锁定邮件服务器外，你还可以通过另一个 SMTP 服务器中继邮件。在 `/etc/postfix/main.cf` 文件中，定义你想要中继的 `relayhost`：

```bash
# nano /etc/postfix/main.cf

relayhost = mail.example-com
```

现在它通过指定的主机中继你的邮件。如果你在这里添加一些安全性，可以配置中继使用 SASL 以实现安全连接。再次编辑 `/etc/postfix/main.cf` 文件：

```conf
# nano /etc/postfix/main.cf

relayhost = mail.example.com
```
