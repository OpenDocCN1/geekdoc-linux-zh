
除了这个 Web 界面外，WREQ 还包括一个电子邮件界面，允许你在没有 Web 浏览器的情况下处理问题。此电子邮件界面允许你通过遵循主题行的简单语法来执行 Web 界面大多数功能。例如，如果我们设置 WREQ 并定义了一个列表 *help desk*，通过发送主题行如表 30.1 所示的电子邮件，我们可以打开、更新、评论或解决一个问题。

### 图 30.1

WREQ 问题录入屏幕。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_940_0.png)

### 表 30.1 WREQ 电子邮件接口主题行语法

| 主题行语法 | 结果操作 |
|---|---|
| `[helpdesk open] help me` | 在帮助台列表中创建一个新问题，主题为 help me。 |
| `[helpdesk #5 update]` | 使用消息正文更新帮助台问题 #5 已采取的行动。 |
| `[helpdesk #5 comment]` | 将消息正文作为评论添加到帮助台问题 #5。 |
| `[helpdesk #5 resolve]` | 将消息正文作为操作添加到帮助台问题 #5 并将其解决。 |
| `[helpdesk #6 merge]` | 将消息正文中指定的编号问题与问题 #6 合并。 |

这些并非全部命令；然而，它们说明了如何使用电子邮件创建、更新或关闭 WREQ 问题。

## 反馈机制

下一个需求是定义明确的反馈机制。WREQ 通过在问题状态发生变化时向问题发起者发送自动邮件来实现这一点，例如当支持人员更新问题或对其发表评论时。WREQ 还可以将此类信息发送到任意电子邮件地址，并具有订阅机制，允许用户监视与特定 WREQ 列表相关的所有问题。如果大型正在进行中的项目分配了自己的列表，并且通过该列表跟踪与特定项目相关的所有问题，则此功能最有用。

## 报告功能

报告功能是下一个需求，WREQ 通过其统计选项提供了这些功能。统计选项允许您跟踪创建、关闭和仍开放的问题数量，以及其他有助于确定帮助台有效性的信息。使用 WREQ 系统的这一部分需要您下载并安装 GD perl 模块。该模块是 Red Hat Linux 附带的 GD 图形库的 perl 接口。您可从 http://www.genome.wi.mit.edu/ftp/pub/software/www/GD.html 获取 GD perl 模块。统计信息可以以文本形式显示，可选择将其邮件发送到任何电子邮件地址，或以图形形式显示。

## 设置优先级

设置问题的优先级是下一个所需功能。WREQ 允许您执行此操作，但只允许单一优先级，而非更理想的双重优先级。WREQ 的一个不错功能是，系统管理员可以使用 WREQ 的配置功能定义优先级。此外，您可以为 WREQ 维护的每个列表定义不同的优先级。

## 定义的升级路径

最终期望的功能是定义的升级路径。不幸的是，WREQ 不支持此功能，但由于该软件包附带用 perl 编写的完整源代码，如果系统管理员认为它绝对关键，则可以添加此功能。

## 为 Red Hat 设置基于 WREQ 的帮助台

确定 WREQ 满足大多数所述需求后，以下各节将介绍在 Red Hat Linux 系统上设置基于 WREQ 的帮助台所涉及的步骤，从检索所需的源代码开始。

### 检索 WREQ 代码

WREQ 系统的代码可从杜克大学 Web 服务器 http://www.math.duke.edu/~yu/wreq 获取。如前所述，为了使用 WREQ 的报告功能，您还必须从 http://www.genome.wi.mit.edu/ftp/pub/software/WWW/GD.html 检索 GD perl 接口模块并安装它。

### 安装 WREQ

检索 WREQ 代码并安装 `GD.pm` 后，您可以开始安装 WREQ。此安装的第一步是解包发行版，该发行版包含在名为 `wreq.tar.gz` 的文件中，并修复权限。以下会话记录演示了此步骤。

