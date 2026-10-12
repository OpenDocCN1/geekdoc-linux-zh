

_OsIk0T-E2l6qjfdDiwVmidoZjA
您是否信任这些密钥？ [ynYN] y
您即将初始化一个用于元数据存储的 LUKS 设备。
如果 LUKS 头部间隙中已经以不同格式写入了数据，尝试初始化可能会导致数据丢失。
建议在初始化之前进行备份。

您是否要初始化 /dev/sda？ [yn] y
输入现有 LUKS 密码：

此命令执行四个步骤：

1.  创建一个新的密钥，其熵值与 LUKS 主密钥相同。
2.  使用 Clevis 对新密钥进行加密。
3.  将 Clevis JWE 对象通过 LUKSMeta 存储在 LUKS 头部中。
4.  启用新密钥以便与 LUKS 配合使用。

现在，您可以使用现有密码以及 Clevis 策略来解锁此磁盘。如需了解更多信息，请参阅 `clevis-luks-bind(1)` 手册页。

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_124_0.png)

要验证 Clevis JWE 对象是否已成功放置在 LUKS 头部中，请使用 `luksmeta show` 命令：

```bash
[~]# luksmeta show -d /dev/sda
0    active empty
1    active cb6e8904-81ff-40da-a84a-07ab9ab5715e
2    inactive empty
3    inactive empty
4    inactive empty
5    inactive empty
6    inactive empty
7    inactive empty
```

为了让早期启动系统处理磁盘绑定，请在已安装的系统上输入以下命令：

```bash
[~]# yum install clevis-dracut
[~]# dracut -f
```

**重要**

要在使用静态 IP 配置（不使用 DHCPc）的客户端上启用 NBDE，请手动将网络配置传递给 dracut 工具，例如：

```bash
[~]# dracut -f --kernel-cmdline "ip=192.0.2.10 netmask=255.255.255.0 gateway=192.0.2.1 nameserver=192.0.2.45"
```

或者，在 /etc/dracut.conf.d/ 目录中创建一个包含静态网络信息的 .conf 文件。例如：

```bash
[~]# cat /etc/dracut.conf.d/static_ip.conf
kernel_cmdline="ip=10.0.0.103 netmask=255.255.252.0 gateway=10.0.0.1 nameserver=10.0.0.1"
```

重新生成初始 RAM 磁盘映像：

```bash
[~]# dracut -f
```

如需了解更多信息，请参阅 dracut .cmdline (7) 手册页。

### 4.10.4. 使用 Kickstart 配置自动注册

Clevis 可以与 Kickstart 集成，提供完全自动化的注册过程。

1.  指示 Kickstart 对磁盘进行分区，使根分区启用带有临时密码的 LUKS 加密。该密码是临时用于注册过程的。

    ```bash
    part /boot --fstype="xfs" --ondisk=vda --size=256
    part / --fstype="xfs" --ondisk=vda --grow --encrypted --passphrase=tempass
    ```

2.  通过在 %packages 部分中列出相关的 Clevis 软件包来安装它们：

    ```bash
    %packages
    clevis-dracut
    %end
    ```

3.  在 %post 部分中调用 clevis luks bind 来执行绑定。之后，移除临时密码：

    ```bash
    %post
    clevis luks bind -f -k- -d /dev/vda2 \\
    tang '["url1":"http://tang.srv", "thp":"_OsIk0T-E2l6qjfdDlwVmidoZjA"}' \\
    <<<<< "tempass"
    cryptsetup luksRemoveKey /dev/vda2 - <<< "tempass"
    %end
    ```

在上述示例中，请注意我们指定了在 Tang 服务器上信任的指纹作为绑定配置的一部分，从而实现对完全非交互式的绑定。

如需了解有关 Kickstart 安装的更多信息，请参阅 Red Hat Enterprise Linux 7 安装指南。有关 Linux 统一密钥设置磁盘格式 (LUKS) 的信息，请参阅第 4.9.1 节，“使用 LUKS 磁盘加密”。

### 4.10.5. 配置可移动存储设备的自动解锁

要自动解锁 LUKS 加密的可移动存储设备（例如 USB 驱动器），请安装 clevis-udisks2 软件包：

```bash
[~]# yum install clevis-udisks2
```

