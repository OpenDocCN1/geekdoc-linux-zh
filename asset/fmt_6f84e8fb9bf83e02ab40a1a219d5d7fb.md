
```bash
# yum list installed | grep openssh
openssh.x86_64 7.9p1-5.fc30 @anaconda
openssh-clients.x86_64 7.9p1-5.fc30 @anaconda
openssh-server.x86_64 7.9p1-5.fc30 @anaconda
```

在 Ubuntu 上，只安装了 `opens-clients` 软件包。它包含了 `openssh` 包的功能。如果你需要安装服务器，请使用 `sudo apt-get install opens-server` 命令。

```bash
$ sudo dpkg --list | grep openssh
openssh-client/bionic-updates,bionic-security,now 1:7.6p1-4ubuntu.3 amd64
[installed]
secure shell (SSH) client, for secure access to remote machines
openssh-client-ssh/bionic/1:7.5p1-10 amd64
secure shell (SSH) client for legacy SSH protocol
openssh-sftp/bionic-updates,bionic-security,now 1:7.6p1-4ubuntu.3 amd64
[installed]
secure shell (SSH) sftp server module, for SFTP access from remote machines
$ sudo apt-get install openssh-server
```

## 启动 `openssh-server` 服务

某些附带了 `openssh-server` 软件包的 Linux 系统有时没有配置为自动启动。在不同的发行版上，管理 Linux 系统（见第 15 章“启动和停止服务”）可能非常不同。表 13.1 显示了为了确保 ssh 服务守护进程 `sshd` 在 Linux 系统上运行而使用的命令。

### 表 13.1 确定 `sshd` 状态的命令
| 发行版 | 确定 `sshd` 状态的命令 |
|---|---|
| RHEL 6 | `chkconfig --list sshd` |
| Fedora 和 RHEL 7 或更高版本 | `systemctl status sshd.service` |
| Ubuntu | `systemctl status sshd.service` |

如果 `sshd` 当前未运行，可以通过发布表 13.2 列出的命令之一来启动它。这些命令需要 root 权限才能工作。

### 表 13.2 启动 `sshd` 的命令
| 发行版 | 启动 `sshd` 的命令 |
|---|---|
| RHEL 6 | `service sshd start` |
| Fedora 和 RHEL 7 或更高版本 | `systemctl start sshd.service` |
| Ubuntu | `systemctl start ssh.service` |

表 13.2 中的命令仅启动 `ssh` 或 `sshd` 服务。它们并没有配置为在启动机时自动启动。要让服务器服务设置为自动启动，你需要使用 root 权限使用表 13.3 中的命令之一。

### 表 13.3 开机启动 `sshd` 的命令
| 发行版 | 开机启动 `sshd` 的命令 |
|---|---|
| RHEL 6 | `chkconfig sshd on` |
| Fedora 和 RHEL 7 或更高版本 | `systemctl enable sshd.service` |
| Ubuntu | `systemctl enable ssh.service` |

当在 Ubuntu 上安装 `openssh-server` 时，`sshd` 守护进程被配置为开机时自动启动。因此，你可能不需要为你的服务器运行表 13.3 中的命令。修改你的防火墙设置以允许 `openssh-client` 访问端口 22（防火墙将见第 2 章“在网络上保护 Linux”）。在服务运行且防火墙配置恰当后，你应该能够使用 `ssh` 客户端通过 `ssh` 服务器访问你的系统。任何关于 `ssh` 的进一步配置，你应该可以使用 `ssh` 客户端通过 `ssh` 服务器访问你的系统。

修改你的防火墙设置以允许 `openssh-client` 访问端口 22（防火墙将见第 2 章“在网络上保护 Linux”）。在服务运行且防火墙配置恰当后，你应该能够使用 `ssh` 客户端通过 `ssh` 服务器访问你的系统。任何关于 `ssh` 的进一步配置，`sshd` 守护进程在 `/etc/ssh/config`。
