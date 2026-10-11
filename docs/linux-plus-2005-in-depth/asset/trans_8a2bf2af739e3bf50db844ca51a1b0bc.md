

## 安全

请确保您的计算机 BIOS 阻止从 USB 端口启动，并且设置系统 BIOS 密码，以防止其他用户更改启动顺序。

基于同样的思路，任何能够物理接触 Linux 计算机的人都可能启动该计算机并与 LILO 或 GRUB 引导加载器进行交互。这允许用户指定选项，以单用户模式启动系统，从而在不输入密码的情况下获得系统的 root 访问权限。为了防止这种情况，只需确保在 LILO 或 GRUB 配置文件中设置引导加载器密码，如第 9 章所述。

对于 Linux 计算机，另一个重要的安全考量是限制对图形桌面和 shell 的访问。如果您离开工作站几分钟而仍保持登录状态，其他用户可以在您离开期间使用您的计算机。因此，在离开计算机之前锁定您的桌面环境或退出命令行 shell 是一个良好的安全实践。要锁定 GNOME 或 KDE 桌面，只需导航至 Red Hat 按钮并选择“锁定屏幕”；您需要输入密码才能再次使用您的桌面。退出命令行 shell 也会终止所有后台进程，因为这些进程的父进程是您的 shell。如果您运行需要较长时间完成的后台进程，可以使用 `nohup command` 运行它们；这样可以让您退出命令行 shell 而不会终止任何后台进程。例如，要运行 `updatedb` 命令并在之后退出系统，以便您可以离开工作站，只需执行以下命令：

```bash
[root@server1 root]# nohup updatedb &
[1] 3773
nohup: appending output to 'nohup.out'
[root@server1 root]# exit

Fedora Core release 2 (Tettnang)
Kernel 2.6.5-1.358 on an i686

server1 login:
```

如果您对 Linux 系统拥有 root 访问权限，重要的是要尽量减少以 root 用户登录的时间，以降低其他用户在您意外离开系统（未锁定桌面或未退出 shell）时访问您终端的机会。最佳实践是创建一个普通用户账户，用于检查电子邮件和执行其他日常任务。然后，您可以使用 `su` [切换用户] 命令仅在需要执行管理任务时获取 root 访问权限。完成后，您可以使用 `exit` 命令返回到之前的 shell，此时您登录的是普通用户账户，如下面的输出所示：

```bash
[user1@server1 user1]$ su - root
Password: ****
[root@server1 root]# _
[root@server1 root]# rm -f /etc/security
[root@server1 root]# exit
[user1@server1 user1] _
```

前面输出中 `su` 命令的 `-` 选项会加载 root 用户的环境变量。此外，您可以省略前面输出中 root 用户的名称；如果未指定名称作为 `su` 命令的参数，则默认假设为 root 用户。

如果您只打算以 root 用户运行一条命令，可以选择使用 `su` 命令的 `-c` 选项；这会让您自动返回当前 shell。以下演示了如何使用 `su` 命令的 `-c` 选项运行前面输出中显示的 root 命令：

```bash
[user1@server1 user1]$ su -c "rm -f /etc/security" root
Password: *****
[user1@server1 user1]$
```

然而，某些用户，如软件开发者，在某些情况下需要以 root 用户运行某些命令。与其提供 root 密码，不如通过 **sudo** 命令授予他们以 root 用户运行某些命令的能力。`sudo` 命令检查 `/etc/sudoers` 文件，查看您是否有权限以不同用户身份运行特定命令。下面的 `/etc/sudoers` 文件允许软件开发者 `mary` 和 `bob` 在计算机 `server1` 和 `server2` 上以 root 用户身份运行 `kill` 和 `killall` 命令：

```bash
[root@server1 root]$ cat /etc/sudoers
User_Alias SD = mary, bob
Cmd_Alias KILL = /bin/kill, /usr/bin/killall
Host_Alias SERVERS = server1, server2

SD   SERVERS = (root) KILL
[root@server1 root]$
```

现在，如果 `mary` 需要终止 `server1` 上的 `cron` 守护进程（该进程是以 root 用户身份启动的）以测试她编写的程序，她需要使用 `sudo` 命令，如下面的输出所示，并提供她自己的密码：

```bash
[mary@server1 mary]$ ps -ef | grep crond
root    2281    1    0 21:20 ?    00:00:00 crond
[mary@server1 mary]$ kill -9 2281
-bash: kill: (2281) - Operation not permitted
[mary@server1 mary]$ sudo kill -9 2281

We trust that you have received the usual lecture from the local System Administrator. It usually boils down to these two things:

#1) Respect the privacy of others.
#2) Think before you type.
Password: *****
[mary@server1 mary]$
```

