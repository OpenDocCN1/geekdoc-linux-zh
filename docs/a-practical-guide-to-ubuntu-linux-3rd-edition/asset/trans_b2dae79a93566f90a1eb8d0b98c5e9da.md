

dc_minimaldns='bool'
将 **bool** 设置为 **true** 以最小化 DNS 查询（对拨号连接有用），或设置为 **false** 以根据需要执行 DNS 查询。

dc_other_hostnames='host-list'
*host-list* 是一个以分号分隔的 IP 地址和/或 FQDN（完全限定域名）列表，本地系统接受（但不中继）这些主机的邮件；假定 **localhost** (127.0.0.1) 包含在此列表中。

dc_readhost='hostname'
*hostname* 用于替换源自本地系统的邮件报头中的本地邮件名称（mailname）。仅当 **dc_hide_mailname** 设置为 **true** 且 **dc_eximconfig_configtype** 设置为 **smarthost** 或 **satellite** 时，此设置才有效。

dc_relay_domains='host-list'
*host-list* 是一个以分号分隔的 IP 地址和/或 FQDN 列表，本地系统接受这些主机的邮件，但不投递到本地系统。本地系统会将邮件中继到这些系统。例如，本地系统可能是这些系统的二级服务器。

dc_relay_netse='host-list'
*host-list* 是一个以分号分隔的 IP 地址和/或 FQDN 列表，本地系统为这些系统中继邮件。对于这些系统，本地系统充当智能主机（smarthost，第 717 页）。

dc_smarthosts='host-list'
*host-list* 是一个以分号分隔的 IP 地址（优先）和/或 FQDN 列表，本地系统通过向这些主机发送邮件来中继到非本地系统（即智能主机；第 717 页）。示例请参见第 716 页的“JumpStart I”。

dc_use_split_config='bool'
控制 update-exim4.conf 使用哪些文件来生成 exim4 的配置文件。有关更多信息，请参见第 725 页的“拆分配置”（Split configuration）。

## dpkg-reconfigure：配置 exim4

**dpkg-reconfigure** 实用程序重新配置已安装的软件包副本。它显示一个伪图形窗口，可用于任何基于字符的设备，包括终端模拟器。以下命令允许您交互式地重新配置 exim4：

```
sudo dpkg-reconfigure exim4-config
```

此命令显示的第一个窗口简要说明了 *拆分*（split）和 *非拆分*（unsplit）配置之间的区别（第 725 页），告知您可以在哪里找到有关此主题的更多信息，并询问您是否希望设置拆分配置（图 20-1）。如果您选择设置拆分配置，**dpkg-reconfigure** 会将 **dc_use_split_config** 的值分配为 **true**（参见第 725 页的“拆分配置”），并继续执行，就好像您选择了使用 *非拆分* 配置一样：它不会修改 */etc/exim4/conf.d* 目录层次结构中的文件。此设置会导致 **update-exim4.conf** 读取 */etc/exim4/conf.d* 目录层次结构中的文件，并将您对那些文件所做的任何更改纳入其中。

![](img/2344fc4a798f29dca9e8b5ed7288171a_777_0.png)

**图 20-1** 在 **exim4-config** 上使用 **dpkg-reconfigure**

**dpkg-reconfigure** 实用程序继续提供信息、提问并分配给 **/etc/exim4/update-exim4.conf.conf**（第 724 页）中的变量赋值。它也可能更改 **/etc/mailname**（第 718 页）中的字符串。完成后，它会重启 **exim4**，在此过程中运行 **update-exim4.conf**。

## SPAMASSASSIN

垃圾邮件——或者更准确地说是 **UCE**（非请求商业电子邮件）——占所有邮件的四分之三以上。SpamAssassin 评估每封 incoming（传入）邮件并为其分配一个数字，表示该邮件是垃圾邮件的可能性。数字越高，该邮件为垃圾邮件的可能性就越大。您可以根据其评级过滤邮件。SpamAssassin 安装后即可使用，但您可以修改其配置文件使其更适合您的需求。有关 SpamAssassin 的更多信息来源，请参见第 715 页。

