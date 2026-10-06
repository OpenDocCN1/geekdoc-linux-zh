
- 9. 在命令提示符处输入 `docker ps` 并按回车。注意退出 Busybox shell 后，你的容器不再运行。接着，输入 `docker ps -a` 并按回车。注意基于 Busybox 镜像的两个容器。
- 10. 在命令提示符处输入 `docker container prune` 并按回车。提示时按 Y 移除所有容器。文件系统释放了多少空间？接着，输入 `ps -a` 并按回车。列出了容器吗？
- 11. 在命令提示符处输入 `docker search apache | less` 并按 `q` 返回命令提示符。Apache HTTP Server Project 镜名为 `httpd`，按 `q` 返回提示符。
- 12. 在命令提示符处输入 `docker pull httpd` 并按回车，从 Docker Hub 下载最新版本的 httpd 容器镜像。
- 13. 在命令提示符处输入 `docker images` 并按回车。列出了你的 httpd 容器吗？

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

14. 在命令提示符处，输入 `docker run -d -p 50001:80 --name site1 httpd` 并按回车，运行一个名为 site1 的 http 镜像的后台副本，并将 Apache Web 服务器的 80 端口映射到 Ubuntu Linux 系统内的 50001 端口。
- 15. 在命令提示符处，输入 `docker run -d -p 50002:80 --name site2 httpd` 并按回车，运行一个名为 site2 的 http 镜像的后台副本，并将 Apache Web 服务器的 80 端口映射到 Ubuntu Linux 系统内的 50002 端口。
- 16. 在命令提示符处，输入 `docker ps` 并按回车。注意两个容器都在运行。每个容器的 80 端口是否映射到了操作系统中正确的端口？输出中的哪个 IP 地址标识了操作系统？
- 17. 在命令提示符处，输入 `docker exec -it site1 sh` 并按回车，在 site1 容器内启动一个 shell。
- 18. 在 site1 shell 提示符下，输入 `pwd` 并按回车。注意你处于 `/usr/local/apache2` 目录。接着，输入 `ls -F` 并按回车查看文件列表。
- 19. 在 site1 shell 提示符下，输入 `cd hdocs` 并按回车进入容器内的 Apache 根目录。接着，输入 `cat index.html` 并按回车查看网页内容。
- 20. 在 site1 shell 提示符下，输入 `echo "<h1>Site 1 works!</h1></html>" > index.html` 并按回车，向 Apache 文档根目录下的 index.html 文件写入简单的网页。接着，输入 `exit` 并按回车退出 site1 容器内的 shell。
- 21. 在命令提示符处，输入 `docker exec -it site2 sh` 并按回车，在你的 site2 容器内启动一个 shell。
- 22. 在 site2 shell 提示符下，输入 `cd hdocs` 并按回车进入容器内的 Apache 文档根目录。接着，输入 `echo "<h1>Site 2 works!</h1></html>" > index.html` 并按回车，向 Apache 文档根目录下的 index.html 文件写入简单的网页。最后，输入 `exit` 并按回车。

## 项目 13-12

**预计耗时：** 60 分钟

**目标：** 配置 Kubernetes。

**描述：** 这是一个上手项目，你将一个单节点 Kubernetes 集群并配置它以托管和自动扩展你在项目 13-11 中创建的 webapp 容器。

