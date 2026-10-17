
登录打算作为存储库的计算机。更新的 RPM 默认存储在`/var/spool/update2`目录。确保更新的 RPM 不被删除。要做到这一点，请运行`up2date-config`命令。你将看到图 7-6 所示的界面。

## 注意

如果你在 GUI 中，你可能需要运行`up2date-config --nox`命令来访问图 7-6 中的所示选项。

```
root@enterprise-la:~~
keepAfterInstall      Yes
useGPG               No
headerCacheSize       40
forcecache           No
systemd              No/etc/sysconfig/rhn/system
returnAfterSource     Yes
enablePolls           No
gpgcheck              No/etc/sysconfig/rhn/up2date-keying.gpg
url                   #localhost
addaddresses         Yes
serverURL             https://xmlrpc.rhn.redhat.com/XMLRPC
filesAsList           No
versionOrder         No
selCACert             No
nohelpConfig         Yes
desallowChange       '#Reboot','useSSLCert','ForPackages','useSSLSe
headerCount          10
prekeyvar             '*kernel'
removeupdatelist      No
up2date               No
```

输入要编辑的项目编号 <按回车退出，按 q 退出且不保存>:

图 7-6 配置代理更新以保留 RPM

输入 17（该选项编号可能会不同）。这与`keepAfterInstall`变量相关。如果设置为`yes`，软件包在安装后将保留在`/var/spool/update2`中。当你下次从 Red Hat 网络下载软件包时，软件包将被存储在该目录中，且不会被删除。

## 注意

你也可以使用`keepAfterInstall`之前的选项来禁用对`up2date` RPM 的自动更新，这通常是`/etc/sysconfig/rhn/up2date`中的默认设置。如果`up2date` RPM 升级，你可以从相同目录下的`up2date.rpmnew`文件恢复你的自定义设置，并在下次有新版本的 update 可用时禁用更新。

## 使用适当的分区配置存储库

正如你在书中所看到的，存储库需要几个 GB 的空间。将存储库配置在单独的分区是有意义的。为了这个存储库，我将`/var/spool/update2`分配到了新分区。有关如何配置新分区的详细信息，请参考《Linux Administration Handbook》（Evi Nemeth, Garth Snyder, Upper River, NJ: Prentice Hall, 2002）或《Mastering Red Hat Linux 3》（Michael Jang, Alameda, CA: Wiley, 2004）。如果你想了解更多关于这些命令的信息，请参考本书。如果你的分区有剩余空间，可以将其分配给`/var/spool/update2`。这种方法如下，假设你添加了一个新硬盘。如果该硬盘是系统的第一个 SCSI 或 SATA 硬盘，运行`fdisk /dev/sda`命令。

1. 使用`fdisk /dev/sda`命令分配一个新分区。

2. 分配编号 1，从第一个磁道开始，在提示时分配 +10G。按`w`将分区表写入硬盘。

3. 格式化硬盘。运行以下命令：

```
mkfs -t ext3 /dev/sda
```

4. 挂载`/var/spool/update2`目录：

```
mount /dev/sda /var/spool/update2
```

5. 确保下次重启计算机时，将以下行添加到你的`/etc/fstab`：

```
/dev/sda /var/spool/update2 ext3 defaults 1
```

## 从存储库获取 RPM

现在你可以从 Red Hat 网络下载所需的 RPM。你可以下载你订阅的所有可用通道。通过以下命令（指定 RHEL 4 工作站通道），你可以下载系统中尚未安装的 RPM。稍后，你将从安装光盘添加 RPM。

```
up2date -d --installall --channel=rhel-i386-ws-4
```

## 7.6 创建企业存储库

Red Hat 网络没有独立的存储库。软件包被整合到现有通道中。自然地，由于安装 RPM 有大约 2GB 的数据，下载量可能很大。根据你的连接速度，你可能需要等待几个小时。示例如图 7-7 所示。

```
xorg-doc-6.8.9.23.EL3 ########################### Done.
xorg-lib-6.8.9.23.EL3 ########################### Done.
xorg-wm-6.8.9.23.EL3 ########################### Done.
pxdf-300.1.5.1386.rpm ######################## Done.
rkstop-0.2.4.1386.rpm ############################# Done.
sane-02.9.1386.rpm ################################# Done.
sane-02.31.5.1386.rpm ########################### Done.
term-1992-1.1386.rpm ########################## Done.
sifs-tools-0.6.1.1386.rpm ####################### Done.
zsh-4.2.0-1386.rpm ############################## Done.
zsh-html-4.2.0-1386.rpm ############################ Done.
```

以下软件包被你的配置跳过了：

| 名称 | 版本 | 原因 |
| :--- | :--- | :--- |
| `kernel` | `2.6.9` | `5.0.5.EL` name/pattern |
| `kernel-dev` | `2.6.9` | `5.0.5.EL` name/pattern |
| `kernel-doc` | `2.6.9` | `5.0.5.EL` name/pattern |
| `kernel-hugme` | `2.6.9` | `5.0.5.EL` name/pattern |
| `kernel-hugme-devel` | `2.6.9` | `5.0.5.EL` name/pattern |
| `kernel-core` | `2.6.9` | `5.0.5.EL` name/pattern |
| `kernel-smp-dev` | `2.6.9` | `5.0.5.EL` name/pattern |

图 7-7 下载更新

## 从安装光盘添加 RPM

现在你应该从 RHEL 安装光盘添加 RPM。这是基础操作。如果你有物理光盘（像我一样），`mount`命令需要一个小技巧。例如，如果你将 ISO 存储在`/mnt/test`分区，我可以使用以下命令挂载第一个 RHEL ISO：

```
mount -o loop /mnt/test/RHEL4-i386-AS-disk.iso /media/cdcorreder
```

然后你可以使用以下命令将 RPM 复制到`/var/spool/update`目录：

```
cp -ar /media/cdcorreder/RedHat/RPMs* /var/spool/update/
```

自然地，对第一个光盘重复此过程，你需要卸载并重复其他的 RHEL 光盘，直到将所有可用 RPM 复制到`/var/spool/update`目录。

## 7.6.2 让 RHEL 更新存储库“Yum 化”

在 RHEL 存储库中配置好所需的文件后，你可以将其设置为 yum 存储库。正如本章前面提到的，这需要`yum-arch`或`createrepo`命令，具体取决于你的发行版。`createrepo`软件包针对 Fedora Core 3 进行了适配。由于 RHEL 4 是从 Fedora Core 3 构建的，我们将使用该软件包来对该存储库进行“Yum 化”。
