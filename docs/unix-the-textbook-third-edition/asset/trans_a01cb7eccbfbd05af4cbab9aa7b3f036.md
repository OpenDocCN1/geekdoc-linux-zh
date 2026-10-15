

+   2. SSH 认证协议：验证客户端机器上用户登录角色的有效性

+   3. SSH 通道协议：处理远程 shell 会话、端口转发或 X11 转发的加密通道和逻辑连接状态

以下小节假定 ssh 服务已在不仅你的客户端本地计算机上，而且在远程服务器主机上默认安装并已启动。我们不提供如何获取或安装 ssh 客户端或服务器程序的细节，但我们提供了如何对 sshd 守护进程进行初步配置以及如何在 PC-BSD 和 Solaris 上启动/重启守护进程的说明。

默认情况下，sshd 在我们的 PC-BSD 和 Solaris 系统上均已启用并启动，要使用本节所示的 ssh 命令，我们只需让本地客户端机器和远程服务器机器上的守护进程最初交换加密密钥，如以下示例会话所示。

有关 ssh、scp 和 sftp 命令的更完整描述，请参阅这些命令的手册页。

## 11.8.10.1 ssh 的初步配置以及如何启动/重启 sshd 守护进程

以下小节给出了 PC-BSD 和 Solaris 上 ssh 的初步配置信息，并展示了如果守护进程未在默认情况下启动，或因某种原因已停止，如何启动或重启守护进程。

+   1. PC-BSD 上 ssh 的配置

如果你不想在使用 ssh 时输入密码，并且使用 RSA 或 DSA 密钥进行身份验证，可以在运行其他应用程序之前运行 ssh-agent 命令。X 用户通常通过他们的 .xsession 或 .xinitrc 文件来执行此操作。有关详细信息，请参阅 ssh-agent 的手册页。

+   a. 使用 ssh-keygen 命令生成密钥对并将其放置在你的 $HOME/.ssh 目录中。你的公钥是 $HOME/.ssh/id_dsa.pub 或 $HOME/.ssh/id_rsa.pub，具体取决于你分别使用 DSA 或 RSA 进行身份验证。

+   b. 将你的公钥发送给为你设置提交者权限的人员，以便将其放入 /etc/ssh-keys/ 中的你的登录项中。默认情况下，在我们的 PC-BSD 和 Solaris 机器上，这些密钥已自动生成并存储。

+   2. 在 PC-BSD 上启动或重启 sshd

要确定 sshd 是否正在运行，或重启服务，运行以下命令序列：

```
% /etc/rc.d/sshd start
sshd already running? (pid=1523)
```

```
% /etc/rc.d/sshd restart
Stopping sshd.
Waiting for PIDS: 1523
Starting sshd.
%
```

启动 ssh 守护进程的另一种方法是，通过在 /etc/rc.conf 文件中添加以下行，在启动时自动启动 sshd 服务器：

```
sshd_enable="YES"
```

现在通过在命令行输入以下内容启动 sshd 服务器：

```
% /etc/rc.d/sshd start
```

+   1. Solaris 上 ssh 的配置

在本地客户端机器上，检查文件 /etc/ssh_config 和 /etc/ssh/sshd_config，分别是 ssh 的客户端和服务器端配置文件。这些文件中未被注释掉的行（即第一个字符不是 #），是你的 ssh 会话的配置设置，分别作为客户端和服务器。

+   2. 在 Solaris 上启动或重启 sshd

要启动远程服务器上的 sshd，如果它尚未运行，运行以下命令：

```
$ svcadm enable svc:/network/ssh:default
```

要重启远程服务器上的 sshd，输入以下内容：

```
$ svcadm restart svc:/network/ssh:default
```

## 11.8.10.2 ssh 命令

ssh 命令允许你执行基本上与 telnet、rlogin 和 rsh 命令相同的任务，但方式更安全。如果你机器名在远程主机上的 /etc/host.equiv 或 /etc/shosts.equiv 文件中找到，并且你的登录名在你的机器和远程机器上相同，则允许你登录到远程主机或在其上执行命令。如果你登录名在本地和远程主机上不同，并且你的本地机器名和其上的登录名包含在 ~/.rhosts 或 ~/.shosts 文件中，也允许你登录到远程主机。ssh 还使用额外的安全功能，包括公钥加密，在允许用户登录到远程机器之前对用户及其主机进行身份验证。我们仅描述 ssh 命令中一些相当基本的功能，这些功能用于远程登录、远程执行命令以及在客户端和服务器机器之间传输文件。以下是 ssh 命令的简要描述：

