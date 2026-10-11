
## 第 24 章：使用 SELinux 增强 Linux 安全

1. 要将系统设置为 SELinux 许可模式（permissive Operating Mode），请在命令行输入 `setenforce permissive`。在命令行输入 `setenforce 0`。

2. 在不更改 SELinux 主配置文件的情况下，将系统设置为强制模式（enforcing Operating Mode），请小心。在启用强制之前最好不要运行此命令。在准备好启用 SELinux 之前，可以在你的系统上使用以下命令进行练习。在命令行输入 `setenforce enforcing` 或 `setenforce 1` 也可以接受。

3. 要查找并查看当前的 SELinux 策略，请前往 SELinux 主配置文件，在命令行输入 `cat /etc/selinux/config`。

4. 要列出文件的安全上下文并识别不同的安全上下文属性，请在命令行使用 `ls -Z filename`。
- 文件的用户上下文以 `u` 结尾。
- 文件的角色以 `r` 结尾。
- 文件的类型以 `t` 结尾。
- 文件的敏感性级别以 `s` 开头并以数字结尾。它可能以数字范围的形式列出，例如 `s0-s3`。
- 文件的类别以 `c` 开头并以数字结尾。它可能以数字范围的形式列出，例如 `c0-c102`。

## 第 VI 部分：附录

5. 更改文件类型属性的命令是 `chcon -t newtype filename`。（注意：除非你想更改文件类型，否则不要在系统上使用该命令。）

6. 要列出进程的安全上下文并识别不同的安全上下文属性，请使用命令行 `ps -Z pid`。
- 进程的用户上下文以 `u` 结尾。
- 进程的角色以 `r` 结尾。
- 进程的类型或域以 `t` 结尾。
- 进程的敏感性级别以 `a` 开头并以数字结尾。它可能以范围的形式列出，例如 `s0.s3`。
- 进程的类别级别以 `c` 开头并以数字结尾。它可能以范围的形式列出，例如 `c0.102`。

7. 恢复文件 SELinux 默认文件上下文的命令是 `restore -R filename`。（注意：除非你了解其影响，否则不要在系统上运行此命令。）

8. 要获取系统上当前布尔值（Booleans）的列表，请使用命令行 `getbool -a`。你可以使用以下任命令之一修改布尔值：`setbool Boolean off` 或 `setbool Boolean_name on` 或 `togglebool Boolean_name`。

9. 列系统中所有 SELinux 模块及其版本号的命令是 `module -l`。注意：如果你将 `ls *.pp` 作为答案是可以的，但此命令不会提供模块的版本号。只有 `module` 会给你提供版本号。

10. 要创建一个 AVC 拒绝消息并查看该消息的日志，执行以下操作：
- 作为非管理员用户，在命令行输入 `chcon -u fake_u filename`。
- 如果你的系统上运行了 `auditd` 守护进程，在命令行输入：
```
aureport | grep AVC ausearch -m avc
```
- 如果你的系统上只运行了 `rsyslogd` 守护进程，在命令行输入：
```
grep "SELinux is preventing" /var/log/messages
```
- 如果你的系统上运行了 `rsyslogd` 守护进程和 `setroubleshoot` 守护进程，在命令行输入：
```
grep "SELinux is preventing" /var/log/messages
sealert -l AVC_denial_message_id number
```

## 第 25 章：网络上的 Linux 安全

1. 在你的本地 Linux 系统上安装网络映射（即 `nmap`）工具：
- a. 在 Fedora 或 RHEL 上，在命令行输入 `yum install nmap`。
- b. 在 Ubuntu 上，`nmap` 可能已预安装。如果没有，在命令行输入 `sudo apt-get install nmap`。

2. 在你的本地回环地址上运行 TCP 连接扫描，请在命令行输入 `nmap -sT 127.0.0.1`。你在 Linux 服务器上运行的端口会有所不同。但是，它们可能看起来如下：

```
# nmap -sT 127.0.0.1
```

| PORT | STATE | SERVICE |
|---|---|---|
| 25/tcp | open | smtp |
| 631/tcp | open | ipp |

3. 要从远程系统对你的 Linux 系统运行 UDP 扫描：
- a. 使用命令行 `ifconfig` 确定你 Linux 服务器的 IP 地址。输出将类似于下所示，你的系统 IP 地址位于 `ifconfig` 输出的 `inet addr:` 之后。

```
# ifconfig
```

```
p21 Link enc:Ethernet Haddr 08:00:27:E5:B9:5A

inet addr:10.140.67.23
```

- b. 从远程 Linux 系统，使用命令行命令 `nmap -sU IP address`，使用你从上面获取的 `IP address`。

4. 检查 Linux 系统上的 `ssh` 守护进程是否使用 TCP Wrapper 支持，如果在命令行执行 `ldd /usr/bin/sshd | grep libwrap`，输出将类似于下。如果不支持，则没有输出。

```
$ ldd /usr/bin/sshd | grep libwrap

libwrap.so => /libwrap/libwrap.so (0x0012f000)
```

5. 要允许从指定的远程系统以及任何其他使用 TCP Wrappers 访问你 Linux 系统上的 `ssh` 工具，你需要修改 `/etc/hosts.allow` 允许文件和 `/etc/hosts.deny` 文件。修改将类似于如下：

```
# cat /etc/hosts.allow

sshd: 10.140.67.32
```

```
# cat /etc/hosts.deny

...

ALL: ALL
```
