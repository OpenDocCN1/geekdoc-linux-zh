
# 第五部分 网络

## 第 24 章 通过调制解调器访问其他 UNIX 系统

### 使用 cu 传输文件

5. `cu` 程序将提示你文件传输到远程系统后要命名的名称。你可以直接按回车键使用相同的名称。

6. `cu` 程序将指示传输何时完成。

7. 输入 `- .` 断开连接并返回 shell 提示符。

列表 24.2 说明了上述步骤的执行过程，显示了将文件 `/home/report` 传输到远程连接的系统。注意，也可以使用其他转义序列来传输文件。输入 `-` 命令列出你的 `cu` 程序实现中的可用命令。

### 列表 24.2 使用 cu 传输文件

```
-[local_host]?
[Escape sequences]
[.- hangup] [!CMD run shell]
[-$CMD stdout to remote] [-CMD stdin from remote]
[+CMD stdin and stdout to remote]
[# send break] [-CDIR change directory]
[-> send file] [<- receive file]
[-pFROM TO send Unix] [-tFROM TO receive Unix]
[-sVAR VAL set variable] [-sVAR set boolean]
[-!sVAR unset boolean] [-v list variables]
[-z suspend]
[%break send break] [%cd DIR change directory]
[%put FROM TO send file] [%take FROM TO receive file]
[~nopstop no XON/XOFF] [-stop use XON/XOFF]
[connected]
[~nopstop no XON/XOFF] [-stop use XON/XOFF]
[connected]
[~nopstop no XON/XOFF]
[connected
]
```

### 在远程 UNIX 系统上运行

1. 远程 UNIX 系统需要配置 `/usr/lib/uucp/Permissions` 文件。

2. 在远程 UNIX 系统上，你需要配置 `/usr/lib/uucp/Permissions` 文件以允许自己远程登录，并定义你想要提供的读、写权限。打开或创建 `/usr/lib/uucp/Permissions` 文件，并添加以下行：

```
LOGNAME=local_machine MACHINE=local_machine
SENDFILES=yes
```

The `/usr/lib/uucp/Permissions` 文件在你允许对 UNIX 主机进行无人 uucp 访问时至关重要。在这种情况下，应该在文件中定义所有你允许访问的主机的条目，并针对以下关键词提供条目：

- `MACHINE` 提供系统名称
- `LOGNAME` 提供在日志文件中显示的系统名称

### 在远程 UNIX 系统上运行

1. 登录 UNIX 并输入 `cu -z remote`（其中 `remote` 是 `/usr/lib/uuc/Systems` 文件指定的系统名称）。如果你的 UNIX 版本反对 `z` 选项，请不要省略它。`cu` 程序会自动连接到远程系统并返回用户名和密码的登录提示符。

2. 登录远程系统。然后输入命令 `-?`。`cu` 程序会显示可用命令列表。

3. 输入 `%put` 将文件传输到远程主机。

4. `cu` 程序将提示你输入要传输到远程系统的本地文件。输入本地文件名。

5. `cu` 程序将提示你文件传输到远程系统后要命名的名称。你可以直接按回车键使用相同的名称。

6. `cu` 程序将指示传输何时完成。

7. 输入 `- .` 断开连接并返回 shell 提示符。

列表 24.2 说明了上述步骤的执行过程，显示了将文件 `/home/report` 传输到远程连接的系统。注意，也可以使用其他转义序列来传输文件。输入 `-` 命令列出你的 `cu` 程序实现中的可用命令。

### 列表 24.2 使用 cu 传输文件

```
-[local_host]?
[Escape sequences]
[.- hangup] [!CMD run shell]
[-$CMD stdout to remote] [-CMD stdin from remote]
[+CMD stdin and stdout to remote]
[# send break] [-CDIR change directory]
[-> send file] [<- receive file]
[-pFROM TO send Unix] [-tFROM TO receive Unix]
[-sVAR VAL set variable] [-sVAR set boolean]
[-!sVAR unset boolean] [-v list variables]
[-z suspend]
[%break send break] [%cd DIR change directory]
[%put FROM TO send file] [%take FROM TO receive file]
[~nopstop no XON/XOFF] [-stop use XON/XOFF]
[connected]
```

### 远程运行 date 命令

1. 登录 UNIX 并执行命令 `uux remote/date`。

2. 该程序在远程主机上执行 `date` 命令并将结果返回到你的 shell（外壳）。

通常情况下，`uux` 命令不会由用户直接执行，而是作为电子邮件和网络新闻服务器等应用程序的一部分使用的。由于此原因，大多数系统会通过 `/usr/lib/uucp/Permissions` 文件限制 `rmail` 和 `rnews` 程序的执行。

### 检查 uucp 任务状态

用户可以通过 `uustat` 程序检查任何待处理的 uucp 文件传输请求的状态。

#### 运行 uustat

1. 登录 UNIX；在 shell 提示符下，输入 `uustat`。

2. 将显示当前队列的任务列表。示例所示：

```
jupiter 02/14 - 20:45:00 (POLL)
mars 02/14 - 20:53:07 jupiter filename.txt
/home/james/docs/sams/uucp/filename.txt
catfish 02/23 - 10:25:00 (POLL)
```

3. 默认情况下，`uustat` 只显示使用 `uustat` 命令的用户队列的任务。要显示当前所有调度的任务，输入 `uustat -all`。

你可以带有某些可选参数运行 `uustat` 程序，以获取有关单个 `uucp` 程序性能的其他信息。

#### 带参数运行 uustat

1. 输入 `uustat -e` 并按回车。这将提供所有当前队列的程序执行请求列表。

2. 输入 `uustat -m` 并按回车。该命令生成连接远程主机状态的摘要。示例所示：

```
remote      05/23 - 10:15 CALLER SCRIPT FAILED
dtc02       05/30 - 11:30 LOGIN FAILED
jupiter     05/30 - 11:30 CONN FAILED (CALLER SCRIPT FAILED)
```

上述代码说明了到三个主机（`remote`、`dtc02` 和 `jupiter`）失败的 uucp 连接。

### 取消 uucp 请求

你可以使用 `uustat` 程序取消一个待处理的 uucp 文件传输或程序执行请求。

#### 使用 uustat 取消 uucp 请求

1. 登录 UNIX。在提示符下，通过输入此行编辑 `/usr/lib/uucp/Systems` 文件：

`vi /usr/lib/uucp/Systems`

2. 按 `o` 添加新行，然后输入以下文本：

`nhost Never modem 19200 123456`

这定义了一个名为 `nhost` 的新系统，它将永远不会被 uucp 程序调用。

3. 通过向 nohost 发送一个你知道永远不会发送的传输请求，在 uucp 队列中放入消息。输入以下内容然后按回车：

`uucp /home/uucp_data nohost!/home/uucp_data`

4. 输入 `uustat 001`。你将看到一行类似下面的代码：

`nohostn001 root 03-15 02:25 Sending home/uucp_data (1864 bytes) to /home/uucp_data`

> **在使用 uustat 取消时注意 Caps Lock 键**
>
> 命令 `uustat -K`（大写字母 K）会移除所有当前队列的 uucp 请求。使用 uustat 取消任务时，请确保 Caps Lock 键没有被意外设置。

5. 要移除传输请求，输入以下命令：

`uustat -k nohost001`

### 通过调制解调器扩展网络 (PPP)
