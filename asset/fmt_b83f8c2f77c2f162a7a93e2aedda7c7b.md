
- 为本地系统上存在的用户名添加别名。
  - `user name:<用户的别名>`
- 为希望将消息转发到的外部电子邮件地址添加别名。
  - `user name:<电子邮件地址>`
- 为希望将邮件转发到的用户列表添加别名。用户列表在单独的文件中指定。
  - `user name> :include: <包含用户名的文件路径>/<文件名>`
- 为希望将用户收到的消息附加到的文件名添加别名。
  - `user name>: <文件路径>/<文件名>`
- 或者，添加一个别名以启用 Sendmail 处理来自标准输入的消息的命令。
  - `user name>: <命令>`
3. 保存并关闭文件。
4. 输入 `newaliases` 以更新别名数据库文件。

#### 操作参考：使用 Postfix 配置电子邮件别名

要使用 Postfix 配置电子邮件别名：

1. 使用 vi 编辑器打开 `/etc/postfix/main.cf` 文件。
2. 验证 `alias_maps` 变量是否已定义别名文件的位置。
   `alias_maps = hash:/etc/aliases`
3. 保存并关闭文件。
4. 使用 vi 编辑器打开 `/etc/aliases` 文件。
5. 为本地系统上存在的用户名添加别名。
   `user name:用户的别名`
6. 保存并关闭文件。
7. 输入 `newaliases` 以更新别名数据库文件。
8. 输入
   `service postfix restart`
   以重启 postfix 服务。

#### 操作参考：配置本地别名

要配置本地别名：

1. 以 root 身份登录。
2. 使用 vi 编辑器打开 `/etc/postfix/main.cf` 文件。
3. 找到 `alias_maps` 指令，并验证该指令是否已定义别名文件的位置。
   `alias_maps = hash:/etc/postfix/aliases`
4. 找到 `alias_database` 指令，并验证该指令是否已定义别名文件的位置。
   `alias_database = hash:/etc/postfix/aliases`
5. 保存并关闭文件。
6. 使用 vi 编辑器打开 `/etc/postfix/aliases` 文件。
7. 添加电子邮件别名。
   `user name:alias1, [alias2, alias3]`
   - 为本地系统上存在的用户名添加别名。
     `user name:用户的别名`
   - 为希望将邮件转发到的外部电子邮件地址添加别名。
     `user name:电子邮件地址`
   - 为包含邮件消息转发目标用户列表的文件添加别名。
     `user name:include:包含用户名的文件路径|文件名`
   - 为接收标准输入消息的 Sendmail 命令添加别名。
     `user name:|命令`
8. 保存并关闭文件。
9. 输入 `postalias /etc/postfix/alias` 以更新别名数据库文件。
10. 输入 `service postfix restart` 以重启 postfix 服务。

#### 操作参考：配置虚拟别名

要配置虚拟别名：

1. 以 root 身份登录。
2. 配置虚拟别名的先决设置。
   a. 使用 vi 编辑器打开 `/etc/postfix/main.cf` 文件。
   b. 找到 `mydestination` 指令并定义将由邮件服务器控制的域名。
   `mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain, mail.$mydomain, www.$mydomain, /etc/postfix/mydestination`
   c. 保存并关闭文件。
   d. 使用 vi 编辑器打开 `/etc/postfix/mydestination` 文件。
   e. 输入域名列表以指定由 Postfix 控制的域名列表。mydestination 文件的示例如下所示。
   `ourglobalcompany.com`
   `ourglobalcompany.org`
   `ourglobalcompany.net`
   f. 保存并关闭文件。
3. 使用 vi 编辑器打开 `/etc/postfix/main.cf` 文件。
4. 在 `alias_maps` 变量下方定义 `virtual_alias_maps` 变量。
   `virtual_alias_maps = hash:/etc/postfix/virtual_maps`
5. 保存并关闭文件。
6. 使用 vi 编辑器打开 `/etc/postfix/virtual_maps` 文件。
7. 将电子邮件地址映射到用户名。
   `{用户名@域名} 用户名`
8. 将发往某个域名的电子邮件消息映射到另一个域名中的特定用户。
   `@域名 {用户名@域名}`
9. 将发往某个域名的电子邮件消息映射到另一个域名。
   `用户名@域名1 {用户名@域名2}`
10. 保存并关闭文件。
11. 输入 `postmap virtual_maps < virtual_maps` 以重新计算虚拟别名文件的散列。
12. 输入 `service postfix restart` 以重启 postfix 服务。

#### 操作参考：配置出站地址重写

要配置出站地址重写：

1. 以 root 身份登录。
2. 导航到 `/etc/postfix` 目录。
3. 使用 vi 编辑器打开 `main.cf` 文件。
4. 在 `alias_maps` 指令的定义下方，输入 `smtp_generic_maps = hash:/etc/postfix/generic_map` 以启用出站地址重写。
5. 保存并关闭文件。

6. 使用 vi 编辑器，创建一个名为 `generic_map` 的文件。
7. 输入 `{用户名@DomainName1} {用户名@DomainName1}`
8. 保存并关闭该文件。
9. 输入 `postmap generic_map < generic_map` 以重新生成该文件的索引。
10. 输入 `service postfix restart` 以重启 postfix 服务。

## 流程参考：配置 Postfix 限制

要配置 postfix 限制：

1. 以 root 身份登录。
2. 使用 vi 编辑器打开 `/etc/postfix/main.cf` 文件。
3. 在文件末尾，输入 `smtpd_sender_restrictions = check_sender_access hash:/etc/postfix/sender_access, [由逗号分隔的零个或多个邮件发送方限制列表]` 以定义发送方限制。
4. 输入 `smtpd_client_restrictions = check_sender_access hash:/etc/postfix/client_access, [由逗号分隔的零个或多个邮件客户端限制列表]` 以定义客户端限制。
5. 输入 `smtpd_recipient_restrictions = check_sender_access hash:/etc/postfix/recipient_access, [由逗号分隔的零个或多个邮件客户端限制列表]` 以定义接收方限制。
6. 保存并关闭该文件。
7. 导航至 `/etc/postfix` 目录。
8. 打开发送方、接收方或客户端访问文件。
9. 定义限制。
   - 输入 `DomainName RELAY` 以允许中继。
   - 输入 `DomainName OK` 以接受来自指定域的邮件消息。
   - 输入 `DomainName REJECT` 以拒绝从指定域发送的邮件消息。
   - 输入 `DomainName ERROR: (### 消息)` 以拒绝来自发送方的邮件并显示任意消息。
   - 输入 `DomainName DISCARD` 以在接受消息后将其丢弃。
10. 保存并关闭该文件。
11. 输入 `postmap 发送方或接收方或客户端访问文件 < 发送方或接收方或客户端访问文件` 以构建相应的访问数据库。
12. 输入 `service postfix restart` 以重启 postfix 服务。

## 活动 13-4

### 配置 Postfix

**开始之前：**