### SpamAssassin 的工作原理

**spamd** 和 **spamc**
SpamAssassin 由 **spamd** 守护进程和 **spamc** 客户端组成。尽管它包含 **spamdassassin** 实用程序，但 SpamAssassin 文档建议使用 **spamd** 而不是 **spamdassassin** 来过滤邮件，因为 **spamd** 比 **spamdassassin** 加载速度快得多。虽然 **spamdassassin** 可以单独工作，但 **spamc** 会调用 **spamd**。**spamd** 守护进程会生成子进程；当 **spamd** 正在运行时，**ps** 除父 **spamd** 进程外还会显示多个 **spamd** 子进程：

```
$ ps -ef | grep spam
root    5073    1  0 10:53 ?   00:00:00 /usr/sbin/spamd --create-prefs ...
root    5106 5073  0 10:53 ?   00:00:00 spamd child
root    5107 5073  0 10:53 ?   00:00:00 spamd child
zach   16080 6225  0 12:58 pts/0 00:00:00 grep spam
```

spamc 实用程序是一个过滤器。也就是说，它从标准输入读取每封邮件，将邮件发送给 spamd 进行处理，并将修改后的邮件写入标准输出。spamd 守护进程使用多种技术来识别垃圾邮件：

- **报头分析**——检查发送垃圾邮件的人使用的那些技巧，这些技巧旨在让您认为邮件是合法的。
- **文本分析**——检查邮件正文中垃圾邮件的特征。
- **黑名单**——检查列表，查看发件人是否以发送垃圾邮件而闻名。
- **数据库**——针对 Vipul's Razor (razor.sourceforge.net)（一个垃圾邮件跟踪数据库）检查消息签名。

### 先决条件

安装以下软件包：

- **spamassassin**
- **spamd**
- **procmail**（在邮件服务器上运行 SpamAssassin 所需；第 730 页）

安装 **spamassassin** 软件包时，**dpkg postinst** 脚本不会启动 **spamd** 守护进程。在启动 **spamd** 之前，您必须将 `/etc/default/spamassassin` 中 `ENABLED` 的赋值更改为 `1`。通常您不需要对此文件进行其他更改。

```
$ cat /etc/default/spamassassin
...
# Change to one to enable spamd
ENABLED=1
...
```

进行此更改后，使用以下命令启动 **spamd** 守护进程：

```
$ sudo service spamassassin start
Starting SpamAssassin Mail Filter Daemon: spamd.
```

修改任何系统 SpamAssassin 配置文件后，给出相同的命令，但将 **start** 替换为 **reload**，以便 **spamd** 重新读取其配置文件。

### 测试 SpamAssassin

在 **spamd** 运行时，您可以通过向它发送一个字符串来查看 **spamc** 的工作方式：

```
$ echo "hi there" | spamc
...
X-Spam-Checker-Version: SpamAssassin 3.3.1 (2010-03-16) on 10.04b1
X-Spam-Flag: YES
X-Spam-Level: *****
X-Spam-Status: Yes, score=6.9 required=5.0 tests=EMPTY_MESSAGE,MISSING_DATE,
MISSING_HEADERS,MISSING_MID,MISSING_SUBJECT,NO_HEADERS_MESSAGE,NO_RECEIVED,
NO_RELAYS autolearn=no version=3.3.1
...
Content analysis details: (6.9 points, 5.0 required)
```

