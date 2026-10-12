
现在我们可以继续安装 FreeIPA 服务器。

您想要配置集成 DNS (BIND) 吗？[no]: yes
检测到现有 BIND 配置，覆盖吗？[no]: yes

输入正在设置服务器的计算机的完全域名。使用格式 `<hostname><domainname>`
示例：example.com。
服务器主机名 [quebec.linux.com]:

警告：跳过主机 `quebec.linux.com` 的 DNS 解析
域名已根据主机名确定。

请确认域名 [linux.com]:

Kerberos 协议要求定义 Realm（领域）。这通常是转换为大写的域名。

请提供领域名称 [LINUX.COM]:

在提供领域名称后，我们需要为目录管理器提供一个密码。某些目录服务器操作需要管理员用户。此用户被称为目录管理器（Directory Manager），具有用于系统管理任务的完全访问权限，并将添加到为 IPA 创建的目录服务器实例中。密码长度至少为 8 个字符。

目录管理器密码：
Password (confirm):

除了目录管理器外，FreeIPA 还使用一个管理员用户，我们也需要指定其密码。IPA 服务器需要一个名为 `'admin'` 的管理员用户。该用户是用于 IPA 管理的普通系统账户。

IPA admin密码：
Password (confirm):

设置程序现在将执行 DNS 检查。

正在检查 DNS 域名 `linux.com.`，请稍候 ...
`ipa-server-install(Server)`: ERROR DNS zone `linux.com` already exists in DNS
`ipa-server-install(Server)`: ERROR The `ipa-server-install` command failed. See `/var/log/ipaserver-install.log` for more information

正如我们所见，安装失败是因为互联网上已存在 `linux.com` 区域。我们将域名更改为 `linux.local`。我们还将编辑服务器主机名和 `/etc/hosts` 文件。

```bash
root@quebec ~ hostnamectl set-hostname quebec.linux.local

root@quebec ~ cat /etc/hosts

127.0.0.1       localhost localhost.localdomain localhost4.localdomain localhost4

::1             localhost localhost.localdomain localhost6.localdomain localhost6

192.168.1.243      quebec.linux.local
```

然后我们可以再次执行 `ipa-server-install`。

```bash
root@quebec ~ ipa-server-install
```

您想要配置 DNS 转发器吗？[yes]:

服务器主机名 [quebec.linux.local]:

警告：跳过主机 `quebec.linux.local` 的 DNS 解析
域名已根据主机名确定。

请确认域名 [linux.local]:

Kerberos 协议要求定义 Realm 节点。这通常是转换为大写的域名。

请提供领域名称 [LINUX.LOCAL]:

某些目录服务器操作需要管理员用户。此用户被称为目录管理器（Directory Manager），具有用于系统管理任务的完全访问权限，并将添加到目录服务器实例中。密码长度至少为 8 个字符。

目录管理器密码：
Password (confirm):

IPA admin密码：
Password (confirm):

设置程序现在将执行 DNS 检查。

正在检查 DNS 域名 `linux.local.`，请稍候 ...
您想要配置 DNS 转发器吗？[yes]:
`/etc/resolv.conf` 中配置了以下 DNS 服务器：`192.168.1.1`
您想将这些服务器作为 DNS 转发器吗？[yes]
来自 `/etc/resolv.conf` 的所有 DNS 服务器已添加。您现在可以为 DNS 转发器输入 IP 地址：

输入 DNS 转发器的 IP 地址，或按 Enter 跳过：
正在检查 DNS 转发器，请稍候 ...
您想要搜索缺失的反向区域吗？[yes]:

IPA 主服务器将配置为：
主机名：`quebec.linux.local`
IP 地址(s)：`192.168.1.243`
域名：`linux.local`
领域名称：`LINUX.LOCAL`

BIND DNS 服务器将为 IPA 域名提供服务：
转发器：`192.168.1.1`
转发策略：仅限
反向区域：无反向区域

使用这些值继续配置系统？[no]: yes

以下操作可能需要几分钟完成。
请等待提示符返回。

配置 NTP 守护进程 (`ntpd`)

配置目录服务器 (`dirsrv`)。预计需要 1 分钟

配置证书服务器 (`pki-tomcatd`)。预计需要 3 分 30 秒

配置目录服务器 (`dirsrv`)。预计需要 10 秒

配置 Kerberos KDC (`krb5kdc`)。预计需要 30 秒

### 配置 kadmin

### 配置 ipa_memcached

### 配置 ipa-otpd

### 配置 ipa-custodia

配置 Web界面 (`httpd`)。预计时间：1 分钟

应用 LDAP 更新

升级 IPA：

### 配置 DNS (`named`)

### 配置 DNS 密钥同步服务 (`ipa-dnskeysyncd`)

### 配置客户端组件

使用现有证书 `'/etc/ipa/ca.crt'`。

客户端主机名：`quebec.linuxaholics.local`
Realm：`LINUXAHOLICS.LOCAL`
DNS 域：`linuxaholics.local`
IPA 服务器：`quebec.linuxaholics.local`
BaseDN: `dc=linuxaholics,dc=local`

已配置 `/etc/openldap/ldap.conf`
已配置 `/etc/ssh/ssh_config`
已配置 `/etc/ssh/sshd_config`
正在将 `linuxaholics.local` 配置为 NIS 域。
客户端配置完成。

================================================================================================

安装完成

后续步骤：

- 1. 你必须确保这些网络端口已开放：
  TCP 端口：
  * 80, 443: HTTP/HTTPS
  * 389, 636: LDAP/LDAPS
  * 88, 464: kerberos
  * 53: bind
  UDP 端口：
  * 88, 464: kerberos
  * 53: ntp
  * 123: ntp

- 2. 你可以使用以下命令获取 Kerberos 票据：
  `kinit admin`
  此票据将允许你使用 IPA 工具（例如 `ipa user-add`）
  以及 Web 用户界面。

务必备份存储在 `/root/cacert.p12` 中的 CA 证书
这些文件是创建副本所必需的。这些文件的密码是 Directory Manager 密码

# 第 23 章从 FreeIPA 开始

我们的服务器已就绪，但我们需要在防火墙中开放一系列端口，以便客户端能够连接。

```bash
[root@quebec ~]# firewall-cmd --permanent --add-service http
success
```

```bash
[root@quebec ~]# firewall-cmd --permanent --add-service https
success
```

```bash
[root@quebec ~]# firewall-cmd --permanent --add-service ldap
success
```

```bash
[root@quebec ~]# firewall-cmd --permanent --add-service ldaps
success
```

```bash
[root@quebec ~]# firewall-cmd --permanent --add-service kerberos
success
```

```bash
[root@quebec ~]# firewall-cmd --permanent --add-service kpasswd
success
```

```bash
[root@quebec ~]# firewall-cmd --permanent --add-service dns
success
```

```bash
[root@quebec ~]# firewall-cmd --permanent --add-service ntp
success
```
