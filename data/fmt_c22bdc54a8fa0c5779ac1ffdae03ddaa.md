
# 备份设备与计划

备份设备可以是磁盘、磁带、CD-ROM R 或 CD-ROM R/W，取决于大小、频率和重要性。各种资产将按照从每天到每月不等的计划进行备份。重要的是，被备份的数据是可以恢复的。只写存储没有用处。备份计划必须包含对关键数据的恢复检查。我们在第 9 章“系统管理”中讨论了 Elsolutions 使用的计划。

Elsolutions 的 Windows Server 安装也将以类似的方式进行备份。Windows 2000 和 Windows XP 有一个类似于 `cron` 的工具，称为任务计划程序。它有一个 GUI 界面，管理员可以通过“开始→程序→附件→系统工具→计划任务”进行访问。这会打开计划任务文件夹。有一个“新建计划任务”图标和每个计划任务的图标。“点击添加计划任务”会打开图 12-11 所示的向导。

下一个面板显示了应用程序列表。我们选择一个进入图 12-12 所示的下一个面板。

在那里，我们为任务命名，以便在列表中识别它。我们有机会指定任务运行的间隔时间、每天运行的次数以及任何所需的授权凭据。任务添加后，它的图标将出现在计划任务文件夹中。管理员可以查看或更改其属性。

还有一个 Windows 2000 的 `at` 命令，允许脚本或管理员使用命令来执行相同的操作。该命令与 Linux 的 `at` 命令非常相似。有关关于备份和恢复的更多信息，请参阅第 16 章“系统备份与恢复”。

## 加密

组织可以选择多种加密技术，以消除以明文传输凭据和数据的要求。

## 计划任务向导

此向导帮助你为 Windows 调度要执行的任务。

你选择想要让 Windows 运行的程序，然后调度在一个方便的时间。

点击“下一步”继续。

图 12–11 添加任务。

## 公钥基础结构

公钥基础结构 (PKI) 使用密钥对。其中一个密钥是所有人知的公钥。另一个密钥是只有一方知道的私密密钥。我们使用密钥对中的一个密钥进行加密，它只能由对应的兄弟密钥解密。这种聪明虽然缓慢的技术是实现不可否认的双向身份验证和记录数字签名的基础。PKI 是安全套接层 (SSL)、安全外壳 (SSH) 和优美隐私 (PGP) 安全技术的构建模块。

## PGP

PGP 使用 PKI 加密数据，不需要在传输端之间共享秘密密钥。发送方需要接收者的公钥。她使用 PGP 用公钥加密消息，并使用任何类型的通道数据传输消息。接收者使用他的秘密私钥解密消息。

由于这种操作方法，PGP 通常用于在事先同意使用 PGP 的双方之间发送安全电子邮件。PGP 是一种

## SSL

Netscape 开发了 SSL 来保护流量。目前的 Netscape、Mozilla 和 Internet Explorer 都支持 SSL。

# 384 第 12 章 安全

`login`、`rsh`、`rcp`、`telnet`、`ftp`、`krdist`、`ksu`、`login` 和 `xdm` 等工作服务会将此票据作为身份验证的证明。`kinit` 和 `kdestroy` 工具允许 Linux 用户显式地获取和销毁票据。通常情况下，票据机制是透明的。

Kerberos 实现了授权委托的概念：“我信任你。你信任我。我信任你。” Windows 2000 和 Windows XP 将 Kerberos 作为协商认证方法的首选。授权委托允许 Windows 2000 域结构进行扩展。

Kerberos 也随 Red Hat Linux 7.1 分发。Windows XP 或 Windows 2000 telnet 用户连接到 Linux 守护进程，如果 Linux 服务器启用了 Kerberos，则将通过 Kerberos 进行身份验证。Kerberos 服务器或 KDC 必须在网络上运行。它应该是物理安全的，以避免损害安全性。服务器由紧耦合的密钥发行中心（KDC）和票据授予服务（TGS）组成。

在 Red Hat 7.1 上，我们在 `/etc/krb5.conf` 中配置 Kerberos 管理、KDC 的位置、KDC 管理配置节点的位置，以及一个或多个认证域（realms），如下例所示：

