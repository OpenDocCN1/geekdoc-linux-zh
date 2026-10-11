
## 禁用根用户登录

如前所述，确保不使用 root 账户登录服务器非常重要。因此，你需要在服务器配置文件中禁用 root 账户的 SSH 端口访问权限。在此之前，让我们看一个示例，创建一个具有 sudo 权限的用户，这样你可以使用 SSH 端口访问服务器并执行必要的任务。当你登录服务器时，如果需要，可以从该用户切换到 root 账户。首先，让我们创建一个新用户。执行以下命令：`useradd user1`。现在，你可以使用以下命令为该用户账户设置密码：`passwd user1`。既然你已经在服务器上创建了一个用户，你可以使用以下行授予它 sudo 权限：`echo 'user1 ALL=(ALL) ALL' >> /etc/sudoers`。然后，你需要使用 SSH 通过新的用户账户访问服务器。这是确保你能够登录服务器的一种方法。

现在，我们需要禁用 root 账户对 SSH 端口的访问权限。这意味着没有任何用户可以使用 SSH 通过 root 账户登录服务器。你需要打开配置文件 `nano /etc/ssh/sshd_conf` 来执行此操作。然后，你需要将文件中的 `PermitRootLogin` 行更新为 no。保存该文件并关闭它。重启后，你会看到设置已更新。

在退出服务器之前，你应该测试是否可以使用之前创建的用户 ID 通过 SSH 登录服务器。为此，你可以在终端中打开另一个实例，并使用 SSH 登录服务器。如果一切正常，你可以以 root 用户身份退出服务器。

## 更改端口

你还可以更改 SSH 用于访问网络的默认端口。你可以添加一层安全性以确保服务器安全。为此，你需要更新 `/etc/ssh/sshd_config` 文件。在该文件中，你需要将端口号 22 替换为你想要使用的端口号。保存文件后，你可以重启服务器。为此，你需要使用以下命令：`service sshd restart`。然后，你可以使用以下命令通过更新的端口号登录服务器：`ssh username@IP -p 1110`。

## 禁用快捷键

当你按下快捷键 Ctrl+Alt+Delete 时，服务器会自动重启。因此，最好禁用此快捷键，以防止有人误操作导致系统重启。该设置在名为 /etc/init/control-alt-delete.conf 的配置文件中。你只需在配置文件中注释掉 ‘#start on control-alt-delete’ 这一行即可。

## 无密码登录

你可以使用 SSH 登录服务器。如果在文件中配置好详细信息，就可以免去密码。你唯一需要做的就是通过生成 SSH 密钥来进入服务器。确保用户只能从他生成 SSH 密钥的那台机器进入服务器非常重要。让我们看看如何生成 SSH 密钥以访问服务器：`ssh-keygen -t rsa`。生成密钥后，你可以使用以下命令将密钥添加到你要访问的服务器：`cat ~/.ssh/id_rsa.pub`。

如果服务器上有多个用户，你可以为每个用户分配一个 SSH 密钥，以便他们从各自的系统访问服务器。你可以使用以下命令执行此操作：

```
cd /home/user1
ls -ll
```

出于安全原因，为了确保只有部分用户拥有 SSH 密钥的访问权限，你可以在 SSH 目录中配置用户列表。你可以使用以下命令执行此操作：

```
mkdir .ssh
cd /home/admin/.ssh
vim authorized_keys
```

在更改所有者之前，你还可以创建一个公共 SSH 密钥并将其添加到配置文件中。为此，运行以下命令：`chown user1 authorized_keys`。

如果你不想使用 SSH 密钥，你需要禁用 SSH 登录。为此，你需要使用以下命令行编辑配置文件：

```
Edit /etc/ssh/sshd_config
PasswordAuthentication no
PermitRootLogin no
```

完成此操作后，你可以使用命令 `ssh user-name@serverIP -p(port Number)` 确保只有授权用户才能进入服务器。

# 使用 fail2ban

如果你想使用应用程序查看服务器频繁遭受攻击的来源，可以使用 fail2ban。该应用还会告诉你服务器上发生的任何自动攻击。它还针对防火墙工作，并在发现服务器存在问题时更新它。Fail2ban 会更改防火墙配置，并推送该配置以封锁 IP 地址，封锁时间长短或永久封锁，具体取决于攻击类型。

