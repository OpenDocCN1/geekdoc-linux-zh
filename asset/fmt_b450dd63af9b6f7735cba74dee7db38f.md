
```perl
# 从标准输入（stdin）读取每一行到 $line 变量中
while ( $line = <STDIN> ) {
    # 查找匹配特定模式的行（Perl 的模式匹配字符
    # 包含在 [] 中
    # 以可选的空白字符开头 [ \^\s* ]
    # 然后是一个 '#' [ # ]
    # 然后是更多的可选空白字符 [ \s* ]
    # 然后是一个以 '/' 开头且不包含空白字符的字符串 [ /\S+ ]
    #
    # 模式的最后一部分被包含在 () 中，
    # 这样如果模式匹配成功，我们就可以通过 $1 变量访问这部分内容。
    #
    # 此模式匹配一个被注释掉的条目/
    if ( $line =~ /^\s*#\s*(\/\\/\S+)/ ) {
        # 发现被注释掉的条目。如果文件存在，
        # 则去除注释字符。
        if ( -e $1 ) {
            $line =~ s/^\s*##//;
            $Additions++;
        }
    # 现在查找一行，它类似于上面那行，
    # 但没有 '#' 注释字符。
    } elsif ( $line =~ /^\s*(\/\\/\S+)/ ) {
        # 发现以 "  /" 开头的条目。如果文件
        # 不存在，则将注释该条目。
        if ( ! -e $1 ) {
            $line = "#" . $line;
            $Removals++;
        }
    }
    # 输出该行（无论是否修改过）
    print $line;
}
# 将统计信息打印到 STDERR，这样它们就不会被 > 重定向
print STDERR "Number of additions: $Additions\n";
print STDERR "Number of removals: $Removals\n";
```

```bash
# chmod +x /usr/local/bin/cleanpol.pl
```

## 8. 现在我们可以使用这个 Perl 脚本来生成自定义的 Tripwire 策略文件：

```bash
# cd /etc/tripwire
# mv twpol.txt twpol.txt.orig
# /usr/local/bin/cleanpol.pl < twpol.txt.orig > twpol.txt
...
Number of additions: 38
Number of removals: 125
```

这个小程序帮我们免去了对 Tripwire 策略文件进行 163 次手动更改！（你在系统上所做的更改数量将取决于你安装了哪些软件包。）你可以使用 `diff` 命令查看所做的更改：

```bash
diff twpol.txt.orig twpol.txt
```

## 9. 现在，使用 `gedit` 或你喜欢的文本编辑器，查看更新后的 `/etc/tripwire/twpol.txt` 文件的内容。特别要注意，定义 `/sbin/e2fsadm` 策略的那一行可能存在问题。如果 `cleanpol.pl` 脚本取消了该行的注释，那么行末的 `tune2fs?` 备注将被 Tripwire 视为指向某个文件的相对路径，从而导致策略文件被拒绝。只需删除此备注即可。换句话说：

```text
/sbin/e2fsadm -> $(SEC_CRIT) ; tune2fs?
```

变为：

```text
/sbin/e2fsadm -> $(SEC_CRIT) ;
```

## 10. 现在我们已设置了 Tripwire 策略文件，下一步是初始化 Tripwire 数据库。这是通过在 `/etc/tripwire` 目录下运行 `twinstal.sh` 脚本来完成的：

```bash
# ./twinstal.sh
```

该脚本要求我们输入站点密码和本地密码（这是用来描述长“密码”的术语），生成加密密钥，并对配置文件和策略文件进行加密保护，以防止未经授权的更改：

```text
[root@rh9 tripwire]# ./twinstal.sh
-----------------------------------------------------------------------
The Tripwire site and local passphrases are used to
sign a variety of files, such as the configuration,
policy, and database files.

Passphrases should be at least 8 characters in length
and contain both letters and numbers.
```

有关更多信息，请参阅 Tripwire 手册。

```text
-------------------------------------------------
Creating key files...
```

```text
(When selecting a passphrase, keep in mind that good passphrases typically
have upper and lower case letters, digits and punctuation marks, and are
at least 8 characters in length.)

Enter the site keyfile passphrase:
Verify the site keyfile passphrase:
Generating key (this may take several minutes)...Key generation complete.
```

```text
(When selecting a passphrase, keep in mind that good passphrases typically
have upper and lower case letters, digits and punctuation marks, and are
at least 8 characters in length.)

Enter the local keyfile passphrase:
Verify the local keyfile passphrase:
Generating key (this may take several minutes)...Key generation complete.
```

```text
-------------------------------------------------
Signing configuration file...
Please enter your site passphrase:
Wrote configuration file: /etc/tripwire/tw.cfg
```

