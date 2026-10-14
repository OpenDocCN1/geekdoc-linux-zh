
确保系统中已安装并启动了 Apache Web 服务器。以 `geeko` 身份登录 GNOME 桌面，并在 Web 浏览器中输入 URL `http://127.0.0.1` 查看默认页面。

接下来，以 `root` 用户身份登录 `ty1`，查看 `/etc/apache2/2.conf` 文件的内容（该文件由 `/etc/apache2/httpd.conf` 引用）。接着，查看 `/srv/www/htdocs/index.html` 文件的所有者权限。Apache 守护进程可以读取其内容吗？

接下来，将 `/srv/www/htdocs/index.html` 文件的权限改为 `600` (`rw----`)，切换回 `ty7` 并刷新 Web 页面 (`http://127.0.0.1`)。你收到了什么？为什么？

完成后，切换回 `ty1`，将 `/srv/www/htdocs/index.html` 文件的权限改为 `644` 并退出终端。切换回 `ty7`，刷新 Web 页面以确保 Apache 守护进程可以读取，然后注销 GNOME 桌面。

## 使用 Apache 托管网页

确保系统中已安装并启动了 Web 服务器。接下来，以 `root` 用户身份登录 `ty1`，查看 `/etc/apache2/mod_user.conf` 文件的内容（该文件由 `/etc/apache2/httpd.conf` 引用）。特别注意指示默认配置允许个人主页的注释。在每个用户的家目录下，默认使用哪个目录来存放个人主页？

以 `geeko` 身份打开 GNOME 桌面并打开一个 GNOME 终端。在你的家目录下创建一个 `public_html` 目录。在该目录内，使用文本编辑器创建一个包含以下行的 `index.html` 文件，并观察更改后的变化：

```html
<html>
<h1>My sample Web page!</h1>
</body>
</html>
```

接下来，打开你的 Web 浏览器并导航到 URL `http://127.0.0.1/~geeko/` 测试你的个人网页。

## 使用 Telnet 测试 Postfix

SMTP 是一种基于命令的协议，用于在互联网上中继电子邮件。因此，使用 telnet 测试其功能很容易。

以 `root` 用户身份登录 `ty1`，输入 `telnet localhost 25` 与监听在 TCP 25 端口上的网络服务进行交互。你能看出你正在与 Postfix 交互吗？接下来，执行以下操作：

- 输入 `EHLO` 以验证 SMTP 支持
- 输入 `HELO` 以验证 SMTP 支持
- 输入 `mail from: billy.gates@microsoft.com` 创建一封来自 Bill Gates 的新邮件
- 输入 `rcpt to:` 指定本地系统上的 `geeko` 用户为收件人
- 输入 `data`
- 输入 `Hello World`
- 输入 `to:` 完成邮件
- 输入 `quit` 退出 telnet 会话

完成后，切换到 `geeko` 并使用 `mail` 命令检查 `geeko` 的邮件。你的消息在里面吗？完成后，删除该消息并退出邮件实用程序。

## 配置基础 Samba 域控制器

利用互联网研究将 Samba 服务器作为 Windows NT 域控制器使用的所需步骤。接下来，以 root 用户身份登录 `tty1`，通过编辑 `/etc/samba/smb.conf` 文件将你的 Samba 服务配置为域控制器。该文件所需的最小行如下：

```
[global]
domain logins = yes
security = user
encrypt passwords = yes
wins support = yes
netbios name = (your NetBIOS name)
workgroup = (put your domain name here)

[netlog]
path=/netlogon (使用权限 777 创建此目录)
public = no
writable = no
locking = no
```

接下来，在系统中创建一个新用户 (`passwd -m tester`)，并在 samba 数据库中为该用户提供加密密码 (`smbspasswd tester`)。然后，通过为加入你 Linux 计算机的每个 Windows 计算机向 `/etc/passwd` 和 `/etc/shadow` 添加包含计算机名后跟 `$` 字符的行，如下所示：

```
/etc/passwd 示例行:
clientcomputer name$:x:5000:5000::/dev/null:/bin/false
/etc/shadow 示例行:
clientcomputer name$*:6445::::
```

