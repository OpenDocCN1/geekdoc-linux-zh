
我会看到以下 IP 别名：

| 设备 | family | 地址 |
| eth0:0 | 2 | 206.171.50.51 |
| eth0:1 | 2 | 206.171.50.52 |

现在来看创建虚拟主机最简单的方法。

## 创建有限的虚拟 FTP 服务

此方法比另一种方法更简单，但也相当受限。虽然你将拥有虚拟 FTP 服务，但无法像那样进行太多自定义。如果你想要一个完全可定制的服务（如主 FTP 服务器），请跳到“创建完整的虚拟 FTP 服务”部分。

要创建此有限版本的虚拟 FTP 服务，你需要制作 `anon-ftp` 包创建的文件/目录结构的多个副本。只需安装 `anonftp` 包并为每个虚拟主机制作其副本。对于前面的示例，我创建两个虚拟 FTP 站点目录（`/home/client1/ftp` 和 `/home/client2/ftp`）并复制 `/home/ftp` 文件和目录的所有内容。制作 `/home/ftp` 的精确副本最简单的方法之一是运行以下命令：

```
cd /home/client1/ ; cp -a /home/ftp .
cd /home/client2/ ; cp -a /home/ftp .
```

这些命令将 `/home/ftp` 文件/目录结构复制到虚拟站点目录中。现在编辑 `/etc/ftpaccess` 文件以添加 `virtual` 关键字，如下所示：

```
virtual 206.171.50.51 root    /home/client1/ftp
virtual 206.171.50.51 banner  /home/client1/ftp/banner.msg
virtual 206.171.50.51 logfile /home/client1/ftp/xferlog

virtual 206.171.50.52 root    /home/client2/ftp
virtual 206.171.50.52 banner  /home/client2/ftp/banner.msg
virtual 206.171.50.52 logfile /home/client2/ftp/xferlog
```

不要忘记用你之前选择的 IP 地址和目录路径替换它们。你现在应该为每个主机修改 `banner.msg` 文件，以反映你想要显示的任何站点特定信息。此外，你的虚拟 FTP 站点不需要 `pub` 子目录，因此可以从每个站点中删除它。

在创建上述配置后，你的虚拟 FTP 服务器即可进行测试。通过 FTP 连接到每个虚拟 IP 地址，注意每个主机的横幅文件有何不同。虽然创建起来相当容易，但此虚拟设置缺乏完全自定义服务器外观和感觉的能力。例如，你不能在 `/etc/ftpaccess` 中使用 `email` 关键字指向适用于虚拟站点的不同电子邮件地址。

请注意，标准 `wu-ftpd` 提供的 `ftpshut` 命令不支持虚拟站点的关闭，因为它仅将关闭消息文件写入 `/etc/ftpaccess` 文件中 `shutdown` 关键字指定的单个位置。此外，当需要重启服务器时，你需要手动删除关闭消息文件。为了解决这个麻烦，你可能想从以下网站获取替换的 `ftpshut`/`ftprestart` 实用程序：

```
www.landfield.com/wu-ftpd/restart
```

你需要自行编译和构建这些实用程序。

## 创建完整的虚拟 FTP 服务

创建完整的虚拟 FTP 服务是托管虚拟 FTP 服务器的更完整方法。此方法要求你自行修补 `wu-ftpd` 源代码并编译它。

按照以下步骤创建虚拟 FTP 服务：

- 1. 下载 `wu-ftpd` 源代码。你可以从 `www.wu-ftpd.org/` 下载它。
- 你还需要从以下 FTP 站点获取补丁文件：
- `ftp://ftp.meme.com/pub/software/wu-ftpd-version/`
- 2. 阅读随补丁 tar-ball 文件提供的 `README` 文件，并将补丁应用到你之前下载的 `wu-ftpd` 源代码上。
- 3. 根据 `wu-ftpd` 源包提供的说明编译并安装修补后的 `wu-ftpd`。将新的 FTP 服务器安装到默认位置 `/usr/sbin/in.ftpd`。

