

此配置文件设置了一些标准的 SMB 服务，包括 smbd 使用的只读主目录和打印机。

上面的示例 smb.conf 文件中有三个部分：[global]、[homes] 和 [printers]。这三个被称为特殊部分。[global] 部分的目的是为文件的其余部分设置默认值；[homes] 和 [printers] 控制对主目录和打印机的访问。

以下是你应该注意的 [global] 部分的一些参数。你可以在各个部分中覆盖其中的大部分。

guest account = username

username 应该是一个无特权的用户，几乎不能做什么（除了打印和访问公共目录）。默认值为 nobody。

browseable = true|false

如果设置为 true，远程主机可以访问 SMB 共享列表。

security = type

设置访问控制的类型。默认值是 user，仅允许已注册的登录访问服务器。其他选项是 share（适用于公共服务器）、server 和 domain。（参见本章后面的问题 35 关于加密密码，了解为什么你可能无法从 Windows 机器登录到 SAMBA 服务器。）

netbios name = name

使服务器在网络上以 name 而不是 Unix 主机名为人所知。

虽然示例 smb.conf 文件指定 SAMBA 服务器应属于 HOME 工作组，但它没有说明周围的机器将如何识别 SAMBA 服务器。服务器未运行任何浏览主服务器，因此如果它出现在任何网络邻居浏览器中，网络上的 Windows 机器可能正在充当浏览主服务器。

要开始使用 SAMBA，请从一个简单的 smb.conf 文件开始，像上面的示例一样。 在你至少能够列出服务器上可用的共享（使用 smbclient -L servername）之后，开始根据自己的需求定制 smb.conf。

使用以下命令启动 SAMBA 守护进程

# nmbd -D -s configfile
# smbd -D -s configfile

其中 configfile 是你的 smb.conf 文件的完整路径名。

## Debugging

你会在名为 log.nmb 和 log.smb 的日志文件中找到调试信息，位于你配置为存储 SAMBA 的 var 的目录中（默认为 prefix/var，其中 prefix 是安装前缀）。

## PROBLEM 32

症状：访问控制过少或过多。

问题：对所需的安全性感到困惑。

修复：如果刚开始使用，请使用 security=share，它会在每次连接到共享时向客户端请求一次密码。默认的 [security=user] 需要登录到 SAMBA 服务器 [我们不讨论这一点]。security=server 设置尝试将登录传递给另一台服务器，而 security=domain 表示 SAMBA 应表现得像在真正的 Windows NT 网络上一样（也就是说，它应询问 Windows NT 主域控制器客户端是否有访问权限）。你可以在 smb.conf（5）手册页中找到每个设置的详细信息。

## Workgroup and Network Browser Options

要在 Windows 机器上使用网络邻居浏览器，你必须在网络机器上运行某种浏览服务器。该服务器收集网络上的 SMB 服务器列表并将其提供给请求它的客户端。有两种方法可以做到这一点：使用 Windows 工作组或使用 Windows NT 域。

### Browse Servers

如果你希望网络邻居能够正常工作，并且你的网络上没有 Windows 机器，你需要将 SAMBA 设置为浏览服务器。与大多数 SAMBA 选项一样，你将在 smb.conf 文件中找到配置。请注意，如果你想为 Windows NT 域设置浏览，可以以与工作组相同的方式设置它。然而，要使你的 Windows NT 登录名和密码与 Unix 网络上的相同，你需要将 SAMBA 设置为域主。那超出了本书的范围。

运行浏览服务器时，你将使用域主浏览器和本地主浏览器的组合。每个工作组需要一个域主，如果你有多个子网，则需要在域主之外的每个子网上设置一个本地主。

