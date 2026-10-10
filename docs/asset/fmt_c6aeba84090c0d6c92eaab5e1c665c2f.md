
`-initrd "file1 arg=foo, file2"`

此语法仅在 `libgrub` 下可用。

使用 `file1` 和 `file2` 作为模块，并将 `arg=foo` 作为参数传递给第一个模块。

`-dtb file`

将 `file` 用作设备树二进制（dtb）镜像，并在启动时传递给内核。

### 调试/专家选项：

`-fw_cfg [name=]name, file=file`

从 `file` 添加名为 `name` 的 `fw_cfg` 条目。`name` 决定了暴露给客户的 `fw_cfg` 文件目录中条目的名称。

`-serial dev`

将虚拟串行端口重定向到主机字符设备 `dev`。默认设备在图形模式下为 `vc`，在非图形模式下为 `stdio`。

此选项可以使用多次，最多设置 4 个串行端口。

使用 `-serial none` 可禁用所有串行端口。

可用的字符设备有：

- `vc[:WxH]`

  虚拟控制台。可选地，可以通过 `vc:800x600` 以像素为单位指定宽度和高度。

  也可以以字符为单位指定宽度或高度：

  `vc:80Cx24C`

- `pty`

  [仅限 Linux] 伪 TTY（会自动分配一个新的 PTY）

- `none`

  不分配设备。

- `null`

  空设备

- `chardev:id`

  使用通过 `-chardev` 选项定义的命名字符设备。

- `/dev/XXX`

  [仅限 Linux] 使用主机 tty，例如 `/dev/ttyS0`。主机串行端口参数将根据所选设置进行配置。

- `/dev/parportN`

  [仅限 Linux，仅限并行端口] 使用主机并行端口 N。目前可以使用 SPP 和 EPP 并行端口功能。

- `file:filename`

  将输出写入 `filename`。无法读取字符。

- `stdio`

  [仅限 Unix] 标准输入/输出

- `pipe:filename`

  以管道方式打开 `filename`。

### QEMU 串口和调试选项

`na pipe` `filena`

### COMn

**[仅限 Windows]** 使用主机串口 *n*

### `udp:remote_host:remote_port[@src_ip]:src_port`

这实现了 UDP 网络控制台。当未指定 `remote_host` 或 `src_ip` 时，它们默认为 `0.0.0.0`。当未使用指定的 `src_port` 时，会自动选择一个随机端口。

如果你只需要一个简单的只读控制台，你可以使用 netcat 或 nc，通过以下方式启动 QEMU：`-serial udp::4555`，以及使用 nc：`nc -u -l -p 4555`。只要 QEMU 向该端口写入任何内容，它都会出现在 netconsole 会话中。

如果你计划通过 netconsole 回传字符，或者你想多次停止和启动 QEMU，你应该让 QEMU 每次使用相同的源端口，例如使用 `-serial udp::`。另一种方法是使用打过补丁的 netcat 版本，该版本可以监听 TCP 端口并通过 udp 发送和接收字符。如果你有一个打过补丁的 netcat 版本，该版本可以激活 telnet 远程回显和单字符传输，那么你可以使用以下选项设置一个 netcat 重定向器，以允许通过端口 5555 的 telnet 访问 QEMU 端口。

- QEMU 选项：

  - `-serial udp::`

- netcat 选项：

  - `-u -P 4555 -L 0.0.0.0:4556 -t -p 5555 -I -T`

- telnet 选项：

  - `localhost 5555`

### `tcp:host:port[server[,nowait][,nodelay][,reconnect=seconds]]`

TCP 网络控制台有两种运行模式。它可以将串行 I/O 发送到某个位置，或者等待来自某个位置的连接。默认情况下，TCP 网络控制台会发送到 *该主机的该端口*。如果你使用 `server` 选项，QEMU 将在继续之前等待客户端套接字应用程序连接到该端口，除非指定了 `nowait` 选项。`nodelay` 选项禁用了 Nagle 缓冲算法。`reconnect` 选项仅在设置 `noserver` 时生效，如果连接断开，它将尝试以给定的间隔重新连接。如果省略 `host`，则假定为 `0.0.0.0`。每次仅接受一个 TCP 连接。你可以使用 telnet 连接到相应的字符设备。

