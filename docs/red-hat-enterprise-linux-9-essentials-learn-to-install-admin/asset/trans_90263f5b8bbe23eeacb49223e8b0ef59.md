
## 使用 firewalld 配置 RHEL 9 防火墙

工具的关键区域可总结如下：

- A - 显示当前所有活动接口及其所分配的区域。要将接口分配到不同区域，请从此面板中选择它，点击“更改区域”按钮并从生成的对话框中选择所需的区域。

- B - 控制工具中显示的信息以及所做的任何更改是应用于运行时规则还是永久规则。

- C - 系统上配置的区域、服务或 IPSets 的列表。此面板中的信息取决于工具栏 F 中所做的选择。从此面板的列表中选择一项会更新标记为 D 的主面板。

- D - 主面板包含工具栏 E 中当前类别选择的信息。在此示例中，面板显示 public 区域的服务。每个服务旁边的复选框控制该服务在防火墙中是否启用。在这些类别面板中，可以添加新规则或配置/删除现有规则。

- E - 控制面板 D 中显示的内容。从此栏中选择项目会显示所选类别的当前规则。

- F - 控制面板 C 中显示的列表。

firewall-config 工具使用起来直接且直观，允许使用 firewall-cmd 可用的许多任务在可视化环境中执行。

### 14.6 摘要

经过精心规划和实施的防火墙对任何安全系统都至关重要。就 RHEL 9 而言，firewalld 服务提供了一个灵活且易于管理的防火墙系统。

firewalld 服务使用区域的概念对防火墙规则集进行分组，并包含一套预定义的区域，旨在满足各种防火墙保护需求。这些区域可以修改以添加或删除规则，或创建并配置全新的区域。系统上连接到网络或互联网的网络设备称为接口。每个接口依次分配给一个区域。操作 firewalld 的主要工具是 firewall-cmd 命令行工具和 firewall-config 图形实用程序。最小的防火墙管理选项也可通过 Cockpit Web 界面使用。

## 第 15 章

## 15. 在 RHEL 9 上配置基于 SSH 密钥的身份验证

当 RHEL 9 系统首次安装时，默认配置为允许通过安全外壳（SSH）连接进行远程命令行访问。SSH 为 root 账户以及在安装阶段添加的任何其他用户提供密码保护和加密的系统访问权限。然而，这种安全级别是不够的，应尽快升级到基于 SSH 密钥的身份验证。

本章将概述通过实施基于密钥的 SSH 身份验证来提高 RHEL 9 系统安全性的步骤。

### 15.1 安全外壳（SSH）概述

SSH 设计用于允许安全远程访问系统以获取 shell 访问并传输文件和数据。如“使用 VNC 进行 RHEL 9 远程桌面访问”中所述，SSH 还可以提供安全隧道，通过该隧道可通过网络连接实现对 GNOME 桌面的远程访问。

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

设置基于 SSH 密钥的身份验证的第一步是在客户端系统上生成密钥对。如果客户端系统运行 Linux 或 macOS，则使用 ssh-keygen 实用程序实现：

```
# ssh-keygen
```

此命令将产生类似以下内容的输出：

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/<username>/.ssh/id_rsa):
```

按 Enter 键接受密钥文件的默认位置。这将在当前用户主目录的 .ssh 子目录中放置两个文件。私钥将存储在名为 id_rsa 的文件中，而公钥将位于名为 id_rsa.pub 的文件中。

接下来，ssh-keygen 将提示输入用于保护私钥的密码短语。如果提供了密码短语，私钥将在本地磁盘上加密，并且需要该密码短语才能访问远程系统。因此，为了更好的安全性，建议使用密码短语。

```
Enter passphrase (empty for no passphrase):
```

最后，ssh-keygen 工具将生成以下输出，表明密钥已生成：

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

下一步是将公钥安装到远程服务器系统上。这可以使用 ssh-copy-id 实用程序按如下方式实现：

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

现在尝试使用以下方式登录机器：“ssh 'neil@192.168.1.100'”并检查是否仅添加了您想要的密钥。

一旦密钥安装完毕，通过使用 ssh 客户端尝试远程登录来测试身份验证是否有效：

```
$ ssh -l <username> <hostname>
```

如果私钥经过加密并使用密码短语保护，请在提示时输入该短语以完成身份验证并建立对 RHEL 9 系统的远程访问：

```
Enter passphrase for key '/home/neil/.ssh/id_rsa':
Last login: Fri Mar 31 14:29:28 2023 from 192.168.86.21
```
