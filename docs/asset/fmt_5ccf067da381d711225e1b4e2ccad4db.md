
| order=data,control | 先将控制文件发送到远程打印机（默认） |

# 设置打印机与类 第 3 章

`serial://dev/ttyS0`

`serial://dev/serial/0`

串口后端支持多种选项，如表 3.4 所示：

### 表 3.4 串口设备选项

| 选项 | 描述 |
| :--- | :--- |
| baud=N | 设置串口波率为每秒比特数（波特）。默认值通常为 9,600 波特。最大值由 `ipinto` 命令报告。 |
| bits=7 | 将每个字符的数据位数设置为 7 位。 |
| bits=8 | 将每个字符的数据位数设置为 8 位（默认）。 |
| flow=rtcts | 设置流控制为使用请求发送（RTS）和清除发送（CTS）信号线。 |
| flow=dtrsr | 设置流控制为使用数据终端就绪（DTR）和数据设置就绪（DSR）信号线。 |
| flow=hard | 设置流控制为使用请求发送（RTS）和清除发送（CTS）信号线。 |
| flow=none | 完全禁用流控制（默认）。 |
| flow=soft | 使用 XON 和 XOFF 字符进行流控制；这种方法在打印机上通常不可靠。 |
| parity=even | 每个字符发送奇偶性校验；所有比特位之和的结果必须为偶数。 |
| parity=none | 不发送奇偶性校验（默认）。 |
| parity=odd | 每个字符发送奇偶性校验；所有比特位之和的结果必须为奇数。 |

在端口 1 上运行、波特率为 19200、使用 7 位数据位、偶校验校验以及 DTE-DSR 流控制的打印机需要以下设备 URI：

```
serial://dev/ttyS0baud=19200+bits=7+parity=even+flow=dtedsr
```

由于串口端口与其他接口相比非常慢，它通常作为最后的选择，或用于向针式打印机打印文本。

### SMB 设备

SMB 设备支持使用 SMB 协议打印到 Windows 打印机，由 SAMBA 软件提供。SMB 打印机的 URI 如下：

```
smb:////workgroup/server/name
```

### 使用 CUPS

其中 `workgroup` 是服务器所属的工作组名称，`server` 是服务器的 NetBIOS 名称，`name` 是打印机的共享名称。对于工作组 "ESP" 中服务器 "foo" 上的名为 "bar" 的打印机，其 URI 为：

```
smb://ESP/foo/bar
```

如果共享打印机需要用户名和密码（通常从 Windows NT 或 2000 服务器共享的打印机都是如此），可以在 URI 中提供：

```
smb://username:password@workgroup/server/name
```

## 注意

由于在 URI 中包含用户名和密码可能存在安全问题，你可能希望改用 Windows NT 提供的 TCP/IP 打印服务或 Windows 2000 提供的 IPP 打印服务。

这些服务的额外益处是将正确的用户名与打印作业关联，因为 `sm` 后端只能发送你在 URI 中提供的用户名。

### Socket 设备

`socket` 设备支持使用 TCP/IP 套接字进行直接打印，通常称为 AppSocket 打印或 JetDirect 协议。设备 URI 只需要服务器名称以及可选的端口号：

```
socket://server
```

```
socket://server:port
```

默认端口号为 9100，所有 HP JetDirect 接口和许多其他网络打印机均使用它。表 3.5 显示了各种设备使用的端口号：

### 表 3.5 Socket 设备的 URI

| 制造商 | URI |
| :--- | :--- |
| Axis | `socket://server:9100` (Parallel 1) <br> `socket://server:9101` (Parallel 2) <br> `socket://server:9102` (Parallel 3) |
| EPSON | `socket://server` |
| Hewlett Packard | `socket://server` (Internal) <br> `socket://server:9100` (Parallel 1) <br> `socket://server:9101` (Parallel 2) <br> `socket://server:9102` (Parallel 3) |
| Lexmark | `socket://server:5503` |

### 表 3.5 续

| 制造商 | URI |
| :--- | :--- |
| Linksys | `socket://server:4010` (Parallel 1) <br> `socket://server:4020` (Parallel 2) <br> `socket://server:4030` (Parallel 3) |
| NETGEAR | `socket://server:4010` (Parallel 1) <br> `socket://server:4020` (Parallel 2) <br> `socket://server:4030` (Parallel 3) |
| Tektronix | `socket://server` |
| XEROX | `socket://server:5503` |

`socket` 设备是网络打印机或服务器支持的性能最好且最可靠的设备。`socket` 设备还可以将打印数据流到打印机，而其他网络设备在发送到打印机之前需要将打印数据存储在临时文件中。

### USB 设备

USB 设备支持通过通用总线（USB）打印。USB 目前适用于 Linux 和 PC BSD 操作系统。USB 打印机的设备 URI 差异很大，即使在 Linux 发行版之间也是如此，例如

```
usb://dev/bus/usb/001/002
usb://dev/bus/usb/n/n
```

其中 `n` 是 USB 端口号。对于 USB 打印机，`n` 是动态分配的。注意：USB 打印机不支持流控制。

## 打印机驱动

CUPS 打印机使用 PPD（打印描述文件）来配置打印机。CUPS 包含 PPD 文件。对于 CUPS 提供的 PPD 文件，在表 3.6 中列出了这些文件。

PPD 文件通常位于 `/usr/share/cups/ppd/`。