- 1. 在你的 Ubuntu Linux 虚拟机上，登录 tty 并使用用户名 root 和密码 LINUXRocks！
- 2. 在命令提示符下，输入 `curl -sL https://get.k3s.io | sh` 并按 Enter 下载并安装 K3s。
- 3. 在命令提示符下，输入 `kubectl get nodes` 并按 Enter。是否存在一个单节点集群？
- 4. 在命令提示符下，输入 `kubectl create deployment webapp --image=username/webapp:latest` 并按 Enter，其中 username 是你的 Docker Hub 用户名。这将创建一个配置从 Docker Hub 调用你的 webapp 容器镜像的部署。
- 5. 在命令提示符下，输入 `kubectl get deployment` 并按 Enter。每隔几分钟重复此命令，直到你的 webapp 从 Docker Hub 下载并在 Kubernetes 集群中启动。
- 6. 在命令提示符下，输入 `kubectl expose deployment webapp --nodeport=port=80` 并按 Enter 创建一个服务以便在集群节点上暴露你的 webapp 部署。NodePort 确保该服务在集群的每个节点上使用相同的端口访问你的 webapp 部署。
- 7. 在命令提示符下，输入 `kubectl get service` 并按 Enter。注意该服务暴露在 Kubernetes 网络 (10.0.0.0) 中。
- 8. 在命令提示符下，输入 `kubectl get pod` 并按 Enter。注意为该部署创建了一个 pod。
- 9. 在命令提示符下，输入 `kubectl edit deployment webapp` 并按 Enter。找到 `replicas: 1` 行并将其修改为 `replicas: 3`。完成后，保存更改并退出编辑器。
- 10. 在命令提示符下，输入 `kubectl get deployment webapp` 并按 Enter。注意现在有三个容器运行在相同的镜像上。对服务的请求将在这些容器之间进行负载均衡。
- 11. 在命令提示符下，输入 `kubectl get pods -l app=webapp` 并按 Enter。注意创建了三个 pod。
- 12. 在命令提示符下，输入 `kubectl logs -f -l app=webapp --prefix=true` 并按 Enter。注意与 webapp 相关的事件。此输出在排查部署相关问题时有用。
- 13. 在命令提示符下，输入 `kubectl get service webapp -o yaml` 并按 Enter。注意 `nodePort` 中的端口号：该端口通过 Traefik ingress 暴露在 Kubernetes 集群之外。
- 14. 在你的 Windows 或 macOS 上，打开浏览器并导航到 `http://IP:port`，其中 IP 是你 Ubuntu 虚拟机的 IP 地址，port 是上一步中的端口。验证 web 是否可以访问。
- 15. 返回你的 Ubuntu 虚拟机并运行 `kubectl top` 监控资源使用情况。
- 16. 在命令提示符下，输入 `kubectl autoscale deployment webapp --min-replicas=3 --max-replicas=8 --cpu-percent=50` 并按 Enter。这将创建一个水平 pod 自动伸缩器 (HPA)，当 CPU 使用率超过 50% 时自动扩展部署。
- 17. 要删除 HPA，在命令提示符下输入 `kubectl delete hpa webapp` 并按 Enter。删除完成后，退出。

## 584 CompTIA Linux+ 和 LPIC-1：Linux 认证指南

无需登录安装在相应硬盘上的操作系统，即可访问 Linux 计算机硬盘上的文件系统。为了防止这种情况，你应当将重要的计算机（如 Linux 服务器）锁定在特定的房间内，使得只有 Linux 管理员或受信任的用户才能访问。该房间通常被称为服务器房。遗憾的是，Linux 计算机（如工作站）位于公共区域。你应该移除计算机上的 CD 和 DVD 驱动器。此外，你还应该配置计算机 BIOS 密码，以防止其他用户更改启动顺序。

> 注意 1
> 为了防止用户无意中传播个人 USB 闪盘存储的病毒和恶意软件，某些组织禁用了工作站上的所有 USB 端口。其他组织也出于相同的原因不建议使用 USB 闪盘。

某些组织使用运行亭机软件的公共计算机为访客提供信息。通常，运行该软件的 Linux 计算机锁定在机柜或显示罩内，以防止用户访问系统。然而，用户经常尝试使用 `Ctrl-Alt-Del` 组合键重启计算机，并在亭机软件加载之前与操作系统进行交互。因此，防止公共系统通过 `Ctrl-Alt-Del` 组合键重启是好的。通过 SysV init 实现这一点，你可以注释 `/etc/init.d` 文件中包含 `ctrlaltdel` 操作的行并重启守护进程。对于使用 systemd 的系统，你可以使用 `systemctl mask ctrl-alt-target` 来防止 `Ctrl-Alt-Del` 组合键重启系统。

