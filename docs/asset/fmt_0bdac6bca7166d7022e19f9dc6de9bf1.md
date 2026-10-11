
这识别为一个被轮询的远程系统。`uName` 用于登录，密码为 `pSsd`。

## 配置文件：dial

`dial` 文件包含拨号器。每个 `dial` 条目用于指定如何拨打电话。`chat` 脚本与拨号器相关。

（注：原文后续部分严重重复，已按指令要求不重复输出翻译内容）

### Linux 内部

```
Chat script incosing bytes stripped to seven bits

At any time may call if any work

May retry the call at any time

Make local requests when calling

Make local requests when called

Send by local request: /

Send by remote request: /

Accept by local request: /

Receive by remote request:

Execute next poll

Execution path /usr/bin/usr/local/usr/lib/news/usr/lib/news/bin

will leave 5000 bytes available

Public directory is /var/spool/ucppublic

Will use any known protocol

stamp $
```

`uchk` 的输出应该与之前“检查初始配置”部分捕的内容不同。如果相同，在正确的目录下吗？你应该检查 `uchk` 的输出。你是否将配置文件存储在正确的目录下？你是否使用了正确的配置文件名？你还应该检查各种配置文件的内容，以确保你使用的是正确的键。

如果你仔细检查 `uchk` 的输出，你会注意到消息 *** Are no matching parts.。如果我们同时查看 `/usr/lib/uucp/sys` 和 `/usr/lib/uucp/port` 文件，我们将看到输出以及 `/usr/lib/uucp/port` 文件。

我们现在展示 `/usr/lib/uucp/port` 文件的内容：

```
# stamp cat $ 

# sys file

# remote entries:

# system ren

time any

123-456-7890

portone

port portone

speed 9600

chat "-U ENC: BREAK-out::-BREAK- \ W word \P

stipy $
```

```
# designation for portone

port portone

device /dev/cu0

speed

type

speed 57600

dilayer layers

# designation for portTwo

port portTwo

device /dev/cu1

type

speed 115200

dilayer layers

stamp $
```

问题在 `/usr/lib/uucp/port` 文件中显而易见：`port` 字段指定的为 `9600`，而 `/usr/lib/uucp/sys` 文件已更改以反映 `57600` 的速度。以下是应用更改后 `uchk` 的输出。

```
bash-2.0.1 epoch

Local node name

Special directory /var/spool/uucp

Public directory /var/spool/ucppublic

Log directory /var/log

Log file /var/spool/uucp/Log

Statistics file /var/spool/uucp/Stats

Global debugging level

uco -l will strip UUCP login names and passwords

uuco will strip UUCP protocol commands

Start uack once per uuco invocation
```

```
system ren

when called using port portone at speed 57600

The possible ports are:

Port name portone

Port type name modem

Using port name as device name

speed 57600

Carrier available

Hardware flow control available
```

### Linux 内部

```
Dialer Hayes script AT77C ATEOV1X4C OK ADTNT CONNECT

Chat script timeout 60

Chat script inscribing bytes stripped to seven bytes

Wait for dialtone

Pause dialing

Carrier available

Wait 60 seconds for carrier

Phone number 123-456-7890

Chat script "VGN:BREAK:-V- word: :P

Chat script timeout

Chat script inscribing bytes stripped to seven bytes

At any may may call if any work

May retry the call up to 26 times.

May make local requests when calling

May make local requests when called

May send by local request -

May send by local request -

May receive by local request -

May receive by reset request -

Execution path /usr/bin/usr/local/bin/usr/lib/news/bin/news/bin

# file 5000 bytes by alias

Public directory is /var/local/ucppublic

Will use any known protocol

s$ 
```

你会发现所有关于端口的问题都已解决。`uoch` 命令对于确定 UCCP 和配置文件中可能发生的任何问题非常有用。每当你怀疑 UCCP 有问题时，请使用 `pooch`。

# 配置：HoneyDanBer (HDB) UCCP

UCCP 最新的实现版本是 HoneyDanBer (HDB)。HDB UCCP 在 UNIX 系统中更为常见，在 Linux 中也能找到。如果 Taylor 是你选择的 UCCP 实现，选择 HDB UCCP 可能会让你感到困惑。然而，在学习了格式之后，配置 HDB 其实非常简单。

必须访问多个文件，表 14.2 列出了这些涉及的文件。

| 文件 | 描述 |
|---|---|
| `/usr/lib/ucp/Devices` | 此文件描述了参与与远程系统连接的设备。 |
| `/usr/lib/ucp/Dialers` | 此文件包含拨号并与远程建立连接所需的 chat 脚本。 |
| `/usr/lib/ucp/Permissions` | 此文件维护了远程和本地机器处理文件所需的权限设置。 |
| `/usr/lib/ucp/Systems` | Systems 文件包含关于远程系统的信息以及每个系统相关的其他属性。 |

你可能记得，在 Taylor UCCP 下，`/usr/lib/ucp/sys` 文件维护了系统名称，并用于向远程标识它。在 HDB 中，格式如下：

```
$$ hostname
```

以下是 `hostname` 文件的示例。`hostname` 的语法为：

```
$$ hostname
```

以下是 `/usr/lib/ucp/systems` 文件的示例：

```
rabbit ACY 22800 123-456-7890; uucp sswd password
```
