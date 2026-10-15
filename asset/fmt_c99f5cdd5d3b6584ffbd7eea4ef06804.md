
你希望通过向 root-shell 发布命令或简单地重启系统（如果不方便的话）来首次启动它。

# 注意

请注意，在对启动序列（包括报警启动脚本、创建新内核）进行任何更改时，确保你有一种简单的方法可以重启系统并撤销你的更改，以防你犯下错误导致系统无法启动。

这涉及一组救援磁盘。通常，这些磁盘在安装系统时创建，并且在重大更新后也应该这样做。它们由你的内核副本（经过 `rdev` 补丁处理，以便在软盘上寻找根文件系统）以及一个合适的救援根文件系统的压缩镜像组成。救援根文件系统可以通过 `dd` 从 Linux 发行版的 CD-ROM 中复制。所有这些步骤在《Linux 管理员文档》中都有描述。

最后，你需要在 `/etc/syslog.conf` 中添加该条目以读取

```
auth.notice | /usr/local/etc/syslog_auth
```

然后使用 `kill` 向 `syslog` 发送一个 `SIGHUP` 信号。现在你已经准备好通过尝试错误的密码或登录 ID 进行 `telnet` 登录来测试它。

# 16.5 为自动分页构建你的示例

你以那种特定的方式编写脚本，是因为它允许你轻松扫描其他事件并为它们生成自定义页面。在大型系统中，某些人的密码会很弱（除非你在第一部分中确保不讨论易于破解的密码）。

因此，一种常用技术是猜测某些用户的密码作为破入的第一步，然后尝试执行操作。（第一部分讨论了如何配置系统，使 `root` 仅能从物理安全的控制台登录，而不能通过破解机房的某处的 `telnet` 登录。）

当然，你可能会在失败的 `su` 尝试中需要分页显示。`su` 程序也会通过 `auth.notice` 记录尝试。因此，向你的脚本中添加几行代码并重启它。

```bash
#!/bin/csh -f

loop:

  set x="$$"

  echo "$x" | grep -q ' invalid password'

  if ($status == 0) then

    echo "$x"

    sed "s/\.*/.*\:\^([^ ]*)\*: invalid password for /BAD PW:\/"/\"

    Mail 1234567@skytel.com

  endif

  echo "$x" | grep -q 'su[:].*: Authentication failed'

  if ($status == 0) then

    echo "$x"

    sed "s/\.*/.*\^([^ ]*)\*: Authentication failed for /BAD SU:\/"/\"

    Mail 1234567@skytel.com

  endif

goto loop
```

这在对 `root` 执行 `su` 失败时将产生以下页面：

`BAD SU:cavu:root`

你不需要向 `syslogd` 发送消息，因为它的配置文件没有更改。

这第二个示例主要展示了如何为单个脚本添加消息处理程序。如果你的助手再次在调整系统，那么知道哪个账户尝试 `su` 到 `root` 以及在哪个终端上操作，将非常有帮助。

`su` 程序会记录这些额外信息，但处于调试级别。因为许多其他程序也会在此记录安全相关信息，请将所有这些信息通过你的脚本发送，你可以从中挑选要分页的消息。因此，编辑 `/etc/syslog.conf` 显示以下内容并向 `syslogd` 发送 `SIGHUP` 信号：

```
auth.* |/usr/local/etc/syslog_auth
```

（你也可以选择以其他方式处理某些信息，例如发送邮件到你的账户，可能在另一个系统上。在成功的破解中，你所有的“触丝线”都会失效，但通过将它们放置在所有入口处以便在系统被攻破之前获得“警告”，你仍然会收到警告，并希望在及时阻止破解者。）

原始日志消息如下所示：

```
Nov 24 13:13:18 cavu su[426]: tty2 bob-root
```

以下脚本将很好地处理此。（它可以从任何 `shell` 调用。）

