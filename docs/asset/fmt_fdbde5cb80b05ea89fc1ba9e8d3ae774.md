
```
mynfsserver:/data    /data nfs    _netdev 0 0
```

# 配置自动挂载

在某些情况下，将你的 NFS 挂载放在 `/etc/fstab` 中效果良好。在其他情况下，它有更好的挂载 NFS 共享的方法。

这种情况场景的一个示例是你想自动挂载 NFS 共享。要执行此操作，你需要遵循以下步骤：

- 1. 启动 `autofs` 服务。
- 2. 编辑 `/etc/master`。
- 3. 创建 `auto.data` 文件。

`/etc/master` 中的配置看起来如下：

```
/data      /etc/auto.data
```

以及

```
/misc     /etc/auto.misc
```

这告诉 Automount 对于 `/data` 目录，应该查找 `/etc/auto.data`，对于 `/misc` 目录，查找 `/etc/auto.misc`。

`/auto.data` 中的配置看起来如下：

```
%home      -rw,soft:/home
```

这告诉 Automount 当用户导航到 `/home` 的子目录时，从远程服务器挂载相应的子目录。

## 配置自动挂载 Automount

`/home` 也是其主目录的 NFS 挂载。假设主目录可以通过名为 `nfsserver` 的服务器上的 NFS 导出来可用，你可以进行以下 Automount 配置。

首先，在 `/etc/auto.master` 中，包含以下行来监控 `/home/ldap` 的内容：

`/home/ldap      /etc/auto.ldap`

这一行告诉 Automount，`/home/ldap` 的额外配置在 `/etc/auto.ldap` 中。在该文件中，你需要添加以下内容：

* -rw `nfsserver:/home/ldap/`

你可以这样理解这一行：*`*`（即你所想象的每一个子目录）* 在 `/home/ldap` 目录中，应该创建一个可读可写的挂载到 `&`（即使用使用 `nfsserver:/home/ldap` 名称的目录）。在练习 13.5 中，你将学习如何将所有这些整合在一起。

# 练习 13.5

为主目录创建自动挂载配置

在本次练习中，你将在主机计算机上创建一个 NFS 共享，从而访问用户主目录。你将在虚拟机上设置 Automount，以透明的方式挂载这些主目录。

- 1. 在主机计算机上，打开 `/etc/exports`，并添加以下行：

   `/home      * (rw)`
- 2. 在主机计算机上，使用 `service nfs restart`（重）启动 NFS 服务。
- 3. 在主机计算机上，使用 `useradd lucy` 创建用户 `lucky` 和目录 `/home/lucy`。
- 4. 在虚拟机上，使用 `mount -e yourserver` 验证 NFS 服务器是否提供了该共享。
- 5. 在虚拟机上，打开 `/etc/auto.master`，并插入以下行：

   `/home      /etc/auto.home`
- 6. 在虚拟机上，创建文件 `/etc/auto.home`，并赋予其以下内容：

   * -rw `nfsserver:/home/`
- 7. 在虚拟机上使用 `service autofs restart` 重启 Automount，并 `cd /home/lucy` 以访问 `/home/lucy` 的内容。你现在可以访问 NFS 服务器上的 `/home/lucy` 了。

# 配置 Samba

你刚刚学习了如何使用 NFS 访问远程计算机上的文件系统。NFS 快速且方便，但它也有一个主要的缺点：它只能工作于 Linux 和 UNIX 机器之间。为了访问其他类型的客户端，你需要使用那些客户端上可用的文件共享协议。通用互联网系统 `CIFS` 就是这样一种协议，它由 Linux Samba 服务器提供。在本章中，你将学习如何设置 Samba 服务器来提供文件共享。

Samba 是一个非常多功能的服务，你可以将其用于网络中的多种用途。除了共享文件外，它还可以共享打印机，并提供 Windows 域服务（如目录服务）。你甚至可以将 Samba 集成到 Active Directory 域中，并使其成为 Active Directory 的成员服务器。这意味着 Active Directory 中的所有用户都可以轻松访问你在 Samba 服务器上提供的资源。然而，Samba 最流行的用法是作为文件服务器。

## 设置 Samba 文件服务器

设置 Samba 文件服务器非常直观。要设置一个文件服务器，你需要执行以下操作：

- 1. 在 Samba 服务器的 Linux 文件系统上创建一个目录。
- 2. 如果需要，创建 Linux 用户并为你刚刚创建的目录赋予相应的权限。
- 3. 安装 Samba 服务器。
- 4. 在 `/etc/samba/smb.conf` 中定义共享。
- 5. 创建一个具有共享访问权限的 Samba 用户。
- 6. （重）启动 Samba 服务。
- 7. 告诉 SELinux 允许访问 Samba 共享。

之前的步骤中有一些需要进一步的解释。让我们从用户账户开始。在 Samba 上提供访问有多种方法，这在本章的下一节中也会进一步解释。要设置 Samba 服务器（如你将在下面的练习中所做的那样），你同时需要 Linux 用户和 Samba 用户。Linux 用户用于本地文件系统上的 Linux 权限。然而，Windows 用户无法使用 Linux 用户的凭据进行验证。这就是为什么你还需要一个与 Linux 用户同名的 Samba 用户。通常，Windows 用户需要与 Samba 用户协同工作，这意味着只有 Samba 用户的密码是相关的。Linux 用户用于本地访问。作为管理员，你只需要确保它拥有适当的权限。

要定义共享，你将将其放在 Samba 的主配置文件，即 `/etc/samba/smb.conf`。基本的共享定义非常简单：它为共享指定名称，并告诉 Samba 要共享什么。一个最基本的共享定义可能如下：

```
[myshare]

# 配置 Samba

path=/mysharefolder
```

在定义共享时，你还可以使用许多选项来定义谁以及以什么样的访问权限可以使用该共享。例如，它可能如下：

```
[myshare]
path = /mydatafiles
comment = some shared files
allow hosts = 192.168.1.
writable = yes
public = yes
write list = +mygroup
```

在这个示例中，添加了一些选项。首先指定了注释，这使得客户端在浏览网络以查找可用服务时更容易识别该共享。接下来，`allow hosts` 参数将访问限制为仅使用 `192.168.1` IP 地址的主机。

# 练习 13.6

```
comment = samba files
path = /sambafiles
writable = yes
valid user = lucy, linda, lori
```

- 6. 使用 `usadd lucy` 为用户 lucy 创建用户账户。不要设置密码，因为 Samba 用户在 Linux 系统上不需要密码。
- 7. 使用 `smpasswd -a lucy` 创建 Samba 用户 lucy。
- 8. 使用 `service smb restart` 重启 Samba 服务，并使用 `chconfig smb on` 确保它随服务器启动而启动。
- 9. 使用 `smbclient -L //localhost`。这将显示你当前的 Samba 服务器参数，你会看到你刚刚创建的共享已列其中。`smbclient -L` 命令会显示一个登录提示，你可以通过按两次回键来忽略它。

## Samba 与 SELinux

你创建了一个 Samba 共享，但目前它无法工作。这是因为在 Red Hat 上使用 Samba 之前，你必须先应用 SELinux 设置。除了你可以使用的布尔值（Booleans）之外，最重要的更改是你将想要与 Samba 共享的目录设置为 `samba_share_t` 上文类型。如果你想向其他文件共享服务授予 Samba 共享目录，你也可以将上下文设置为 `public_content_t`。

要设置合适的 Samba 上文类型，请使用以下命令：
