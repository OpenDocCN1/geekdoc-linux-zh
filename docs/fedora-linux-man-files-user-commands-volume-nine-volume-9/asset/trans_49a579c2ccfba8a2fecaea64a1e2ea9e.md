
# 信号

信号的行为在 `signal(7)` 手册页中有详细说明。

## 示例

**snice -c seti -c crack +7**
减慢 seti 和 crack 命令。
**skill -KILL -t /dev/pts/**
终止 PTY 设备上的用户。
**skill -STOP -u viro -u lm -u davem**
停止三个用户。

## 另请参阅

`kill(1)`, `exit(2)`, `signal(1)`, `sigaction(2)`, `kill(2)`, `raise(3)`, `signal(7)`

# 标准

没有适用的标准。

# 作者

Albert Cahalan 于 1999 年编写了 skill 和 snice，作为非自由版本的替代品。

# 报告错误

请将错误报告发送到项目的邮件列表或错误跟踪器。

# SLABTOP

## 名称

slabtop - 实时显示内核 slab 缓存信息

## 概要

**slabtop** [*选项*]

## 描述

**slabtop** 实时显示详细内核 slab 缓存信息。它会显示按列出的某个排序标准排序的顶级缓存列表。它还显示一个包含 slab 层信息的统计页眉。

## 选项

正常调用 **slabtop** 不需要任何选项。然而，可以通过指定以下一个或多个标志来微调其行为：

-   -d, --delay=N
    每 *N* 秒刷新一次显示。默认情况下，**slabtop** 每三秒刷新一次显示。要退出程序，请按下 **q**。
-   -s, --sort=S
    按 *S* 排序，其中 *S* 是其中一个排序标准。
-   -o, --once
    显示一次输出然后退出。
-   -V, --version
    显示版本信息并退出。
-   -h, --help
    显示用法信息并退出。

## 排序标准

以下是用于对各个 slab 缓存进行排序的有效排序标准，从而决定显示哪些“顶级” slab 缓存。默认排序标准是按对象数量（“o”）排序。

也可以在 slabtop 运行期间通过按下相应的字符来更改排序标准。

| 字符 | 描述 | 页眉 |
| :--- | :--- | :--- |
| a | 活动对象数量 | ACTIVE |
| b | 每个 slab 的对象数 | OBJ/SLAB |
| c | 缓存大小 | CACHE SIZE |
| l | slab 数量 | SLABS |
| v | 活动 slab 数量 | N/A |
| n | 名称 | NAME |
| o | 对象数量 | OBJS |
| p | 每个 slab 的页数 | N/A |
| s | 对象大小 | OBJ SIZE |
| u | 缓存利用率 | USE |

## 命令

**slabtop** 在使用期间接受用户输入的键盘命令。支持以下命令。对于字母，大小写均可接受。

每个有效的排序字符也可以被接受，以更改排序例程。请参阅 **排序标准** 部分。

-   **<空格键>**
    刷新屏幕。
-   **Q**
    退出程序。

## 文件

-   */proc/slabinfo*
    slab 信息

## 另请参阅

`top(1)`, `vmstat(8)`, `slabinfo(5)`, `free(1)`

## 备注

目前，**slabtop** 需要 2.4 或更高版本的内核（具体而言，是版本 1.1 或更高版本的 `/proc/slabinfo`）。未来将支持内核 2.2。

slabtop 统计页眉跟踪正在使用的 slab 字节数，并不是物理内存的度量。`/proc/meminfo` 文件中的 ‘Slab’ 字段正在跟踪关于已使用 slab 物理内存的信息。

# 作者

由 Chris Rivera 和 Robert Love 编写。

**slabtop** 受到 Martin Bligh 的 Perl 脚本 **vmtop** 的启发。

# 报告错误

请将错误报告发送到项目的邮件列表或错误跟踪器。

# SLEEP

## 名称

sleep - 延迟指定时间

## 概要

`sleep NUMBER[SUFFIX]... sleep OPTION`

## 描述

暂停 NUMBER 秒。后缀（SUFFIX）可以是表示秒的 ‘s’（默认值）、表示分钟的 ‘m’、表示小时的 ‘h’ 或表示天的 ‘d’。与大多数要求 NUMBER 必须为整数的实现不同，这里的 NUMBER 可以是任意浮点数。如果给出两个或多个参数，则暂停的时间由这些值的总和指定。

-   --help
    显示此帮助并退出
-   --version
    输出版本信息并退出

## 作者

由 Jim Meyering 和 Paul Eggert 编写。

# 报告错误

