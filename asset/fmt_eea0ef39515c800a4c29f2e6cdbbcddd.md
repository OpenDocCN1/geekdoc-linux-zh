
如果你发现 FTP Config 不满足你的需求，或者你对 `proftpd.conf` 文件感到好奇，`proftpd.conf` 与 Apache 配置文件非常相似。你可以拥有单行命令（称为指令），也可以拥有跨越多行并将一组指令组合在一起的容器标签。例如，以下摘自 `proftpd.conf` 的代码片段将 FTP 获取操作限制在 `turbinolux.com` 域。所有其他均被拒绝。

```
<Limit RETR>
Order Allow,Deny
Allow turbinolux.com
Deny ALL
</Limit>
```

上一个容器块很可能位于目录容器块内，并且仅适用于该目录。或者，它可能位于虚拟主机容器块内，在这种情况下，它适用于虚拟主机的整个目录。

上一个示例中 `Limit` 容器内的行是单行指令的良好示例。单行指令的通用语法为：`<directive-keyword> <value>`，其中 `<directive keyword>` 是某些有效的指令字符串，而值取决于指令直到行尾。

`Limit` 容器的语法为 `"<directive [可选额外参数]"`，后面跟着零或多个指令和/或行，最后以 `</directive>` 结束。我特意给角括号加了引号。

某些指令适用于整个服务器，不能出现在容器块内。这些示例包括 `ServerType` 和 `MaxInstances`。

有几种容器类型。常见的有 `GLOBAL`、`Anonymous`、`VirtualHost`、`Directory` 和 `Limit`。

`GLOBAL` 容器可以包含你希望应用于所有匿名和虚拟主机 FTP 实例的指令。`Anonymous` 和 `VirtualHost` 容器可以通过在其块内精炼这些指令来覆盖它们。`Anonymous` 容器可以定义一个匿名登录可访问的 FTP 目录。任何人登录此位置。同样，`VirtualHost` 容器定义了管理给定 IP 别名 FTP 请求的目录位置。`Directory` 容器定义了给定目录的访问权限，`Limit` 容器定义了哪些 FTP 操作组受到限制。

列表 29-1 展示了我提到的许多指令。

```
Listing 29-1: Sample /etc/proftpd/proftpd.conf
##################################################
#这是一个手动创建的 ProFTPd 配置文件。
# 你可能会发现 FTP Config 会破坏你的注释。
####################################################
# ServerName <string>
# Description: 连接时显示的字符串
ServerName    "Personal FTP Site"

# Server Type [inetd|standalone]
# Description: ProFTPd 服务器的运行方式
Servertype    inetd

#- DefaultServer [on|off]
# Description: 表示服务器是否处理
# 除 VirtualHost 条目定义的
# 以外连接
DefaultServer on

# Port <number>
# Description: ProFTPd 监听连接的端口。
# 仅当 ServerType 为
# standalone 时有效
Port     21

# MaxInstances <number>
# Description: 如果你认为此选项是必要的，
# 请限制运行的并发实例数量。
MaxInstances      30
##################################################
# GLOBAL: GLOBAL 容器设置适用于
# 所有 FTP 条目的参数，除非被显式覆盖。
<GLOBAL>

  # ServerIdent [off]
  # Description: 在连接/登录时显示 ServerName 字符串
    ServerIdent               on
  # DeferWelcome [off]
  # Description: 在用户通过身份验证之前
# 延迟显示主机名和 ServerName。
    DeferWelcome             on

  # Umask [bit mask]
  # Description: 用于新创建的文件
  # 和目录的[位掩码]。022 确保禁用了组
  # 写入权限
    Umask                     022

  # User <user name>
  # Group <group name>
  # Description: 运行 ProFTPd 的用户和组。
    User                      nobody
    Group                     nobody

  # PAMConfig <pam configuration file>
    PAMConfig                proftd  ~

  # AuthPAMAuthoritative [On]
  # Description: 这将身份验证限制为仅 PAM。
# 不将使用其他 ProFTP 验证模块
    AuthPAMAuthoritative      On

  # 通常，我们希望文件是可以覆盖的。
  # 一个基础的匿名配置，没有上传目录。
  <Directory /*>               AllowOverwrite  on
  </Directory>

</GLOBAL>
##################################################
##################################################
# Anonymous: 主要匿名 FTP 站点, ~ftp
<Anonymous> ~ftp>
```

# 第 29 章 使用 FTP 提供文件服务

```
User               ftp
Group              ftp
# UserAlias <name><name2> ... <name>
# Description: 用户名 ftp 的别名
UserAlias          anonymous ftp
# 限制匿名登录的最大数量
MaxClients 10 "the maximum number of anonymous connections has been reached
try back later."
## DisplayLogin <file>
# DisplayFirstChdir <file>
# 我们希望在登录时显示 'welcome.msg'，并在每个新切换 (chdir) 目录时显示 '.message'
DisplayLogin       welcome.msg
DisplayFirstChdir  .message
# RequireValidShell [onoff]
# 我们希望客户端能够使用 "anonymous" 以及 "ftp" 登录
# 在 TurboLinux 系统上，ftp 用户没有 shell。
RequireValidShell  off
# 限制匿名 chroot 范围内的写入权限
<Limit WRITE>
Deny from All
</Limit>
</Anonymous>
# 虚拟主机: gabriele.home.org
<VirtualHost gabriele.home.org>
User                nobody
Group              nobody
ServerName         "Virtual Host Gabrielle*"
DefaultRoot        /home/http/gabriele/ftp
AllowOverride      on
ServerAdmin        admin@gabriele.home.org
MaxLoginAttempts   3
RequireValidShell  no
TransferLog        /var/log/gabriele.proft.log
<Anonymous /home/http/gabriele/ftp/pub>
UserAlias          anonymous nobody

<Limit WRITE>
DenyAll
</Limit>

<Directory incoming/*>
```

# 列表 29-1（续）

```
<Limit STOR>
  AllowAll
</Limit>
<Limit WRITE DIRS>
  DenyAll
</Limit>
<Limit CWD XCCD CDUP>
  AllowAll
</Limit>
</Directory>
</Anonymous>

</VirtualHost>
```
