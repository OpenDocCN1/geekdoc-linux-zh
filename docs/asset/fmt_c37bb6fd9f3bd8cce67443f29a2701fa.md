
为了使此项生效，你必须更改命令定义中的命令行（该命令通过`-c`传递），如下所示：

```
-c "$ARG1$/check_disk -w $ARG2 -c $ARG3 -p $ARG4$"
```

注意：这会导致每个`$ARGx`宏对应的`-w`、`-c`和`-p`的数字都向后移动一位。

# 第 10 章。Nagios 远程插件执行器 (NRPE)

Nagios 远程插件执行器（简称为 NRPE）顾如其名，在远程主机上执行程序。这些程序通常是用于本地测试相应计算机的插件，因此必须安装在这些计算机上。NRPE 的使用不仅限于本地插件；任何插件都可以执行，包括旨在测试网络服务的插件——例如，测试无法从 Nagios 服务器访问的计算机（参见第 224 页的 10.6 节间接检查）。

虽然在启动插件时，远程计算机上必须有一个可用的通用用户账户，但 NRPE 仅限于已配置的目标（见第 9 章），这些目标也可以用于执行启动插件以外的其他操作。如果你愿意或被迫在目标上使用登录 shell，可以使用 NRPE，即使这比使用安全外壳（secure shell）涉及稍微多一点配置工作。除了 Nagios 配置和在 Nagios 服务器上安装`check_nrpe`插件外，目标系统上还需完成以下任务：

- 必须安装`nrpe`插件。
- 必须以管理员权限配置`inet`守护进程（`inetd`或`xinetd`）。
- 所有通过 NRPE 调用的插件都必须安装。

## 10.1 安装

NRPE 和插件可以从源码安装，也可以退而使用发行发行版提供的软件包。你应该使用至少 2.0 版本的 NRPE，因为它与之前的版本不兼容。从 2.6 版本开始，NRPE 引入了`-u`开关。如果目标系统上的 NRPE 服务无法访问，Nagios 服务器上的`check_nrpe`插件将针对该开关返回`UNKNOWN`。从 2.8 版本开始，NRPE 支持 Nagios 3.0 引入的插件多行输出。

所有发行版都包含了至少 1.4 版本的插件集。你是否需要最新版本取决于你对相应插件的预期。

### 10.1.1 特定于发行版的软件包

SuSE Linux 10.3 包含了软件包`nagios-nrpe-2.10-4.1.i586.rpm`、`nagios-plugins-1.4.10-12.1.i586.rpm`和`nagios-plugins-extras-12.4.10-12.1.i586.rpm`。`nagios-nrpe`包含了守护进程和`check_nrpe`插件。

`nagios-plugins-extras`安装了多个额外的插件，例如数据库检查、FPing 测试或 Radius 测试，可以根据你具体的监控需求省略。

为了简单起见，设计包由 YAST2 或`rpm-ihv`软件包安装，第二种方法也适用于 Fedora 用户。

对于 Fedora Core 和 Red Hat Enterprise Linux，Dag Wiers 提供了他们版本的 Nagios 软件包。

Debian/Sarge 将 NRPE 守护进程和 NRPE 插件分别称为`nagios-server`和`nagios-nrpe-plugin`，它们可以通过`apt-get`分别安装在不同的软件包。如果你不想制作文档，可以省略`nagios-nrpe-doc`软件包，仅将`nagios-nrpe`插件添加到目标主机上。

程序`nrpe`、配置文件`nrpe.cfg`以及插件目录的路径列表 10-1 所示。

| 发行版 | NRPE 程序 | 配置文件 | 插件 |
| --- | --- | --- | --- |
| 自编译 | `/usr/local/sbin/nrpe` | `/etc/nagios/nrpe.cfg` | `/usr/local/libexec` |
| SuSE | `/usr/bin/nrpe` | `/etc/nagios/nrpe.cfg` | `/usr/libexec` |
| Debian | `/usr/sbin/nrpe` | `/etc/nagios/nrpe.cfg` | `/usr/lib/nagios` |
| Fedora | `/usr/sbin/nrpe` | `/etc/nagios/nrpe.cfg` | `/usr/lib/nagios` |

### 10.1.2 从源码安装

NRPE 源码从 Nagios 主页获取。

```bash
mkdir /local/src
cd /local/src
tar -xzf nrpe-2.1.tar.gz
```

解压后进入`/local/src`目录。

```bash
./configure --sysdir=/etc/nagios --enable-ssl
```

编译并安装：

```bash
make
make install
```

编译完成后，NRPE 应该已安装到指定目录。

```bash
linux:- # /etc/init.d/inetd reload
```

## 10.2.2 inetd 配置

在标准的 inetd 中，该行被添加到配置文件`/etc/inetd.conf`中：

```
nrpe stream tcp noway nobody /usr/bin/tcpd /usr/local/sbin/nrpe -c/etc/nagios/nrpe.cfg --inetd
```

由于空格原因，该行被拆分成了多行，但在配置文件中必须是单行。这里使用了 TCP 包装器`tcpd`。如果不打算使用它，只需省略此条目¹⁰⁰即可。在这里，你还需要显式地输入用户`nobody`、`nrpe`二进制文件的完整路径以及配置文件的路径（同样带有完整路径）。这些在上方以*斜体*打印的字符串必须根据你自己的系统进行调整。在更改配置后，重新加载 inetd：

```bash
linux:- # /etc/init.d/inetd reload
```

### 10.2.3 Inet 守护进程是否正在监听 NRPE 端口？

简单的测试可以显示 inet 守护进程是否想要响应 5666 端口的查询：

```bash
linux:- # netstat -int | grep ':5666'
tcp      0 0 0.0.0.0:5666      0.0.0.0:*               LISTEN
```

`netstat`程序使用`-l`选项显示服务正在等待传入查询的所有端口，即处于`LISTEN`状态的服务。`-n`选项抑制主机和端口的解析并加快信息的显示，而`-t`则将输出限制为 TCP 端口。

该测试显示了 inet 守护进程是否已正确配置并新启动，例如当`/etc/services`中正确输入了`nrpe`服务时。它并没有说明 NRPE 守护进程及其配置文件的路径是否正确。这些错误只有在对 NRPE 5666 端口发生具体的访问时，inet 守护进程才会提示。随后的完整功能测试只有在 NRPE 守护进程配置完成后才会进行。这见第221页的 10.4 NRPE 功能测试。

> ¹⁰⁰ inetd 没有内置仅从特定 IP 地址访问服务的方法。此功能在 TCP 包装器`tcpd`中添加。访问配置由文件`/etc/hosts.allow`和`/etc/hosts.deny`接管。更多信息请参阅`man host_access`。

## 10.3 被监控计算机上的 NRPE 配置

在编译 NRPE 时，源码目录下会创建一个`nrpe.cfg`文件，其中包含了多个参数以及运行 NRPE 的命令。这些内容被手动复制到配置目录，该目录通常必须在目标计算机上创建：

```bash
linux:src/nrpe-2.11 # mkdir /etc/nagios
linux:src/nrpe-2.11 # cp nrpe.cfg /etc/nagios/
```

特定发行版的包从第215页表 10-1 中指定的位置解压。

`nrpe`在运行时具有守护进程配置中指定的的用户（在我们的案例中是`nobody`）的权限。因此，`nrpe.cfg`需要该用户可读。由于该文件不包含任何密码（实际上不应该使用密码）或其他关键信息，可以允许所有人拥有读取权限。

配置文件包含许多注释；以下命令显示激活的参数.¹⁰¹¹
