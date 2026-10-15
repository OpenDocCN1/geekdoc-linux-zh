
例如，用户目录下的 setuid 程序将是不寻。

## 密码安全性

验证密码、组和影子密码文件是否受到保护。特别是影子密码文件应该是写保护的且仅供 root 读取。文件名和建议权限见表 22-7。

### 表 22-7：文件名及其权限

| 文件名 | 所有者 | 权限 |
| --- | --- | --- |
| `/etc/group` | root.root | 644 |
| `/etc/passwd` | root.root | 644 |
| `/etc/shadow` | root.root | 400 |

## 第 22 章：系统与网络安全

### 由 xinetd 启动的服务

许多 Internet 服务（如 Telnet 和 POP3）是由 `xinetd` 服务器启动的。开启其中某些服务取决于系统如何连接到互联网以及如何使用系统等因素。你通常可以关闭 `xinetd` 服务。

可以通过以下方式之一检查开启了哪些 `xinetd` 服务：

- 检查 `/etc/xinetd.d` 目录下的配置文件，以查看 `xinetd` 可以启动的所有服务。如果某个服务已启用，配置文件中会有类似下面的一行：
  `disable = yes`

请记住，如果 `disable = yes` 这一行开头有 `#` 号被注释掉了，则它是不生效的。

- 输入以下命令：
  `chkconfig --list | more`

在输出中，查找后续的行：
`xinetd based services:`
这些行列出了 `xinetd` 可以启动的所有服务，以及它们是处于开启还是关闭状态。例如，这里是显示系统上 `xinetd` 服务状态的行：

```
charger: off

charger-udp: off

cvs: off

daytime: off

daytime-udp: off

echo: off

echo-udp: off

eklogin: off

gssftp: off

login: off

krb5-telnet: off

shell: off

ktalk: off

rsync: off

telnet: off

time: off

time-udp: off
```

在这种情况下，所有服务都是关闭的。

同时检查以下文件，以查看用于用于 `xinetd` 服务的任何访问控制：

- `/etc/hosts.allow` 列出了允许访问特定服务的宿主机。
- `/etc/hosts.deny` 列出了应被拒绝访问服务的宿主机。

### 独立服务

许多服务（如 HTTP（Web 服务器）和 sendmail（邮件服务器））在启动时会自动启动，前提是它们被配置为这样启动。你可以使用 `chkconfig` 命令检查哪些独立服务器被设置为在不同的运行级别启动。通常情况下，你的 Linux 系统在运行级别 3（文本登录）或 5（图形界面登录）下启动：因此，重要的是级别 3 和级别 5 中服务器的设置。如需查看服务器列表，请输入以下命令：

```
chkconfig --list | more
```

这里是你可能会看到的部分列表：

| NetworkManager | 0:off | 1:off | 2:off | 3:off | 4:off | 5:off | 6:off |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| acpid | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off | 6:off |
| anacron | 0:off | 1:off | 2:off | 3:on | 4:on | 5:off | 6:off |
| apmd | 0:off | 1:off | 2:off | 3:on | 4:on | 5:off | 6:off |
| atd | 0:off | 1:off | 2:off | 3:off | 4:on | 5:off | 6:off |
| auditd | 0:off | 1:off | 2:on | 3:on | 4:on | 5:off | 6:off |
| autofs | 0:off | 1:off | 2:off | 3:on | 4:on | 5:off | 6:off |
| bluetooth | 0:off | 1:off | 2:off | 3:off | 4:off | 5:off | 6:off |
| crond | 0:off | 1:off | 2:off | 3:on | 4:on | 5:off | 6:off |
| cups | 0:off | 1:off | 2:off | 3:on | 4:on | 5:off | 6:off |
| cups-config-daemon | 0:off | 1:off | 2:off | 3:off | 4:on | 5:off | 6:off |
| dc_client | 0:off | 1:off | 2:off | 3:off | 4:on | 5:off | 6:off |
| dc_server | 0:off | 1:off | 2:off | 3:off | 4:off | 5:off | 6:off |
| ldiskd | 0:off | 1:off | 2:off | 3:off | 4:off | 5:off | 6:off |
| dovecot | 0:off | 1:off | 2:off | 3:off | 4:off | 5:off | 6:off |
| gpm | 0:off | 1:off | 2:on | 3:on | 4:on | 5:off | 6:off |
| haldaemon | 0:off | 1:off | 2:off | 3:on | 4:on | 5:off | 6:off |
| httpd | 0:off | 1:off | 2:off | 3:on | 4:on | 5:off | 6:off |
| innd | 0:off | 1:off | 2:off | 3:off | 4:off | 5:off | 6:off |
| iptables | 0:off | 1:off | 2:on | 3:on | 4:on | 5:off | 6:off |

第一列显示服务器名称。查看以 3 开头的列以及以 5 开头的列：这些是显示级别 3 和 5 服务器状态的。标记为 `on` 的项会在 Linux 系统启动时自动启动。如果你在对网络进行自评估时发现某些服务器不应该运行，你可以像这样使用 `chkconfig` 关闭它们的级别 3 和 5：

```
chkconfig --level servicename
```