### 防御网络攻击

回顾本章早些时候的内容，网络服务在特定端口号上监听网络流量并与之交互。只要计算机上存在网络服务，就始终存在攻击者通过以异常方式交互来操纵网络服务的可能性。此类网络攻击的一个例子是**缓冲区溢出**，它可以用新的程序信息替换网络服务在内存中使用的程序信息，从而改变网络服务的操作方式。

保护计算机免受网络攻击（如缓冲区溢出）的第一步是最小化运行的网络服务数量。如果您只运行组织所需的最少网络服务，可以大大降低遭受网络攻击的可能性。要查看网络上正在运行哪些网络服务，您可以运行 **nmap**（网络映射器）命令。下面的输出演示了如何使用 `nmap` 来确定 `server1` 计算机上运行的服务数量：

```bash
[root@server1 root]# nmap -sT server1
Starting nmap 3.5 (http://www.insecure.org/nmap/) at 2005-09-05 9:29 EDT
Interesting ports on server1 (127.0.0.1):
(The 1648 ports scanned but not shown below are in state: closed)

| PORT      | STATE  | SERVICE       |
|:----------|:-------|:--------------|
| 22/tcp    | open   | ssh           |
| 25/tcp    | open   | smtp          |
| 80/tcp    | open   | http          |
| 111/tcp   | open   | rpcbind       |
| 139/tcp   | open   | netbios-ssn   |
| 443/tcp   | open   | https         |
| 445/tcp   | open   | microsoft-ds  |
| 631/tcp   | open   | ipp           |
| 783/tcp   | open   | hp-almgr      |
| 32770/tcp | open   | sometimes-rpc3|
| 32771/tcp | open   | sometimes-rpc5|

Nmap run completed - 1 IP address (1 host up) scanned in 0.928 seconds
[root@server1 root]#
```

根据前面的输出，您可以通过在 `/etc/services` 文件或互联网上搜索端口号的描述来确定计算机上正在运行哪些服务。对于不需要的服务，确保它们不会通过 `/etc/rc.d/rc*.d` 目录中的条目或其他启动脚本（如 `/etc/rc.d/rc.local`）中的行被 Internet 超级守护进程自动启动。

对于因对组织至关重要而必须使用的服务，您可以采取某些步骤以确保它们尽可能安全。例如，您可以为支持加密通信的网络服务启用加密（例如，`sshd`），并使用 netfilter/iptables INPUT 链规则仅允许所需的网络流量到达您的网络服务。同样重要的是，确保网络服务守护进程尽可能不以系统上的 root 用户身份运行。如果攻击者通过以 root 用户身份运行的网络服务守护进程获得系统访问权限，那么攻击者也将拥有 root 访问权限。许多网络守护进程（如 Apache）在其配置文件中设置执行它们的用户账户。

此外，由于网络攻击在开源社区中有报道，网络服务的新版本通常包含针对已知网络攻击的修复。因此，这些新版本对网络攻击具有更强的抵抗力。基于此，定期查看网络服务的新版本、安装它们，并检查相关文档中可在配置文件中设置的与安全相关的新参数是良好的做法。

如果您使用由 Internet 超级守护进程启动的网络服务，可以使用 TCP wrappers 提供额外的安全性。**TCP wrapper** 是一个可以启动网络服务的程序（`/usr/sbin/tcpd`）。要启用 TCP wrappers，您必须修改 `/etc/xinetd.d` 目录中的适当文件，并将网络守护进程作为 TCP wrapper 的参数启动。对于 telnet 守护进程，您修改 `/etc/xinetd.d/telnet` 文件，如下面的示例所示：

```bash
[root@server1 root]# cat /etc/xinetd.d/telnet
# default: on
# description: The telnet server serves telnet sessions; it uses \n#
uncrypted username/password pairs for authentication.

service telnet
{
    flags            = REUSE
    socket_type    = stream
    wait           = no
    user           = root
    server         = /usr/sbin/tcpd
    server_args    = /usr/sbin/in.telnetd
    log_on_failure += USERID
    disable        = yes
}
[root@server1 root]# _
```

现在，telnet 守护进程（`/usr/sbin/in.telnetd`）将由 TCP wrapper（`/usr/sbin/tcpd`）启动。在 TCP wrapper 启动网络守护进程之前，它首先检查 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。这允许您限制网络服务，使其只能被组织内的特定主机访问。下面的 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件仅允许计算机 `client1` 和 `client2` 使用 telnet 工具连接到您的 telnet 服务器。

```bash
[root@server1 root]# cat /etc/hosts.deny
in.telnetd: ALL
[root@server1 root]# _
```

