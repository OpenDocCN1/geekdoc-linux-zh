
```json
"frontend": {
  "EndpointID": "",
  "Gateway": "10.89.1.1",
  "IPAddress": "10.89.1.6",
}
```

5.4. 在 `db_client` 容器中安装 `iputils` 包。

```
[student@server]$ podman exec -it db_client dnf install -y iputils \
...output omitted...\
Complete!
```

5.5. 从 `db_client` 容器 ping `db_01` 容器名。

# 第 11 章 | 容器

```
[student@server ~] $ podman exec -it db_client ping -c4 db_01
PING db_01.dns.pod (10.90.0.3) 56(84) bytes of data.
... output omitted...
db_01.dns.pod ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3048ms
rtt min/avg/max/mdev = 0.043/0.049/0.054/0.004 ms
```

5.6. 退出服务器机器。

```
[student@server ~] $ exit
logout
Connection to server closed.
[student@workstation ~]$
```

## 完成

在工作站机器，切换到学生家目录并使用 `lab` 命令完成本次练习。这一步对于确保之前的练习资源不会影响后续练习非常重要。

> `student@workstation ~ lab finish containers-resources`

本节结束。

# 作为系统服务的方式管理容器

## 目标

将容器配置为 `systemd` 服务，并配置容器服务在启动时运行。

# 使用 systemd Unit 管理小型容器环境

你可以运行一个容器来完成系统任务或获取一系列命令的输出。你可能还想运行无限服务的容器，例如服务器或数据库。在传统环境中，特权用户通常会配置这些服务在系统启动时运行，并使用 `systemd` 命令对它们进行管理。

作为普通用户，你可以创建一个 `systemd` 单元来配置无根（rootless）容器。你可以使用此配置通过 `systemd` 命令将你的容器作为普通服务进行管理。

基于 `systemd` 管理容器对于不进行扩展的基础型和小型部署非常有用。对于多容器应用程序和服务的进行更复杂的扩展和编排，你可以使用基于 Kubernetes 的企业级编排平台，例如 Red Hat OpenShift Platform。

为了讨论本次讲座中的主题，请想象以下场景：

作为系统管理员，你被要求配置基于 `http24` 镜像的 `webserver1` 容器在启动时运行。你还必须挂载 `/app-artifacts` 目录用于服务器内容，并将本地机器的 8080 端口映射到容器。配置容器使用 `systemd` 命令启动和停止。

# systemd 用户服务的要求

作为普通用户，你可以使用 `systemd` 命令启用服务。服务会在打开会话（图形界面、文本控制或 SSH）时启动，并在关闭最后一个会话时停止。这种行为与系统服务不同，系统服务在系统启动时启动并在关闭时停止。

默认情况下，当使用 `useradd` 命令创建用户账户时，系统使用用户 ID 范围内的下一个可用 ID。系统还在 `/etc/subuid` 中为用户的容器预留了一个范围 ID。如果你使用 `useradd -uuid` 创建用户账户，则系统不会为用户容器预留范围。

你决定创建一个专门的用户账户来管理容器。你使用 `useradd` 命令创建 `appdev-admin` 用户，密码设为 `redhat`。

# 第 11 章 | 容器

```
[user@host ~]$ sudo useradd appdev-admin
myapp.service
[user@host ~]$ sudo passwd appdev-admin
Changing password for user appdev-admin.
New password: redhat
BAD PASSWORD: The password is shorter than 8 characters
Retype new password: redhat
passwd: all authentication tokens updated successfully.
```

你随后使用命令切换到 `appdev-adm` 用户，并开始使用 `podman` 命令。

```
[user@host ~]$ su appdev-adm
Password: redhat
[appdev-adm ~]$ podman info
ERROR[0000] XDG_RUNTIME_DIR "/run/user/1000" is not owned by the current user
[appdev-adm ~]$
```

`Podman` 是一个无状态工具，需要完整的登录会话。`Podman` 必须在 SSH 会话中使用，不能作为 `sudo` 或类似使用。你必须退出 shell 并通过 SSH 登录机器。

```
[appdev-adm ~]$ exit
[user@host ~]$ exit
[user@example ~]$ ssh appdev-adm@host
[appdev-adm ~]$
```

你随后配置容器并使用凭据进行身份验证。你使用以下命令运行容器：

```
[appdev-adm ~]$ podman run -d -name webserver1 -p 8080:8080 -v
--mount=/app-artifacts:Z registry.access.redhat.com/ubi8/httpd
de4a3cdc96f3d50cc39ea4873cf15a7e88b54d56470e5ae7a35
[appdev-adm ~]$ podman ps
CONTAINER ID    STATUS     PORTS               NAMES
CREATED         5 seconds ago   de4a3cdc96f
Exited (1) 2 seconds ago   0.8080/8080  webserver1
```

你发现 `webserver1` 没有启动，因此你运行 `podman` 命令来查看日志。

# 第 11 章 | 容器

```
[appdev-adm ~]$ podman container logs webserver1
=> sourcing 10-set.sh
=> sourcing 20-config.sh
=> sourcing 40-certs.sh
--> Generating SSL pair for httpd...
0052: error on line 11 of /etc/httpd/conf:
Document '/var/www/html' is not a directory
```

错误是因为容器找不到 `html` 目录。你删除现有容器，运行命令如下：

```
[appdev-adm ~]$ podman run -d -name webserver1 -p 8080:8080 -v \
--mount=/app-artifacts:Z registry.access.redhat.com/ubi8/httpd
de4a3cdc96f3d50cc39ea4873cf15a7e88b54d56470e5ae7a35
[appdev-adm ~]$ podman ps
CONTAINER ID    STATUS     PORTS               NAMES
CREATED         5 seconds ago   de4a3cdc96f
Up 4 seconds ago   0.0.0.0:8080/8080  webserver1
```
