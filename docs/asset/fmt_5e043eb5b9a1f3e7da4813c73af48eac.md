
# 178 第二章：系统服务与 SELinux

或者，你可以运行以下命令将服务设置为仅在运行级别 3 和 5 下自动启动：

```
# chkconfig nfs --level 35 on
```

你可以使用 `chkconfig-list nfs` 命令确认 NFS 服务的设置结果。如果只激活了运行级别 3 和 5，你应该看到下方的输出：

```
nfs 0:off 1:off 2:off 3:on 5:on 6:off
```

理所当然，除非另有说明，否则你应该对书中配置或在生产系统中配置的任何和所有服务重复此过程。红帽（Red Hat）的目标应该激励你建立此类生产环境级别的系统。

## 配置 SELinux 以支持该服务

红帽已经让 SELinux 变得更容易处理。通常情况下，在为 SELinux 配置服务时，你需要做两件事：

- 配置与服务关联的文件类型，通常是正在共享的目录中的 SELinux 文件类型。
- 激活 `/selinux/booleans` 目录下的 SELinux 布尔值（booleans）。

默认文件类型列在 `/etc/selinux/targeted/contexts/files` 目录下的 `file_contexts` 文件中。通常从默认目录共享文件时，请确保上下文（contexts）与默认匹配。例如，以下命令将 `/var/www/html` 目录的文件内容与假设的 `/www.example.net` 目录匹配：

```
# chkcon -R --reference=/var/www/html /www.example.net
```

`/selinux/booleans` 目录下的布尔值通常用于控制各种服务的功能。例如，某些与 Samba 相关的 SELinux 设置以 `samba_` 开头。这些设置大部分几乎是不言自明的；例如，`samba_enable_home_dirs` 控制了通过 Samba 服务器导出家目录。该选项默认是禁用的；若要通过 samba 共享家目录，你需要启用此布尔值。

某些页面包含了针对不同 SELinux 布尔值的详细信息；获取相关页面完整列表的一种方法是使用以下命令：

```
$ apropos _selinux
```

此外，通过 GUI 运行 `system-config-selinux` 命令可以进入 SELinux 管理工具，它支持查看布尔值，按服务模块轻松分组，并对每个布尔值提供简要描述。

你还可以使用以下命令获取这些描述的数据库及其当前状态：

```
# manageage boolean -l
```

在搜索数据库时，请注意与某些服务相关的不同名称。例如，我运行以下命令来识别所有与 Samba 相关的布尔值：

```
# manageage boolean -l | grep samba
```

```
# manageage boolean -l | grep cifs
```

## 配置基于密钥认证

基于密钥的认证被列在 RHCE 目标中，作为 SSH 服务器配置的一部分。它基于一对密钥——一个私钥，一个公钥。私钥保留在 SSH 服务器上，并限制所有者拥有读写（rw）权限。私钥对他人不可用。对于主机，私钥和公钥存储在 `/etc/ssh` 目录中。对于用户，相应的密钥存储在每个用户家目录下的 `.ssh/` 子目录下。

当你第一次登录到远程系统时，使用如下命令用用户名登录：

```
ssh tester@gamma.example.net
```

SSH 客户端和服务器之间第一次建立连接时，会提示以下消息：

主机 'gamma.example.net (192.168.122.20)' 的真实性无法确认。RSA 密钥指纹为 81:09:03:9e:c4:91:28:25:7c:f7:12:56:1a:05bf。确定要继续连接吗 (yes/no)?

一旦确认，来自 `/etc/ssh` 目录的远程 SSH 服务器公 RSA 密钥将被复制到 SSH 客户端，并附加到用户家目录 `.ssh/` 子目录下的 `known_hosts` 文件中。随后系统会提示输入 SSH 服务器上目标用户的密码。

# 第 11 章：系统服务与 SELinux

完全配置后，基于密钥的认证支持安全连接，无需通过任何网络传输密码。你可以使用 `ssh-keygen` 命令创建基于用户的私钥/公钥对，它会提示输入密码串（passphrase）。默认情况下，它会创建一个 2048 位的密钥对，这比标准密码安全得多。你可以在家目录的 `.ssh/` 子目录下找到私钥和公钥。默认情况下，密钥命名为 `id_rsa` 和 `id_rsa.pub`。

然后你可以将公钥发送到远程 SSH 服务器。以下 `ssh-copy-id` 命令将其发送到系统 gamma：

```
$ ssh-copy-id -i .ssh/id_rsa.pub testuser@gamma.net
```

你会发现本地 `id_rsa.pub` 文件的副本附加到 SSH 服务器上用户 `~/.ssh/` 子目录下的 `authorized_keys` 文件末尾。你可以像以前一样连接到 SSH 服务器，但现在会提示你输入创建密钥对时使用的密码串。

## 配置文档描述的附加选项

尽管此目标限于 SSH 服务，但它仍然非常开放。