新修补的 `wu-ftpd` 程序（`in.ftpd`）现在接受 `-a` 选项的参数。通常，`-a` 告诉服务器你希望它读取 `/etc/ftpaccess` 文件。现在修补后的版本允许服务器为 `ftpaccess` 文件指定不同的路径。因此，此选项允许新服务器查看创建虚拟 FTP 站点所需的不同的 `ftpaccess` 配置文件。

- 4. 现在修改 `/etc/xinetd.d/wu-ftpd` 文件，使 FTP 服务定义如下：

```
service ftp
{
    flags           = REUSE NAMEINARGS
    socket_type     = stream
    wait            = no
    user            = root
    server          = /usr/sbin/tcpd
    server_args     = /usr/sbin/in.ftpd
    log_on_success += DURATION USERID
    log_on_failure += USERID
    nice            = 10
    disable         = no
}
```

此文件通过 TCP wrapper（`tcpd`）调用 FTP 服务器。现在为每个 FTP 服务器（即主服务器和所有虚拟 FTP 服务器）修改 `/etc/hosts.allow` 文件，使其行类似于以下内容：

```
# For the primary server
ftpd@206.171.50.50 : ALL : twist exec \
/usr/sbin/in.ftpd -l -a /etc/ftp/ftpaccess
```

```
# For the virtual FTP server
ftpd@206.171.50.51 : ALL : twist exec \
/usr/sbin/in.ftpd -l -a /etc/ftp/client1.ftpaccess
```

```
# For the second virtual FTP server
ftpd@206.171.50.52 : ALL : twist exec \
/usr/sbin/in.ftpd -l -a /etc/ftp/client2.ftpaccess
```

- 5. 现在创建 `/etc/ftp` 目录并将 `/etc/ftpaccess` 文件移入该目录。
- 6. 复制 `/etc/ftp/ftpaccess` 文件两份，使你拥有 `/etc/ftp/client1.ftpaccess` 和 `/etc/ftp/client2.ftpaccess` 文件。
- 7. 从用于邮件 FTP 服务器的 `/etc/ftp/ftpaccess` 文件中删除任何 `virtual` 关键字。
- 8. 修改 `client1.ftpaccess` 文件，使其包含如下行：
  `virtual 206.171.50.51 root /home/client1/ftp`
- 9. 同样地，修改 `client2.ftpaccess` 文件，使其包含如下行：
  `virtual 206.171.50.52 root /home/client2/ftp`
  不要忘记用你自己的 IP 地址和目录路径替换。
- 10. 现在将 `anonftp` 文件复制到 `/home/client1/ftp` 和 `/home/client2/ftp` 目录中。
- 11. 使用以下命令重启 `xinetd` 服务器：
  `killall -USR1 xinetd`
  就这样！现在你有两个虚拟 FTP 站点，可以通过各自的主机名或 IP 地址访问。

## 监控传输日志

日志记录对于 FTP 服务非常重要，因为你想知道谁在对你的文件进行什么操作。`wu-ftpd` 服务器在 `xferlog` 文件中记录传输，该文件通常位于 `/var/log` 目录中。你可以使用前面讨论过的 `log` 命令和 `log transfers` 关键字来自定义日志记录。

如果你有兴趣定期监控 `xferlog`，可以尝试 Dump xfer。你可以从以下 FTP 地址下载此软件包：

```
ftp://ftp.microimages.com/tools/dump_xfer.1.2.tar.gz
```

## 成为高效的 FTP 用户

本节我将向你展示如何有效地使用 FTP 服务从 FTP 服务器下载或上传文件。

### 使用命令行 FTP 客户端

几乎所有现代操作系统默认都提供命令行 FTP 客户端。是的，甚至较新的 Windows（98 或更新版本）也内置了命令行 FTP 客户端。有趣的是，各种流行操作系统上的几乎所有 FTP 客户端的行为都非常相似。因此，如果你知道如何使用 Linux FTP 客户端，你应该能够在 Windows 下甚至 Mac OS X（基于 FreeBSD）下使用它。

### 连接到 FTP 服务器
