
- `sha384sum`

- `sha512sum`

这些工具的工作原理与 `sha1sum` 命令一样，当然，它们使用的是 SHA-2 密码哈希标准。各种 SHA-2 工具之间唯一的区别在于它们使用的密钥长度。`sha224sum` 命令使用的密钥长度为 224 位，`sha256sum` 命令使用的密钥长度为 256 位，以此此类推。记住，密钥越长，破解密码的概率就越小。

SHA-2 密码哈希标准是由国家安全局（NSA）创建的。SHA-3 是另一种密码哈希标准，由 NIST 在 2015 年 8 月发布。

# 在安装时加密 Linux 文件系统

你可能需要加密你 Linux 服务器上的整个文件系统。这可以通过多种方式实现，使用自由开源软件（FOSS）第三方工具，例如 Linux 统一密钥设置 [LUKS](https://github.com/cryptsetup/cryptsetup)。

在 Linux 中，选项之一是在安装时加密根分区（第 9 章，“安装 Linux”）。许多 Linux 发行版在安装过程中都包含加密选项。图 23.3 显示了红帽企业 Linux 安装过程中的加密选项。

在安装期间选择此选项后，系统会要求你输入密码。这是使用密码保护单个密钥的对称加密。图 23.4 显示了安装程序请求密钥密码。密码至少需要是八个字符。

## 图 23.3

红帽企业 Linux 加密选项

| 存储配置 |
| :--- |
| ○ 自动 ● 自定义 |
| 加密 |
| $\boxtimes$ 加密我的数据。你将创建一个口令。 |

## 图 23.4

Fedora 加密对称密钥密码

![](img/cc1e2b1a5739a47bac1a4c7cfac7c1a6_652_0.png)

## 图 23.5

在启动时请求加密对称密钥密码

![](img/cc1e2b1a5739a47bac1a4c7cfac7c1a6_653_0.png)

如果你选择了此加密选项，每次启动系统时，都会被要求输入对称密钥密码。图 23.5 显示了界面。只要其所在的磁盘是稳定的，这将保护根分区。

如果你继承了一个带有加密磁盘的系统，可以使用 root 权限通过 `lvs` 和 `cryptsetup` 命令以及 `/etc/crypttab` 文件来帮助。在接下来的示例中，`lvs` 命令显示系统上所有的逻辑卷及其底层设备名称。请参考第 12 章“管理磁盘和文件系统”以回顾不同的 LVM 命令。

```
# lvs -o devices
Devices
/dev/mapper/luks-b099fbbe-0e56-425f-91a6-44f129db9f4b(56)
/dev/mapper/luks-b099fbbe-0e56-425f-91a6-44f129db9f4b(0)
```

在该系统中，注意底层设备名称以 `luks` 开头。这表明已使用 Linux 统一密钥（LUKS）硬盘加密标准。

> 注意
> 字体 Ubuntu 默认安装了 `lvm` 命令。若要安装它，请在命令行运行 `sudo apt-get install lvm2`。

加密的逻辑卷在启动时使用 `/etc/crypttab` 文件中的信息进行挂载。然而，其内容用于触发在启动时获取密码，并解密 `/etc/fstab` 条目。如下文所示。注意 luks 名称与之前示例中列出的名称相同。

```
# cat /etc/crypttab
luks-b099fbbe-0e56-425f-91a6-44f129db9f4b UUID=b099fbbe-0e56-425f-91a6-44f129db9f4b none
```

你还可以使用 `cryptsetup` 命令帮助获取有关你 Linux 系统加密卷的信息。在示例示例中，使用了 `status` 选项结合 luks 设备名称来确定进一步信息。

```
# cryptsetup status luks-b099fbbe-0e56-425f-91a6-44f129db9f4b
/dev/mapper/luks-b099fbbe-0e56-425f-91a6-44f129db9f4b
is active and in use.
type: LUKS
cipher: aes-xts-plain64
keysize: 512 bits
device: /dev/sda3
offset: 4096 sectors
size: 49381904 sectors
mode: read/write
```

# 加密 Linux 目录

你可以使用 `encryptfs` 工具在 Linux 系统上进行加密。`encryptfs` 工具并不是文件系统类型（如其名称暗示的那样）。相反，它是一个符合 POSIX 标准的工具，允许你在任何文件之上创建加密层。

`encryptfs` 工具默认未在 Fedora 中安装且在 RHEL 中不可用。要在 Fedora 中安装它，请使用命令 `dnf install encryptfs-utils`。如果 Debian 系统上未安装，请使用命令 `sudo apt-get install encryptfs-utils`。

> 因为 encryptfs 工具用于加密……（此处继续）

# 第 23 章：理解高级 Linux 安全

当你挂载此加密目录时，它还会发出警告，因为该密钥以前没有使用过。该工具允许你对挂载的目录应用数字签名，这样当你再次挂载它时，它将挂载该目录而不需要密码。

提示

在第一次挂载 ecryptfs 文件夹时，写下你所做的选择。下次重新挂载文件夹时，你需要选择完全相同的选项。

要验证加密目录现在是否已挂载，你可以再次使用 `mount` 命令。在接下来的示例中，使用了 `mount` 命令并管道到 `grep` 以搜索 `/home/johnd/Secret` 目录。你可以看到，该目录是以 `ecryptfs` 类型挂载的。

```
# mount | grep /home/johnd/Secret
```

```
/home/johnd/Secret on /home/johnd/Secret type ecryptfs
(rw, realtime,ecryptfs_sig=70993b8d4361e067,ecryptfs_cipher=aes,ecryptfs_key_bytes=16,ecryptfs_unlink_sigs)
```

到目前为止，你还没有看到这个挂载并加密目录的效果。在后面的文中，将 `my_secret_file` 复制到加密目录中。用户也可以使用 `cat` 命令以明文形式显示文件。该文件由 `ecryptfs` 层自动解密。

```bash
$ cp my_secret_file Secret
$ cat /home/johnd/Secret/my_secret_file
Shh.. It's a secret.
```

root 用户也可以使用 `cat` 命令以明文形式显示文件

```bash
# cat /home/johnd/Secret/my_secret_file
Shh.. It's a secret.
```

然而，在使用 `umount` 命令卸载加密目录后，文件将不再自动解密。现在，文件 `my_secret_file` 变成了乱码，root 用户也无法读取。

```bash
# /home/johnd/Secret
```

因此，`ecryptfs` 工具允许你在文件系统中创建一个位置来非常方便地加密和解密文件。然而，当该目录不再作为 `ecryptfs` 类型挂载后，文件就是安全的，且无法被解密。

提示

作为非 root 用户，你可以使用 `ecryptfs-setup-private` 和 `ecryptfs-mount-private` 命令以非 root 用户身份配置加密挂载点。

# 第五部分：学习 Linux 安全技术

# 加密 Linux 文件

Linux 系统上最流行的文件加密工具是 OpenPGP 工具 GNU 守护（GNU Privacy Guard），即 `gpg`。它的灵活性和各种选项，加上它在大多数 Linux 发行版中默认安装的特性，增加了它的吸引力。

注意

如果你的组织使用第三方云存储公司，你需要知道其中一些公司（例如 Dropbox）在接收文件之前不会对其进行加密。这意味着该公司拥有解密你的文件所需的密钥，并可能使你组织的数据处于危险之中。在将文件发送到云端之前在 Linux 系统上进行加密可以增加额外的保护。

你还可以使用 Linux 系统上的其他加密工具来加密文件。就像 `gpg` 一样，许多此类工具允许你执行远比文件加密更多的多的操作。以下是你可以用于加密文件的流行 Linux 加密工具：

aescript：它使用对称密钥加密算法 Rijndael，也称为 AES。这个第三方开源软件（FOSS）工具可以从 www.aescript.com 下载。

bcrypt：此工具使用对称密钥加密算法 blowfish。它不是默认安装的。安装 `bcrypt` 后，可以使用相应的手册页（man pages）。

- 对于 Fedora（RHEL 中不可用）：`yum install bcrypt`
