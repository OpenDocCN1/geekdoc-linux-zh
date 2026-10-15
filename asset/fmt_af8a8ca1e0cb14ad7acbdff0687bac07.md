
1. 在命令提示符处输入`mkdir /home/user1/source`并按回车，在示例用户的主目录下创建一个用于托管安装文件的目录。（注意：对于 NFS 安装，目录名称是任意的，需要在安装期间指定。）
2. 将第一张 Red Hat 7.2 安装 CD-ROM 插入 FTP 服务器的 CD-ROM 驱动器。
3. 在命令提示符处输入`mount -r -t iso9660 /dev/cdrom/mnt/cdrom`并按回车来挂载 CD-ROM。
4. 输入`cp -r /mnt/cdrom/RedHat /home/user1/source`将 `RedHat` 目录及其内容复制到`/home/user1/source`目录。
5. 接下来，输入`umount /mnt/cdrom`从`/mnt/cdrom`目录卸载第一张 Red Hat Linux 7.2 安装 CD-ROM。
6. 将第二张 Red Hat 7.2 安装 CD-ROM 插入 FTP 服务器的 CD-ROM 驱动器。
7. 在命令提示符处输入`mount -r -t iso9660 /dev/cdrom/mnt/cdrom`并按回车来挂载 CD-ROM。
8. 在命令提示符处输入`cp -r /mnt/cdrom/RedHat /home/user1/source`并按回车。这将 Red Hat 目录及其内容复制到`/home/user1/source`目录。
9. 接下来，输入`umount /mnt/cdrom`从`/mnt/cdrom`目录卸载第二张 Red Hat Linux 7.2 安装 CD-ROM。
10. 在命令提示符处输入命令`chown -R user1 /home/user1/source`并按回车，递归地将`/home/user1/source`目录的所有更改更改`user1`。
11. 接下来，编辑`/etc/xinetd.d/wu-ftpd`文件并更改该行：
    ```
    disable = yes
    disable = no
    ```
    使其读取为：

保存文件更改并返回命令提示符。

在命令提示符处输入以下命令并按回车，重启允许 FTP 会话的`xinetd`进程：

```
/etc/rc.d/init.d/xinetd restart
```

## 使用 HTTP 进行网络安装

如果网络上无法使用 NFS 和 FTP，那么使用超文本传输协议（HTTP）从网络上的 Web 服务器进行安装也是一种备选方案。请记住，Web 服务器从目录树中的特定目录处理输出 HTML 文件和其他 Web 内容。如果你在该目录下创建一个包含 Red Hat Linux 7.2 安装文件的子目录，你就可以可以在安装期间指定此目录以及 Web 服务器的 IP 地址或名称。

要配置 Apache Web 服务器以托管其他计算机使用 Red Hat 7.2 安装的文件，你可以执行以下步骤：

1. 在命令提示符处输入`mkdir /var/www/html/source`并按回车，在 Web 内容下创建一个用于托管安装文件的目录。（注意：对于 NFS 安装，目录名称是任意的，需要在安装期间指定。）
2. 将第一张 Red Hat 7.2 安装 CD-ROM 插入 Web 服务器的 CD-ROM 驱动器。
3. 在命令提示符处输入`mount -r -t iso9660 /dev/cdrom /mnt/cdrom`并按回车来挂载 CD-ROM。
4. 输入`cp -r /mnt/cdrom/RedHat /var/www/html/source`将 Red Hat 目录及其内容复制到`/var/www/html/source`目录。
5. 接下来，输入`umount /mnt/cdrom`从`/mnt/cdrom`目录卸载第一张 Red Hat Linux 7.2 安装 CD-ROM。
6. 将第二张 Red Hat 7.2 安装 CD-ROM 插入 Web 服务器的 CD-ROM 驱动器。
7. 在命令提示符处输入`mount -r -t iso9660 /dev/cdrom /mnt/cdrom`并按回车来挂载 CD-ROM。
8. 在命令提示符处输入`cp -r /mnt/cdrom/RedHat /var/www/html/source`并按回车。这将 Red Hat 目录及其内容复制到`/var/www/html/source`目录。
9. 接下来，输入`umount /mnt/cdrom`从`/mnt/cdrom`目录卸载第二张 Red Hat Linux 7.2 安装 CD-ROM。
10. 在命令提示符处输入以下命令并按回车启动 Apache 服务器：
    ```
    /etc/rc.d/init.d/httpd start
    ```