1. 在 srvA 上，切换到 GUI。选择 **系统**→**管理**→**网络**。在 **网络配置** 对话框中，选择 **DNS** 选项卡。
2. 在 **主机名** 文本框中，输入 *srvA.ourglobalcompany.com* 并按 **Tab** 键。将 *192.168.0.2* 设置为主 DNS 和 DNS 搜索路径。
3. 选择 **主机** 选项卡。在 **地址** 文本框中，将 *192.168.0.2* 输入为 IP 地址。在 **主机名** 文本框中，将 *srvA.ourglobalcompany.com* 输入为主机名。在 **别名** 文本框中，将 *srvA ourglobalcompany.com* 输入为别名。
4. 在 **添加 / 编辑主机条目** 对话框中，点击 **确定**。保存配置并点击 **确定** 以重启网络服务。
5. 在 srvA 上，切换到 CLI。您已在 CLI 中以 root 身份登录。显示第一个终端。在命令提示符下，输入 `service sendmail stop` 以停止 sendmail 服务。输入 `chkconfig sendmail off` 以停止在系统启动时启用 sendmail 服务。清屏。
6. 在 srvB 上，切换到 GUI。选择 **系统**→**管理**→**网络**。在 **网络配置** 对话框中，选择 **DNS** 选项卡。在 **主机名** 文本框中，输入 *srvB.ourglobalcompany.com* 并按 **Tab** 键。将 *192.168.0.2* 设置为主 DNS 和 DNS 搜索路径。
7. 选择 **主机** 选项卡。在 **地址** 文本框中，将 *192.168.0.3* 输入为 IP 地址。在 **主机名** 文本框中，将 *srvB.ourglobalcompany.com* 输入为主机名。在 **别名** 文本框中，将 *srvB* 输入为别名。
8. 在 **添加 / 编辑主机条目** 对话框中，点击 **确定**。保存配置并点击 **确定** 以重启网络服务。切换到 srvA 的 CLI。

**场景：**
您的公司已使用 Sendmail 为 ourglobalcompany.com 域实现了邮件服务器。现在，由于组织规模扩大，访问邮件服务器的用户数量增加，从而导致服务器性能下降。作为系统管理员，您决定将邮件服务器从 Sendmail 迁移到 Postfix。

