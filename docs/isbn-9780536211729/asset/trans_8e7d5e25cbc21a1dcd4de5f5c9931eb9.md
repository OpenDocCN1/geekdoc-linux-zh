

## 3.4.1.7 可执行文件和动态库

```bash
cd /home/ftpusers
mdir joe sally
chgrp users joe sally
chown joe joe
chown sally sally
ln -s /home/ftpusers/joe /home/joe/ftp
ln -s /home/ftpusers/sally /home/sally/ftp
```

- `-d` 选项导致调试信息通过 syslog 机制记录。
- `-a` 选项导致使用 /etc 中的 ftpaccess() 文件来控制 FTPD 的配置。这允许更详细的配置。/etc/inetd.conf 中 ftp 的一个典型条目可能是：

```text
ftp stream tcp nowait /usr/sbin/tcpd.ftp -l -i -a
```

当 ftp 用户执行 `ls` 命令或其同义词 `nls` 时，ftpd 会调用 `ls` Linux 命令来生成数据，ftpd 随后将这些数据发送回用户。问题在于，ftpd 守护进程运行在一个 chroot 环境中（匿名 FTP 访问通常也是如此），它无法访问 `/bin/ls` 或 `ls` 可能用到的任何动态库。解决方案是将 `ls` 放入 `~ftp/bin`，并在 `~ftp/lib` 中提供它可能需要的任何动态链接库。大多数发行版（如 Red Hat）都这样做，Red Hat 甚至提供了一个包含这些程序和动态库的匿名 FTP RPM 包。

如果你请求加载相应的软件包，所有必需的文件应该已经安装在你的系统上。Slackware 构建了一个特殊的静态链接程序，安装为 `~ftp/bin/ls`，这样系统管理员就不必担心动态库问题。Red Hat 没有这样做，但它在那里放了 `tar` 和 `gzip`，以便 ftpd 可以自动在压缩文件和未压缩文件之间进行转换，以及进行 tar 和 untar 操作。它还包括 shell，`sh`。

我担心这个看似无限制 shell 的存在打开了一个安全漏洞。我可能更喜欢 Slackware 的解决方案。当然，因为它是 Linux，你可以将 Slackware 的 `~ftp/bin` 程序放在你的 Red Hat 系统上，在从 `~ftp/bin` 和 `~ftp/lib` 中移除 Red Hat 的程序和动态库之后，它应该能正常工作。这是假设 Slackware 的 `ls` 程序版本与 Red Hat 内核版本兼容。这通常不是问题，如果存在问题，它将拒绝运行。

多年来，我一直在 Slackware 上编译复杂的 CGI C 程序，并在许多不同版本的 Red Hat 和 Mandrake 上运行它，以绕过 Red Hat `ctime()` 库中的一个 bug，该 bug 现已修复。

## 3.4.1.8 允许受控上传

通常允许公开匿名上传是个坏主意。当允许这样做时，黑客和其他不良人员会很快发现这一点，并利用你的站点进行恶意用途。这通常是为了破解系统、色情内容（肯定与你可能感兴趣的不同）以及其他你不想出现在你系统上的东西。如果你选择不允许上传，只需将目录设置为 755（或 555）权限，并由 ftpdadmin 拥有。这样，被称为匿名用户的 ftp 用户将被阻止上传任何页面。

如果你选择提供无限制的上传功能，惯例是为此目的拥有 `~ftp/incoming` 目录，并由 ftpdadmin 拥有。为了完全访问权限，它应该是模式 777，但如果系统可以从 Internet 访问，则不建议这样做；可能，该目录会被经常检查是否有不良文件并立即移除。另一种选择是将文件模式设置为 733。这意味着所有者 ftpdadmin 拥有完全访问权限，但其他人只有写和执行权限。该账户 ftpdadmin 应该与用于匿名 FTP 登录的账户（通常是 ftp）不同。这允许匿名用户上传文件，但 ftp 用户无法看到该目录中的内容，从而防止该目录被用于公共交换。

当然，上传者可以告诉其他人文件名，然后他们就可以下载它。一种解决方案是通过 cron 作业定期将这些文件“扫入”一个 ftp 完全无法访问的不同目录。扫描目录可能是 `~ftp/sweep`，由 ftpdadmin 拥有，模式为 700。这是一个简单的 ftpdadmin cron 作业，每小时将这些文件扫入该目录。它没有保护文件覆盖同名先前文件的机制，但这允许某人更新提交内容。

```bash
* * * * * /bin/mv /home/ftp/incoming/* /home/ftp/sweep/ > /dev/null 2>&1
```

有些站点会将 `~ftp/incoming` 设置为模式 711，并使用名为 733 的秘密名称子目录。想要上传文件的人必须先向系统管理员询问其中一个秘密目录的名称并上传到其中，但我认为这与之前讨论的方法相比并没有显著改进，并且需要更多的开销。

