
列表。例如，/etc/ftpaccess 文件中的以下行允许 mrfrog 组（在 /etc/group 中找到）的任何成员成为访客用户：

```
guestgroup mrfrog
```

换句话说，FTP 服务器执行 chroot 操作。对于 mrfrog 用户，FTP 服务器将根目录更改为 /home/mrfrog。

## 第 8 步：测试账户

现在通过 FTP 连接到服务器并以 mrfrog 身份登录。如果一切设置正确，你只能看到该用户的 home 目录。尝试上传文件或创建目录。你应该被允许执行这些操作。然而，mrfrog 是否被允许删除、覆盖或重命名文件取决于 /etc/ftpaccess 中对这些操作的设置。例如，默认的 /etc/ftpaccess 文件包含以下行：

```
chmod      no  guest,anonymous
delete     no  guest,anonymous
overwrite  no  guest,anonymous
rename     no  guest,anonymous
```

这些行禁止访客账户执行 chmod、delete、overwrite 或 rename 操作。如果你希望允许访客账户执行这些操作，你必须从这些行中的默认 typelist 中移除 guest，并将它们改为以下行：

```
chmod      no  anonymous
delete     no  anonymous
overwrite  no  anonymous
rename     no  anonymous
```

最后，如果你不想保留 anonftp 包或不希望在 FTP 服务器上拥有 anonftp 功能，你可以从适当的 (/ftp) 目录中删除包文件，或直接运行以下命令：

```
rpm -e anonftp-3.0-6.i386.rpm
```

不要忘记使用适当的文件名，因为你的版本或架构可能与本行中的描述不同。

## 创建虚拟 FTP 站点

如果你有多个域名并且需要支持独立的 FTP 服务器（ftp.domain-1.com、ftp.domain-2.com 等），你可以使用虚拟 FTP 服务。虚拟 FTP 服务使你能够为多个域名共享单一服务器系统。你可以通过至少两种不同方式配置 wu-ftpd 服务器以支持虚拟 FTP 服务。本文将讨论这两种方法。因为这两种方法都要求在系统上设置 IP 地址别名，所以我先讨论 IP 别名方法。

## 创建 IP 别名

为了拥有虚拟 FTP 服务器，首先你需要为每个 FTP 主机设置适当的 DNS 记录。你需要多个 IP 地址（每个 FTP 服务器主机一个）路由到你的 FTP 服务器机器。使用 IP 别名技术，你必须为所有 IP 地址创建虚拟以太网接口。例如，假设我需要在名为 ftp.evoknow.com 的 FTP 服务器上创建两个虚拟 FTP 服务器（ftp.client-01.com 和 ftp.client-02.com）。另外假设我已经为每个域名设置了 DNS 记录，使得以下行成立：

```
; In client-01.com DNS database
ftp.client-01.com. IN A 206.171.50.51

; In client-02.com DNS database
ftp.client-02.com. IN A 206.171.50.52

; In evoknow.com DNS database
ftp.evoknow.com. IN A 206.171.50.50
```

在 ftp.evoknow.com 机器上设置 IP 别名和路由后（按照第 6 章中的说明），如果我运行以下命令

```
cat /proc/net/aliases
```

我会看到以下 IP 别名：

| 设备 | family | 地址 |
| eth0:0 | 2 | 206.171.50.51 |
| eth0:1 | 2 | 206.171.50.52 |

现在来看创建虚拟主机最简单的方法。

## 创建有限的虚拟 FTP 服务

此方法比另一种方法更简单，但也相当受限。虽然你将拥有虚拟 FTP 服务，但无法像那样进行太多自定义。如果你想要一个完全可定制的服务（如主 FTP 服务器），请跳到“创建完整的虚拟 FTP 服务”部分。

要创建此有限版本的虚拟 FTP 服务，你需要制作 anon-ftp 包创建的文件/目录结构的多个副本。只需安装 anonftp 包并为每个虚拟主机制作其副本。对于前面的示例，我创建两个虚拟 FTP 站点目录（/home/client1/ftp 和 /home/client2/ftp）并复制 /home/ftp 文件和目录的所有内容。制作 /home/ftp 的精确副本最简单的方法之一是运行以下命令：

```
cd /home/client1/ ; cp -a /home/ftp .
cd /home/client2/ ; cp -a /home/ftp .
```

这些命令将 /home/ftp 文件/目录结构复制到虚拟站点目录中。现在编辑 /etc/ftpaccess 文件以添加 virtual 关键字，如下所示：

```
virtual 206.171.50.51 root    /home/client1/ftp
virtual 206.171.50.51 banner  /home/client1/ftp/banner.msg
virtual 206.171.50.51 logfile /home/client1/ftp/xferlog

virtual 206.171.50.52 root    /home/client2/ftp
virtual 206.171.50.52 banner  /home/client2/ftp/banner.msg
virtual 206.171.50.52 logfile /home/client2/ftp/xferlog
```

不要忘记用你之前选择的 IP 地址和目录路径替换它们。你现在应该为每个主机修改 banner.msg 文件，以反映你想要显示的任何站点特定信息。此外，你的虚拟 FTP 站点不需要 pub 子目录，因此可以从每个站点中删除它。

在创建上述配置后，你的虚拟 FTP 服务器即可进行测试。通过 FTP 连接到每个虚拟 IP 地址，注意每个主机的横幅文件有何不同。虽然创建起来相当容易，但此虚拟设置缺乏完全自定义服务器外观和感觉的能力。例如，你不能在 /etc/ftpaccess 中使用 email 关键字指向适用于虚拟站点的不同电子邮件地址。

请注意，标准 wu-ftpd 提供的 ftpshut 命令不支持虚拟站点的关闭，因为它仅将关闭消息文件写入 /etc/ftpaccess 文件中 shutdown 关键字指定的单个位置。此外，当需要重启服务器时，你需要手动删除关闭消息文件。为了解决这个麻烦，你可能想从以下网站获取替换的 ftpshut/ftprestart 实用程序：

```
www.landfield.com/wu-ftpd/restart
```

你需要自行编译和构建这些实用程序。

## 创建完整的虚拟 FTP 服务

创建完整的虚拟 FTP 服务是托管虚拟 FTP 服务器的更完整方法。此方法要求你自行修补 wu-ftpd 源代码并编译它。

按照以下步骤创建虚拟 FTP 服务：

- 1. 下载 wu-ftpd 源代码。你可以从 www.wu-ftpd.org/ 下载它。
- 你还需要从以下 FTP 站点获取补丁文件：
- ftp://ftp.meme.com/pub/software/wu-ftpd-version/
- 2. 阅读随补丁 tar-ball 文件提供的 README 文件，并将补丁应用到你之前下载的 wu-ftpd 源代码上。
- 3. 根据 wu-ftpd 源包提供的说明编译并安装修补后的 wu-ftpd。将新的 FTP 服务器安装到默认位置 /usr/sbin/in.ftpd。

新修补的 wu-ftpd 程序（in.ftpd）现在接受 -a 选项的参数。通常，-a 告诉服务器你希望它读取 /etc/ftpaccess 文件。现在修补后的版本允许服务器为 ftpaccess 文件指定不同的路径。因此，此选项允许新服务器查看创建虚拟 FTP 站点所需的不同的 ftpaccess 配置文件。

- 4. 现在修改 /etc/xinetd.d/wu-ftpd 文件，使 FTP 服务定义如下：

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

此文件通过 TCP wrapper（tcpd）调用 FTP 服务器。现在为每个 FTP 服务器（即主服务器和所有虚拟 FTP 服务器）修改 /etc/hosts.allow 文件，使其行类似于以下内容：
