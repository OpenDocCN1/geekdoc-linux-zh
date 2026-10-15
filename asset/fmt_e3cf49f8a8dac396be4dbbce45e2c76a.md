
删除 `/tmp/man1_directory` 后，你可以运行 `rsync` 将所有文件拷贝到 `/tmp/man1_directory`，使用 `-a`（递归）、`-v`（详细）和 `-l`（符号链接）。然后立即运行该命令，你会发现没有任何文件被复制。`rsync` 命令知道所有文件都已经在那里，所以它不会进行复制。对于包含数 GB 文件但仅有几 MB 变化的目录，这可以极大节省网络带宽。

同样从 `-l` 可以注意到，符号链接被保留了，并且文件上有日期/时间戳。如果你以后需要恢复这些文件，可以按原样将其放回去。

这种 `rsync` 的用法非常适合备份。但如果你想合并两个目录，使两台机器上的两个目录内容完全相同呢？以下命令说明了如何使用之前的 `rsync` 命令所示目录，在两台机器上创建目录结构的精确镜像。

首先，在远程系统中，向正在拷贝的目录拷贝一个新文件：

```bash
# cp /etc/services /usr/share/man/man
```

接下来，在本地系统上运行 `rsync` 来拷贝任何新文件（在本例中，只有远程目录和新文件）：

```bash
$ rsync -avl johndoe@10.140.67.23:/usr/share/man/man1 /tmp

johndoe@10.140.67.23:password:

************

sending incremental file list

man1/

man/services
```

之后，回到远程系统删除该新文件：

```bash
$ sudo rm /usr/share/man/man/services
```

现在，在本地系统上再次运行 `rsync`，发现什么都没有发生。此时，远程和本地目录是不同的，因为本地系统拥有文件而远程系统没有。这是备份目录的正确行为（你希望在备份中保留文件，以防某些文件被删除）。然而，如果你想远程和本地目录保持镜像，则必须添加 `--delete` 选项。

# 第四部分：成为 Linux 服务器管理员

结果是 `services` 文件在本地系统中被删除，使得远程和本地目录结构保持同步。

```bash
$ rsync -avl /usr/share/man/man1 localhost:/tmp

johndoe@10.140.67.23:password: ************

sending incremental file list

man/
```
```bash
$ rsync -avl --delete johndoe@10.140.67.23:/usr/share/man/man1 /tmp

johndoe@10.140.67.23:password: ************

sending incremental file list

deleting man1/services
```

## 使用 sftp 进行交互式拷贝

如果你不知道如何使用 `sftp` 从远程系统拷贝或向其拷贝，可以使用 `nsftp` 命令在 SSH 会话中创建一个交互式的 SFTP 风格会话。使用 `sftp`，你可以通过 SSH 连接到远程系统、更改目录、列出目录内容，然后（在权限允许的情况下）获取文件并将文件放置在服务器上。请记住，尽管名称如此，但 `sftp` 与 FTP 协议没有任何关系，且无法使用 FTP 服务器。它仅仅是在客户端和 ssh 服务器之间使用 SFTP 类型的交互。

以下示例显示了用户 `johndoe` 连接到 `jd.example.com`：

```bash
$ sftp johndoe@jd.example.com

Connecting to jd.example.com

johndoe@jd.example.com:password: ************

sftp>>
```

此时，你可以开始交互式 SFTP 会话。你可以像使用任何 FTP 客户端一样对文件使用 `get` 和 `put` 命令，但由于知道自己正通过加密且安全的连接工作，会感到非常轻松。FTP 协议以明文处理用户名、密码和数据，因此在 SSH 上使用 `sftp` 是允许用户交互式地从服务器拷贝文件的更好替代方案。

## 基于密钥（无密码）的验证

如果你全天都在使用 SSH 工具连接到同一系统，可能会发现反复输入密码非常不便。SSH 不再使用密码验证，而是允许你设置基于密钥的验证在此处使用。操作方法如下：

- 创建一个公钥和一个私钥。
- 保护好私钥，但将公钥拷贝到你想要进行基于密钥验证的远程主机的用户帐户上。
- 将密钥拷贝到正确的位置后，你可以使用任何 SSH 工具连接到远程主机上的用户账户，但远程 SSH 服务不会向你索要密码，而是比较公钥和私钥，如果两个密钥匹配，则允许你访问。

# 第13章：理解服务器管理

当你创建密钥时，可以选择为你的私钥添加一个密码短语（passphrase）。如果你决定添加密码短语，尽管你不需要输入密码来验证远程系统，你仍需要输入短语来解锁私钥。如果你不添加密码短语，就可以以完全无密码的方式使用私钥/公钥对进行通信。然而，如果有人持有了你的私钥，他们可以在任何需要该密钥的通信中冒充你的身份。

以下步骤演示了本地用户如何为 IP 地址为 `10.140.67.23` 的远程用户 `johndoe` 设置基于密钥的验证。如果你有两个 Linux 系统，可以通过系统上的两个用户帐户来模拟这一点。我首先以本地用户 `chris` 登录并输入以下内容生成公钥/私钥：

```bash
$ ssh-keygen

Generating public/private RSA key pair.

Enter file in which to save the key (/home/ssh/id_rsa): 

Enter passphrase (empty for no): 

Enter same passphrase again: 

Identification has been saved in /home/ssh/id_rsa.

Your public key has been saved in /home/ssh/id_rsa.pub.

Your fingerprint is: SHA256:...

Key's random image is: ...
```

在创建密钥时，你可以选择为私钥添加一个密码短语。如果你决定添加密码短语，尽管你不需要输入密码来验证远程系统，你仍需要输入短语来解锁私钥。如果你不添加密码短语，就可以以完全无密码的方式使用私钥/公钥对进行通信。然而，如果有人持有了你的私钥，他们可以在任何需要该密钥的通信中冒充你的身份。
