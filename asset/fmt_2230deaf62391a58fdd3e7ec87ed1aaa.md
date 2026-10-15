
在 Debian 和 Ubuntu 中，使用 `update-rc.d` 命令关闭独立服务器，并使用 `invoke-rc.d` 命令交互式地启动或停止服务器。要获取可用服务的线索，输入 `ls /etc/init.d`，并查看所有用于开启或关闭服务的脚本文件。当你想要开启或关闭服务时，必须使用这些文件名。例如，要关闭 Samba 服务，输入 `update-rc.d -f samba`。如果服务已经在运行，输入 `invoke-rc.d stop` 来停止该服务。你可以以类似的方式使用 `invoke-rc.d` 命令停止任何服务。

在 Fedora 和 SUSE 中，你可以使用 `systemctl` 命令开启和关闭独立服务器。你可以通过输入 `ls /etc/init.d` 获取服务脚本的名称。然后你可以通过输入 `sudo systemctl stop smb` 来关闭服务（如 Samba）。如果服务已经在运行，输入 `/etc/init.d/smb stop` 来停止该服务。你可以运行 `/etc/init.d` 目录下的脚本并带有 `stop` 参数以类似的方式停止任何服务。

## 配置互联网服务器

除了 Web 和邮件服务器等独立服务器外，`inetd` 和 `xinetd` 服务器必须单独配置。这些服务器是*互联网超级服务器*，因为它们可以根据需要启动其他服务器。输入 `ps ax | grep inetd` 查看运行的是哪个互联网服务器——`inetd` 还是 `xinetd`。

Debian 和 Ubuntu 使用 `inetd`，而 Fedora 和 SUSE 使用 `xinetd`。要禁用某个服务，可以通过在 `inetd.conf` 文件中在该行开头添加井号（#）来注释掉。保存文件后，输入 `inetd restart` 来重启 `inetd` 服务。

配置 `xinetd` 服务器要复杂一些。`xinetd` 服务器在启动时读取名为 `xinetd.conf` 的文件。`/xinetd.d` 目录下的配置文件告诉 `xinetd` 监听哪些端口。输入 `ls /xinetd.d` 查看 `/xinetd.d` 目录中的文件。每个文件代表一个 `xinetd` 可以启动的服务。要关闭这些服务中的任何一个，请编辑文件并添加 `disable = yes` 行。对 `xinetd` 配置文件进行任何更改后，必须重启 `xinetd` 服务器；否则更改不会生效。重启 `xinetd` 服务器，输入 `/etc/init.d/xinetd`。此命令会停止并重新启动 `xinetd`。当服务器重启时，它会读取配置文件，更改就会生效。

## 配置 TCP wrapper

`inetd` 和 `xinetd` 的一项常见特性是使用 TCP wrapper 来启动各种服务。*TCP wrapper* 是一种为互联网服务提供访问控制的代码块，类似于保护包。TCP wrapper 可以启动 FTP 和 Telnet 等服务，但在启动服务之前，它会查询 `/etc/hosts.allow` 文件以查看请求服务的主机是否允许使用该服务。如果文件中没有关于该主机的记录，TCP wrapper 将检查 `/etc/hosts.deny` 文件查看是否拒绝该服务。如果两个文件都是空的，TCP wrapper 将允许访问请求的服务。

以下是加固 `inetd` 或 `xinetd` 配置启动的服务访问的步骤：

1. **使用文本编辑器编辑 `/etc/hosts.deny` 文件，在该文件中添加行：**

   `ALL:ALL`

   此设置拒绝所有主机访问系统上的任何互联网服务。

2. **编辑 `/etc/hosts.allow` 文件，并在其中添加可以访问系统的主机名称。**

   要仅允许来自 192.168.1.0 网络和本地主机（IP 地址 127.0.0.1）访问服务，请在 `/etc/hosts.allow` 文件中放置以下行：

   `ALL: 192.168.1.0/255.255.255.0 127.0.0.1`

3. **如果你想允许特定的远程主机访问特定的服务，请在 `/etc/hosts.allow` 文件中使用以下格式：**

   *server_program_name*: *hosts*

   在这里，*server_program_name* 是服务器程序的名称，*hosts* 是可以访问该服务的逗号分隔列表。