如果你想在系统上安装 fail2ban，请运行以下命令：`sudo apt install fail2ban -y`。然后，你应该使用以下命令复制系统中找到的配置文件：`sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local`。如果你没有 jail.local 文件，你需要创建它，然后将 jail.conf 文件的内容复制到 jail.local 文件中。你可以使用以下命令：

```
cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
Edit /etc/fail2ban/jail.local file
```

现在你需要对文件进行必要的更改：

```
[sshd]
enabled = true
port = ssh (如果默认端口已更改，请提供端口号)
protocol = tcp
filter = sshd
logpath = /var/log/secure
maxretry = 3 (主机被禁止连接的最大尝试次数)
findtime = 600
bantime = 600
```

注意：`findtime = 600`（你可以使用此参数设置应用程序在几秒钟内寻找重复的错误身份验证时关注的窗口）和 `bantime = 600`（主机被禁止连接的时间持续时间 - 以秒为单位）。

在重启应用程序之前，你需要通过将 `bantime` 参数设置为 -1 来封锁 IP。完成此操作后，你可以使用以下命令重启应用程序：`sudo service fail2ban restart`。

就这么简单。该应用程序将继续检查系统上的日志文件并查找任何攻击。该应用程序还将拥有一组 IP 地址列表，它将从中阻止访问服务器。如果你想查看此列表，请使用以下命令：`sudo fail2ban-client status sshd`。

你还可以使用 fail2ban 来记录 SSH 登录。你需要确保定期更新该应用程序，以便你可以通过 SSH 访问服务器。

# 创建新的特权账户

现在你应该创建一个用户账户。请记住，不要使用 root 账户登录服务器。你也可以创建自己的账户。如前所述，你应该创建一个 sudo 账户并用于访问服务器。现在，使用 sudo 账户登录服务器。我们已经查看了如何创建新账户并赋予其 sudo 权限访问。

# 上传 SSH 密钥

创建新服务器时，你需要 SSH 密钥来访问服务器。如果你想使用预生成的 SSH 密钥，或者创建新密钥。为此，运行以下命令：`ssh-copy-id <username>@<ip_address>`。现在，使用 SSH 密钥登录新服务器时，你可以避免输入密码。

# 保护 SSH

完成此操作后，你需要进行以下更改：

- 第一步：移除 SSH 协议的密码认证
- 第二步：不允许用户远程访问 root 账户
- 第三步：你还需限制对 IPv6 和 IPv4 的访问

为此，你需要修改 SSH 配置文件。打开文件后，你会找到以下代码行：

```
PasswordAuthentication yes
PermitRootLogin yes
```

你需要更改它，使这些行看起来如下：

```
PasswordAuthentication no
PermitRootLogin no
```

然后你需要限制 SSH 服务使用的 IP 类型 – 要么 IPv4 要么 IPv6。你可以通过修改配置文件中的 AddressFamily 选项来实现。如果你想更改为仅使用 IPv4，进行以下更改：

```
AddressFamily inet
```

只有当你重启 SSH 服务时，你的更改才会在服务器上生效。请记住，在重启 SSH 服务器之前，应该有两个活动的服务器连接。当你有一个额外的连接时，如果重启没有按计划进行，你可以修复可能出现的任何问题。如果你使用 Ubuntu，可以运行以下命令：`sudo service sshd restart`。如果你使用具有 Systemd 配置的任意 Linux 发行版，请运行以下命令：`sudo systemctl restart sshd`。

## 创建防火墙

在上一章中，我们看了如何在系统上安装、启用和配置防火墙，使其仅允许你允许的网络流量访问服务器。如果你需要，也可以在服务器上使用简易防火墙，具体取决于你的编码能力。如果你不能编码，使用简易防火墙。你可以使用以下命令在系统上安装它：`sudo apt install ufw`。

简易防火墙默认拒绝任何传入连接，并允许所有出站流量。这意味着你系统或服务器上的所有工具和应用都可以连接到互联网，但如果任何外部事物试图连接服务器，它将不允许。你需要使用以下命令确保你可以访问服务器上的 HTTPS、HTTP 和 SSH 协议：

```
$ sudo ufw allow ssh
$ sudo ufw allow http
$ sudo ufw allow https
```