向 192.168.0.2 的 4444 端口发送 tcp 控制台的示例

```
-serial tcp:192.168.0.2:4444
```

在 4444 端口监听并等待连接的示例

```
-serial tcp:4444,server
```

不等待并在 ip 192.168.0.100 的 4444 端口监听的示例

```
-serial tcp:192.168.0.100:4444,server,nowait
```

### `telnet:host:port[,server[,nowait[,nodelay]]]`

使用 telnet 协议而不是原始 tcp 套接字。选项的操作方式与指定 `-serial tcp` 时相同。区别在于，该端口使用 telnet 选项协商，充当 telnet 服务器或客户端。如果你使用支持发送中断序列的 telnet，这将允许你发送 `MAGICKBRK` 序列。通常在 unix telnet 中，你通过 Control-] 实现，然后输入 “send break” 并按下回车键。

### `unix:path[,server][,nowait][,reconnect=seconds]`

使用 unix 域套接字而不是 tcp 套接字。该选项的操作方式与指定 `-serial tcp` 时相同，只是使用 unix 域套接字路径进行连接。

### `mon:dev_string`

这是一个特殊选项，允许将监控器复用到其他串行端口上。监控器通过按键序列 `Control-a` 然后按下 `c` 来访问。`dev_string` 可以是上述任何串行设备。一个将监控器复用到监听端口 4444 的 telnet 服务器上的示例是：

```
-serial mon:telnet::4444,server,nowait
```

当监控器以这种方式复用到 stdio 时，Ctrl+C 将不再终止 QEMU，而是传递给来宾。

### `braille`

盲文设备。这将使用 BrAPI 在真实或虚拟设备上显示盲文输出。

### `msmouse`

三键串行鼠标。配置来宾使用微软协议。

### `-parallel dev`

将虚拟并行端口重定向到主机设备 `dev`（与串行端口相同的设备）。在 Linux 主机上，`/dev/parportN` 可用于使用连接在相应主机并行端口上的硬件设备。

此选项可以使用多次以模拟最多 3 个并行端口。

使用 `-parallel none` 来禁用所有并行端口。

### `-monitor dev`

将监控器重定向到主机设备 `dev`（与串行端口相同的设备）。默认设备在图形模式下为 `vc`，在非图形模式下为 `stdio`。使用 `-monitor none` 来禁用默认监控器。

### `-qmp dev`

与 `-monitor` 类似，但以‘控制’模式打开。

### `-qmp-pretty dev`

与 `-qmp` 类似，但使用漂亮的 json 格式化。

### `-mon [chardev=chardev_id[,mode=readline|control][,default]]`

在字符设备 `chardev_id` 上设置监控器。

### `-debugcon dev`

将调试控制台重定向到主机设备 `dev`（与串行端口相同的设备）。调试控制台是一个 I/O 端口，通常是端口 `0xe9`；向该 I/O 端口写入会将输出发送到此设备。默认设备在图形模式下为 `vc`，在非图形模式下为 `stdio`。

### `-pidfile file`

将 QEMU 进程 PID 存储在 `file` 中。如果你从脚本启动 QEMU，这将很有用。

### `-singlestep`

以单步模式运行仿真。

### `-S`

启动时不启动 CPU（你必须输入 ‘c’ 在监控器中）。

### `-realtime=on|off`

以实时功能运行 QEMU。可以通过 `lock=on` 启用锁定 QEMU 和来宾内存（默认启用）。

### `-gdb dev`

等待 gdb 在设备 `dev` 上的连接。典型的连接可能是基于 TCP 的，但 UDP、伪 TTY 甚至 stdio 也是合理的使用场景。后者允许从 gdb 内部启动 QEMU 并通过管道建立连接：

```
(gdb) target remote | exec qemu-system-i386 -gdb stdio...
```

### `-s`

`-gdb tcp::1234` 的简写形式，即在 TCP 端口 1234 上打开一个 gdbserver。

### `-d item1[,...]`

启用指定项的记录。使用 ‘`-d help`’ 获取日志项列表。