```
[root@quicksilver /root]# cd /home/httpd/cgi-bin
[root@quicksilver cgi-bin]# tar xvfz /tmp/wreq.tar.gz
wreq/index.html
wreq/req
wreq/req-common
wreq/req-config
wreq/req-convert
wreq/req-create
wreq/req-list
wreq/req-listfaq
wreq/req-login
wreq/req-mail
wreq/req-misc
wreq/req-newreq
wreq/req-null
wreq/req-search
wreq/req-show
wreq/req-showfaq
wreq/req-socket
wreq/req-status
wreq/req-time
wreq/req-tty
wreq/req-update
wreq/wreq
wreq/data/
[root@quicksilver cgi-bin]# chown -R root.root wreq
[root@quicksilver cgi-bin]# cd wreq
[root@quicksilver wreq]# ls
data    req.config  req-listfaq  req-newreq  req-showfaq  req-tty
index.html  req-convert  req-login  req-null  req-socket  req-update
```

```
req      req-create  req-mail  req-search  req-status  wreq
req-common  req-list  req-misc  req-show  req-time
[root@quicksilver wreq]# chown nobody.nobody data
```

将 `data` 目录设置为所有者 nobody 且组为 nobody 的原因是，这是 Apache Web 服务器子进程在执行 WREQ cgi 程序时运行的用户。现在您已解包发行版，必须通过编辑以下四个文件进行一些手动配置：

- `/home/httpd/cgi-bin/wreq/req`
- `/home/httpd/cgi-bin/wreq/req-mail`
- `/home/httpd/cgi-bin/wreq/req-config`
- `/etc/aliases`

`req` 脚本所需的更改是将第 1 行更改为反映 perl 解释器的位置。在默认的 Red Hat 安装中，这是 `/usr/bin/perl`。`req-mail` 脚本也需要此更改。

为了使 `req-mail` 脚本与默认的 Red Hat 安装一起工作，需要对 `req-mail` 脚本进行额外更改。此更改是必需的，以便 sendmail 能够执行 `req-mail` 脚本。从 `req-mail` 脚本中注释掉第 11 行和第 12 行。这些行内容为：

```
$rcf=$0; $rcf=~s|\-mail\$|/\.config/;
require "$rcf";
```

注释掉这两行后，取消注释第 10 行并将其更改为如下所示：

```
require '/home/httpd/cgi-bin/wreq/req-config';
```

完成这些编辑后，您必须使用 `ln` 命令按如下方式从 `/etc/smrsh/req-mail` 创建到 `/home/httpd/cgi-bin/wreq/req-mail` 的符号链接：

```
[root@quicksilver wreq]# cd /etc/smrsh
[root@quicksilver smrsh]# ln -sf /home/httpd/cgi-bin/wreq/req-mail .
```

如果您使用 `smrsh` 以便允许 sendmail 代表您调用 `req-mail`，则需要此符号链接。如果您未使用 `smrsh`，可以跳过此步骤。

WREQ 将其部分配置变量存储在名为 `req-config` 的文件中，您必须接下来更改此文件。使 WREQ 在 Red Hat Linux 上运行所需的最小更改在表 30.2 中描述。

### 表 30.2 req.config 中的 WREQ 配置变量

| 变量 | 值 |
|---|---|
| `$sendmail` | 对于 Red Hat Linux 系统，将其设置为 `/usr/sbin/sendmail` 而不是 `/usr/lib/sendmail` |
| `$error_cc` | 应接收错误消息副本的人员的 userid（通常是系统管理员）。 |
| `$wreq_host` | 如果它与邮件服务器不同，请将其设置为运行 WREQ 的机器的名称。 |
| `$ph_host` | 除非您正在运行电话簿服务器，否则将其设置为空字符串以禁用此功能。 |

如果您完全按照这些说明操作，则不应更改 `req.config` 文件中的任何其他配置变量。