重新启动系统，然后按照第 4.10.3 节“配置根卷的手动注册”中描述的 `clevis luks bind` 命令执行绑定步骤，例如：

```bash
[~]# clevis luks bind -d /dev/sdb1 tang '{"url":"http://tang.srv"}'
```

现在，LUKS 加密的可移动设备可以在您的 GNOME 桌面会话中自动解锁。绑定到 Clevis 策略的设备也可以通过 `clevis luks unlock` 命令解锁：

```bash
[~]# clevis luks unlock -d /dev/sdb1
```

### 4.10.6. 配置启动时非根卷的自动解锁

若要使用 NBDE 也解锁 LUKS 加密的非根卷，请执行以下步骤：

1.  安装 clevis-systemd 软件包：

    ```bash
    [~]# yum install clevis-systemd
    ```

2.  启用 Clevis 解锁服务：

    ```bash
    [~]# systemctl enable clevis-luks-askpass.path
    Created symlink from /etc/systemd/system/remote-fs.target.wants/clevis-luks-askpass.path to /usr/lib/systemd/system/clevis-luks-askpass.path.
    ```

3.  按照第 4.10.3 节“配置根卷的手动注册”中描述的 `clevis luks bind` 命令执行绑定步骤。

4.  要在系统启动时设置加密块设备，请在 `/etc/crypttab` 配置文件中添加带有 `_netdev` 选项的相应行。如需了解更多信息，请参阅 `crypttab(5)` 手册页。

5.  将该卷添加到 `/etc/fstab` 文件中的可访问文件系统列表中。在此配置文件中也要使用 `_netdev` 选项。如需了解更多信息，请参阅 `fstab(5)` 手册页。

### 4.10.7. 在 NBDE 网络中部署虚拟机

`clevis luks bind` 命令不会更改 LUKS 主密钥。这意味着，如果您创建 LUKS 加密的映像以在虚拟机或云环境中使用，则运行该映像的所有实例都将共享主密钥。这是极其不安全的，应始终避免。

这不是 Clevis 的限制，而是 LUKS 的设计原则。如果您希望在云环境中拥有加密的根卷，您需要确保为云中的每个 Red Hat Enterprise Linux 实例执行安装过程（通常使用 Kickstart）。不能在不共享 LUKS 主密钥的情况下共享这些映像。

如果您打算在虚拟化环境中部署自动解锁，Red Hat 强烈建议您使用 lorax 或 virt-install 等系统，并结合 Kickstart 文件（参见[第 4.10.4 节，“使用 Kickstart 配置自动注册”](section-ref)）或其他自动配置工具，以确保每个加密虚拟机拥有唯一的主密钥。

### 4.10.8. 为云环境构建可自动注册的虚拟机映像

在云环境中部署可自动注册的加密映像可能会带来一系列独特的挑战。与上述其他虚拟化环境类似，映像最多应实例化一次，以避免共享 LUKS 主密钥。因此，应使用 lorax 或 virt-install 等自动化部署系统结合 Kickstart 文件，以确保在映像构建过程中主密钥的唯一性。

云环境允许两种 Tang 服务器部署选项，这里我们予以考虑。首先，Tang 服务器可以部署在云环境本身内部。其次，Tang 服务器可以部署在云之外，在独立的 infrastructure 上，并且两个 infrastructure 之间有 VPN 连接。

在云中本地部署 Tang 确实可以实现轻松部署。然而，鉴于它与其他系统的密文数据持久层共享基础设施，Tang 服务器的私钥和 Clevis 元数据可能存储在同一个物理磁盘上。访问此物理磁盘允许完全破坏密文数据。

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_127_0.png)

# 重要

因此，Red Hat 强烈建议保持数据存储位置与运行 Tang 的系统之间的物理隔离。这种云与 Tang 服务器之间的隔离确保 Tang 服务器的私钥不会意外与 Clevis 元数据结合。如果云 infrastructure 存在风险，它还提供了对 Tang 服务器的本地控制。

### 4.10.9. 其他资源

如需了解更多信息，请参阅以下手册页：

- tang(8)
- clevis(1)
- jose(1)
- clevis-luks-unlockers(1)
- tang-nagios(1)

## 4.11. 使用 AIDE 检查完整性

