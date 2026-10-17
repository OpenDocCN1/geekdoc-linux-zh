
在编译 NRPE 时，源码目录下会创建一个 `nrpe.cfg` 文件，其中包含了多个参数以及运行 NRPE 的命令。这些内容被手动复制到配置目录，该目录通常必须在目标计算机上创建：

```bash
linux:src/nrpe-2.11 # mkdir /etc/nagios
linux:src/nrpe-2.11 # cp nrpe.cfg /etc/nagios/
```

特定发行版的包从第215页表 10-1 中指定的位置解压。

`nrpe` 在运行时具有守护进程配置中指定的的用户（在我们的案例中是 `nobody`）的权限。因此，`nrpe.cfg` 需要该用户可读。由于该文件不包含任何密码（实际上不应该使用密码）或其他关键信息，可以允许所有人拥有读取权限。

配置文件包含许多注释；以下命令显示激活的参数.¹⁰¹¹

```bash
user@linux:~ grep -v '^#\|$' nrpe.cfg | less
server_port=5666
allowed_hosts=127.0.0.1
nrpe_user=nobody
nrpe_group=nogroup
dont_blame_nrpe=0
debug=0
command_timeout=60
```

参数 `server_port`、`allowed_hosts`、`nrpe_user` 和 `nrpe_group` 仅在 `nrpe` 作为守护进程运行时才相关。当使用守护进程时，程序会忽略这些值，因为它们已经由 `(x) inet` 配置确定。

条目 `dont_blame_nrpe=0` 防止 `nrpe` 接受参数，从而关闭了一个安全漏洞。`debug=1` 允许详细日志记录，如果你正在寻找错误这非常有用（`debug=0` 关闭调试信息的输出），`command_timeout` 指定了 `nrpe` 强制中断挂起插件后的秒数时间间隔。配置文件中的注释也解释了所有这些参数。

此之后，命令默认由 NRPE 执行。配置文件 `nrpe.cfg` 已经包含了一些命令，但首先必须将它们全部注释掉，并且仅激活那些确实打算使用的命令。

关键字 `command` 后面紧跟方括号，其中是 `check_nrpe` 调用命令的名称。在等号 (`=`) 之后，指定了相应的插件命令及其完整路径：¹⁰²

```
command[check_users]=/usr/local/nagios/libexec/check_users -w 5 -c 10
command[check_load]=/usr/lib/nagios/libexec/check_load -w 8,5 -c 15,10,7
command[check_zombies]=/usr/lib/nagios/libexec/check_procs -w 1 -c 2 -s Z
```

在使用路径时，必须小心它直接指向本地插件目录。在指定的 `/usr/local/nagios/libexec` 中，位于自编译的插件¹³；而对于安装包，路径通常是 `/usr/lib/nagios/libexec`。由于路径，必须确保它直接指向本地插件目录。这里在目标机器上通过 `check_nrpe`：

```bash
linux:src/nrpe-2.11 # mkdir /etc/nagios
linux:src/nrpe-2.11 # cp nrpe.cfg /etc/nagios/
```

### 10.2.3 Inet 守护进程是否正在监听 NRPE 端口？

一个简单的测试可以显示 `inet` 守护进程是否想要响应 5666 端口的查询：

```bash
linux:- # netstat -int | grep ':5666'
tcp      0 0 0.0.0.0:5666      0.0.0.0:*               LISTEN
```

`netstat` 程序使用 `-l` 选项显示服务正在等待传入查询的所有端口，即处于 `LISTEN` 状态的服务。`-n` 选项抑制主机和端口的解析并加快信息的显示，而 `-t` 则将输出限制为 TCP 端口。

该测试显示了 `inet` 守护进程是否已正确配置并新启动，例如当 `/etc/services` 中正确输入了 `nrpe` 服务时。它并没有说明 NRPE 守护进程及其配置文件的路径是否正确。这些错误只有在对 NRPE 5666 端口发生具体的访问时，`inet` 守护进程才会提示。随后的完整功能测试只有在 NRPE 守护进程配置完成后才会进行。这见第221页的 10.4 NRPE 功能测试。