```text
A clear-text version of the Tripwire configuration file
/etc/tripwire/twcfg.txt
has been preserved for your inspection. It is recommended
that you delete this file manually after you have examined it.
```

```text
-------------------------------------------------
Signing policy file...
Please enter your site passphrase:
Wrote policy file: /etc/tripwire/tw.pol
```

```text
A clear-text version of the Tripwire policy file
/etc/tripwire/twpol.txt
has been preserved for your inspection. This implements
a minimal policy, intended only to test essential
Tripwire functionality. You should edit the policy file
to describe your system, and then use twadmin to generate
a new signed copy of the Tripwire policy.
```

## 11. 初始化的最后一步是运行命令 `tripwire --init`。系统会提示我们输入本地密码，然后 Tripwire 扫描配置文件列出的所有文件，并收集基准数据，所有未来的扫描都将以此为依据。这可能需要几分钟时间，请耐心等待：

在初始化数据库之前，我们必须确信系统处于良好状态，否则使用 Tripwire 就没什么意义了。数据库初始化完成后，最好将副本存储到一次写入介质（例如 CD-ROM）中，这样它就无法被篡改：

```bash
# tripwire --init
Please enter your local passphrase:
Parsing policy file: /etc/tripwire/tw.pol
Generating the database...
*** Processing Unix File System ***
Wrote database file: /var/lib/tripwire/rh9.twd
The database was successfully generated.
```

### 设置 Tripwire 自动运行

我们已经看到 `logwatch` 是如何被设置为每天 04:02 自动运行的。我们可以很容易地将 Tripwire 设置为在同一时间运行。

创建一个名为 `/etc/cron.daily/run-tripwire` 的两行脚本，内容如下：

```bash
#!/bin/sh
/usr/sbin/tripwire --check
```

确保该脚本由 `root` 所有，且权限为 `500` (`r-x------`)，这样只有 `root` 才能执行它。此脚本调用 Tripwire，使其根据策略文件中的规则检查系统的完整性，并使用我们刚刚创建的数据库作为基准。当 `cron` 每天在 04:02 运行此脚本时，其输出将发送给 `root`（或在 `/etc/crontab` 中配置的 `MAILTO` 变量中指定的任何人）。

### 更新 Tripwire 数据库

我们将通过立即运行脚本来测试它。以 `root` 身份在命令提示符下输入 `/etc/cron.daily/run-tripwire`，并检查 Tripwire 是否成功运行。仔细检查生成的输出，我们应该看到 Tripwire 发现 `/etc/cron.daily` 中添加了 `run-tripwire` 脚本，并将其标记为关键更改。

为了阻止 Tripwire 每次运行时都报告这个我们已知且确认无误的策略违规更改，我们需要更新 Tripwire 的数据库。我们通过运行 `tripwire --update` 来执行此操作，并指定我们要用于更新的 Tripwire 报告文件。要查看可用文件，请运行 `ls -ltr /var/lib/tripwire/report`；选择列出的最后一个报告，因为它是最新的。

要运行的命令（全部在一行内）如下：

```bash
# tripwire --update --twrfile /var/lib/tripwire/report/rh9-20030209-040304.twr
```

用你系统上最近的 `.twr` 文件替换报告文件名。这将生成一个文本文件并启动 `vi`，以便我们可以编辑该文件。每个建议的数据库更新都标记有 `[x]`，如果我们不想应用该更新，只需删除 `x` 即可。如果我们不想使用 `vi`，则在命令中添加 `--visual gedit`，Tripwire 将启动图形编辑器。

退出编辑器后，系统会要求输入本地密码，然后更新将应用到数据库。后续的 Tripwire 完整性检查不应再警告关于 `/etc/cron.daily` 的更改。

## 网络安全

几乎所有的 Red Hat Linux 9 系统在某个时刻都会通过网络连接到其他计算机。这可能通过网络适配器到局域网（LAN）的永久连接、到互联网的“始终在线”连接，或仅在需要时激活的到互联网服务提供商的拨号连接。无论连接类型如何，我们都需要确保黑客无法利用该连接获得对我们系统的访问权限，或发动“拒绝服务”攻击，从而阻止我们计算资源的合法使用。在本节中，我们将探讨一些可用于保护系统并使潜在黑客生活变得艰难的技术。

除非我们连接到一个孤立的网络，其中每台机器都是安全且可信的，否则我们必须假设我们通过网络发送和接收的所有信息都可能被第三方（即除我们和数据预期接收者之外的人）截获。

### 网络服务

黑客试图获得我们系统未经授权的访问权限的一种方式是利用我们在 Red Hat Linux 系统上运行的网络服务中的弱点。这些程序——通常在后台运行，没有控制终端（在 Unix 中称为“守护进程”，在 Microsoft Windows 中称为“服务”）——为其他计算机提供服务。示例包括文件传输协议（`ftp`）、Web、网络文件系统（`NFS`）和打印服务器。