## 从客户端进行安装

要从客户端计算机启动任何此类网络安装，你必须创建一个网络安装启动盘。要在 Windows 系统上创建此磁盘，你可以执行以下步骤：

- 将第一张 Red Hat 7.2 安装 CD-ROM 插入你的 CD-ROM 驱动器。
- 双击“此电脑”并选择你的 CD-ROM 驱动器（例如 `D:`）。
- 双击 Red Hat 7.2 CD-ROM 上的 `dosutils` 目录。
- 双击重写程序执行它。当提示源镜像时，输入`D:\images\boot.img`（如果 `D:` 是你的 CD-ROM 驱动器）并按回车。当提示目标驱动器时，将格式化好的软盘插入软盘驱动器，输入`A:`并按回车。

如之前所述，你可以使用 Linux 创建此启动盘：

- 将第一张 Red Hat 7.2 安装 CD-ROM 插入 CD-ROM 驱动器。
- 在命令提示符处输入`mount -r -t iso9660 /dev/cdrom /mnt/cdrom`并按回车来挂载 CD-ROM。
- 在命令提示符处输入`cd /mnt/cdrom/images`并按回车。
- 将格式化好的软盘插入软盘驱动器，在命令提示符处输入`dd if=boot.img of=/dev/fd0 bs=144K`并按回车将 `boot.img` 文件映像到软盘。

一旦创建了软盘，你就可以直接使用它启动客户端计算机，并在之前图 7-7 所示的屏幕上按回车。在文本界面安装程序加载后，你会被提示选择语言和键盘类型，这与之前讨论的硬盘安装相同，如图 7-18 和图 7-19 所示。接下来，你会被提示选择网络安装类型，如图 7-21 所示。

## 高级安装方法 325

![](img/6148a12ef656b46c092b21c2e023d928_342_0.png)

图 7-21 使用网络启动引导软盘进行文本安装时选择网络安装类型

无论在图 7-21 中选择哪种安装类型，你随后都会被提示配置网络设置，如图 7-22 所示。

![](img/6148a12ef656b46c092b21c2e023d928_342_1.png)

图 7-22 使用网络启动引导软盘进行文本安装期间配置网络设置

IP 地址和子网掩码的值通常由互联网服务提供商（ISP）或网络管理员分配，以便使使用该 IP 地址的计算机能够与网络上正确的机器进行通信。然而，你也可以选择自动从网络上的 `DHCP` 或 `BOOTP` 服务器接收配置。如果手动配置，默认网关和主 DNS 名称服务器是可选的，但如果已知这些值，则应当使用它们。

如果你选择 NFS 安装，安装程序将提示输入网络上 NFS 服务器的 DNS 名称或 IP 地址以及导出目录。这些选择在图 7-23 中所示，使用了之前在设置 NFS 服务器时导出的 `/source` 目录。

# 第 7 章 高级安装

![](img/6148a12ef656b46c092b21c2e023d928_343_0.png)

图 7-23 使用网络启动引导软盘进行文本安装期间输入 NFS 配置

或者，如果你选择执行 FTP 安装，系统将提示输入 FTP 安装的类型（匿名或用户）以及 FTP 服务器的 DNS 名称或 IP 地址。图 7-24 显示了在之前讨论的 FTP 配置下你会做的选择；系统将提示你使用有效密码作为“用户”登录。指定的目录必须是 `/home/user` 目录下的目录，并且包含安装 CD-ROM 中的 Red Hat 目录。

![](img/6148a12ef656b46c092b21c2e023d928_343_1.png)

图 7-24 使用网络启动引导软盘进行文本安装期间输入 FTP 配置

与 FTP 安装类似，HTTP 安装需要 Web 服务器的 DNS 名称或 IP 地址，以及 Web 服务器内容下（默认认为`/var/www/html`）包含安装 CD-ROM 中 Red Hat 目录的目录名称，如图 7-25 所示。

## 高级安装方法 327

![](img/6148a12ef656b46c092b21c2e023d928_344_0.png)

图 7-25 使用网络启动引导软盘进行文本安装期间输入 HTTP 配置