```
[logging]
default = FILE:/var/log/krb5libs.log
kdc = FILE:/var/log/krb5kdc.log
admin_server = FILE:/var/log/kadminmd.log
```

```
[libdefaults]
ticket_lifetime = 24000
default_realm = BELLMEADE
dns_lookup_realm = false
dns_lookup_kdc = false
```

```
[realms]
BELLMEADE = {
kdc = pavilion.bellmeade:88
admin_server = pavilion.bellmeade:bellmeade:749
default_domain = pavilion.bellmeade
}
```

```
[domain_realm]
.example.com = BELLMEADE
example.com = BELLMEADE
```

```
[kdc]
profile = /var/kerberos/krb5kdc kdc.conf
```

```
[pam]
debug = false
ticket_lifetime = 36000
renew_lifetime = 3600
forwardable = true
krb4_convert = false
```

对应的示例 `kdc.conf` 配置文件为：

```
[kdcdefaults]
ac_file = /var/kerberos/krb5kdc/kadm5.acl
dict_file = /usr/dict/words
admin_keytab = /var/kerberos/krb5kdc/kadm5.keytab
kdc_ports = 88

[realms]
BELLMEADE = {
kdc = BELLMEADE:88
kadmin_port = 749
max_life = 10h 0m 0s
max_renewable_life = 7d 0h 0m 0s
master_key_type = des-cbc
supported_envelopes = des-cbc-crc:normal des3-cbc-caw:normal des3-cbc-shal:normal des-cbc-crc:v4 des-cbc-crc:afs3
}
```

```
[logging]
kdc = FILE:/var/kerberos/krb5kdc/kdc.log
admin_server = FILE:/var/kerberos/krb5kdc/kadmin.log
default = FILE:/var/kerberos/krb5kdc/krb5lib.log
```

`kadmin` 和 `kadmin.local` 客户端用于管理系统。除了认证方式外，它们提供相同的功能。`kadmin.local` 客户端仅运行在 KDC 本地机器上，且不使用 Kerberos 进行身份验证，从而消除了“鸡生蛋蛋”的问题。

Red Hat Linux 分发了一个 Kerberos 管理 Gnome 应用程序，如图 12-13 所示。

解决方案将启用 Linux telnet 的 Kerberos 认证。Windows XP 或 Windows 2000 专业版客户端将与 Red Hat Linux 进行身份验证。telnet 守护进程启用了 Linux，从而避免了密码以明文发送。该解决方案不用于安全数据传输。也就是说，它不对在网络传输的数据进行加密。

要了解关于在 Linux 上安装、管理或使用 Kerberos 的良好论述，请使用 `info` 命令。

```
info krb5-install
info Krb5-Admin
info Krb5-User
```

## SSH

SSH 允许我们使用 PKI 建立安全的远程会话。SSH 使用多种标准加密技术。认证交互使用标准的共享密钥算法进行加密。在双向认证期间，数据流量通过 PKI 安全传输。目的地必须拥有对方的公钥。这是如何实现的？脚本以明文将密钥发送给对方。这并不算安全泄露，因为毕竟密钥是公开的。SSH 似乎是 telnet 的替代品，因为它加密了所有流量。它还为 `rsh`、`rexec` 和 `ftp` 提供了安全的替代方案。主要的困难在于 SSH 是专有的。幸运的是，Red Hat 绑定了 openSSH。Red Hat 没有随 Linux 一分发 Windows openSSH 客户端，但 Cygwin 发行版包含一个对于 Windows 目的效果良好的 SSH 客户端。

## 完整性检查

有很多实用的工具可以帮助管理员检查其系统的完整性。在“文件安全”部分提到的 Tripwire 适于检查 Linux 文件系统是否被破坏很有用。SATAN 扫描已知漏洞。如果它发现漏洞，将提供一个关于黑客如何利用该漏洞的 HTML 教程。Dan Farmer 和 Wiet 编写了。

# 390 第 13 章 网络文件系统

（对于 Windows 以及 `.profile` 或 `.bashrc` 文件则用于 Linux）。遗憾的是，用户在 Windows 上需要管理员权限才能添加登录脚本。

我们将讨论 Linux 和 Windows 上可用的三种基于网络的文件系统。