```bash
#!/bin/csh -f

loop:

  set x="$$$"

  echo "$x" | grep -q ' : invalid password'

  if ($status == 0) then

    echo "$x"

    sed "s/\/.../...\\([^*]*\*: invalid password for /BAD PW:\" /\

    Mail 1234567@skytel.com

  endif

  echo "$x" | grep -q 'su[:].*: Authentication failed'

  if ($status == 0) then

    echo "$x"

    sed "s/\.*/.*\^([^ ]*)\*: Authentication failed for /BAD SU:\/"/\"

    Mail 1234567@skytel.com

  endif

goto loop
```

## 16.8 使用 tcpdump 监控你的局域网

美国政府能源和核研究实验室之一的劳伦斯·伯克利实验室（LBL）提供了 `tcpdump` Linux/Unix 工具。该工具是一个网络嗅探器，供系统管理员分析计算机和网络中的通用网络问题和安全问题。

在客户端/服务器软件开发的调试期间，我也发现 `tcpdump` 非常有用用。一个周六晚上，我接到一个电话，说服务器（我和 Larry Gee 共同创建的）对某些客户端请求没有响应。客户端工程师坚信不是他的问题，而且他自己水平非常高。

在免费晚餐的承诺下，我开车去了客户那里。在不到五分钟的时间内，`tcpdump`（来自第三台系统）证明了服务器发送了正确的回复。后来，确定 `bug` 在 Win 9x 中，是它没有交付数据包。

### 16.8.1 编译 tcpdump

可以从实验室下载 `tcpdump` 程序及相关软件，它易于设置和使用。首先，下载这三个文件：

- `ftp://ftp.ee.lbl.gov/libpcap.tar.Z`
- `ftp://ftp.ee.lbl.gov/pcapture-0.2.1.tar.Z`
- `ftp://ftp.ee.lbl.gov/tcpdump-3.4.tar.Z`

执行以下命令将文件解压到名为 `libpcap-0.4`、`pcapture-0.2.1` 和 `tcpdump-3.4` 的包含源码的子目录：

```
tar -xzovf libpcap.tar.Z

tar -xzovf pcapture-0.2.1.tar.Z

tar -xzovf tcpdump-3.4.tar.Z
```

然后，使用以下编译 `libpcap`：

```
cd libpcap-0.4

./configure

make

cd

ln -s libpcap-0.4 libpcap
```

编译 `pcapture`：

```
cd pcapture-0.2.1

./configure

make

su

make install

make install-man

exit
```

最后，编译并安装 `tcpdump`。

```
cd ../tcpdump-3.4

./configure

make

su

make install

make install-man
```

如果你使用的是 `csh`，请执行 `rehash` 命令。要观察 ARP 数据包，以下是一个起点：

```
tcpdump arp
```

同样，可以使用以下命令观察 ICMP 数据包：

```
tcpdump icmp
```

### 16.8.2 使用 tcpdump

这里讨论了 `tcpdump` 一些最有用的标志。`-i` 标志用于指定要使用的接口。`-i` 标志会导致 `tcpdump` 即使不输出到 `tty` 也进行行缓冲。这在以下情况下非常有用：希望立即输出到屏幕上，同时也捕获到文件中以便稍后详细分析。

```
tcpdump -l other options | tee foo
```

或者

```
tcpdump -l other options > foo & tail -f foo
```

- `-N` 标志在第一个点处截断显示的主机名。在任何标志后面都可以跟一个可选表达式，指定转储哪些数据包。缺少表达式将导致转储所有数据包。如果你通过网络 `telnet` 或 X 会话运行 `tcpdump`，此 I/O 将被显示出来。表达式（想象成“无限循环”）类似于语言或 `find` 程序中的表达式。

用于构建表达式的某些“原始”元素包括以下内容。

- **type** 这个命名有点不准确，它是按主机、网络或端口选择的。这些每个都接受一个指定符，例如主机名或 IP 地址。`net` 原始元素接受 `addressbits`，其中 `address` 是 IP 地址，`bits` 是要匹配的高位字节数。因此，Pentacorp 的 "B" 类用户使用：

```
net 192.168.0.0/16
```
