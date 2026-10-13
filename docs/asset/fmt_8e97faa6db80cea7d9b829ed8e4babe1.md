
### 3. 定义出站邮件访问
与您的邮件服务器相关的最关键安全问题是其将接受哪些邮件消息以中继到其他邮件服务器。通过编辑 `/etc/mail/access` 文件，您可以指定服务器将接受本地投递或中继邮件的主机和用户。

### 4. 配置虚拟服务器
默认情况下，`sendmail` 假设您正在为服务器所属的域设置邮件服务器。若要使单台计算机上的 `sendmail` 成为多个域（称为虚拟服务器）的邮件服务器，您需要在 `/etc/mail/local-host-names` 文件中定义每个域名。

### 5. 配置虚拟用户
使用 `/etc/mail/virtusertable` 配置文件，您可以指示 `sendmail` 守护进程如何处理为其配置的用户和域接收的邮件。此文件赋予您很大的灵活性，可将指定给特定用户的邮件定向到特定邮箱、转发到不同的邮件地址，或以多种方式拒绝该邮件。

### 6. 添加用户账户
您需要为将在邮件服务器上拥有邮箱的每个用户添加一个用户账户。

### 7. 启动 sendmail 并生成数据库文件
启动 `sendmail` 会运行 `sendmail` 服务器守护进程，但还会将您的配置文件编译为 `sendmail` 可使用的数据库文件。如果服务器已在运行，您可以仅编译配置文件，使新设置生效而无需重启服务器。

以下小节提供了这些步骤的详细信息。

#### 获取域名
为了让人们能够向你邮件服务器上的用户发送邮件，你必须拥有自己的域名。第 25 章描述了如何获取自己的域名并设置 DNS 服务器。对于你的邮件服务器而言，关键问题是要确保 DNS 服务器上你域名的 MX 记录指向你邮件服务器的地址。

#### 配置基本 sendmail 设置 (`sendmail.mc`)
你的 `sendmail` 服务器的许多配置信息来自 `/etc/mail/sendmail.mc` 文件。由于此文件设置了大多数情况下都可以使用的 `sendmail` 默认值，因此你可能不需要对 `sendmail.mc` 做太多改动。不过，我建议你逐步浏览本节内容，以便了解你的邮件服务器是如何配置的。

你对 `sendmail.mc` 文件所做的更改不会立即生效。首先，你必须编译 `sendmail.mc` 设置以生成 `/etc/mail/sendmail.cf` 文件。我在“启动 sendmail 和生成数据库文件”一节中描述了如何做到这一点。

生成的 `/etc/mail/sendmail.cf` 文件包含超过 1,700 行用于指导 `sendmail` 守护进程行为的设置和注释。你在 `sendmail.mc` 文件中使用的 m4 宏与 `sendmail.cf` 文件中的最终设置不同。

若要查找 `sendmail.cf` 文件中某项设置应使用哪些宏，请参阅 `/usr/share/doc/sendmail/README.cf` 文件。如果你对 `sendmail.cf` 文件的内容细节感兴趣，我在 Red Hat Linux Bible 网站（www.wiley.com/redhatarabible）上收录了 sendmail.cf 的详尽描述。

> **注意：** 鉴于 Fedora 中 `sendmail` 的配置方式，你不应该直接修改 `sendmail.cf` 文件。如果 `sendmail.mc` 发生更改，`sendmail.cf` 文件会在 `sendmail` 重启时自动重新生成。因此，直接对 `sendmail.cf` 所做的任何修改都会丢失。

以下代码示例来自随 Fedora 版 `sendmail` 附带的 `/etc/mail/sendmail.mc` 文件。

> **说明：** `sendmail.mc` 文件中以 `dnl`（删除到行尾）开头的行是注释行。在大多数情况下，我在所示示例中省略了这些行。