完成后，通过将 Windows 客户端加入域测试域登录来验证你的配置。完成后注销 Samba 上的 `tty1`。

# 第 8 节 理解与安全相关的工具

在本节中，你将学习如何使用各种工具执行安全相关的管理任务，并学习如何为 SLES 11 配置远程访问解决方案。

# 目标

1. 管理并保护 Linux 用户环境
2. 使用 OpenSSH 提供安全的远程访问
3. 使用 PAM 配置用户认证
4. 确保文件完整性
5. 使用安全相关的工具
6. 理解 SELinux

# 目标 1

## 管理并保护 Linux 用户环境

作为 SLES 11 的系统管理员，你需要了解如何管理和保护 Linux 上的用户环境。在本目标中，将涉及以下主题：

- 管理 root 的使用
- 使用 sudo 委托管理任务
- 为新用户账户设置默认值
- 使用 OpenSSH 提供安全的远程访问
- 使用 PAM 配置用户认证
- 确保文件完整性
- 使用安全相关的工具
- 理解 SELinux

## 管理 root 的使用

（注：此处后续原文存在大量重复，已按逻辑精简处理）

每个命令的密码（与 `su -c` 命令一样），因为它在执行 `sudo` 后会被缓存几分钟。

```
geekoodal: ~ sudo /sbin/shutdown -h now
```

我们相信你已经接受了本地系统管理员的常规教导。这通常归结为以下三点：

- #1) 尊重他人的隐私。
- #2) 在输入之前先思考。
- #3) 能力越大，责任越大。

root 密码：

你可以更改 `sudo` 的配置，使其要求输入用户密码而不是 root 密码。要实现这一点，使用 `sudo` 命令在 `/etc/sudoers` 文件中的两行前面加上注释符号（`#`）：

```
# 在默认（未配置）的配置中，sudo 会提问
# 密码。这种方法使用普通用户账户来 
# 管理新安装的系统。在配置 
# sudo 时，请删除以下两行：
Defaults target # 以及目标用户的密码，即 root
ALL ALL=(ALL) # 警告！仅与 'Defaults' 配合使用
# targets=!'
```

使用 `visudo`，你可以通过配置 `/etc/sudoers` 文件来指定用户可以或不可以输入的命令。以下是配置文件中条目的通用语法：

```
user/group host = command1, command2 ...
```

例如

`geeko ALL = /sbin/shutdown`

在此示例中，用户 `geeko` 能够在所有计算机（`ALL`）上以 root 权限执行 `/sbin/shutdown` 命令。通过在 `/etc/sudoers` 中指定特定的计算机，允许你将相同的文件复制到不同的计算机上，而无需在所有涉及的计算机上授予相同的权限。

`/etc/sudoers` 文件还可以通过别名（aliases）进行配置，定义谁可以以 root 身份执行什么。使用了以下别名：

- `User_Alias`. 允许运行命令的用户。
- `Cmnd_Alias`. 允许用户运行的命令。
- `Host_Alias`. 允许运行命令的主机。
- `Runas_Alias`. 可以运行命令的用户名。

你需要使用 `User_Alias` 来定义一个包含用户账户（用逗号分隔）的别名，必须运行它们以允许命令：

```
User_Alias alias = users
```

例如，要创建一个名为 `POWERUSERS` 的别名，包含 `tux` 和 `geeko` 用户账户，你会在 `/etc/sudoers` 文件中输入以下内容：

```
User_Alias POWERUSERS = tux, geeko
```

所有别名名称必须大写字母开头。

你需要使用 `Cmnd_Alias` 来定义一个包含命令（使用完整路径）的别名，这些命令是 `User_Alias` 中定义的用户的用户的。你可以用逗号分隔多个命令。

例如，如果你是开发者，需要经常杀死进程，你可以定义一个名为 `KPROCS` 的别名，其中包含 `kill` 和 `killall` 命令，如下所示：

```
Cmnd_Alias KPROCS = /bin/kill, /usr/bin/killall
```