GNU coreutils 在线帮助：[https://www.gnu.org/software/coreutils/](https://www.gnu.org/software/coreutils/)
请将 sleep 翻译错误报告至 [https://translationproject.org/team/](https://translationproject.org/team/)

## 版权

版权所有 2015 自由软件基金会。许可证 GPLv3+：GNU GPL 第 3 版或更高版本 [https://gnu.org/licenses/gpl.html](https://gnu.org/licenses/gpl.html)。这是自由软件：您可以自由地修改和重新分发它。在法律允许的范围内，无担保。

## 另请参阅

`nanosleep(3)`

完整文档位于：[https://www.gnu.org/software/coreutils/sleep](https://www.gnu.org/software/coreutils/sleep)
或本地可通过：info ‘(coreutils) sleep invocation’ 获取

# SSH

## 名称

ssh - OpenSSH SSH 客户端（远程登录程序）

## 概要

```
ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-b bind_address] [-c cipher_spec]
    [-D [bind_address:]port] [-E log_file] [-e escape_char]
    [-F configfile] [-I pkcs11] [-i identity_file] [-L address]
    [-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] [-p port]
    [-Q cipher | cipher-auth | mac | kex | key | protocol-version]
    [-R address] [-S ctl_path] [-W host:port] [-w local_tun[:remote_tun]]
    [user@]hostname [command]
```

## 描述

**ssh**（SSH 客户端）是一个用于登录远程机器并在远程机器上执行命令的程序。旨在替代 rlogin 和 rsh，并在不安全的网络上提供两个不受信任的主机之间的安全加密通信。X11 连接、任意 TCP 端口和 UNIX 套接字也可以通过安全通道进行转发。

**ssh** 连接到指定的 *hostname*（可选带有 *user* 名称）并登录。用户必须使用取决于所用协议版本（见下文）的几种方法之一向远程机器证明其身份。

如果指定了 *command*，则会在远程主机上执行该命令，而不是登录 shell。选项如下：

-   **-1**
    强制 **ssh** 仅尝试协议版本 1。
-   **-2**
    强制 **ssh** 仅尝试协议版本 2。
-   **-4**
    强制 **ssh** 仅使用 IPv4 地址。
-   **-6**
    强制 **ssh** 仅使用 IPv6 地址。
-   **-A**
    启用认证代理连接的转发。也可以在配置文件中按主机指定。

    应谨慎启用代理转发。拥有绕过远程主机（针对代理的 UNIX 套接字）文件权限能力的用户可以通过转发连接访问本地代理。攻击者无法从代理获取密钥材料，但他们可以执行操作以使用加载到代理中的身份进行身份验证。
-   **-a**
    禁用认证代理连接的转发。
-   **-b *bind_address***
    在本地机器上使用 *bind_address* 作为连接的源地址。仅适用于拥有多个地址的系统。
-   **-C**
    请求压缩所有数据（包括标准输入、标准输出、标准错误以及转发的 X11、TCP 和 UNIX 连接的数据）。压缩算法与 `gzip(1)` 使用的相同，协议版本 1 的“级别”可以通过 **CompressionLevel** 选项进行控制。在调制解调器线路和其他慢速连接上，压缩是理想的，但在快速网络上只会减慢速度。默认值可以在配置文件中按主机设置；参见 **Compression** 选项。
-   **-c *cipher_spec***
    选择用于加密会话的密码规范。

    协议版本 1 允许指定单个密码。支持的值为 “3des”、“blowfish” 和 “des”。对于协议版本 2，*cipher_spec* 是按偏好顺序列出的逗号分隔的密码列表。更多信息请参见 *ssh_config(5)* 中的 **Ciphers** 关键字。
-   **-D [*bind_address:*]***
    指定本地“动态”应用层端口转发。这是通过分配一个套接字在本地端监听 *port* 来实现的，可选择绑定到指定的 *bind_address*。每当有连接建立到此端口时，连接将通过安全通道转发，然后使用应用程序协议来确定从远程机器连接到哪里。目前支持 **SOCKS4** 和 **SOCKS5** 协议，**ssh** 将充当 SOCKS 服务器。只有 root 才能转发特权端口。动态端口转发也可以在配置文件中指定。

    IPv6 地址可以通过将地址括在方括号中来指定。只有超级用户才能转发特权端口。默认情况下，本地端口根据 **GatewayPorts** 设置进行绑定。然而，可以使用显式的 *bind_address* 将连接绑定到特定地址。“localhost”的 *bind_address* 表示监听端口仅绑定用于本地使用，而空地址或“*”表示端口应从所有接口可用。
-   **-E *log_file***
    将调试日志追加到 *log_file* 而不是标准错误。
-   **-e *escape_char***
    设置带 pty 的会话的转义字符（默认：`~`）。转义字符仅在行首被识别。转义字符后跟一个点（`.`）会关闭连接；后跟控制-Z 会挂起连接；后跟自身会发送一次转义字符。将字符设置为“none”禁用任何转义并使会话完全透明。
-   **-F *configfile***
    指定一个替代的每用户配置文件。如果在命令行中给出了配置文件，系统将忽略系统范围的配置文件 (/etc/ssh/ssh_config)。每用户配置文件的默认值是 ~/.ssh/config
-   **-f**
    请求 **ssh** 在命令执行前进入后台。如果 **ssh** 即将询问密码或短语，但用户希望其在后台运行，则此选项很有用。这隐含了 **-n**。在远程站点启动 X11 程序的推荐方法是使用类似 **ssh -f host xterm** 的命令