> ¹⁰⁰ `inetd` 没有内置仅从特定 IP 地址访问服务的方法。此功能在 TCP 包装器 `tcpd` 中添加。访问配置由文件 `/etc/hosts.allow` 和 `/etc/hosts.deny` 接管。更多信息请参阅 `man host_access`。

## 10.3 被监控计算机上的 NRPE 配置

在编译 NRPE 时，源码目录下会创建一个 `nrpe.cfg` 文件，其中包含了多个参数以及运行 NRPE 的命令。这些内容被手动复制到配置目录，该目录通常必须在目标计算机上创建：

```bash
linux:src/nrpe-2.11 # mkdir /etc/nagios
linux:src/nrpe-2.11 # cp nrpe.cfg /etc/nagios/
```

特定发行版的包从第215页表 10-1 中指定的位置解压。

`nrpe` 在运行时具有守护进程配置中指定的的用户（在我们的案例中是 `nobody`）的权限。因此，`nrpe.cfg` 需要该用户可读。由于该文件不包含任何密码（实际上不应该使用密码）或其他关键信息，可以允许所有人拥有读取权限。

配置文件包含许多注释；以下命令显示激活的参数.¹⁰¹¹

```bash
user@linux:~ grep -v '^#\|$' nrpe.cfg | less
server_port=5666
allowed_hosts=127.0.0.1
nrpe_user=nobody
nrpe_group=nogroup
dont_blame_nrpe=0
debug=0
command_timeout=60
```

参数 `server_port`、`allowed_hosts`、`nrpe_user` 和 `nrpe_group` 仅在 `nrpe` 作为守护进程运行时才相关。当使用守护进程时，程序会忽略这些值，因为它们已经由 `(x) inet` 配置确定。

条目 `dont_blame_nrpe=0` 防止 `nrpe` 接受参数，从而关闭了一个安全漏洞。`debug=1` 允许详细日志记录，如果你正在寻找错误这非常有用（`debug=0` 关闭调试信息的输出），`command_timeout` 指定了 `nrpe` 强制中断挂起插件后的秒数时间间隔。配置文件中的注释也解释了所有这些参数。

此之后，命令默认由 NRPE 执行。配置文件 `nrpe.cfg` 已经包含了一些命令，但首先必须将它们全部注释掉，并且仅激活那些确实打算使用的命令。

关键字 `command` 后面紧跟方括号，其中是 `check_nrpe` 调用命令的名称。在等号 (`=`) 之后，指定了相应的插件命令及其完整路径：¹⁰²

```
command[check_users]=/usr/local/nagios/libexec/check_users -w 5 -c 10
command[check_load]=/usr/lib/nagios/libexec/check_load -w 8,5 -c 15,10,7
command[check_zombies]=/usr/lib/nagios/libexec/check_procs -w 1 -c 2 -s Z
```

在使用路径时，必须小心它直接指向本地插件目录。在指定的 `/usr/local/nagios/libexec` 中，位于自编译的插件¹³；而对于安装包，路径通常是 `/usr/lib/nagios/libexec`。由于路径，必须确保它直接指向本地插件目录。这里在目标机器上通过 `check_nrpe`：

```bash
linux:src/nrpe-2.11 # mkdir /etc/nagios
linux:src/nrpe-2.11 # cp nrpe.cfg /etc/nagios/
```

### 10.2.3 Inet 守护进程是否正在监听 NRPE 端口？

一个简单的测试可以显示 `inet` 守护进程是否想要响应 5666 端口的查询：

```bash
linux:- # netstat -int | grep ':5666'
tcp      0 0 0.0.0.0:5666      0.0.0.0:*               LISTEN
```

`netstat` 程序使用 `-l` 选项显示服务正在等待传入查询的所有端口，即处于 `LISTEN` 状态的服务。`-n` 选项抑制主机和端口的解析并加快信息的显示，而 `-t` 则将输出限制为 TCP 端口。
