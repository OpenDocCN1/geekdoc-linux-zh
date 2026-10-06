
# C-Kermit 使用说明

在选项中，有一组所谓的命令行操作选项（`action options`），这些选项需要执行特定操作才能完成任务。如果命令中没有操作选项，`C-Kermit` 将在交互式命令模式下启动；显示欢迎消息和 `C–Kermit` 提示符。如果在命令行上指定了操作选项，`C-Kermit` 将执行指示的操作然后返回到 `UNIX`。无论何种情况，`C-Kermit` 在执行任何其他命令之前，都会执行初始化文件 `ckermit`（通常位于目录 `/usr/share/lib/kermit`）中的命令。异常情况是显式请求了备初始化。

`C-Kermit` 是一个极其强大且功能多样的程序，其 `C-Kermit` 命令用于：

- 程序管理
- 连接的建立与释放
- 终端连接
- 文件传输
- 文件管理
- 客户端/服务器操作
- 脚本编程

每个列出的命令组都包含相当的 `C-Kermit` 命令；合在一起它可以成功完成最复杂的任务。用大写字母指定 `C-Kermit` 命令是常见做法，我们将遵循这一惯例。

大量现有的选项还可以分为：

- 类似于 `connect`、`发送/接收文件`、进入/终止服务器模式等类型的操作选项
- 设置选项，更详细地指定涉及文件传输、连接过程及类似的不同 `kermit` 参数
- 其他类型，如跳过/备初始化、前台、后台、强制驻留、显式交互、远程或调试模式。

## 文件传输常见场景

为了更好地理解 `C-Kermit` 如何工作，让我们看看直接连接的计算机之间 `C-Kermit` 文件传输的常见场景，在这里被标识为本地计算机和远程计算机。网络上的文件传输略有不同。虽然其他方法也是可行的，但这种方法在所有情况下都适用，它包括：

- 在本地计算机上启动 `C-Kermit` 并建立到远程计算机的连接。使用序列：
  * `SET MODEM TYPE modem-name`
  * `SET LINE device-name`
  * `SET SPEED bits-per-second`
  * 如果拨号，则执行 `DIAL phone-number`。
  * 网络连接下使用 `SET network-type` 和 `HOST host-name-or-address`。
- 设置任何其他必要的通信参数，如 `PARITY`、`DUPLEX` 和 `FLOW-CONTROL`。
- 发出 `CONNECT` 命令。
- 登录远程计算机，针对文件、通信或协议相关参数给出任何所需的 `SET` 命令。如果要传输二进制文件，则在发送端对 `C-Kermit` 程序执行 `SET FILE TYPE BINARY`。
- 要传输文件或文件组，向本地 `C-Kermit` 发出 `SEND` 命令，后跟文件名或“通配符”文件规范：
  * `send filename.txt` # 发送一个文件
  * `send filename` # 发送一组文件
- 要接收文件或多个文件，向远程 `C-Kermit` 发出 `RECEIVE` 命令。发送端和接收端的 `Kermit` 将交换每个文件的名称和属性。
- 转逸 `Escape` 回到本地计算机上的 `C-Kermit` 程序以获取本地 `Kermit` 程序的提示符。
- 要传输二进制文件，向发送文件的 `Kermit` 程序给出命令 `SET FILE TYPE BINARY`。
- 要接收文件，告诉本地 `C-Kermit` 程序 `RECEIVE`；要传输文件，让 `C-Kermit` 程序 `SEND`，并发送文件名或通配符规范。换句话说，先告诉 `C-Kermit` 程序执行什么 `SEND` 或 `RECEIVE`，然后转逸回到本地 `C-Kermit` 并给它相反的命令 `RECEIVE` 或 `SEND`。
- 传输完成后，发出 `CONNECT` 命令与远程计算机上的 `C-Kermit` 通。输入 `EXIT` 返回远程计算机的命令提示符。当一切完成后，注销并（如有必要）转逸回到本地计算机上的 `Kermit`。然后可以建立另一个连接，或从本地 `C-Kermit` 程序 `EXIT`。

## 性能优化

`C-Kermit` 的文件传输协议默认值是刻意保守的，导致文件传输几乎总是有效的，但可能较慢。为了在允许的计算机和连接上提高传输性能：

- `RECEIVE PACKET-LENGTH` 以增加包长度
- `SET WINDOW` 以增加包窗口大小
- `SET PREFIXING` 以减少控制字符前缀的开销

另一种，尝试使用 `FAST` 命令一次性启用所有这些性能选项是值得的。在串口连接上，如果可用，使用硬件流控 `SET FLOW RTS/XTS` 而不是软件 `XON/XOFF` 流控。

显然，为了成功的输出，有很多步骤应该妥善完成。编写脚本处理相当复杂的场景并让一切变得简单得多是个好主意。以下是关于如何使用 `C-Kermit`：

- 远程模式，当 `C-Kermit` 通过直接串口连接、拨号调制调器或建立网络连接到另一台计算机时使用。
- 本地模式，当 `C-Kermit` 使用实际终端、仿真器或 `UNIX` 工作站终端窗口或用于特定终端仿真的控制台驱动程序，为远程计算机提供终端连接时的模式。

`C-Kermit` 还有两种类型的命令：

- 1. 熟悉的 `UNIX` 风格命令，带有提示符，它提供了 `C-Kermit` 用于终端连接和文件传输的一个较小但实用的功能集，并具有将文件通过管道 `pipe` 输入或输出到 `C-Kermit` 进行传输的能力。它还提供了拨号、脚本编程、字符集转换的访问，并且通常提供了对 `C-Kermit` 所有特性的详细控制和显示。交互式命令也可以收集到命令文件或宏中。

```
kermit [command-file] [options...]
```

## 脚本示例

```bash
#!/bin/bash

# 此脚本是一个示例模板，展示了如何通过脚本来处理 C-Kermit 文件传输的复杂场景。

# 这种方法可以使手动操作变得简单得多。

# 定义变量

REMOTE_HOST="192.168.1.100"

REMOTE_USER="user"

LOCAL_FILE="data_report.csv"

REMOTE_DIR="/home/user/downloads"

MODEM_NAME="your_modem_name"

DEVICE="/dev/ttyS0"

SPEED=9600

echo "开始 C-Kermit 文件传输脚本..."

# 1. 在本地计算机上启动 C-Kermit 并建立连接

# 模拟序列：

# SET MODEM TYPE $MODEM_NAME

# SET LINE $DEVICE

# SET SPEED $SPEED

# DIAL 123456789

# SET network-type none

# SET HOST $REMOTE_HOST

# 2. 设置其他必要的通信参数

# SET PARITY NONE

# SET DUPLEX FULL

# SET FLOW-CONTROL HARD

# 3. 发出 CONNECT 命令

# CONNECT

# 4. 登录远程计算机并设置参数

# login $REMOTE_USER@$REMOTE_HOST

# SET FILE TYPE BINARY

# 5. 传输文件

echo "正在发送文件 $LOCAL_FILE..."

# send $LOCAL_FILE

# 6. 传输完成后并退出

# CONNECT

# EXIT

echo "传输任务完成。"

# 注意：此脚本仅为逻辑演示，实际执行需要根据环境取消注释对应的命令。
```
