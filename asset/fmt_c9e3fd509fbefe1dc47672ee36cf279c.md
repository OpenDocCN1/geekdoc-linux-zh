
例如，行 `/srv/nfs-data *(ro) 192.168.1.11(rw) 192.168.1.12(rw)` 定义了我们想要将 `/srv/nfs-data` 文件夹的内容导出到所有主机名（由于使用了 `*` 符号）；只读（`ro`）意味着每个客户端都可以读取文件内容但不能修改。对于 IP 地址为 192.168.1 以 11 和 12 结尾的客户端，我们允许读取和写入（`rw`）。第二行定义了我们将 `/home` 目录导出到 `*.example.com` 的所有子域，并具有读/写能力。每当你更改 `/etc/exports` 文件时，运行 `exports -r` 命令将更改应用到 NFS 服务器。

最后，我们可以说，CentOS 7 中的 NFSv4 非常易于设置和启动。它是 Linux 系统之间共享文件或用于集中化主目录的完美解决方案。

# 使用 NFS

在客户端计算机可以使用由 NFS 服务器共享的文件系统之前，它必须经过正确配置以访问该系统。在本份食谱中，我们将向你展示如何在客户端机器上设置和使用 NFS。

### 准备工作

完成此食谱，你将需要一个具有 root 权限且运行良好的 CentOS 7 操作系统安装、一个任选的控制台文本编辑器，以及一个可以连接到互联网以方便下载额外的包。预计你已经遵循了“安装和配置 NFS”的食谱，并像本示例一样设置了 NFS 服务器。预计所有客户端都能相互 ping 通并已连接到 NFS 服务器，并将使用静态 IP 地址（参见第 2 章“配置系统”中的“构建静态网络连接”食谱）。在我们的示例中，NFS 服务器运行在 IP `192.168.1.10`，两个客户端的 IP 分别 `12.168.1.11` 和 `192.168.1.12`。

### 如何操作...

在我们的客户端上，我们需要相同的 NFS 软件软件包，以及与服务器类似的配置，以在它们之间建立通信：

1.  首先，以 root 身份登录你的客户端，并执行与“安装和配置 NFS”食谱完全相同的步骤，直到第 3 步结束。跳过第 4 步，因为不需要打开防火墙服务。然后，不要执行第 5 步，而是使用以下命令，它们将建立通信：

    ```bash
    systemctl start rpcbind
    systemctl enable rpcbind
    systemctl start nfs-server
    systemctl enable nfs-server
    ```

2.  编辑 `/etc/hosts` 文件并添加以下内容：

    ```text
    192.168.1.10  myServer.example.com
    192.168.1.11  myClient1.example.com
    192.168.1.12  myClient2.example.com
    ```

3.  编辑 `/etc/exports` 文件并添加以下内容：

    ```text
    /srv/nfs-data  *(ro) 192.168.1.11(rw) 192.168.1.12(rw)
    /home         *.example.com(rw)
    ```

4.  运行命令以应用更改：

    ```bash
    exports -r
    ```

5.  在服务器上，执行以下命令：

    ```bash
    groupadd -g 50000 nfs-share
    chown -R root:nfs-share /srv/nfs-data
    chmod -R 775 /srv/nfs-data
    ```

6.  在客户端上，执行以下命令以准备用户：

    ```bash
    groupadd -g 50000 nfs-share
    useradd -G nfs-share john
    ```

7.  在客户端上，挂载共享目录：

    ```bash
    mount -t nfs 192.168.1.10:/srv/nfs-data /mnt/nfs-data
    mount -t nfs 192.168.1.10:/home /mnt/home
    ```

8.  编辑 `/etc/fstab` 以实现自动挂载：

    ```text
    192.168.1.10:/srv/nfs-data  /mnt/nfs-data  nfs  defaults  0 0
    192.168.1.10:/home          /mnt/home      nfs  defaults  0 0
    ```

9.  测试自动挂载：

    ```bash
    umount /mnt/nfs-data /mnt/home
    mount -a
    ```

10. 验证挂载情况：

    ```bash
    touch /mnt/nfs-data/test.txt
    ls /mnt/nfs-data
    ls /home
    cat /mnt/nfs-data/test.txt
    ```

### 第 7 章

```ini
dos charset = CP932
workgroup = <WORKGROUP_NAME>
server string = <MY_SERVERS_NAME>
netbios name = <MY_SERVERS_NAME>
dns proxy = no
wins support = no
interfaces = 127.0.0.0/8 XXX.XXX.XXX/24 <NETWORK_NAME>
bind interfaces only = no
log file = /var/log/samba/slog.%m
log size = 1000
syslog object = no
syslog = 0
panic action = /usr/share/samba/panic-action %d
```

> `WORKGROUP_NAME` 是 Windows 工作组的名称。如果你没有此值，请使用标准的 Windows 名称 `WORKGROUP`。`MY_SERVERS_NAME` 指的是你的服务器名称。在大多数情况下，这可以是 `FILESSERVER` 或 `SERVER1` 等形式。`XXX.XXX.XXX/XX` 指的是你的 Samba 服务运行的主网网络地址，例如 `192.168.1.04`。`NETWORK_NAME` 指的是你的以太网接口名称，这可能是 `en0s8`。

5.  我们将把 Samba 配置为独立服务器。要做到这一点，只需继续向你的主配置文件添加以下几行：

    ```ini
    security = user
    encrypt passwords = true
    passdb backend = tdbsam
    obey restrictions = yes
    unix password sync = yes
    password program = /usr/bin/passwd %u
    password chat = *Enter\n\s*password:* %\n*Retype\n\s*password:* %\n*password*updated\ssuccessfully*
    pam password changes = yes
    map to guest = bad user
    usershare allow guests = no
    ```

6.  出于本教程的目的，我们并不将 Samba 配置为域主或主浏览器。要做到这一点，请添加以下行：

    ```ini
    domain master = no
    local master = no
    preferred master = no
    os level = 8
    ```

    ![](img/a6dbf7df749be83c0faae2334e970c0b_605_0.png)

7.  我们现在将通过允许有效用户访问其家目录，来支持家目录共享。此功能将支持适当的读写权限，且文件夹将对其他用户保持私密。要做到这一点，请添加以下新行：

    ```ini
    [homes]
      comment = Home Directories
      browseable = no
      writable = yes
      valid users = %S
      create mask = 0755
      directory mask = 00755
    ```

8.  保存并关闭文件。要测试我们刚刚创建的 Samba 配置文件的语法，请使用以下命令：

    ```bash
    testparm
    ```

9.  现在，将现有的系统用户 `john` 添加到 Samba 用户管理系统中（这是为了稍后进行测试；请根据你的情况将其更改为用户名）：

    ```bash
    smbpasswd -a john
    ```

10. 现在，保存文件并关闭；回到命令行界面，在防火墙中打开端口：

    ```bash
    firewall-cmd --permanent --add-service=samba
    firewall-cmd --reload
    ```

11. 配置 SELinux 使用 Samba 家目录：

    ```bash
    setsebool -P samba_enable_home_dirs on
    ```

12. 现在，确保 `samba` 和 `nmb` 服务将在启动过程中启动，并立即启动它们：

    ```bash
    systemctl enable smb && systemctl enable nmb
    systemctl start smb && systemctl start nmb
    ```
