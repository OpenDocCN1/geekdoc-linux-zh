
`maria:$6g$Jg6.d8mN.en...:1002:1002:/home/maria:/bin/bash`

`hugh:$6sUinuqQY$ID59.N...:1003:1003:/home/hugh:/bin/bash`

`john`在几秒钟发现了两个特别不安全的密码。`peter`使用了他的名字作为密码，而`hugh`使用了常用密码“123456”。然而，`Maria`的密码无法立即破解，这就是为什么在运行一段时间后通过按下`Ctrl+C`停止了进程：

```
user John hashes

Loaded 3 password with 3 different salts

Press 'q' or Ctrl-C to abort, almost any other key for status

peter (peter)

123456 (hugh)

<Strg++C>
```

你可以使用`git`从GitHub下载常用密码列表。（注意：这些列表所需的空间大约为750 MiB！）这些字典中实际上有一个一个包含了`Maria`的密码！它的内容是`secret`：

```bash
user$ git clone https://github.com/danielmiessler/SecLists.git

user$ john --wordlist=SecLists/Passwords/Common-Credentials/\
10-million-password-list-top-10000.txt hashes

Loaded 3 password hashes with 3 different salts

Remaining 1 password hash with 1 different salt

(maria)
```

## 替代方案

在GitHub上有一个大幅扩展的、由社区维护的“jumbo”版本`john`：

`https://github.com/openwall/john`

如果你想通过GPU支持显著加快哈希码的破解，你应该考虑使用`hashcat`。在这种情况下，最大的障碍是安装合适的GPU驱动程序。要检查网络服务是否存在不安全的密码，你可以使用在线密码破解器：`hydra`。

> `journalctl [options] [search expression]`

`journal`是属于`systemd`的`syslog`服务。它现在运行在大多数常见的Linux发行版上，有时会与传统的日志系统（通常是`rsyslogd`）并行运行。

`journal`文件以二进制格式保存，只能使用此处描述的`journalctl`命令进行读取。

一个或多个搜索表达式可以表示为程序的路径，或者使用`field=value`语法。然后`journalctl`只显示符合所有搜索表达式的日志目。带有逻辑或关系的搜索表达式可以使用`+`构造，即`field1=value1 + field2=value2`。

字段允许使用`MESSAGE`、`PRIORITY`、`ERNO`以及`_UID`、`_PID`、`GID`或`_SELINUX_CONTEXT`关键字。附加搜索参数的参考及其含义的详细说明可以通过`man systemd.journal-fields`找到。

在不带进一步参数的情况下调用时，`journalctl`通常返回一个几乎无尽的日志消息列表，但你可以使用选项来过滤输出：

- `-b`
显示自计算机上次重启以来的消息。

- `--disk-usage`
显示`journal`文件占用`/var/log`多少空间。

- `-e`
立即跳转到要显示的消息的末尾。

- `-f`
以连续模式启动`journalctl`，不断显示当前到达的消息。`Ctrl + C`终止命令。

- `-k`
仅显示内核消息。

- `-n systemd.Journal`
仅显示最后`n`行。

- `--no-pager`
直接将输出写入到标准输出，而不是使用分页器。

- `-p`
显示指定优先级别的消息。

- `--since`
显示自指定时间之后的消息。

- `--until`
显示到指定时间为止的消息。

- `--vacuum-size=SIZE`
删除`journal`文件，直到空间达到指定的大小。

- `--vacuum-time=TIME`
删除指定时间之前的`journal`文件。

- `--unit`
只显示指定单元的消息。

- `-t`
显示指定标签的消息。

- `--user`
显示指定用户的消息。

在第二步中，你必须激活新内核——可以通过`kexec -e`立即激活，也可以在通过`systemd`停止正在运行的服务后激活。在服务器上，这是确保数据库服务器等能够完成所有打开的事务并正常关闭文件的唯一方法。

```bash
root# kexec -e
```
立即重启

```bash
root systemctl isolate kexec
```
先停止服务，然后重启

## `kill [-s signal] 进程号`

`bash`命令`kill`向正在运行的进程发送信号。如果使用`kill`时不带`-s`选项，默认会发送`SIGTERM`信号 (`15`) 来终止（`kill`意为杀死，因此该命令以此为名）进程。在特殊情况下，使用`-9`、`-s SIGKILL`或`-KILL`会有帮助。然而，进程将没有机会执行任何清理工作。

然而，`kill`也可以用于发送更无害的信号。经常使用`-1`、`-s SIGHUP`或`-HUP`来请求守护进程重新加载配置文件。通过这种方式，你可以为某些程序激活新配置，而无需完全停止并重启守护进程。

获取所需进程号 (`PID`) 的`kill`方便变体最简单的方法是使用`ps`命令：要终止的程序可以直接用鼠标“点掉”。

```
killall [-signal] 进程名
```

`killall`的工作方式几乎与`kill`命令一样。区别在于它指定的不是进程号 (`PID`)，而是进程名称。如果有多个同名进程，它们都会接收指定的信号（同样默认为`SIGTERM`）。所需的信号可以通过`-n`或如`-HUP`的名称指定。你可以通过`killall -l`获取所有信号列表。

### 示例

以下示例终止了所有运行的`firefox`实例。如果由`root`执行`kill`命令，将终止所有用户的所有`firefox`进程。

```
user$ kill firefox
```

## `kpartx [磁盘设备]`

来自包的底层命令`kpartx`指定数据媒体的所有分区并创建相应的设备文件。通常，当连接USB磁盘时，`udev`系统会自动创建设备文件。`kpartx`主要用于编辑数据媒体或虚拟机镜像。

- `-a`为指定的数据媒体创建新的设备文件。
- `-d`删除数据媒体的设备文件。
- `-l`读取数据媒体的分区但不创建任何设备文件。
- `-u`更新数据媒体的设备文件。
- `-v`提供执行操作的信息。

### 示例

以下命令连接原始镜像文件中包含的所有`loop`设备：

```
root# kpartx -av image.raw

map loop0p1 (252:12): 0 102400 linear /dev/loop0
map loop0p2 (252:13): 0 199457 linear /dev/loop0
```

整个硬盘可以通过`/dev/mapper/loop0`访问。

```
kvm [options] [镜像文件]
```

`kvm`脚本在Ubuntu上常用于运行虚拟机。`qemu`模拟器和基于内核的虚拟机 (`KVMs`)在大多数其他发行版中，虚拟机通过`qemu`命令启动，那里描述了大量的相同选项。

## `l2ping [options] 蓝牙`

来自`bluez`包的`l2ping`向由MAC地址指定的蓝牙设备发送L2CAP回显请求。通过这种方式，你可以测试本地蓝牙适配器与外部设备之间是否可以连接。`l2ping`必须以`root`权限运行。你可以使用`hcitool scan`确定外部设备的MAC地址。

## `lame [options] 输出文件`

`LAME`的缩写并不是MP3编码器，但`lame`命令实际上用于将WAV文件转换为与MP3格式兼容的压缩音频文件。`lame`的替代方案是`toolame`或`twame`，它们都创建MPEG-1 Layer 2（即MP2）。大多数MP3播放器也可以这种文件。

- `r`源文件为原始格式（而非WAV文件）。
- `s`指定原始文件的采样频率。WAV文件不需要此选项。

### 示例

以下命令创建兼容MP3的音频文件：

```
user$ lame title.wav
```