#### 启用和禁用服务

降低我们脆弱性的第一种也是最简单的方法是禁用所有我们不需要的服务。特别是，我们需要非常小心那些以任何形式（纯文本）在未加密的情况下通过网络发送敏感信息（如用户名和密码）的旧服务。此外，尽可能避免那些无偿提供有关我们系统信息的 服务。

下表将帮助你决定需要运行哪些服务。

## 第 12 章

| 服务 | TCP/UDP 端口号 | 描述 | Red Hat 软件包 | 安全级别 | 是否运行？ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `echo` | 7 | 将接收到的字符回传给发送者。 | `xinetd` | 无。 | 否。（除非你真的需要调试远程终端问题） |
| `daytime` | 13 | 将当前的日期和时间作为 ASCII 字符串回传给发送者。 | `xinetd` | 无。 | 否。请使用 NTP 进行时间同步。它更准确且具有更好的安全特性。 |
| `chargen` | 19 | 生成连续的 ASCII 字符流以测试终端。 | `xinetd` | 无。 | 否。（除非你真的需要调试远程终端问题） |
| `ftp` | 20 (数据) 21 (控制) 大于 1023 的随机端口 | 文件传输协议。允许将文件传输到远程系统或从远程系统传输文件。 | `vsftpd` 或 `wu-ftpd` | 弱。用户名和密码以明文发送。“匿名 FTP”允许无密码访问。 | 否。请改用 `ftp`。 |
| `ssh` | 22 | 安全外壳。允许远程系统访问本地机器上的命令行 shell。 | `Openssh` | 良好。数据经过加密，连接可以进行身份验证，以确保远程系统是合法的，而不是冒名顶替者。 | 仅当需要远程访问命令行时。 |
| `telnet` | 23 | 允许远程系统访问本地机器上的命令行 shell。 | `telnet-server` | 弱。用户名和密码以明文发送。 | 否。请改用 `ssh`。 |
| `SMTP` | 25 | 简单邮件传输协议。用于在系统之间传输邮件。 | `sendmail` | 弱。邮件以明文传输。 | 仅当邮件需要在本地处理时。在发送前对敏感邮件进行加密。 |
| `time` | 37 | 将当前时间（自 1900 年 1 月 1 日 00:00 以来的秒数）回传给发送者。 | `xinetd` | 无。 | 否。请使用 NTP 进行时间同步。它更准确且具有更好的安全特性。 |
| `finger` | 79 | 向远程机器提供关于本地系统或用户的信息。 | `finger-server` | 无。 | 否。 |
| `http` | 80 | Web 服务器。 | `Httpd` | 取决于服务器配置。 | 仅当系统需要运行 Web 服务器时。 |
| `auth` (`Ident`) | 113 | 身份识别协议。允许远程系统确定特定 TCP/IP 连接的用户身份。 | `pident` | 支持对返回信息进行 DES 加密。 | 仅当需要访问某些公共服务时（例如某些 `ftp` 站点和 IRC）。 |
| `sftp` | 115 | 安全文件传输协议。通过安全的 SSH 连接进行类似 FTP 的数据传输。 | `openssh` | 良好。 | 仅当需要文件传输时。 |
| `nntp` | 119 | 网络新闻传输协议。用于传输 USENET 新闻组。 | `inn` | 取决于服务器配置。 | 仅当系统需要运行新闻组服务器时。 |
| `smb` | 137, 138, 139 | 服务器消息块。允许 Microsoft Windows 系统将 Red Hat Linux 文件系统作为网络共享访问。 | `Samba` | 弱。通过网络传输的信息未加密。密码可能会加密，但算法较弱。 | 仅用于访问非敏感信息。 |
| `https` | 443 | 安全的 Web 服务器。 | `Httpd` | 取决于服务器配置。 | 仅当系统需要运行 Web 服务器时。 |
| `lpd` | 515 | 打印守护进程。允许远程机器向我们的打印机发送打印作业。 | `LPRng` 或 `cups` | 弱。通过网络传输的信息未加密。 | 仅当系统有你想共享的打印机时才运行。 |
| `rsh`/`rlogin` | 514 | 允许远程系统在不提供密码的情况下访问本地机器上的命令行 shell。 | `rsh-server` | 弱。依赖 DNS（域名服务）来识别远程系统，因此如果 DNS 被破坏则存在漏洞。 | 否。 |
| `nfs` | 2049 (要求 `portmapper` 在 111 端口监听) | 网络文件系统。允许其他系统远程访问文件系统。 | `nfs-utils` | 弱。通过网络传输的信息未加密。 | 仅用于访问非敏感信息。 |
