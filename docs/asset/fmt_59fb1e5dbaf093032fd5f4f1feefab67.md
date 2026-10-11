
bootpef 构建由 RFC 1497（标记 18）描述的扩展路径文件。如果指定了任何 `CLIENT_NAME` 参数，`bootpef` 将为这些客户端编译扩展文件。

# 网络管理：chat 211

| 选项 | 描述 |
| --- | --- |
| `-c CHDIR_PATH` | 设置创建扩展文件时使用的当前目录。当扩展文件名指定为相对路径，且 `bootpd` 需要使用 TFTP 服务器使用相同的当前目录（通常为 `/tftpboot`）时，这非常有用。 |
| `-d DEBUG_LEVEL` | 设置 `DEBUG_LEVEL` 值，控制生成的调试消息。例如，`-d4` 或 `-d 4` 将调试级别设置为 4。 |
| `-f CONFIG_FILE` | 设置指定发送到每个客户端的选项数据的配置文件名称。默认值为 `/etc/bootptab`。 |

# boottest

`boottest OPTION ... SERVER_NAME [ TEMPLATE_FILE ]`

`boottest` 向指定为 `SERVER_NAME` 的主机按一个间隔发送 `BOOT REQUEST`，直到收到响应或十个请求未被答复。收到响应后，`boottest` 将再等待一秒，监听额外的响应。可以指定 `TEMPLATE_FILE`，其中可以指定选项。

| 选项 | 描述 |
| --- | --- |
| `-f CONFIG_FILE` | 设置指定发送到每个客户端的选项数据的配置文件名称。 |
| `-h` | 指定一个 `TEMPLATE_FILE`。 |
| `-m` | 指定 `TEMPLATE_FILE`。 |
| `-s` | 指定 `TEMPLATE_FILE`。 |
| `-t` | 指定 `TEMPLATE_FILE`。 |
| `-u` | 指定 `TEMPLATE_FILE` |
| `-v` | 打印版本并退出 |

# 214 网络管理: dip, diplogin, and diplogini

>>继续

```bash
#创建新连接默认路由并进入 CSLIP（带有压缩
#数据报头部的 SLIP）模式。
done:
default
mode CSLIP
goto exit
```

error:

打印：连接失败

exit:

## pppconfig

```bash
pppconfig [--help] [--version]
```

`pppconfig` 是一个交互式的菜单驱动实用程序，可以帮助自动设置拨号连接 PPP 连接。

| 选项 | 描述 |
|---|---|
| `--help` | 打印帮助信息并退出。 |
| `--version` | 打印版本号并退出。 |

## pppd

```bash
pppd [ TTY_NAME ] [ SPEED ] [ OPTIONS ]
```

`pppd` 是点对点协议（PPP）守护进程。它是通过串行点对点链路传输数据报的首选方法。PPP 由三部分组成：一种在串行链路上封装数据报的方法，一个可扩展的链路控制协议（LCP），以及一组用于建立和配置不同网络层协议的网络控制协议（NCP）。

封装方案由内核中的驱动代码进行认证，该代码提供了基本的 LCP、认证支持以及用于建立和配置 Internet 协议（IP）的 NCP——称为 IP 控制协议，或 IPCP。

`pppd` 接受大量的命令行选项。最常用的选项列如下表所示：

| 选项 | 描述 |
|---|---|
| `SPEED` | 将波特率设置为 `SPEED`（十进制）。 |
| `TTY_NAME` | 进行通信的串行设备名称。如有必要，将添加 `/dev` 前缀。如果没有给设备设备名称，或者给出的是连接到标准输入的终端名称，`pppd` 将使用该终端，且不会派生并将自己置于后台。 |

## 网络管理: pppp 25

| 选项 | 描述 |
|---|---|
| `asyncmap MAP` | 将异步字符映射设置为 `MAP`。此映射描述了哪些控制字符无法在串行线路上成功接收。`pppp` 会要求对端以双字节转义序列的形式发送这些字符。该参数是一个 32 位的十六进制数，每位代表一个需要转义的字符。位 0 (`00000001`) 代表字符 `0x00`；位 1 (`00000010`) 代表字符 `0x1f` 或 _。如果给出多个 `asyncmap` 选项，这些值将通过或 操作组合。如果没有给出 `asyncmap` 选项，则接收方向将不会协商异步字符映射。对端应该对所有控制字符进行转义。 |
| `auth` | 要求对端在允许发送或接收网络包之前进行身份认证。 |
| `call NAME` | 从文件 `/etc/ppp/peers/NAME` 读取选项。字符串名称不能以 `/` 开头，或包含 `..` 作为路径组件。 |
| `connect SCRIPT` | 使用 `SCRIPT` 指定的可执行文件或 shell 命令来设置串行链路。此脚本通常使用 `chat` 程序拨号调制解调器并启动 PPP 会话。 |
| `crtscts` | 使用硬件流控来控制串口上的数据流。 |
| `defaultroute` | 当 IPCP 协商成功完成后，向内核路由表添加默认路由，使用对端作为网关。当 PPP 连接断开时，该项将被移除。 |
| `disconnect SCRIPT` | 在 `pppp` 终止链路后，运行 `SCRIPT` 指定的可执行文件或 shell 命令。 |
| `escape CHARS` | 指定在传输时转义某些字符，无论对端是否要求通过其异步控制字符映射进行转义。`CHARS` 是一个用逗号分隔的十六进制列表。 |
| `file NAME` | 从文件 `NAME` 读取选项。 |
| `lock` | 指定 `pppp` 应为串行设备创建一个 UUCP 类型的锁，以确保对设备的独占访问。 |
| `mru N` | 将最大接收单元（MRU）值设置为 `N`。`pppp` 将要求对端发送不超过 `N` 字节的数据包。最小 MRU 值 128。 |
| `mtu N` | 将 MTU（最大传输单元）值设置为 `N`。除非对端通过 MRU 协商请求更小的值，否则 `pppp` 将要求内核通过 PPP 接口发送不超过 `N` 字节的数据包。 |
| `passive` | 启用 LCP 中的“被动”选项。当 `pppp` 尝试启动连接时如果没有收到对端的回复，`pppp` 将被动等待来自对端的有效 LCP 包，而不是像没有此选项时那样退出。 |

## 网络管理: pppp

以下 bash 脚本用于启动 PPP 连接。这是这对脚本的第一部分。尽管这些脚本很简单，但它们是不安全的，因为代码可以通过 `ps` 命令看到。

```bash
#!/bin/sh
#
## 这些是参数。根据需要更改。
TELEPHONE=555-1212    # 连接的电话号码
ACCOUNT=mistered      # 登录账户名
PASSWORD=wilbur       # 该账户的密码
LOCAL_IP=0.0.0.0      # 如果需要的本地 IP 地址。动态 IP = 0.0.0.0
REMOTE_IP=0.0.0.0    # 如果需要的远程 IP 地址。通常为 0.0.0.0
NETMASK=255.255.255.255
```

## 网络管理: pppstats 27

以下脚本用于关闭由前面的脚本建立的 PPP 连接。