## 限制对系统的访问

除了限制对 Linux 计算机的物理访问外，提供限制未经授权访问 Linux 系统的机制也很重要。在用户使用密码时强制执行复杂密码以及在多次尝试密码后锁定账户是限制未经授权访问系统的最常用方法。要启用密码强制或账户锁定，你可以通过编辑 `/etc/pam.d` 目录下的相应文件，在你的 Linux 系统上配置相应的可插认证模块 (PAM)。在 Fedora 或 Ubuntu 上，你使用 `/etc/pam.d/password-auth` 或 `/etc/pam.d/system-auth` 或 `/etc/pam.d/common-password` 文件。例如，为了确保用户创建的密码至少包含 10 个字符（minlen），且至少包含一个大写字母（ucredit）、一个小写字母（lcredit）以及四个与之前密码不同的字符（difok=4），你需要在 `/etc/pam.d` 目录下的相应文件中添加以下行：

```
password pam_cracklib.so minlen=10 dcredit=1 ucredit=1 lcredit=1
```

注意，用于强制密码复杂性的 PAM 称为 `pam_cracklib.so`。为了在多次无效登录后锁定用户账户，你可以使用 `pam_tally.so` 或 `pam_failock.so`。要使用 `pam_tally.so` 在用户在 300 秒内（unlock_time=300）连续登录失败三次后锁定用户，你可以在 `/etc/pam.d` 目录下的相应文件中添加以下行：

```
auth pam_tally.so deny=3 unlock_time=300
```

要使用 `pam_failok.so` 强制执行账户锁定设置，你也可以在 `/etc/pam.d` 目录下的相应文件中添加以下行：

```
auth pam_failok.so deny=3 unlock_time=300
```

## 第 14 章 安全、故障排除与性能

如果用户在 300 秒内提供了三次错误密码，他们将无法登录系统，直到其用户账户被解锁。你可以使用 `pam_tally2` 或 `faillock` 命令列出被 `pam_tally2` 锁定的用户，因此要解锁被 `pam_failock` 锁用户 bob，你可以使用 `pam_tally2 --reset user bob`；要解锁被 `pam_failock` 锁出的用户 mary，你可以使用 `faillock --reset user` 命令。

认证服务也可以受到限制，以防止对操作系统的非法访问。大多数认证服务使用安全协议（如 Kerberos）来验证用户，并将信息和认证要求存储在轻量级访问协议 (LDAP) 数据库中。例如，LDAP 数据库中的信息可以用于确保该账户的所有用户都允许登录财务部门内的计算机。

Microsoft Active Directory 是如今组织内部最常用的服务。它在 LDAP 数据库中存储配置，该数据库通过 DNS 域名表示组织，并使用 Kerberos 验证用户。当用户通过 Active Directory 身份验证后，他们会收到一个 Kerberos 票据，用于验证他们在组织内所有其他系统的身份，这一功能称为单点登录 (SSO)。如果 Bob Burt 以用户 `bob@example.com` 的身份登录 Active Directory，Active Directory 域 `example.com` 的每个系统将自动识别他为用户 `bob.burt`，并授予他访问其获得权限的资源，例如 SMB 共享文件夹和打印机。

如果你将 Linux 系统加入 Active Directory 域，你将能够使用 Active Directory 用户名和密码登录图形显示管理器或命令行终端，并使用 SSO 访问资源。此外，用户的 Linux 系统将通过其收到的 Kerberos 票据进行认证，并为他们创建家主目录。Linux 系统上的系统服务守护进程 (sssd) 提供 LDAP 和 Kerberos 连接，而 Realm 守护进程 (realm) 用于发现和加入 Active Directory 域。在 Fedora 工作站上，`sssd` 和 `realm` 是默认安装的；你可以通过点击图形设置中的 Active Login 按钮将你的系统加入 Active Directory 域。用户的 Linux 系统将通过其收到的 Kerberos 票据进行认证，并为他们创建家主目录。