| 操作 | 执行方法 |
| :--- | :--- |
| 1. 安装 Postfix。 | a. 在标记为 srvA 的系统上，安装 **postfix-2.3-2.1.el5_2.1386.rpm** 软件包。 <br> b. 输入 <br> `alternatives --set mta /usr/sbin/sendmail.postfix` 以将 Postfix 设置为默认 MTA。 |
| 2. 配置标记为 srvA 的服务器上的 incoming 邮件。 | a. 导航到 /etc/postfix 文件夹。 <br> b. 使用 vi 编辑器打开 main.cf 文件。 <br> c. 找到 “inet_interfaces = all” 一行并取消注释。 <br> d. 找到 “inet_interfaces = localhost” 一行并将其注释。 <br> e. 按 Esc 切换到命令模式。 <br> f. 找到 “#mydestination = $myhostname” 代码。 <br> g. 取消注释以下行 <br> #mydestination = $myhostname, <br> localhost.$mydomain, localhost, <br> $mydomain, 和 #mail.$mydomain, <br> www.$mydomain, ftp.$mydomain。 |
| 3. 配置标记为 srvA 的服务器上的邮件别名。 | a. 找到 “alias_maps = hash:/etc/aliases” 指令。 <br> b. 光标位于 `alias_maps = hash:` 之后。要将别名文件位置更改为 `/postfix/aliases`，将光标移动到 `/etc/` 末尾。输入 **postfix/** <br> c. 按 **Esc** 切换到命令模式。 <br> d. 找到 “alias_database = hash:/etc/aliases” 指令。 <br> e. 光标位于 `alias_database = hash:` 之后。要将别名文件位置更改为 `/postfix/aliases`，将光标移动到 `/etc/` 末尾。输入 **postfix/** <br> f. 按 **Esc** 切换到命令模式。 <br> g. 保存并关闭文件。 <br> h. 使用 **vi** 编辑器打开 aliases 文件。 <br> i. 输入 **hr: chris, pat,** <br> j. 输入 **root: jsmith** <br> k. 按 **Esc** 切换到命令模式。 <br> l. 保存并关闭文件。 <br> m. 输入 **postalias /etc/postfix/aliases** 以更新别名数据库文件。 <br> n. 启动 postfix 服务。 <br> o. 设置 postfix 服务在系统启动时运行。 |

**主题 E**
控制互联网服务

您已配置电子邮件服务。互联网提供了众多服务和优势。这使得互联网成为几乎所有组织的基本必需品。在本主题中，您将控制互联网服务。

### xinetd 守护进程

*xinetd* 守护进程控制网络上的系统服务，并基于客户端-服务器架构。*xinetd* 的配置文件列出了各种服务。当守护进程收到来自端口的特定服务请求时，它会查看配置文件，然后启动包含该服务的相应服务器。

### Telnet

**定义：**

*Telnet* 是一种终端仿真协议，允许站点上的用户模拟远程主机上的会话。

### /etc/xinetd.conf 文件

`/etc/xinetd.conf` 文件是 xinetd 守护进程的配置文件。

### 语法

在 xinetd 配置文件中指定服务的语法是 *{Attribute} {Assignment Operator} {Value}*。

### libwrap.so 库

`libwrap.so` 文件是链接到由 xinetd 守护进程控制的服务的库。

### /etc/xinetd.d 目录

`/etc/xinetd.d` 目录包含由 xinetd 管理的服务配置脚本。

### xinetd 访问控制

xinetd 守护进程拥有一组用于控制对其管理的服务访问的功能。

### 服务和应用访问控制

服务访问控制和应用访问控制本质上是守护进程，用于限制对某些重要服务和应用的访问。

### 如何控制互联网服务

**程序参考：配置由 xinetd 管理的服务**

要配置由 xinetd 管理的服务：

- 1. 以 root 身份登录。
- 2. 输入 `ls -l /etc/xinetd.d/` 列出由 xinetd 守护进程管理的服务。
- 3. 在系统启动时管理 xinetd 守护进程。
  - 输入 `chkconfig --list xinetd` 确保 xinetd 守护进程已配置为在所需的运行级别启动。
  - 输入 `chkconfig --level (levels) xinetd {on/off}` 更新 xinetd 守护进程的运行级别配置。
  - 输入 `service xinetd {start/stop/status/restart/reload}` 管理 xinetd 守护进程的状态。
- 4. 管理由 xinetd 守护进程控制的服务。
  - 输入 `chkconfig {Service Name} {on/off}` 在系统启动时启用或禁用指定服务。

## 操作参考：在 /etc/xinetd.conf 文件中定义全局设置

要在 `/etc/xinetd.conf` 文件中定义全局服务设置：

- 以 root 用户登录。
- 输入 `vi /etc/xinetd.conf` 以编辑 xinetd 守护进程配置文件。
- 编辑 `{Attribute}`（属性） `{Assignment Operator}`（赋值运算符） `{Value}`（值） `{Value}`（值）以定义由 xinetd 守护进程管理的所有服务的全局设置。
- 保存并关闭文件。
- 输入 `service xinetd restart` 以应用更改。

### 操作参考：配置 xinetd 管理服务的访问控制

要配置 xinetd 管理服务的访问控制：

- 以 root 用户登录。
- 在 `/etc/xinetd.conf` 文件中定义特定于服务的访问控制。
  - 输入 `vi /etc/xinetd.d/{Service Configuration File}` 以编辑特定于服务的配置文件。
  - 输入 `only_from = {List of IP Addresses}` 以定义该特定服务可用的远程主机。
  - 输入 `no_access = {List of IP Addresses}` 以定义该特定服务不可用的远程主机。
  - 输入 `access_times = hour: min-hour: min` 以定义服务可被访问的时间间隔。
- 保存并关闭文件。
- 输入 `service xinetd restart` 以应用更改并重启 xinetd 守护进程。

## 活动 13-5
### 启用服务访问控制

**准备工作：**

- 在 srvA 上，您已以 root 身份在 CLI 中登录。
- 切换到 CLI 的第一个终端。
- 输入 `cd /root` 以导航到根目录。
- 输入 `clear` 以清屏。

## 第 13 课后续

在本课中，您配置了 Apache Web 服务器，为 Apache 和代理服务器实施了访问控制，配置了邮件服务，并控制了互联网服务。

## 第 14 课 保护 Linux

**课时：** 1 小时 30 分钟

### 课程目标：

在本课中，您将实施保护 Linux 的措施。

### 主题 A
#### 检查系统安全的基础

### 密钥

密钥是一个信息块，用于授权用户访问数据。

### 身份验证

*身份验证*用于核实用户是否确实是其声称的身份。

### 身份验证要素

通过身份验证展示用户身份所使用的要素数量，决定了身份验证的有效性。

## 生物特征身份验证

为了提高系统的可靠性和用户的易用性（超越密码身份验证），可以引入生物特征身份验证。

## sshd_config 文件

`sshd_config` 文件包含用于在不可靠网络上启用主机之间加密通信的选项。

## 加密

加密是一种通过配置数据使其表现为未经授权用户无法解读的代码，从而控制用户访问信息的方法。

### 加密解决方案

加密计算机数据的授权用户必须拥有用于加密数据的密钥，才能对其进行解密。

### 随机数生成

**随机数生成**是一种加密方法，其中内核用于在传输之前为文件生成分配随机数。

## 加密散列

加密散列用于一种加密方法，其中任意数据被封装在指纹中，该指纹附加到文件上。

## 对称加密

对称加密仅使用单个密钥进行，该密钥用于加密和解密。

## 1. 实用工具

| 实用工具 | 功能 |
| :--- | :--- |
| `openssl` | 用于通过创建密钥、证书和签名，使用 SSL 协议加密和解密消息。该实用工具的语法为 `openssl {command} [options] [arguments]`。 |
| `make` | 用于生成数字证书和密钥对。此命令必须从 `/etc/pki/tls/certs/` 目录运行。`make` 实用工具的语法为 `make {key_file/digital_certificate}`。 |

## 2. 非对称加密
*非对称加密*是通过对密钥对中的两个密钥进行操作来实现的。

### 3. 协议说明

| 协议 | 说明 |
| :--- | :--- |
| 协议 1 | 在协议 1 中，发送方和接收方之间仅交换一个密钥。 |
| 协议 2 | 在协议 2 中，数字签名与密钥加密一起使用。 |

### 4. 非法公钥

非法公钥是由未经授权的用户生成的，用于绕过公钥密码学。

### 5. 数字证书类型

数字证书是一种对称加密方法。数字证书主要有两种类型。

### 6. 软件包完整性

Linux 中的每个软件包都被分配一个公钥，该公钥随软件包一起安装。

| 命令 | 允许你执行的操作 |
| :--- | :--- |
| `rpm --verify` *package name* | 验证软件包是否已安装。 |
| `gpg --import */etc/pki/rpm-gpg/RPM-GPG-KEY-redhat*` | 将公钥导入到 rpm 数据库中。 |
| `rpm --checksig` *package name* | 检查软件包是否具有有效签名。 |
| `rpm --addsig` *package name* | 为软件包分配有效签名。 |

### 7. RADIUS
远程认证拨号用户服务（RADIUS）是一种客户机/服务器协议，用于促进通过网络进行集中式的认证、授权和计费。

### 8. RADIUS
远程认证拨号用户服务（RADIUS）是一种客户机/服务器协议，用于促进通过网络进行集中式的认证、授权和计费。

### 9. 作为网络访问服务器的 RADIUS 服务器

当网络中包含多个远程访问服务器时，你可以将其中一个服务器配置为 RADIUS 服务器，并将所有其他服务器配置为 RADIUS 客户端。

### 10. 如何实现加密服务

#### 10.1 操作参考：配置加密
要配置加密：

1.  以 root 身份登录。
2.  输入 `vi /etc/{application}/{configuration file}` 打开文件。
3.  定位包含加密详情的行。
4.  如有必要，取消该行的注释。
5.  修改该行以更改加密类型。
6.  保存文件并退出编辑器。
7.  重新启动应用程序或设备的服务，以使更改生效。

#### 10.2 操作参考：实施密码服务
要实施密码服务：

1.  以 root 身份登录。
2.  实施密码服务。
    -   输入 `openssl rand` *Options* *Number of pseudo-random bytes* 生成一个随机数。
    -   或者，生成一个消息摘要。
    -   输入 `sha1sum [command options] {File Name}` 计算并检查 SHA1 消息摘要。
    -   输入 `md5sum [command options] {File Name}` 计算并检查 MD5 消息摘要。
    -   输入 `openssl dgst {Message digest options} {File Name}` 输出所提供文件的消息摘要。

#### 10.3 操作参考：使用 rpm 命令验证软件包完整性
要使用 `rpm` 命令验证文件完整性：

1.  以 root 身份登录。
2.  验证软件包完整性。
    -   输入 `rpm --verify {Package Name}` 报告与原始 rpm 版本不同的文件。
    -   输入 `rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-*` 导入 GPG 密钥以将其添加到软件包中。
    -   输入 `rpm --checksig {Package Name}` 验证 rpm 软件包是否由 Red Hat 打包。

#### 10.4 操作参考：生成数字证书
要生成数字证书：

1.  以 root 身份登录。
2.  使用 `openssl` 命令生成密钥。
    -   A. 输入 `openssl genrsa -out {Absolute or relative path of key file} {Key size}` 生成公钥或私钥对。
    -   B. 输入 `openssl req -new -key {Absolute or relative path of...`

## 主题 B：保护用户账户

你现在已熟悉加密和基础系统安全。你需要为用户提供安全的计算环境。在本主题中，你将保护用户账户。

### 环境文件

在 Linux 中，有几个可以自定义的环境文件。

| 文件 | 描述 |
| :--- | :--- |
| /etc/hosts.allow | 允许访问某些服务和主机。 |
| /etc/hosts.deny | 拒绝访问某些服务和主机。 |
| /etc/limits | 当系统安装了影子密码时，限制用户的资源。 |
| /etc/login.defs | 在具有影子密码的系统上设置用户登录功能。 |
| /etc/passwd | 显示用户的用户名、真实姓名、主目录、加密密码和其他信息。 |
| /etc/security | 标识 root 用户允许从中登录的安全终端。 |
| /var/log/secure | 跟踪用户登录。建议定期检查此文件。 |

### /etc/login.defs 文件

* /etc/login.defs* 文件与影子密码一起使用，用于设置初始路径和其他参数。

### 登录级别

在 Linux 中，你可以提供 root 级别或用户级别对资源的访问权限。

### Root 用户的别名

如果你使用的是 Bash shell，你可以将 root 创建为一个别名，作为一种预防措施。

### su 命令

*替代或切换用户* 命令 (*su*) 用于更改登录会话的所有权，而无需注销。

## 登录 Shell 与非登录 Shell

登录 Shell 是在用户登录期间创建的 Shell。

## id 命令

您可以使用 `id` 命令查看用户身份。

## sudo 命令

超级用户 do (sudo) 命令允许用户以 root 用户的安全权限运行程序。

### 语法

`sudo` 命令的语法是 *sudo command-name command-options*。

### 密码策略

*密码策略* 是一组指导原则，有助于形成有效的密码。

## 如何保护用户账户

**操作参考：以超级用户身份执行命令**

要以超级用户身份执行命令：

1. 以非 root 用户身份登录。
2. 输入 *sudo* (*需要 root 访问权限的命令*) 以超级用户身份运行该命令。
3. 输入超级用户或该用户的密码。
4. 观察命令已被执行。

**操作参考：禁用 Telnet 和 FTP 服务的 Root 访问**

要禁用 Telnet 和 FTP 服务的 root 访问：

1. 以 root 身份登录。
2. 禁用 Telnet 服务的 root 访问。
   - 在任何编辑器中打开 *etc/security* 文件。
   - 删除 *tty0*–*tty9* 条目。
   - 保存文件。
   - 如有必要，重启 Telnet 服务。
3. 禁用 FTP 服务的 root 访问。
   - 在任何编辑器中打开 *etc/vsftpd/ftpusers* 文件。
   - 删除 root 条目。
   - 保存文件。
   - 如有必要，重启 vsftpd 服务。

# 主题 C

## 启用防火墙功能

您已保护用户账户作为网络安全防御的一个级别。现在，您将研究数据包过滤，以为路由器、网关和 Linux 服务器及工作站提供防火墙功能。在本主题中，您将实施 iptables 通过数据包过滤提供防火墙功能。

### 防火墙

**定义：**
防火墙是一种软件程序或硬件设备，通过阻挡未经请求的流量来保护系统或网络免受未授权访问。

### 软件防火墙

“防火墙”一词通常用于指基于软件的防火墙。

## 硬件防火墙

硬件防火墙是一种硬件设备，可以是独立设备，也可以集成在大多数路由器中，用于保护私有网络中的计算机免受未经授权流量的侵害。

## 防火墙定位

防火墙可以逻辑上放置在内部网络与外部世界之间。

### 数据包过滤

*数据包过滤*是在检查每个数据包的预定义内容（例如 IP 地址）后，传递或阻止入站和出站数据包的过程。

## 代理服务器实现

代理服务器，也称为应用网关，是一种比纯数据包过滤器更安全且更灵活的防火墙解决方案。

## iptables 程序

**定义：**

*iptables* 程序是 Linux 中的一个防火墙程序，为内部网络提供保护。

**语法**

*iptables* 程序的语法为 `iptables [-t table] {commands} {chain/rule specification} [options/parameters]`。

### ipchains 程序

*ipchains* 程序是一个用于在 Linux 服务器上管理数据包过滤的 Linux 工具。

## iptables 和 ipchains

*ipchains* 和 *iptables* 之间的一个区别在于，*iptables* 可以配置为有状态数据包过滤器。

## 语法

要检查 *ipchains* 的安装状态，请使用命令 `rpm -q iptables`。

## ipchains 的使用

*ipchains* 用于阻止对 Linux 服务器特权端口的访问。

## 如何实施 iptables

### 程序参考：配置 iptables

要配置 iptables：

1. 以 root 身份登录。
2. 输入 `service iptables start` 以启动 `iptables` 服务。
3. 输入 `chkconfig iptables on` 以在系统启动时自动启动 `iptables` 服务。
4. 使用 `iptables` 管理规则。
   - 输入 `iptables -A forward -p icmp -j ACCEPT` 以添加规则。
   - 输入 `iptables -D forward -p icmp -j ACCEPT` 以删除规则。

## 主题 D

# 实施安全审计

你已实施 iptables 以使 Linux 工作环境对用户更安全。你需要设置文件和身份验证审计，以便识别和追踪可能的安全漏洞。在本主题中，你将实施安全审计。

### 如何实施安全审计

### 程序参考：实施安全审计

要实施安全审计：

1. 使用 `iptables` 命令将 `iptables` 设置为将可能的入侵发送到日志文件。
2. 输入 `service iptables save` 命令以保存 `iptables` 规则。
3. 将 `iptables` 的输出重定向到 `/var/log/iptables` 文件。

## 主题 E

### 检测入侵

你已实施安全审计。为了保护包含机密数据的文件，你需要持续监控网络。在本主题中，你将实施一个入侵检测系统。

### 网络监控实用工具

有各种实用工具可用于监控网络设备及其连接的系统。

| 工具 | 用于 |
| :------ | :------ |
| nmap | 扫描整个网络的各种端口及其上运行的服务及其状态。 |
| tcpdump | 从发送到网络接口的查询字符串中获取数据包信息。 |
| wireshark | 获取数据包信息。它是一个基于 GUI 的实用工具。 |

### 入侵检测系统

**定义：**
*入侵检测系统 (IDS)* 是一种保护门户、网络和文件免受黑客攻击的安全传感器。

**示例：Snort**
Snort 是一种监控网络上每个数据包的 IDS。

### 被动式和主动式 IDS

IDS 可以是被动式的或主动式的。

### Tripwire

**定义：**
*Tripwire* 是一种入侵检测工具，它将文件或目录的内容与包含该文件或目录位置及修改日期的数据库进行比较。

### Tripwire 数据库

*Tripwire 数据库* 包含基线，即在特定时间记录的文件和目录的快照。

### tw.cfg 文件

`tw.cfg` 文件是 Tripwire 配置文件。

### Snort

**定义：**
Snort 是一种监控网络流量的网络 IDS。

#### Snort 选项

下表列出了 snort 命令的一些常用选项。

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `-v` | 以详细模式运行 Snort。 |
| `-i interface` | 监听特定接口上的数据包。 |
| `-l directory` | 指定输出日志目录。 |
| `-n number of packets` | 指定退出前要处理的数据包数量。 |
| `-D` | 以守护进程模式运行 Snort。 |

## Portsentry

**定义：**

*Portsentry* 是一种能够检测和响应端口攻击的入侵检测系统（IDS）。

**示例：**

## Nessus

**定义：**

*Nessus* 是一种用于审计远程主机安全以及网络上运行服务的入侵检测系统（IDS）。

## 如何检测入侵

### 参考步骤：安装 Tripwire

要在 Linux 服务器上安装 Tripwire：

- 1. 在 Linux 服务器上，以 root 身份登录。
- 2. 从 http://sourceforge.net/projects/tripwire/files/ 下载 tripwire-2.4.1.2-src.tar.bz2 文件。
- 3. 将下载的文件复制到 `/etc/` 目录。
- 4. 输入 `bunzip2 tripwire-2.4.1.2-src.tar.bz2` 以解压缩文件。
- 5. 输入 `tar -xvf tripwire-2.4.1.2-src.tar` 以解压文件。
- 6. 导航至 `/etc/tripwire-2.4.1.2-src` 目录。
- 7. 输入命令 `sed -i -e 's@TWDB="$prefix"@TWDB="/var@' install/install.cfg` && `.configure --prefix=/usr --sysconfdir=/etc/tripwire && make` 以将 Tripwire 数据库和报告安装在 `/var/lib/tripwire` 目录中。
- 8. 输入 `make install && cp -v policy/*.txt /usr/doc/tripwire` 以创建 Tripwire 安全密钥，安装二进制文件，并将 Tripwire 示例策略文件复制到程序文档目录中。
- 9. 查看并同意协议以继续安装。

### 参考步骤：配置 Tripwire

要配置 Tripwire：

- 1. 导航至 `/etc/tripwire` 目录。
- 2. 如有必要，编辑 `twcfg.txt` 文件以修改 Tripwire 文件的位置并自定义其设置。
- 3. 如有必要，编辑 `twpol.txt` 文件。

## 加密密钥

Tripwire 使用加密密钥对配置、策略、数据库和报告文件进行加密。

## 参考步骤：检查文件完整性

要检查由 Tripwire 监控的文件完整性：

- 1. 运行完整性检查，以确定由 Tripwire 监控的文件是否有任何更改。
  - `/usr/sbin/tripwire --check`
- 2. 查看由完整性检查生成的报告。
  - `/usr/sbin/twprint -m r --twrfile /var/lib/tripwire/report/file name.twr`

## 参考步骤：更新 Tripwire 数据库

要更新 Tripwire 数据库：

- 1. 使用 tripwire 命令配合最新的报告。
  - `/usr/sbin/tripwire --update --twrfile /var/lib/tripwire/report/latest report.twr`
- 2. 报告将在默认文本编辑器中显示。添加或移除文件名中的 "x" 字符，以将您希望包含或排除在 Tripwire 数据库中的文件包含或排除。
- 3. 保存并关闭文件。
- 4. 根据提示，输入用于签署数据库文件的密码。

## 参考步骤：更新 Tripwire 策略文件

要更新 Tripwire 策略文件：

- 1. 重新生成 twpol.txt 文件。
  - `/usr/sbin/twdadmin --print-polfil e > /path/twpol.txt`
- 2. 生成新的策略文件。
  - `/usr/sbin/twdadmin --create-polfi le -S site.key /path/twpol.txt`
- 3. 删除现有的 Tripwire 数据库并创建另一个数据库。
  - `rm /path/domainname.twd`
  - `/usr/sbin/tripwire --init`
- 4. 手动运行完整性检查并查看报告，以验证数据库是否已创建。
  - `/usr/sbin/tripwire --check`
  - `/usr/sbin/twprint -m r --twfil e /var/lib/tripwire/report/file name.twr`

## 更新 Tripwire

您可以访问 http://sourceforge.net/projects/tripwire 网站以获取有关最新安全更新和错误修复的信息。

## 参考步骤：实施 Portsentry

要实施 Portsentry：

- 1. 从互联网获取 Portsentry 源文件。
- 2. 解压源文件。
  - `gunzip portsentry-{version}.{release}.tar.gz`
  - `tar xvf portsentry-{version}.{release}.tar`
  - `cd portsentry_beta`
- 3. 阅读 README.install 文件。
- 4. 安装源代码。
  - `make`
  - `make install`
- 5. 如有必要，在 /usr/local/portsentry/portsentry.conf 文件中，指定要扫描的 TCP 或 UDP 端口。

## 参考步骤：实施 Snort

要实施 Snort：

- 1. 在 Linux 服务器上，以 root 身份登录。
- 2. 挂载包含 Snort RPM 的 Linux 安装介质。
- 3. 导航至 /media/介质名称/Packages 目录。
- 4. 安装 Snort RPM。
  - `rpm -ivh snort-(version),(release).rpm`
- 5. 启动 Snort IDS。
  - `service snortd start`
- 6. 使用 snort 命令选项来检测网络入侵。
  - `snort Snort 选项`

## 更新 Snort

您可以访问 http://www.snort.org/vrt/ 网站以下载最新的 Snort 规则，保护您的系统免受新发现的漏洞攻击。

## 参考步骤：使用 nmap 扫描端口

要使用 nmap 扫描端口：

- 1. 安装 nmap RPM 文件。
  - `rpm -ivh nmap-(version),(release).rpm`
- 2. 使用 nmap 命令查看有关开放端口的信息。
  - `nmap IP 地址`

## nmap 命令选项

下表给出了一些常用的 nmap 命令选项。

| 使用此选项 | 以此执行此操作 |
|---|---|
| sT | 扫描 TCP 端口 |
| sU | 扫描 UDP 端口 |
| p 端口范围 | 扫描特定端口 |
| F | 仅在 nmap-services 文件中搜索，该文件包含有关端口的信息 |

## 参考步骤：实施 Nessus

要实施 Nessus：

- 1. 以 root 身份登录。
- 2. 从 http://www.nessus.org/download/ 下载 nessus-{version},{release}.rpm 包。
- 3. 安装 Nessus RPM。
  - `rpm -ivh nessus-{version},{release).rpm`

## 14. 保护 Linux
### 使用 Tripwire 检测入侵

**数据文件：**
tripwire-2.4.1.2-src.tar.bz2

## 15 管理硬件

课时：2 小时 10 分钟

## 课程目标

在本课中，你将管理 Linux 机器相关的硬件。

## 主题 A

### 识别常见的硬件组件和资源

市场上有各种计算机硬件和外围组件。然而，并非所有组件都与 Linux 兼容。

### 硬件组件

Linux 系统的基本硬件组件包括中央处理器（CPU）/浮点单元（FPU）处理器、硬盘、内存、网络适配器和视频卡。

### 硬件资源

硬件资源，如 IRQ、DMA、内存地址和小型计算机系统接口（SCSI）ID，可能会导致 Linux 系统中的系统配置冲突。

### SCSI 类型

SCSI 发音为 “skuzzy”，是一组将外围设备连接到计算机的标准。

| SCSI 类型 | 总线宽度和最大吞吐量 |
|---|---|
| SCSI-1 | 8 位，5 MB/秒 |
| Wide SCSI | 16 位，10 MB/秒 |

## SCSI ID

每个 SCSI 设备都有一个唯一的 SCSI ID（也称为 SCSI 地址）分配给它。

### IRQ 设备说明

检查非即插即用设备的 IRQ 地址，以确保没有冲突。

### 磁盘空间跟踪

`df` 和 `du` 命令有助于磁盘空间跟踪。

## 如何识别常见的硬件组件和资源

### 操作参考：识别硬件组件和资源

要识别硬件组件和资源：

- 以 root 身份登录。
- 切换到 `/proc` 目录。
- 记录硬件组件以供将来参考。
  - 使用 `cat cpuinfo` 命令显示 CPU 信息。
  - 使用 `cat devices` 命令显示设备信息。
  - 使用 `cat partitions` 命令显示分区信息。
  - 使用 `df -h` 命令显示当前硬盘大小和使用情况。
  - 使用 `cat interrupts` 命令显示当前 IRQ 资源。

## 主题 B
### 配置电源管理

您已识别出可用于 Linux 系统的硬件组件和资源。

### 电源管理

高效的电源管理需要硬件和软件解决方案的结合。

| 解决方案 | 描述 |
| :--- | :--- |
| **高级电源管理 (APM)** | APM 读取 `/proc/apm` 文件，其中提供了电池状态信息。 |
| **高级配置与电源接口 (ACPI)** | ACPI 规范为 APM 提供了替代方案。 |
| **不间断电源 (UPS)** | UPS 执行三项主要功能。 |

**apmd**

高级电源管理守护进程（apmd）是一个监控守护进程，用于控制 APM 系统。

### ACPI 功能领域

ACPI 规范涵盖了各种功能领域。

### ACPI 电池管理

电池管理策略涵盖 APM BIOS 和 ACPI 操作系统。

### 改变电池行为

操作系统可能会选择改变电池的行为。

# apcupsd 包

`apcupsd` 包是一个提供 UPS 电源管理功能的软件包。

# apcupsd.conf 文件

`apcupsd.conf` 文件是 apcupsd 包与 UPS 通信所需的配置文件。

# 系统电源状态

Linux 系统可能支持多种电源状态。

# 如何配置电源管理

**操作步骤参考：配置 CPU 电源管理**

要配置 CPU 电源管理：

1. 切换到 `/proc/acpi/processor/CPU{CPU 编号}` 目录。
2. 使用 `cat info` 命令验证电源管理和降频功能是否已开启。
3. 使用 `cat power` 命令显示当前电源设置。
4. 验证您的机器是否有适当的可用状态。
5. 使用 `cat throttling` 命令显示当前降频设置。
6. 输入 `echo -n [throttle_state] > throttling` 命令以调整降频级别。

# 降频技术

这是一种技术，通过该技术使系统以低于其最大容量的能力运行，目的是节省电力。

# 主题 C

# 配置可移动硬件

您已处理了必要的电源管理选项。

# 可移动硬件

Linux 系统允许您利用可移动设备。

| 设备 | 示例 |
| :--- | :--- |
| 输入 | 键盘、指点设备、摇杆、扫描仪、网络摄像头、数位板和数码相机 |
| 网络 | 调制解调器和网卡 |
| 输出 | 打印机、声卡和扬声器 |
| 存储 | CD、DVD、磁带驱动器、软盘、zip 驱动器、闪存驱动器和硬盘驱动器 |

# PC 卡

PC 卡， formerly 被称为 PCMCIA，尺寸与信用卡相当。

# PCMCIA 组织

PCMCIA 组织是一个成员联盟，旨在促进便携式计算机之间的互换性和兼容性。

# 卡和插槽服务

当便携式计算机启动时，卡和插槽服务会被加载到内存中。

# cardmgr 实用工具

`cardmgr` 实用工具监控 PCMCIA 插槽中的卡片插入和移除事件。

## 任意命令

基于 PCMCIA 卡片配置数据库的内容，`cardmgr` 实用工具在适当卡片插入或移除时也可能执行任意命令。

## pcmcia 文件

存储在 `/etc/pcmcia/config` 目录中的 pcmcia 文件是一个卡片配置数据库。

### 固定文件更新

每当插入或弹出卡片，或者当 `cardmgr` 工具接收到信号时，`stab` 文件都会由 `cardmgr` 工具进行更新。

### pccardctl 工具

`pccardctl` 工具取代了 `cardctl` 工具。

| 命令 | 描述 |
| :--- | :--- |
| `status` | 显示当前插槽的状态标志。 |
| `config` | 显示插槽配置，包括电源设置、中断和 I/O 窗口设置以及配置寄存器。 |

### 选择 PCMCIA 配置方案

你可以使用 `cardctl` 工具从多个 PCMCIA 配置方案中进行选择。

### USB

通用串行总线 (USB) 是一种硬件接口标准，旨在为众多外设提供连接。

### USB 标准

USB 2.0 是最常用的标准，其通信速率最高可达 480 Mbps。

### USB 即插即用功能

USB 设备还集成了即插即用技术，该技术允许设备在连接建立后立即进行自配置。

### 内核支持

在使用 USB 设备时，请确保你拥有包含 USB 支持的内核。

### Linux 中的 USB

Linux 将 USB 设备视为 SCSI 磁盘，将第一个设备注册为 `/dev/sda`。

### FireWire

*FireWire* 是符合 IEEE 1394 标准的高速串行总线，类似于 USB。

### FireWire 电缆

在 FireWire 电缆中，电气触点位于 IEEE 1394 电缆连接器的结构内部。

### 1394 子系统核心

1394 子系统的核心是一个模块，它管理高级和低级驱动程序。

### 回环设备

Linux 系统中的回环设备允许你将文件或一组文件作为块设备访问。

### 如何配置可移动硬件

**步骤参考：配置 USB 硬件**

要配置 USB 硬件：

- 1. 验证系统内核版本为 2.4 或更高。
- 2. 验证已创建 `/proc/bus/usb` 目录。
- 3. 安装设备的驱动程序。
- 4. 插入设备。

**步骤参考：配置 PCMCIA 硬件**

要配置 PCMCIA 硬件：

- 1. 检查内核中是否已编译 PCMCIA 模块。
- 2. 验证已创建 `/etc/pcmcia/config.opts` 文件。
- 3. 安装该设备所需的任何驱动程序。
- 4. 插入设备。
- 5. 使用 `cardmgr` 工具配置设备。

### 主题 D

### 配置大容量存储设备

你已为 Linux 系统添加了可移动硬件。

### 大容量存储设备

硬盘或固定磁盘是一种存储设备，它们能在一个小而相对可靠的物理包中提供对大量数据的快速访问。

| 设备 | 描述 |
| :--- | :--- |
| *Zip* | 早于闪存盘的便携式存储设备。 |
| *Flash drive* | 提供与 CD-ROM 相同优势的便携式存储设备。 |
| *Optical disc* | CD-RW 是一种可重写紧凑型光盘 (CD) 格式。 |

### ATAPI

*AT 附加包接口 (ATAPI)* 是一种用于控制大容量存储设备的协议。

### RAID

**定义：**

*独立磁盘冗余阵列 (RAID)* 是一种方法，用于在服务器或独立磁盘存储系统的多个硬盘的不同位置存储相同的数据。

## RAID 级别

RAID 可以根据系统要求以不同的级别实现。

| **RAID 级别** | **描述** |
| :--- | :--- |
| RAID 0 | RAID 0 通常被称为数据条带化。 |
| RAID 1 | RAID 1 通常被称为磁盘镜像。 |
| RAID 5 | RAID 5 是 RAID 4 的改进级别。 |

## 软件 RAID

**定义：**

*软件 RAID* 是应用于内核磁盘代码并使用软件实现的 RAID。

**硬件 RAID 与软件 RAID**

硬件 RAID 系统是使用磁盘控制器卡实现的。

## mdadm 工具

`mdadm` 工具用于管理 RAID 设备。

| 选项 | 用途 |
| :----- | :----- |
| -A | 组装之前创建的阵列的组件。 |
| -B | 构建无超级块的阵列。 |
| -C | 创建 RAID 阵列。 |

### 语法

`mdadm` 工具的语法为 `mdadm {模式} {RAID 设备} [选项] {组件设备}`。

### mdadm 操作模式

`mdadm` 实用程序有几种操作模式。

## 如何配置大容量存储设备

### 操作参考：配置软件 RAID

要配置软件 RAID：

1. 在 CLI 中以 root 身份登录。
2. 输入 `rpm -qi mdadm` 以确保已安装 RAID 软件包。
3. 创建软件 RAID。
    a. 创建 RAID 0 阵列。
        - 输入 `mdadm --create --verbose /dev/md{device_number} --level=0 --raid-devices=2 /dev/{device_name}{device_number} /dev/{device_name}{device_number}` 以创建 RAID 0 阵列。
    b. 创建 RAID 1 阵列。
        - 输入 `mdadm --create --verbose /dev/md{device_number} --level=1 --raid-devices=2 /dev/{device_name}{device_number} /dev/{device_name}{device_number}` 以创建 RAID 1 阵列。
    c. 创建 RAID 5 阵列。
        - 输入 `mdadm --create --verbose /dev/md{device_number} --level=5 --raid-devices=3 /dev/{device_name}{device_number} /dev/{device_name}{device_number} /dev/{device_name}{device_number}` 以创建 RAID 5 阵列。
4. 输入 `mdadm --detail --scan > /etc/mdadm.conf` 以创建包含 RAID 阵列信息的 RAID 配置文件。
5. 输入 `vi /etc/mdadm.conf` 以打开 `/etc/mdadm.conf` 文件并指定设备信息。
6. 输入 `mkfs -t {filesystem_type} /dev/md{device_number}` 以在 RAID 磁盘上创建文件系统。
7. 创建挂载点并挂载 RAID 磁盘。
8. 输入 `cat /proc/mdstat` 以验证 RAID 磁盘是否已创建。
9. 输入 `mdadm -S /dev/md{device_number}` 以停止或停用 RAID 服务。
10. 输入 `mdadm -AS /dev/md{device_number}` 以启动或激活 RAID 服务。
11. 输入 `mdadm -E /dev/{device_name}{device_number}` 以检查设备名称信息。

## 主题 E

# 使用逻辑卷管理器管理逻辑卷

你已添加了新的存储设备以在 Linux 系统上存储大量数据。

## LVM

**定义：**
*逻辑卷管理器（Logical Volume Manager，LVM）* 是一种用于管理计算机系统中磁盘存储的软件工具。

## LVM 组件

LVM 包含五个主要组件。

| 组件 | 描述 |
| :--- | :--- |
| 卷组（VG） | VG 组件是 LVM 中最高级别的抽象。 |
| 物理卷（PV） | PV 是一种用于管理目的并带有额外数据的物理介质。 |

## LVM 架构

在存储驱动器中，每个 PV 被划分为大小相等的 PE。

## LVM 管理工具

LVM 包含许多执行各种功能 的工具。

| 工具 | 用于 |
| :--- | :--- |
| lvcreate | 创建 LV。 |
| lvdisplay | 显示有关 LV 的信息。 |
| lvextend | 为 LV 添加空间。 |

## 语法

使用 LVM 工具的语法为：*{工具名称} {磁盘分区}*。

## LVM 快照

在系统崩溃的情况下，可以使用 LVM 快照来恢复文件系统。

## 快照卷

快照卷是一个包含在创建快照时卷内存在的数据记录的卷。

## 如何使用逻辑卷管理器管理逻辑卷

**操作参考：使用逻辑卷管理器创建逻辑卷**

若要使用逻辑卷管理器创建逻辑卷：

1. 在 CLI 中以 root 身份登录。
2. 输入 `fdisk /dev/{设备名称}{设备编号}`。
3. 创建类型为 LVM 的分区。
   - a. 输入 `n` 并按 **Enter** 键。
   - b. 输入 `p` 并按 **Enter** 键。
   - c. 输入 `1` 并按 **Enter** 键。

## 操作参考：使用 LVM 工具调整逻辑卷大小

若要使用 LVM 工具调整逻辑卷大小：

1. 以 root 身份登录。
2. 输入 `pvcreate /dev/{设备名称}(设备编号)` 创建物理卷。
3. 输入 `vgextend {卷组名称} /dev/{设备名称}(设备编号)`，将分区添加到现有卷组。
4. 输入 `lvextend -L +{大小} /dev/{卷组名称}/{逻辑卷名称}` 扩展文件系统。
5. 输入 `resize2fs /dev/{卷组名称}/{逻辑卷名称}` 调整文件系统大小。

## 操作参考：管理 LVM 快照

若要管理 LVM 快照：

1. 以 root 身份登录。
2. 输入 `lvcreate -L {大小} -s {快照卷名称} /dev/{卷组名称}/{逻辑卷名称}` 创建卷的快照。
3. 输入 `mount /dev/{卷组名称}/{快照卷名称} {挂载点}` 挂载快照卷。
4. 删除快照卷。
    a. 输入 `umount {挂载点}` 卸载快照卷。
    b. 输入 `lvremove /dev/{卷组名称}/{快照卷名称}` 删除快照卷。

## 主题 F

## 配置磁盘配额

您已管理了文件服务器上的磁盘空间。

### 磁盘配额

**定义：**

*磁盘配额* 是为计算机上用户文件存储分配的磁盘空间。

**示例：**

### 配额管理命令

配额管理是对所有用户配额的有效分配和监控。

| 命令 | 用于 |
| :--- | :--- |
| edquota -u (用户名) | 编辑特定用户的配额。 |
| edquota -g (组名) | 编辑特定组的配额。 |

### 配额报告

配额报告是由系统创建用于查看每个用户的磁盘空间使用情况的。

### quotacheck 命令

`quotacheck` 命令检查启用了配额的文件系统，构建当前磁盘使用表，并更新 `aquota.user` 文件。

## 配额报告生成命令

有一些命令可用于生成有效的配额报告。

| 命令 | 允许您 |
| :--- | :--- |
| repquota -a | 显示所有用户的配额报告。 |
| repquota -u {文件系统名称} | 显示特定文件系统的配额报告。 |

## 如何配置磁盘配额

### 操作参考：为文件系统设置磁盘配额

要为文件系统设置磁盘配额：

1. 以 root 身份登录到 CLI。
2. 指定您要分配给用户的分区的用户配额。
   1. 输入 `vi /etc/fstab`。
   2. 在分区条目的第四列中，更改默认值。
      - 将 `defaults` 更改为 `defaults,usrquota` 以定义指定分区的用户配额。
   3. 保存并关闭文件。
3. 输入 `mount -o remount {挂载点}` 以重新挂载该分区。
4. 输入 `quotacheck -c {分区挂载点}` 以扫描磁盘使用情况并创建配额文件。

### 操作参考：管理系统中的配额服务

要管理系统中的配额服务：

1. 以 root 身份登录到 CLI。
2. 管理系统中的配额服务。
   - 输入 `quotaon [命令选项] {挂载点}` 以开启配额。
   - 输入 `quotaoff [命令选项] {挂载点}` 以关闭配额。

### 操作参考：为用户设置配额

要为使用者设置配额：

1. 以 root 身份登录到 CLI。
2. 为用户设置配额。
   - 使用 `edquota` 命令设置用户配额。
     1. 输入 `edquota [命令选项] {用户或组名}`。
     2. 指定块和 inode 的软限制和硬限制。
     3. 保存并关闭文件。

### 操作参考：查看配额报告

要查看配额报告：

1. 以 root 身份登录到 CLI。
2. 查看配额报告。
   - 输入 `quota [命令选项] {用户或组名}` 以显示用户或组的配额报告。
   - 输入 `repquota [命令选项] {挂载点}` 以显示指定挂载点的配额报告。

## 16
## 排除 Linux 系统故障

**课时时长：** 1 小时

## 课程目标：

在本课中，您将排除 Linux 系统问题。

## 主题 A

# 排除基于系统的问题

您管理了组成 Linux 系统的硬件设备。

## 故障排除策略

故障排除策略是识别系统相关问题原因并解决其影响的行动计划。

| 准则 | 描述 |
| --- | --- |
| 分析问题 | 在尝试排除问题之前，尝试通过其症状（如错误消息）来识别问题。 |
| 备份数据 | 在实验配置文件之前，建议进行备份。 |

### 基本故障排除模型

一些公司开发了系统且合乎逻辑的故障排除流程。

## Linux 救援环境

Linux 救援环境是一个独立的 Linux 程序，用于排查损坏的 Linux 安装问题。

## chroot 模式

`chroot` 模式将 `/root` 目录转移到一个不同的位置以便恢复。

## 救援环境实用工具

救援环境中提供了一组用于排查不同问题的实用工具。

## 环境配置问题

配置问题可能会阻止用户登录系统并访问服务器提供的服务。

## 核心系统变量

核心系统变量会影响应用程序和命令的行为。

| 使用此变量 | 如果需要指定 |
| :--- | :--- |
| `HOSTNAME=Hostname` | 系统的主机名。 |
| `SHELL=Shell path` | 系统的 Shell 路径。 |

## 单用户模式

Linux 中的单用户模式可以通过将运行级别更改为 1 来初始化。

## 启动磁盘

**定义：**

启动磁盘是包含操作系统文件（如 `init`、`klogd` 和 `syslogd`）以启动系统的磁盘。

## 内存盘 (Ramdisk)

内存盘是分配并用作分区的一部分内存。

## Ramdisk Word 关键字

Ramdisk word 关键字是一个指定根文件系统位置的关键字。

## boot.iso 文件

`boot.iso` 文件是用于创建可引导 CD- 或 DVD-ROM 的 ISO-9660 映像。

## diskboot.img 文件

`diskboot.img` 文件是用于创建可引导 USB 闪存驱动器的 VFAT 文件系统映像。

## 根磁盘

**定义：**

*根磁盘*是包含目录（如 `etc`、`bin`、`home` 等）的磁盘。

## 零填充文件

你需要创建一个不包含任何数据或分区表的文件系统来构建压缩的根文件系统。

## 引导加载程序问题

如果用户无法启动系统，可能是由于引导加载程序或硬件设备导致的磁盘错误。

| 症状 | 原因和解决方案 |
| :--- | :--- |
| 显示错误消息“L”。 | **原因：** LILO 无法加载 /boot/boot.b 文件。 |

## 如何排除 Linux 相关问题故障

### 程序参考：通过收集数据来分析问题

要通过收集数据来分析问题：

1. 以 root 身份登录到 CLI。
2. 使用适当的命令和文件收集有关该问题的数据。
   - 输入 `history` 以分析用户运行命令的历史记录。
   - 输入 `grep {关键字} {日志文件名}` 以在日志文件中查找指定关键字。

## 排除启动过程故障

| **原因** | **解决方案** |
| :--- | :--- |
| 如果引导加载程序屏幕未出现，则 GRUB 可能未正确配置。 | 在救援模式下配置 `/boot/grub/grub.conf`。 |

## 程序参考：使用 Linux 救援环境

要使用 Linux 救援环境：

1. 修改 BIOS 设置以从恢复光盘启动。
2. 将第一张红帽安装 CD 插入 CD-ROM 驱动器并启动系统。
3. 在启动提示符处，输入 `linux rescue` 以进入救援模式。
4. 如有必要，指定访问安装文件所需的设置。
5. 显示一条消息，说明根分区将挂载在 `/mnt/sysimage` 目录中。选择 **Continue** 以挂载文件系统并拥有读写权限。
6. 选择 **OK** 以继续启动过程。
7. 现在根目录已挂载到 ramdisk 上。输入 `chroot /mnt/sysimage` 以将根目录更改为挂载在 `/mnt/sysimage` 目录中的那个。
8. 进行故障排除以查找系统故障的原因，并进行必要的更改以恢复系统。
9. 输入 `exit` 以退出 chroot 环境。
10. 输入 `sync`，以便所做的更改反映在硬盘上的文件系统中。
11. 输入 `exit` 以退出救援模式。系统将重新启动。

# 活动 16-1
## 排除 GRUB 故障

**开始前：**

1. 在 srvB 上，您已以 root 身份登录到 CLI。
2. 在命令行中，输入 `cd /boot/grub` 以打开 GRUB 目录。

**场景：**

您的系统从 **grub** 提示符启动，而不是从 GUI 提示符启动。

| 您做什么 | 您怎么做 |
| :--- | :--- |
| 1. 更正 GRUB 设置。 | a. 在 **grub** 提示符处，输入 `root` |
| 2. 检查更正后的 grub.conf 文件，以确保设置正确。 | a. 按 **Ctrl+Alt+F1** 切换到 CLI。 |

# 活动 16-2
## 排除分区故障

**开始前：**

1. 在 *srvB* 上，您已以 root 身份登录到 CLI。

**场景：**

一名新员工 Jim 不小心操作了一些文件。

| 您做什么 | 您怎么做 |
| :--- | :--- |
| 1. 排除分区标签问题。 | a. 在命令提示符处，输入 root 密码。 |
| 2. 检查系统是否已恢复。 | a. 验证系统已重新启动并显示 GUI 登录屏幕。 |

## 主题 B
### 故障排查硬件问题

你已修复了 Linux 系统中的基于系统的问题。

### 故障排查工具

根据你所面临的问题类型以及工作环境的类型，可以使用许多故障排查工具。

| 工具 | 描述 |
| :--- | :--- |
| dmesg | 一种用于检查和控制内核初始化过程的系统管理命令。 |
| /dev | 一个用于创建启动盘或可恢复磁盘的文件。 |

### LNX-BBC

LNX-BBC 是一个足够小的 Linux 发行版，可以容纳在 CD-ROM 中。

### 启动和停止进程以定位和纠正问题

如课程中之前所述，服务和进程都可以停止和重新启动。

**pgrep** 命令用于根据名称或其他属性查找或向进程发送信号。

**pkill** 命令可以与 **pgrep** 命令配合使用来停止进程。

### 硬件问题

硬件设备可能在系统使用过程中随时发生故障。

| 症状 | 原因和解决方案 |
| :--- | :--- |
| 用户无法从扬声器听到声音。 | **原因**：扬声器或声卡工作不正常。 |

## 查看硬件详情

以下表格列出了常用于查看硬件详情的一些命令。

| 命令 | 用途 |
| :--- | :--- |
| dmesg | 查看启动信息。 |
| /bin/lsPCI | 查看 PCI 卡的信息。 |

## 如何排查硬件问题

### 程序参考：排查声卡问题

1. 验证扬声器已连接、已开启并且工作正常。
2. 如果扬声器工作正常但问题仍然存在，请在启动时验证声卡是否被检测到。
   - a. 验证声卡是否列在 `lsPCI` 命令的输出中。
   - b. 如果未检测到声卡，请联系您的硬件工程师解决声卡问题。

### 程序参考：排查调制解调器问题

要排查调制解调器问题：

1. 验证调制解调器已正确连接到系统并已通电。
2. 检查您的电话线，并验证其是否已正确连接到调制解调器。
3. 验证调制解调器速度是否已正确设置。
