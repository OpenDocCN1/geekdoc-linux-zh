
第 1 行定义端口将使用的拨号器名称。第 2 行定义调制调器连接到远程 UUCP 主机所需的 `chat` 脚本。`\T` 变量用于 `chat` 脚本将端口文件中列出的电话号插入调制调器拨号字符串中。

## UUCP 命令

创建 UUCP 配置文件后，Linux 系统已准备好通过 UUCP 与远程主机进行通信。为此，额外的 Linux 命令已准备好通过 UUCP 与远程主机进行通信。

## uustat

`uustat` 命令是一个极其强大的命令。root 用户可以使用它来检查 UUCP 池文件，报告等待处理的作业或正在处理的任务，并删除或启动队列中的 UUCP 任务。`uustat` 命令有许多不同的格式，取决于你想要执行的功能。

`-o` 选项用于显示所有队列的文件传输任务。`-K` 选项可用于杀死 UUCP 任务。可以通过任务 ID、远程系统名、用户名以及许多其他参数来选择被杀死的任务。列表 9.6 是 `uustat` 输出示例。

### 列表 9.6 uustat 输出示例

```
$rich@shadrach$ uustat -

nismail.CLMCwusAAAdm ismail 10-02 06:57 Executing email

Rich.@blum.org (sending 387 bytes)

nismail.CLNXU37AAAdm ismail 10-02 06:58 Executing email

rich@smallorg.org (sending 398 bytes)

ismail.CLP0GGOZAAdZ ismail 10-02 06:59 Executing email

pre@microsoft.com (sending 456 bytes)

ismail.CLP0GGOZAAdm ismail 10-02 06:59 Executing email

postmaster@linux.org (sending 449 bytes)

$rich@shadrach$
```

在列表 9.6 中，第 2 到 5 行是通过 UUCP 发送的邮件任务。第一个字段是任务 ID。第二个字段是远程 UUCP 主机，第三个字段是启动任务的用户名。

## uucp

`uucp` 命令用于允许用户向远程 UUCP 计算机的用户传输文件。`uucp` 命令的格式为：

`uucp [options] source destination`

源文件可以指定为本地或远程文件名。远程文件名的格式为：

`remotehost|filepath`

其中 `remotehost` 是文件所在计算机的 UUCP 名称。如果文件在本地计算机上，则 `remotehost` 名称既不是本地计算机或远程计算机的文件名，也不是目录名。

`uucp` 命令的成功取决于 UUCP 配置中为传输文件位置指定的权限以及执行传输的用户名。

## uux

`uux` 命令用于在远程计算机上执行命令。请求的命令作为任务排在 UUCP 溢空目录中，并在下一次 UUCP 通过 `uuicmo` 程序调用远程计算机时进行处理。`uux` 命令像普通文件传输一样处理，但它被标记为可执行文件。当命令发送到远程计算机时，将由远程计算机上的 `uuxqt` 命令执行。

## Linux UUCP 实现

如上一节所述，由 Ian Taylor 编写的 Taylor UUCP 软件包已成为 Linux 系统的标准 UUCP 软件包。大多数发行版都包含它的二进制包。本书光中的 Mandrake 系统在 `uucp-1.05.1586.rpm` 文件中包含了它。你可以使用 RPM 安装器以 root 安装 UUCP 功能。

如果你的 Linux 没有包含 UUCP 分发版，则有一个源码包可供 Linux 编译。我在常用的 Linux 站点 `site.unc.edu` 的 `/pub/linux/systems/network/uucp` 目录下找到了名为 `uucp-1.05.tar.gz` 的文件。如果你一直在跟着书学习，你应该知道安装和编译 UUCP 源码的标准步骤。如果不知道，这里是基本步骤：

1. 将源文件解压到工作目录：
   `tar -xvzf uuco-1.05.tar.gz`
2. 进入新创建的 `uucp-1.05` 子目录。
3. 运行 `configure` 命令创建一个适用于你系统的 `Makefile`。如果你想更改 UUCP 配置或日志文件的默认位置，可以为 `configure` 添加参数。输入 `configure --help` 查看操作操作说明。
4. 运行 `GNU make` 编译源码。
5. 作为 root 用户，运行 `make install` 选项将二进制文件安装到相应的目录。

安装二进制文件后，你就可以开始配置 UUCP 了。在 Linux 邮件服务器上使用 UUCP 需要了解服务器如何连接到 UUCP 从机，以及将使用什么方法和时间。以下章节展示了将 Linux 服务器同时作为 UUCP 主机和 UUCP 从机进行配置的示例。UUCP 主机将调用主机服务器（一个 IP）来递送和检查邮件。UUCP 从机将配置为接受来自远程 UUCP 计算机的连接。这种技术可以将邮件从远程 Linux 邮件服务器移动到主办公室的 Linux 邮件服务器。图 9.6 显示了 UUCP 主机和从机之间的关系。

## Linux UUCP Master

第一个要配置的 UUCP 文件是 `config` 文件。这是一个简单任务，因为不需要更改参数。列表 9.7 显示了客户端的示例 `config` 文件。

### 列表 9.7 Taylor UUCP 主机配置示例

```
nodename      shadrach
```

下一个要配置的文件是 `sys` 文件，它定义了我们将调用的远程主机。列表 9.8 显示了设置为调用的示例 `sys` 文件。

### 列表 9.8 Taylor UUCP 主机配置示例

```
system        shadrach

time          0800-1700

port          ispmail

speed         3840
```
