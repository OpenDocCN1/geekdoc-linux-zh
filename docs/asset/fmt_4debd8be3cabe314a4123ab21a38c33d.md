
```
root@ubuntu:~# apt-cache show firefox
Package: firefox
Architecture: amd64
Version: 1:1snap1-0ubuntu2
Priority: optional
Section: web
Origin: Ubuntu
Maintainer: Ubuntu Mozilla Team <ubuntu-mozillateam@lists.ubuntu.com>
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 255
Provides: gnome-www-browser, iceweasel, www-browser, x-www-browser
Pre-Depends: debconf (>= 0.5) | debconf-2.0
Depends: firefox-dbgsym (<< 1:1snap1), firefox-dev (<< 1:1snap1), firefox-geckodriver (<< 1:1snap1), firefox-mozsymbols (<< 1:1snap1)
Replaces: firefox-dbgsym (<< 1:1snap1), firefox-dev (<< 1:1snap1), firefox-geckodriver (<< 1:1snap1), firefox-mozsymbols (<< 1:1snap1)
Filename: pool/main/f/firefox/firefox_1snap1-0ubuntu2_amd64.deb
Size: 72292
MD5sum: 4cfb8522595425213edbd344d0dfa6b6
SHA1: ec27ebdf84c2d918ad669cfc94f1163b5937c4dfb66
SHA256: d6ccd2ef5cc7291364ab49bb9e57d68a4ac993488ae561bb67ed31dd6b17659cc
SHA512: 35cb18af4766668b7735713277786946fe2f90abba2f5cabd55f73124de672645a07ac9a6e12ca66677d892f07356f3a90d8c521b5b657b394949b146601f2a
Description-en: Transitional package - firefox -> firefox snap
This is a transitional dummy package. It can safely be removed.
.
firefox is now replaced by the firefox snap.
Description-md5: 28593f0124b124447f7e30b88c6717ba4
Translators:
The Ubuntu l10n Team <ubuntu-devel@lists.
```

![](img/863afa537de4eed7deb11978bfbfa90e_140_0.png)

- 搜索模式为`^ansible`的包（名称或描述以单词`ansible`开头），如图 4.52 所示：

```
root@ubuntu:~# apt-cache search ^ansible
ansible - Configuration management, deployment, and task execution system
ansible-core - Configuration management, deployment, and task execution system
ansible-lint - lint tool for Ansible playbooks
ansible-mitogen - Fast connection strategy for Ansible
shade-inventory - Ansible inventory script for OpenStack clouds
```

![](img/863afa537de4eed7deb11978bfbfa90e_140_1.png)

- 显示包`python3-urllib3`的依赖项，如图 4.53 所示：

```
root@ubuntu:~# apt-cache depends python3-urllib3
python3-urllib3
  Depends: <python3:any>
    python3
  Depends: python3-six
  Recommends: ca-certificates
  Suggests: python3-cryptography
  Suggests: python3-idna
  Suggests: python3-openssl
  Suggests: python3-socks
```

![](img/863afa537de4eed7deb11978bfbfa90e_141_0.png)

命令`apt`是命令`apt-get`和`apt-cache`的前端。该命令可用的操作如表 4.25 所示：

| 操作 | 等效命令 | 操作 | 等效命令 |
| :--- | :--- | :--- | :--- |
| `update` | `apt-get update` | `reinstall` | `apt-get install` |
| `upgrade` | `apt-get upgrade` | `remove` | `apt-get remove` |
| `full-upgrade` | `apt-get dist-upgrade` | `purge` | `apt-get purge` |
| `install` | `apt-get install` | `autoremove` | `apt-get autoremove` |
| `search` | `apt-cache search` | `show` | `apt-cache show` |

![](img/863afa537de4eed7deb11978bfbfa90e_141_1.png)

## 服务介绍

Linux 服务（或有时称为`daemon`）是在后台运行以执行某些任务或等待某些事件的应用程序或一组应用程序。有些服务可以执行某些应用程序，当它们完成时，服务就会停止。例如，配置系统网络的服务就是这种情况。其他服务则持续运行，等待提供某些资源；例如，`SSH`服务正等待用户连接并提供登录服务器的可能性。

大多数 Linux 发行版使用名为`systemd`的服务管理器，它是历史悠久且广受欢迎的`SysV init`守护进程的替代品。当 Linux 发行版启动时，执行的第一项进程是`systemd`，它将负责启动系统中已启用并在启动时启用的其他服务。

`systemd`是一整套应用程序，旨在统一不同 Linux 发行版中的服务配置和行为。管理服务的主要命令是`systemctl`，常用操作描述如表 4.26 所示：

| 操作 | 描述 |
| :--- | :--- |
| `list-units` | 列出系统中可用的`unit`（服务、挂载点、设备和套接字）。 |
| `status` | 检查指定`unit`的状态。 |
| `show` | 显示指定`unit`的属性。 |
| `start` | 启动指定的`unit`。 |
| `stop` | 停止指定的`unit`。 |
| `reload` | 指定的`unit`将重新加载配置。 |
| `restart` | 停止并启动指定的`unit`。 |
| `enable` | 启用指定的`unit`，使其在系统启动时启动。 |
| `disable` | 禁用指定的`unit`，使其在系统启动时不启动。 |

表 4.26: `systemctl`的操作

在下述图示中，列出了命令`systemctl`的一些操作示例：

- 检查名为`cron`的服务的状态，如图 4.54 所示：

![](img/863afa537de4eed7deb11978bfbfa90e_142_0.png)

图 4.54: 关于某个服务状态的输出示例。

- 禁用当前已启用的服务，如图 4.55 所示：

![](img/863afa537de4eed7deb11978bfbfa90e_142_1.png)

图 4.55: 禁用服务的输出示例。

- 启用一个已禁用的服务，如图 4.56 所示：
