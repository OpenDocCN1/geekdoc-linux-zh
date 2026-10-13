
基本的 SSH 配置包括客户端（用于建立连接的计算机上使用）和服务器（在要建立连接的系统上运行）。例如，用户可能会使用在 Linux、Windows 或 macOS 系统上运行的 SSH 客户端连接到在 RHEL 9 系统上运行的 SSH 服务器，以获取 shell 命令行提示或执行文件传输。客户端和服务器之间的所有通信，包括用于获取访问权限的密码，都经过加密以防止外部方拦截数据。

基本 SSH 实现的固有弱点在于它完全依赖于系统上账户分配的密码强度。如果恶意方能够识别出账户的密码（无论是通过猜测、欺骗还是暴力攻击），系统就会变得脆弱。这种弱点可以通过实施基于 SSH 密钥的身份验证来解决。

### 15.2 基于 SSH 密钥的身份验证

基于 SSH 密钥的身份验证使用非对称公钥加密为远程系统访问增加额外的安全层。公钥加密的概念由 Whitfield Diffie 和 Martin Hellman 于 1975 年提出，基于使用一对私钥和公钥。

在公钥加密系统中，公钥用于加密数据，而只有私钥所有者才能解密该数据。

在基于 SSH 密钥的身份验证的情况下，私钥保存在 SSH 客户端所在的计算机上，而相应的公钥则驻留在运行 SSH 服务器的系统上。因此，保护私钥至关重要，因为拥有该密钥的人可以登录到远程系统。作为额外的保护层，私钥也可以加密并通过密码保护，每次建立到服务器的连接时都必须输入该密码。

### 15.3 设置基于密钥的身份验证

设置基于密钥的 SSH 身份验证有四个步骤，可总结如下：

- 1. 生成公钥和私钥。
- 2. 在服务器上安装公钥。
- 3. 测试身份验证。
- 4. 在服务器上禁用基于密码的身份验证。

本章的其余部分将更详细地介绍这些步骤，适用于基于 Linux、macOS 和 Windows 的客户端操作系统。

### 15.4 安装和启动 SSH 服务

如果 SSH 服务器尚未安装并在系统上运行，可以使用以下命令添加：

```
# dnf install openssh-server
# systemctl start sshd.service
# systemctl enable sshd.service
```

### 15.5 来自 Linux 和 macOS 客户端的基于 SSH 密钥的身份验证

设置基于 SSH 密钥的身份验证的第一步是在客户端系统上生成密钥对。如果客户端系统运行 Linux 或 macOS，则使用 `ssh-keygen` 实用程序实现：

```
# ssh-keygen
```

此命令将产生类似以下内容的输出：

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/<username>/.ssh/id_rsa):
```

按 Enter 键接受密钥文件的默认位置。这将在当前用户主目录的 `.ssh` 子目录中放置两个文件。私钥将存储在名为 `id_rsa` 的文件中，而公钥将位于名为 `id_rsa.pub` 的文件中。

接下来，`ssh-keygen` 将提示输入用于保护私钥的密码短语。如果提供了密码短语，私钥将在本地磁盘上加密，并且需要该密码短语才能访问远程系统。因此，为了更好的安全性，建议使用密码短语。

```
Enter passphrase (empty for no passphrase):
```

最后，`ssh-keygen` 工具将生成以下输出，表明密钥已生成：

```
Your identification has been saved in /home/neil/.ssh/id_rsa.
Your public key has been saved in /home/neil/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:FOLGWEEGFijWnCT5wtTOv5VK4hdimzWghZizUEM Ybfo <username>@<hostname>
The key's randomart image is:
+---[RSA 2048]----+
|.BB+=+*..       |
|o+B= * . .      |
|===.. + .       |
|*+ * . .        |
|.++ o S         |
|..E+ * o        |
|   o B *        |
|    + +         |
|     .          |
+----[SHA256]----+
```

下一步是将公钥安装到远程服务器系统上。这可以使用 `ssh-copy-id` 实用程序按如下方式实现：

```
$ ssh-copy-id username@remote_hostname
```

例如：

```
$ ssh-copy-id neil@192.168.1.100
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/neil/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
neil@192.168.1.100's password:
Number of key(s) added: 1
```

现在尝试使用以下方式登录机器：`ssh 'neil@192.168.1.100'` 并检查是否仅添加了您想要的密钥。

一旦密钥安装完毕，通过使用 `ssh` 客户端尝试远程登录来测试身份验证是否有效：

```
$ ssh -l <username> <hostname>
```

如果私钥经过加密并使用密码短语保护，请在提示时输入该短语以完成身份验证并建立对 RHEL 9 系统的远程访问：

```
Enter passphrase for key '/home/neil/.ssh/id_rsa':
Last login: Fri Mar 31 14:29:28 2023 from 192.168.86.21
```

## 在 RHEL 9 上配置 SSH 基于密钥的身份验证

```
[neil@demosystem02 ~]$
```

对于服务器上需要远程访问的任何其他账户，请重复这些步骤。如果还需要从其他客户端系统访问，请将 `id_rsa` 私钥文件复制到其他系统上您主文件夹的 `.ssh` 子目录中。

按当前配置，仍可使用安全性较低的密码身份验证访问远程系统。一旦您验证基于密钥的身份验证正常工作，系统上就需要禁用密码身份验证。要了解如何更改此设置，请先打开 `/etc/ssh/sshd_config` 文件并找到以下行：

```
Include /etc/ssh/sshd_config.d/*.conf
```

这告诉我们 `sshd` 配置设置由 `/etc/ssh/sshd_config.d` 目录中的文件控制。这些文件名必须以数字为前缀，并具有 `.conf` 文件扩展名，例如：

```
01-permitrootlogin.conf
50-redhat.conf
```

数字前缀指定文件相对于文件夹中其他文件的优先级，其中 01 为最高优先级。这确保了如果配置文件包含与另一个文件冲突的设置，则优先级最高的文件始终占优。

在 `/etc/ssh/sshd_config.d` 文件夹中，创建一个名为 `02-nopasswordlogin.conf` 的新文件，内容如下：

```
PasswordAuthentication no
```

保存文件并重启 `sshd` 服务以实施更改：

```
# systemctl restart sshd.service
```

从此时起，只能使用 SSH 基于密钥的身份验证远程访问系统，并且在这种情况下，您无需输入密码。

### 15.6 管理多个密钥

在客户端系统上驻留多个私钥是很常见的，每个私钥提供对不同服务器的访问。因此，在建立连接时存在多种选择特定密钥的选项。例如，可以在启动 `ssh` 客户端时指定要使用的私钥文件，如下所示：

```
$ ssh -l neilsmyth -i ~/.ssh/id_work 35.194.18.119
```

另外，SSH 客户端用户配置文件可以将密钥文件与服务器关联。配置文件名为 `config`，必须位于用户主目录的 `.ssh` 目录中，可用于配置各种选项，包括私钥文件、连接时使用的默认端口、默认用户名以及用于引用服务器的简写昵称。以下示例 `config` 文件为两个服务器定义了不同的密钥文件，并允许通过昵称 `home` 和 `work` 来引用它们。对于 `work` 系统，文件还指定了身份验证时使用的用户名：