```
divert(-1)dnl
include(`/usr/share/sendmail-cf/m4/cf.m4')dnl
VERSIONID(`setup for Red Hat Linux')dnl
OSTYPE(`linux')dnl
```

`sendmail.mc` 文件的前几行进行了一些清理工作。`divert` 行在生成配置文件时移除多余输出。`include` 行使 `sendmail` 所需的规则集被包含进来。`VERSIONID` 行标识该配置文件是用于 Red Hat Linux 系统的，例如 Fedora（尽管此设置不会进行检查，因此它可以是你喜欢的任何值）。然而，`OSTYPE` 必须设置为 `linux`，以便获取 `sendmail` 所需文件的正确位置。

```
dnl define(`SMART_HOST',`smtp.your.provider')
```

默认情况下，`sendmail` 守护程序会尝试将你的 outgoing 电子邮件直接发送到其寻址的邮件服务器。如果你希望所有电子邮件都通过特定的邮件服务器进行中继，你可以从上面的 `SMART_HOST` 行中移除注释 `dnl`（代表“删除到行尾”）。然后，将 `smtp.your.provider` 更改为你想要使用的邮件服务器的完全限定域名。当然，你需要确保你定义的 `SMART_HOST` 会接受来自你邮件服务器的中继请求。

```
define(`confDEF_USER_ID',`8:12')dnl
```

基于之前设置的 `confDEF_USER_ID` 行，守护程序不再以 root 用户身份运行，而是以 mail 用户（UID 8）和 mail 组（GID 12）身份运行。这是一项良好的策略，因为它可以防止那些可能利用漏洞攻击你的邮件服务器的人获得你机器的 root 访问权限。

```
dnl define(`confAUTO_REBUILD')dnl
define(`confTO_CONNECT', `1m')dnl
```

如果你移除 `dnl`，`confAUTO_REBUILD` 行将指示 `sendmail` 在必要时自动重建别名数据库。`confTO_CONNECT` 行将 `sendmail` 等待初始连接完成的时间设置为一分钟（1m）。

```
define(`confTRY_NULL_MX_LIST',true)dnl
define(`confDONT_PROBE_INTERFACES',true)dnl
```

如果 `confTRY_NULL_MX_LIST` 为 true，则如果接收服务器是某主机最佳邮件交换（MX），请尝试直接连接到该主机。如果 `confDONT_PROBE_INTERFACES` 为 true，则 `sendmail` 守护程序不会将本地网络接口插入已知等效地址列表中。

```
define(`PROCMAIL_MAILER_PATH',`/usr/bin/procmail')dnl
dnl define(`ALIAS_FILE',`/etc/aliases')dnl
dnl define(`STATUS_FILE',`/var/log/mail/statistics')dnl
```

接下来三行（`PROCMAIL_MAILER_PATH`、`ALIAS_FILE` 和 `STATUS_FILE`）分别设置了用于分发传入邮件的程序（默认为 `procmail`）的位置、邮件别名文件的位置以及邮件统计文件的位置。

```
define(`UUCP_MAILER_MAX', `2000000')dnl
define(`confUSERDB_SPEC',`/etc/mail/userdb.db')dnl
define(`confPRIVACY_FLAGS', `authwarnings,noverify,noexpn,restrictqrun')dnl
define(`confAUTH_OPTIONS', `A')dnl
```

`UUCP_MAILER_MAX` 行设置了由 UUCP 邮件程序接收的消息的最大尺寸（以字节为单位）。`confUSERDB_SPEC` 行设置了用户数据库的位置（你可以在其中针对特定用户覆盖默认邮件服务器）。`confPRIVACY_FLAGS` 行促使 `sendmail` 坚持使用某些邮件协议。例如，`authwarnings` 会导致使用 `X-Authentication-Warning` 头部并在日志文件中记录。`noverify` 和 `noexpn` 设置可防止请求这些服务。`restrictqrun` 选项可防止向 `sendmail` 发送 `-q` 选项。
