
此 `m4` 宏允许使用 `mailertable`（名称到特殊代理程序）。`mailertable` 是一个将 `host.domain` 映射到特殊代理程序和域名对的数据库。通过此功能，可以使用指定的或特定的代理投递到新域名。

```
FEATURE(`virtusable`, `-h -o /etc/virtusable`)
```

此 `m4` 宏允许使用 `virtusable`（支持虚拟域名）。`virtusable` 数据库将虚拟域名映射到新域名。通过此功能，虚拟域名可以投递到本地、远程或单用户用户地址。

```
FEATURE(`redirect`)
```

此 `m4` 宏允许使用 `redirect`（支持地址.REDIRECT）。通过此功能，发送到退役用户账户（例如“女主”）的邮件将被退回并带有转发地址指示。退役账户必须在邮件服务器的别名中设置。

```
FEATURE(`always_add_domain`)
```

关于本书的意见和建议请邮寄至 `gomouraani@videotron.ca`

此 `m4` 宏允许使用 `"always_add_domain"`（在本地邮件上添加本地域名）。使用此功能后，所有本地投递的地址都将是完全限定的。设置此功能是安全且推荐的。

## FEATURE(use_cw_file)

此 `m4` 宏允许对本地主机名使用 `/etc/sendmail.cw` 中的 `"use_cw_file"`。通过此功能，你可以在 `/etc/sendmail.cw` 中声明一个主机列表，让本地主机在这些主机上充 MX 接收者的角色。换句话说，此功能通过读取 `/etc/sendmail.cw` 来获取本地主机的别名。

## FEATURE(local_procm)

此 `m4` 宏允许使用 `"local_procm"`（使用 `procmail` 作为投递代理）。使用此功能后，你可以将 `procmail` 作为 `Sendmail` 的投递代理。请记住，建议在你的中央邮件枢（Central Mail Hub）服务器上安装 `procmail` 程序。

## FEATURE(nouucp)

此 `m4` 宏允许使用 `"nouucp"`（消除 UUICP 支持）。使用此功能后，`Sendmail` 的宏将删除或忽略 UUICP 服务。换句话说，如果你的邮件服务器不支持 `uic`，你可以通过此宏在 `Sendmail` 配置中禁用所有支持。

## MAILER(procmail) and MAILER(smtp)

此 `m4` 宏允许使用 `"procmail"` 和 `"smtp"` 作为投递代理（在 `Sendmail` 中，默认情况下投递代理不会自动声明）。通过此功能，你可以指定想要发送哪些代理以及忽略哪些。`MAILER(procmail)` 和 `MAILER(smtp)` 选项选择了 `procmail`、`smtp`、`smtp8` 和 `relay` 投递代理。

## FEATURE(access, db)

此 `m4` 宏启用了访问数据库功能。通过此功能，你有能力访问数据库以允许或拒绝来自特定域的邮件。通常此功能仅应在中央邮件枢服务器上可用。

## FEATURE(blacklist, recipients)

此 `m4` 宏允许拦截某些接收者用户名、主机名或地址的邮件。通过此功能，你可以阻止发送给 `nobody`、`foo.mydomain.com` 或 `guest@bar.mydomain.com` 的邮件。

## FEATURE(rbl)

此 `m4` 宏允许 `Sendmail` 拒绝来自实时黑洞列表数据库 `"rbl.maps.vip.com"` 中任何站点的邮件。`RBL` 是存储在垃圾邮件者 DNS 中的数据库。详情请参阅 `"http://maps.rbl/"`。

> 注意：有时，你希望继续通信的域可能会出现在 RBL 列表中。在这种情况下，`Sendmail` 允许你覆盖这些域以接收它们的电子邮件。

要执行此操作，只需编辑 `/etc/mail/access/` 文件并添加适当的域信息。

例如：
`blacklisted.domain OK`

### Step 2

现在我们的宏配置文件 `"sendmail.mc"` 已创建，我们可以使用以下命令从这些语句中构建 `sendmail` 文件 `"sendmail.cf"`：

![](img/4e12ba68f8ecabb49a9835b8d88a1c6d_256_0.png)

© Copyright 1999-2000 Gerhard Maurani and Open Network Architecture ® 257

关于本书的意见和建议请邮寄至 `gmourani@videotron.ca`

```
[root@deep] # cd /var/tmp/sendmail-version/cf/cf/

[root@deep] # m4 _m4 /etc/sendmail.mc > /etc/sendmail.cf
```

注意：在此处"`m4/m4.cf`" 告诉 `m4` 程序去哪里查找它的默认配置信息。

## 中央邮件枢的 "/etc/mail/access 和 access.db" 文件

`"access"` 数据库文件可以用来拒绝来自所选域的邮件。对于本地或客户端设置，不需要这些 `"access"` 和 `"access.db"` 文件。只有当你决定设置一个中央邮件枢来处理所有邮件时，才需要它们。另外请注意，中央邮件枢将改进你网络上其他服务器和客户端的管理。

### Step 1

创建 `access` 文件（`touch /etc/mail/access`）并添加以下行：

```
# 下面的文件格式来自

# Sendmail 发行版下的 "cf/README" 文件。

# 表格使用电子邮件地址、域名和数字作为键。例如，

# spammer@aol.com REJECT

# cyberspam.com REJECT

# 192.168.212 REJECT

#

# 映射的值部分包含：

# OK 如果其他规则会拒绝它，例如，

# 如果域名是不可解析的。

# RELAY 接收到指定域的邮件或

# 从指定域接收的邮件，通过你的 SMTP 服务器中继。RELAY 也作为其他情况的隐式 OK。

# REJECT 拒绝发送者或接收者。
```

关于此书的意见和建议请邮寄至 `gmourani@v.videotron.ca`

提高查找速度。如果你将 `Sendmail` 配置为由中央服务器（邮件中枢）处理所有邮件，则你不需要在相邻服务器或客户端机器上安装“`aliases`”和“`aliases.db`”文件。

## 第一步

通过以下操作创建 `aliases`（`touch/etc/aliases`）并添加以下行：

```
#

# @(#aliases 8.2 (Berkeley) 3/5/94

#

# 此文件中的别名不会在 Mail 头部中展开，

# 但在网络或 /bin/mail 中可见。

#

# >>>>>>>> 在此文件发生任何更改后，

# >> NOTE >> 必须运行 "newaliases" 程序，

# 才能确保更改应用到 sendmail 中。
```

```
# 基础系统别名 -- 这些必须必须存在。
MAILER-DAEMON: postmaster
postmaster: root

# 伪账户的通用重定向。
bin: root
daemon: root
nobody: root
```

```
# 应该接收 root 邮件的用户
```

`root`: `admin`
