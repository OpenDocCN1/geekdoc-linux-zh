
## 设置传入目录

如果您需要允许匿名用户将文件存放到您的系统中，您需要为他们设置一个特殊的传入目录。放在那里的文件只能由 root 用户检索，而不能由其他匿名用户检索。这是为了防止那些动机不纯的人将您的 FTP 服务器变成他们存放色情内容、盗版软件或非法内容（如被盗信用卡号）的公共访问站点。当然，这意味着作为站点管理员，您需要付出额外的开销，但人工安全屏障是确保匿名上传的文件适合保留在服务器上供他人下载的唯一途径。

要创建此目录，请前往您的匿名 FTP 目录（例如，`/home/ftp`）并创建一个名为 “incoming” 的子目录，如下所示：

```bash
mkdir incoming
```

然后更改权限，使得只有用户 ftp 可以写入，但匿名用户无法读取：

```bash
chmod 300 incoming
chown ftp.ftp incoming
```

最后，在您的 `/etc/ftpaccess` 文件中添加以下两行以控制上传位置：

```text
upload /home/ftp * no
upload /home/ftp/incoming yes ftp ftp 0000 nondos
```

第一个 `upload` 命令拒绝向 FTP 服务器上的所有目录上传。第二个命令明确开放了一个目录，允许匿名用户在该目录中上传文件。

## 仅限注册用户及混合访问

运行支持混合访问的服务器是完全可接受的；也就是说，它既为匿名用户也为常规用户提供对服务器的访问。同样，也可以配置服务器，使其仅允许注册用户访问。

### 混合访问

首先按照仅限匿名访问的方式配置服务器。设置完成后，更改 `/etc/ftpaccess` 文件，使其内容如下：

```text
class all real,guest,anonymous *
class ftp@admin.com
```

```
loginfails  5
readme  README*       login
readme  README*       cwd=* 
message .welcome.msg  login
message .message      cwd=
compress      yes      all
tar         yes      all
chmod       no       guest,anonymous
delete      no       guest,anonymous
overwrite   no       guest,anonymous
rename      no       guest,anonymous
log transfers anonymous,real inbound,outbound
passwd-check rfc822 warn
```

请注意，此配置未向匿名用户开放上传权限。假设你的匿名 FTP 目录位于 `/home/ftp`，你需要在 `/etc/ftpaccess` 文件中添加以下行：

```
upload /home/ftp * no
upload /home/ftp /incoming ftp ftp 0000 nodirs
```

（请阅读有关在匿名 FTP 服务器上设置上传支持的相关章节，以了解如何设置 incoming 目录本身。）

### 仅限注册用户

拒绝匿名 FTP 用户访问有两种技术。第一种是不希望 `/etc/passwd` 文件中有 "ftp" 用户。这种方法非常简单且有效。但是，如果你必须保留匿名 FTP 的配置，你可以使用 `/etc/ftpaccess` 文件中的 `limit` 命令以与匿名 FTP 访问拒绝真实用户相同的方式拒绝匿名 FTP 访问。

用于进行此类配置的 `/etc/ftpaccess` 文件内容如下：

```
class all real,guest *
class anon anonymous
email ftp@domain.com
loginfails 5
limit anon 0 0 wk0000-2359 /home/ftp,nonanonymous
readme  README*       login
readme  README*       cwd=*
message .welcome.msg  login
message .message      cwd=
compress      yes      all
tar         yes      all
chmod       no       guest
delete      no       guest
overwrite   no       guest
rename      no       guest
log transfers real inbound,outbound
password-check rfc822 warn
```

其中 `/home/ftp/noanonymous` 是一个文本文件，发送给尝试以匿名身份连接的客户端，以告知其不允许匿名访问。

## 配置虚拟 FTP 服务器

使用 `wu-ftp`，只要每个服务器拥有自己的 IP 地址，你就可以在同一台主机上设置多个 FTP 服务器。（这是 FTP 协议的限制，而非 wu-ftp 实现本身的限制。）一旦你为主机设置了匿名 FTP，这个过程就相当简单。本节假设你已经配置了 IP 别名并正确调整了 arp 表。（这将在本书稍后的“高级网络”部分中讨论。）这个关于该过程的`快速入门指南`假设你有一块以太网卡，并希望添加单个虚拟 IP 地址：

1. 确保你的新 IP 地址同时存在于本地主机表（`etc/hosts`）和 DNS 表中。（在此示例中，我们将该主机称为“earth”。）

2. 运行 `ifconfig` 命令来配置 `eth0` 设备，指定相应的地址、子网掩码和广播地址。例如，要在 `eth0` 上配置 `192.168.1.42` 设备，我会使用：

```
ifconfig eth0:0 192.168.1.42 netmask 255.255.255.0 broadcast 192.168.1.255
```

3. 调整 arp 表。为此你需要知道你的以太网卡的硬件地址。运行 `ifconfig` -a 命令以获取此信息。假设你的以太网卡硬件地址是 `00:10:48:CB:15:9F`，请输入：

```
arp -s earth 00:10:48:CB:15:9F pub
```

建立虚拟 IP 地址后，你需要创建一个类似于匿名站点的目录结构。这应放置在你希望作为虚拟 FTP 站点的目录中。然后在 `ftp/accesses` 文件的末尾添加 virtual 命令。该命令的格式为：

```
virtual IP ftype directory
```

其中 `IP` 是你的虚拟 FTP 服务器的 IP 地址，`ftype` 是 `directory` 所指的文件类型。`ftype` 的值可以是 root、banner 或 logfile。如果 `ftype` 是 root，`directory` 应为虚拟站点中设置匿名 FTP 文件的`目录`。如果 `ftype` 是 banner 或 logfile，则 `directory` 条目应为相应的文件。

例如，要在 IP 地址 192.168.1.42 上设置虚拟 FTP 服务器，我可以将配置设置如下：

```
virtual 192.168.1.42 root /home/earth
virtual 192.168.1.42 banner /home/earth/.welcome.banner
virtual 192.168.1.42 logfile /var/log/xferlog.earth
```

`注意：` 匿名 FTP 访问所需的所有文件都必须在虚拟 FTP 服务器的根目录中设置。在我们的示例中，这意味着在 `home/earth` 目录中设置 bin、etc、lib 和 pub 子目录。

## 总结

华盛顿大学 FTP 守护进程（`www.wu-ftpd.org`）是一个功能强大的 FTP 服务器，提供了以安全方式运行商业 FTP 服务器所需的所有功能。在本章中，我们讨论了编译、安装和配置 wu-ftpd 服务器的过程。

具体而言，我们涵盖了：

- wu-ftpd 的所有配置选项

- 建立虚拟 FTP 服务器

- 设置匿名 FTP 服务器

- 设置匿名服务器与仅限普通用户的 FTP 服务器结合使用

- FTP 协议及其对防火墙影响的详细信息

这些信息足以让你的 FTP 服务器平稳运行一段时间。当然，像任何关于软件的印刷媒体一样，本文献也会过时，信息终将变得过时。请务必不时访问 wu-ftpd 网站，以了解最新的发展以及最新的文档。

### 第 14 章

使用 Apache 设置你的 Web 服务器
