

在安装完成之前，请安全地存储签名数据库。首先，安装 Tripwire 软件包：

```
$ sudo apt-get install tripwire
```

如果您尚未安装 MTA（邮件传输代理），Tripwire 软件包会将其作为依赖项添加。在 Tripwire 软件包安装过程中，您将被询问一系列关于密钥的问题。Tripwire 使用两个不同的密钥来签名文件并确保其未被篡改。第一个密钥是站点范围的密钥，您可能将其用于特定网络上的所有服务器。第二个密钥是本地密钥，唯一适用于此特定机器。如果您尚未拥有站点密钥或不确定其含义，请回答 Yes 以创建站点密钥。接下来会出现关于本地密钥的类似提示。除非您已拥有本地 Tripwire 密钥，否则在此处也应回答 Yes，以便安装程序可以创建它。在下一个提示中，回答 Yes 以重建 Tripwire 配置文件，并在最后一次提示中再次回答 Yes 以重新创建策略文件。最后，输入用于站点和本地密钥的密码短语。务必记录您选择的密码短语，因为如果忘记，没有方法可以检索或重置它们。

## 更新 Tripwire 策略

Tripwire 策略文件位于 /etc/tripwire/twpol.txt，并定义了 Tripwire 将监控的所有文件和目录，以及要监控的信息和对每个文件更改的响应方式。默认的 twpol.txt 文件是一个不错的起点，但其中包含一些文件和目录，您需要将其删除以避免每次运行 Tripwire 检查时出现大量误报。用文本编辑器打开该文件，并按下面每个文件所述删除行：

- /etc/rc.boot
- Ubuntu 没有此文件，因此删除写有以下内容的行

```
/etc/rc.boot   -> $(SEC_BIN) ;
```

- /proc
- /proc 目录中的文件会不断变化，因此如果扫描此目录，您将收到大量误报。从文件中删除以下行：

```
/proc   -> $(Device) ;
```

## /root

twpol.txt 文件中有一大段列出了 /root 目录下的文件。问题是默认情况下这些文件不存在，因此会产生误报。找到文件中看起来像这样的部分：

```
# These files change the behavior of the root account
(
    rulename = "Root config files",
    severity = 100
)
{
    /root    -> $(SEC_CRIT) ; # Catch all additions to /root
```

删除对 /root 目录下所有文件的引用，除了 /root/.bashrc。修改后的 twpol.txt 文件片段如下所示：

```
# These files change the behavior of the root account
(
    rulename = "Root config files",
    severity = 100
)
{
    /root    -> $(SEC_CRIT) ; # Catch all additions to /root
    /root/.bashrc  -> $(SEC_CONFIG) ;
}
```

保存所有更改，然后使用 twadmin 工具更新策略文件：

```
$ sudo twadmin -m P /etc/tripwire/twpol.txt
```

## 初始化 Tripwire 数据库

策略文件更改后，您就可以初始化数据库了。请注意，Tripwire 将此时系统的状态视为黄金标准，因此您希望在系统创建后尽快初始化数据库。以下是初始化 Tripwire 数据库的命令：

```
$ sudo tripwire -m i
```

不必担心关于 /var/lib/tripwire/foo.twd 文件不存在的任何错误——这就是您现在正在创建的数据库。数据库初始化后，您应该将其安全存储，因为如果攻击者获得 root 权限，他们可以更新数据库并隐藏其踪迹。有几种方法可以保护数据库。其一，您可以将数据库存储在设置了物理写保护位的软盘上，并更改 /etc/tripwire/twcfg.txt 文件以指向该新位置。或者，您可以设置一个您认为安全的 NFS 服务器来托管所有 Tripwire 数据库文件，并将所有数据库设为只读。

由于软盘越来越难获得，我将介绍如何使用 NFS 设置。假设您的 Tripwire 数据库位于 /var/lib/tripwire/host1.twd。您有一个 NFS 服务器位于 10.1.1.7，并且已将 host1.twd 文件复制到 /mnt/tripwire/host1/。然后您将使用 chmod 400 /mnt/tripwire/host1/host1.twd 来确保文件无法被更改。由于 Tripwire 检查以 root 用户身份运行，您可能需要在 NFS 服务器上禁用 root 压缩，至少在您需要更新数据库时。如果您想要额外的安全性，您还可以修改 /etc/exports 文件，以便此共享只能以只读方式挂载。NFS 服务器管理超出了本章的范围，但有关 NFS 服务器配置的更多信息，请参阅第 5 章的 NFS 部分。配置好 NFS 后，在本地机器上创建名为 /mnt/tripwire 的目录并挂载 NFS 共享：

```bash
$ sudo mkdir /mnt/tripwire
$ sudo mount -o ro 10.1.1.7:/mnt/tripwire/host1/ /mnt/tripwire
```

如果您收到此文件系统类型未知的错误，请确保已安装 nfs-common 软件包。共享成功挂载后，在 /etc/fstab 中添加一行新内容，以确保每次系统启动时自动挂载：

```text
10.1.1.7:/mnt/tripwire/host1 /mnt/tripwire nfs defaults,ro 0 0
```

现在如果您运行 sudo ls -l /mnt/tripwire/，您应该能够看到 /mnt/tripwire/host1.twd 文件（文件名将以您的主机名命名