![](img/3e16ea99a8df672d45599724c19769ac_334_0.png)[](img/3e16ea99a8df672d45599724c19769ac_334_0.png)

OpenSSH 软件在 Linux 安装期间会进行安装。表 2-2 列出了 OpenSSH 软件的主要组件。

OpenSSH 使用公钥加密，发送者和接收者都拥有一对密钥：公钥和私钥。公钥免费分发，每个伙伴都知道对方的公钥。发送者使用接收者的公钥加密数据。只有接收者的私钥才能解密这些数据。

要使用 OpenSSH，请启动 `sshd` 服务，然后生成主机密钥。操作方法如下：

- 如果你想在主机上支持基于 SSH 的远程登录，请在你的系统上启动 `sshd` 服务。输入 `ps ax | grep sshd` 来查看服务器是否已经在运行。如果没有运行，请以 `root` 身份登录并开启 SSH 服务。

- 使用以下命令生成主机密钥：

  `ssh-keygen -d -f /etc/ssh/ssh_host_key -N ''`

表 2-2：OpenSSH 软件组件

| 组件 | 描述 |
| :--- | :--- |
| `/usr/sbin/sshd` | 如果你想让远程系统的用户使用 `ssh` 客户端安全登录，此 SSH 守护进程必须在主机上运行。当来自 `ssh` 客户端的连接到达时，`sshd` 使用公钥加密进行身份验证，并与 `ssh` 客户端建立加密通信链路。 |
| `/usr/bin/ssh` | 用户可以运行此 SSH 客户端登录到运行 `sshd` 的主机。用户还可以使用 `ssh` 在另一个主机上执行命令。 |
| `/usr/bin/slogin` | 该组件是指向 `/usr/bin/ssh` 的符号链接。 |
| `/usr/bin/scp` | 该安全拷贝程序的工作方式类似于 `rcp`，但更安全。`scp` 程序使用 `ssh` 进行数据传输，并提供与 `ssh` 相同的认证和安全性。 |
| `/usr/bin/ssh-keygen` | 你使用此程序生成 OpenSSH 中公钥加密所需的公私钥密钥对。`ssh-keygen` 程序可以为 RSA 和 DSA（数字签名算法）认证生成密钥对。（RSA 源于 RSA 算法开发者 Ron Rivest、Adi Shamir 和 Leonard Adleman 姓名的首字母。） |
| `/etc/ssh/sshd_config` | 此 `sshd` 服务的配置文件指定了 `sshd` 的许多参数，包括监听的端口、使用的协议以及其他文件的位置。（SSH 协议有两个版本，即 SSH1 和 SSH2，OpenSSH 都支持这两个版本。） |
| `/etc/ssh/ssh_config` | 此配置文件是用于 `ssh` 客户端的。每个用户还可以在其家目录的 `.ssh` 子目录下拥有名为 `config` 的 `ssh` 配置文件。 |

![](img/3e16ea99a8df672d45599724c19769ac_335_0.png)

![](img/3e16ea99a8df672d45599724c19769ac_335_1.png)

`-d` 导致 `ssh-keygen` 程序生成 SSH2 协议使用的 DSA 密钥。如果你看到消息文件 `/etc/ssh/ssh_host_key` 已存在，说明密钥对是在 Linux 安装期间生成的。你可以直接使用现有文件，而无需重新生成密钥。

想要使用 SSH 登录的用户可以使用如下 `ssh` 命令：

`ssh 192.168.0.4 -l kdulaney`

其中 192.168.0.4 是另一个 Linux 系统的 IP 地址。然后 SSH 显示一条消息：

```
The authenticity of host '192.168.0.4 (192.168.0.4)' can't be established.
RSA key fingerprint is 7b:79:f2:dd:8c:54:00:a6:94:ec:fa:8e:7f:c9:ad:66.
Are you sure you want to continue connecting (yes/no)?
```

输入 `yes` 并按回车键。SSH 将该主机添加到其已知主机列表中，并提示输入另一个 Linux 系统的密码：

```
kdulaney@192.168.0.4's password:
```

输入密码后，你便与该系统建立了安全的登录会话。你也可以使用以下等效命令登录此账户：

`ssh kdulaney@192.168.0.4`