| 点数 规则名称 | 描述 |
|---|---|
| -0.0 NO_RELAYS | 信息性：消息未通过 SMTP 中继 |
| 1.2 MISSING_HEADERS | 缺少 To: 报头 |
| 1.1 MISSING_MID | 缺少 Message-Id: 报头 |
| 1.8 MISSING_SUBJECT | 缺少 Subject: 报头 |
| 2.3 EMPTY_MESSAGE | 消息似乎没有文本部分且没有 Subject: 文本 |
| -0.0 NO_RECEIVED | 信息性：消息没有 Received 报头 |
| 1.4 MISSING_DATE | 缺少 Date: 报头 |
| 0.0 NO_HEADERS_MESSAGE | 消息似乎缺少大多数 RFC-822 报头 |
| ... | ... |

当然，SpamAssassin 会抱怨，因为您提供的字符串不包含标准邮件报头。以 **X-Spam-Status** 开头的逻辑行包含了对字符串 **hi** there 的报告核心。首先它说 **Yes**（它认为该消息是垃圾邮件）。SpamAssassin 使用一种评级系统，为邮件分配命中次数。如果邮件获得的命中次数超过所需命中次数（默认为 5.0），SpamAssassin 会将其标记为垃圾邮件。该字符串因许多原因而失败，这些原因在此状态行中列举。原因在标记为 **Content analysis** details 的部分中详细说明。

以下列表是来自 SpamAssassin 处理的一封真实垃圾邮件。它获得了 **24.5** 次命中，表明这几乎肯定是垃圾邮件。

```
X-Spam-Status: Yes, hits=24.5 required=5.0
   tests=DATE_IN_FUTURE_06_12,INVALID-ID_TZ_ABSURD,
   MSCID_OE_SPAM_4ZERO,MSCID_OUTLOOK_TIME,
   MSCID_SPAMSIGN_4ZEROS,RCD_IN_DSBL,RCD_IN_NJABL,
   RCVL_IN_UNCONFIRMED_DSBL,REMOVE_PAGE,VACATION_SCAM,
   X_NJABL_OPEN_PROXY
   version=2.55

X-Spam-Level: ****************************
X-Spam-Checker-Version: SpamAssassin 2.55 (1.174.2.19-2003-05-19-exp)
X-Spam-Report:* This mail is probably spam. The original message has been attached
along with this report, so you can recognize or block similar unwanted
mail in future.  See http://spamassassin.org/ta/ for more details.
Content preview: Paradise SEX Island Awaits! Tropical 1 week Vacations
where anything goes! We have lots of WOMEN, SEX, ALCOHOL, ETCl Every
man's dream awaits on this is land of pleasure.  [...] 
Content analysis details:  (24.50 points, 5 required)
MSCID_SPAMSIGN_4ZEROS (4.3 points)  Message-Id generated by spam tool (4zeros variant)
INVALID_DATE_TZ_ABSURD (4.3 points)  Invalid Date: header (timezone does not exist)
MSCID_OE_SPAM_4ZERO (3.5 points)  Message-Id generated by spam tool (4-zeros variant)
VACATION_SCAM    (3.9 points)  BODY: Vacation Offers
REMOVE_PAGE      (0.3 points)  URI: URL of page called "remove"
MSCID_OUTLOOK_TIME (4.4 points) Message-Id is fake (in Outlook Express format)
DATE_IN_FUTURE_06_12 (1.3 points)  Date: Is 6 to 12 hours After Received: date
RCD_IN_NJABL     (0.9 points)  RBL: Received via a relay in dsbl.njABL.org
[RBL check: found 94.99.190.200.dsbl.njABL.org]
RCD_IN_UNCONFIRMED_DSBL (0.5 points)  RBL: Received via a relay in unconfirmed.dsbl.org
[RBL check: found 94.99.190.200.unconfirmed.dsbl.org]
X_NJABL_OPEN_PROXY (0.5 points)  RBL: NJABL: sender is proxy/relay/formail/spam-source
RCVD_IN_DSBL     (2.6 points)  RBL: Received via a relay in list.dsbl.org
[RBL check: found 211.157.63.200.list.dsbl.org]
X-Spam-Flag: YES
Subject: [SPAM] re: statement
```