图 14-1：加入 Active Directory 域

# 第 14 章 安全、故障排除与性能

```
Cmnd_Alias KILL = /usr/bin/kill, /usr/bin/killall
Host_Alias SERVERS = server1, server2
```

```
SD SERVERS = (root) KILL
```

```
[root@server1 ~]#
```

现在，如果 mary 需要杀死 `crond` 进程或崩溃的守护进程（以 root 用户身份启动）以停止她编写的程序，她需要使用 `sudo` 命令，如下所示，并提供她的密码：

```
[server1~$] ps -ef | grep crond
root 2281 1 01:20 ? 00:00:00 /usr/bin/crond -n
[server1~$] kill -9 2281
-bash: kill: (2281) - Operation not permitted
[server1~$] sudo password for mary: ********
[server1~$]
```

回想第 10 章，在大多数现代 Linux 发行版中，创建的第一个普通用户会自动分配到 `wheel` 组。`wheel` 组的成员通过 `/etc/sudoers` 文件中的 `%wheel ALL` 行被授予了使用 root 密码执行所有系统管理的权限。作为管理员，你可以登录作为 `wheel` 组成员的普通用户来执行所有管理任务；在这种情况下，每个系统命令都必须带有 `sudo` 前缀。此外，在登录为 `wheel` 组成员的普通用户时，你可以使用 `sudoedit` 命令以 root 用户身份编辑文本文件（如配置文件）。`sudoedit` 使用系统上默认的文本编辑器打开文本文件，该编辑器可以通过 `EDITOR` 环境变量进行修改。

> 注意 4
在 Ubuntu 系统上，使用 `sudo` 组代替 `wheel` 组。

> 注意 5
root 用户对 `/etc/sudoers` 文件没有写权限，但具有覆盖所有文件权限的能力。作为 root，使用 `vi` 编辑器以 root 用户身份编辑 `/etc/sudoers` 文件时，在保存更改时必须使用 `:w` 以确保 `vi` 编辑器允许你覆盖文件权限。或者，你可以使用 `visudo` 命令以 root 用户身份编辑 `/etc/sudoers` 文件；该命令会使用默认文本编辑器创建 `/etc/sudoers` 的副本，并在使用文本编辑器时用该副本替换 `/etc/sudoers`。

Polkit（以前称为 PolicyKit）是 sudo 以 root 身份运行命令的替代方案。Polkit 允许 `wheel` 组成员使用 `pkexec` 命令以 root 身份执行命令。类似于 `/etc/sudoers` 中的行，你可以配置 Polkit 规则，并为系统任务中的特定用户和组提供细粒度的访问。要实现这一点，你必须在 `/etc/polkit-1` 目录下创建具有适当内容的 *.rules、*.conf 或 *.policy 文件。欲了解更多关于这些文件语法的信息，请查看 polkit 手册。

# CompTIA Linux+ 和 LPIC-1：Linux 认证指南

## 使用加密保护数据

加密可以防止具有物理访问文件权限的人读取它们。这对于容易被盗的电脑（如笔记本电脑和公共区域的电脑）尤为重要。对于这些系统，通常使用 Linux 统一密钥设置（LUKS）。最好在 Linux 安装期间在每个文件系统上配置 LUKS；你可以在图 2-10 中选择“加密”密钥以使用 LUKS 加密根文件系统的内容，并在文件系统挂载时提供你选择的口密码。

要在安装后设置 LUKS，你可以运行 `cryptsetup` 命令。例如，要在 `/dev/sd1` 分区上配置 LUKS 加密，你可以运行以下命令并在提示时提供密码：

```
[root@server1 ~]# cryptsetup luksFormat /dev/sd1
WARNING:
=======
这将不可恢复地覆盖 /dev/sd1 上的数据。
确定吗？（输入大写的 'yes'）：YES
Enter passphrase for /dev/sd1: ********
Verify passphrase: ********
```