## 3.4.2 FTP 代理的危险

![image](img/7d04225c75a86d3cf4bd6077596f35b2_166_0.png)

旧的 FTP 服务器允许客户端请求服务器对任意第三方系统执行操作。这导致了一系列安全漏洞，包括发送看起来来自 FTP 服务器系统的电子邮件以及通过防火墙进行隧道传输。如果你的 FTP 服务器在你的网络内部，并且防火墙只允许 Internet 访问你的 FTP 服务器，那么代理功能就可以用来访问防火墙内的任何系统。nmap 网络映射器可以利用此功能探测防火墙后的网络。要查看 Pentacorp 的 FTP 服务器是否易受攻击，假设 Pentacorp 拥有 A 类网络 10.0.0.0/8，可以使用以下命令：

```bash
nmap -F -e eth0 -b ftp.pentacorp.com 10.0.0.0/8
```

如果你的 FTP 服务器不允许这样做，你将看到此消息：

> 你的 FTP 反弹服务器 [censored]，它不让我们提供虚假端口！

从 Red Hat 6.0 开始，FTP 服务器生成此消息并且是安全的。其他防火墙隧道危险在第 71 页的“通过防火墙隧道传输”中讨论。

## 3.5 rsh, rcp, rlogin 和 rexec 服务

![image](img/7d04225c75a86d3cf4bd6077596f35b2_167_0.png)

在第 94 页的“关闭 rsh, rcp, rlogin 和 rexec”中，建议关闭这些服务，因为它们被认为不安全，而 SSH 是一个优秀的替代品。由于这些服务非常流行（因为它们有用），这里提供关于它们如何工作及其不安全性的解释。

> rsh, rcp, rexec 和 rlogin 服务太不安全且太危险，不应使用。从你的系统中移除它们并禁止使用它们。真的。

这些服务允许远程执行进程。换句话说，远程系统 zoro.com 上名为 joe 的账户可以发出以下命令：

```bash
rsh pentacorp.com stab files
```

这将请求 pentacorp.com 以账户 joe 的身份执行命令 `stab files`。身份验证（以验证此请求是否允许）是通过在 pentacorp.com 系统的两个配置文件中查找初始化系统的名称和账户名（zoro.com 和 joe）。

如果初始化系统的名称出现在系统级配置文件 `/etc/hosts.equiv` 中，来自该系统任何用户名到 pentacorp.com 的相同用户名的请求都将被接受。换句话说，如果条目：

```text
zoro.com
```

出现在 pentacorp.com 的 `/etc/hosts.equiv` 中，zoro.com 上的任何用户都可以使用与 pentacorp.com 上相同的用户名执行 rsh 命令。因此，zoro.com 用户 joe 可以请求 pentacorp.com 上的用户 joe 执行命令，zoro.com 上的 cindy 可以请求 pentacorp.com 上的用户 cindy 执行命令，但根据 `/etc/hosts.equiv` 授予的权限作为 cindy 在 pentacorp.com 上执行命令，反之亦然。单个用户可能授予远程用户在其账户下操作的额外权限。这是通过在其主目录中创建文件 `.rhosts` 并添加所需条目来完成的。每个条目占一行，并且可以是两种格式之一。

第一种格式仅列出允许 rsh 的远程系统的主机名。因此，如果 cindy 的主机 Linux 盒子是 hv.isp.com，她在那里的个人账户也是 cindy，她可以添加条目：

```text
hv.isp.com
```

到她的 `.rhosts` 文件中。假设 cindy 也在佐治亚理工学院上夜校，她的账户是 cory.gatech.com 上的 cc02。她不能指定 cory.gatech.com，因为账户不同。相反，她指定主机名、一个空格和远程账户如下：

```text
cory.gatech.com cc02
```

如果她也在上一门比较宗教学课程，那个账户是 cr72，她的 `.rhosts` 文件可能如下：

```text
hv.isp.com
cory.gatech.com cc02
cory.gatech.com cr72
```

rsh 和 rexec 的守护进程具有多项安全功能以减少入侵。

- 1. 为了使支持 rsh 和 rcp 的服务器 `in.rshd` 考虑用户的 `.rhosts` 文件，它确保该文件由用户拥有，且没有其他人拥有写访问权限。因此，权限 600 或 644 是可接受的，但 666 不是。
- 2. `in.rshd` 守护进程还对发出请求的系统的数字 IP 进行反向查找。这意味着它获取数字 IP 地址并确定具有该地址的主机名。它要求该主机名与请求系统声称的主机名匹配。这防止了黑客发出以下命令：

```bash
hostname zoro.com
```

在拥有你域内的系统时，你必须以反向查找显示的方式（无论是完全限定

