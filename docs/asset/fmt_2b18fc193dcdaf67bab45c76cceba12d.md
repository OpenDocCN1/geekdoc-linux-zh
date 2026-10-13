
要撤销此操作，请使用 `systemctl disable-linger` 命令。

## 使用 systemd 以 root 身份管理容器

你可以配置容器通过 systemd 服务文件运行并管理它们。这种方法的优点之一是，你可以配置服务文件工作方式完全像普通的系统单元，而不是针对特定用户。

以 root 身份创建服务文件的程序与之前概述的无根容器程序类似，但有以下例外：

- 不要为容器管理创建专门的用户。
- 服务文件必须位于 `/etc/systemd/system` 目录，而不是 `~/.config/systemd/user` 目录。
- 使用不带 `--user` 选项的 `systemctl` 命令管理容器。
- 不要以 root 用户身份运行 `systemctl enable-linger` 命令。

演示请此节引用中列出的 Red Hat Videos 频 YouTube 视频。

> 参考
`logctl(1)`, `systemd.unit(5)`, `systemd.service(5)`, `subid(5)`, 以及 `podman-generate-systemd(1)` 手页

使用 Systemd Unit 文件在 Podman 中管理容器
https://www.youtube.com/watch?v=AGkM2GTGIY

更多信息，请参阅 Red Hat Enterprise Linux 9 Building, Running, 中的 Running Containers as Systemd Services with Podman

## 引导练习

## 以 root 身份管理容器

在此练习中，你用 systemd 服务配置容器。

## 结果

- 创建一个带有 systemd 服务的容器。
- 配置容器在机器启动时启动。

### 在开始之前

作为工作站上的学生用户，这将准备好你的环境。

## 指南

1. 以学生用户身份登录 `servera`。

### 第11 章 | 运行容器

以学生用户身份返回工作站机器，然后以 `contsvc` 用户身份登录。

```
[student]@servera ~~$ exit

logout

Connection to servera closed.

[student]@workstation ~~$ ssh contsvc@servera

--output omitted...

[contsvc]@servera ~~$
```

1. 创建 `~/.config/containers/` 目录。

```
[contsvc]@servera ~~$ mkdir -p ~/.config/containers/
```

2. 实验脚本拷贝 `/tmp/containers-services/` 目录下的 `registries.conf` 文件。将文件复制到 `~/.config/containers/`。

```
[contsvc]@servera ~~$ cp /tmp/containers-services/registries.conf \
~/.config/containers/
```

3. 验证 `registry.lab.example.com` 仓库是否正常。如果一切运行正常，命令将列出一些镜像。

```
[contsvc]@servera ~~$ podman search ubi
NAME DESCRIPTION

registry.lab.example.com/ubi7/ubi

registry.lab.example.com/ubi8/ubi

registry.lab.example.com/ubi19-beta/ubi
```

4. 创建 `~/webcontent/html/` 目录作为 Web 服务器容器的持久化存储。在目录内创建包含 Hello World 行的 `index.html` 页面。

1. 创建 `~/webcontent/html/` 目录。

```
[student]@servera ~
```

2. 创建 `index.html` 文件并添加 Hello World 行。

```
[contsvc]@servera ~~$ echo "Hello World" > ~/webcontent/html/index.html
```

3. 确认 `index.html` 文件的其他用户权限设置为 `r--`。容器使用非特权用户，该用户必须读取 `index.html` 文件。

### 第 11 章 | 运行容器

```bash
[contsvc@servera] $ ls -ld webcontent/html/
drwxr-xr-x. 2 contsvc Aug 24 08:56 webcontent/html/
[contsvc@servera] $ ls -l webcontent/html/index.html
-rw-r--r-- 1 contsvc Aug 24 08:56 webcontent/html/index.html
```

- 5. 使用 `registry.lab.example.com/rhel8/httpd-24:1-105` 镜像以离散模式运行容器内的 web 应用。将本地主机的 8080 端口重定向到容器的 8080 端口。将主机的 `~/webcontent` 目录挂载到 `/var/www` 目录。
- 以 `admin` 用户身份登录 `registry.lab.example.com`，密码为 `redhat321`。

```bash
[contsvc@servera] $ podman login registry.lab.example.com
Username: admin
Password: redhat321
Login Succeeded!
```

- 5.2. 使用 `registry.lab.example.com/rhel8/httpd-24:1-163` 镜像以离散模式运行容器内的 web 应用。使用 `-p` 选项将 8080 端口映射到容器内的 8080 端口。使用 `-v` 选项将 `~/webcontent` 目录挂载到容器内的 `/var/www`。

```bash
[contsvc@servera] $ podman run -d --name webapp -p 8080:8080 -v \
~/webcontent:/var/www registry.access.redhat/ubi8/httpd-24:1-163
7506a81bd37c6b25290f9be4e347ee2cc24d79f5843911fd6640194d0e6
...output omitted.
```

- 5.3. 验证 web 服务正在 8080 端口上运行。

```bash
[contsvc@servera] $ curl http://localhost:8080
Hello World
```

- 6. 使用 `systemctl` 命令创建一个 systemd 服务来管理 `webapp` 容器。配置 systemd 服务，使得在启动服务时，systemd 守护进程会创建它。配置完成后，停止并删除 `webapp` 容器。记住，systemd 守护进程期望容器最初不存在。

- 6.1. 创建并切换到 `~/.config/systemd/user/`。

```bash
[contsvc@servera] $ mkdir -p ~/.config/systemd/user/
[contsvc@servera] $ cd ~/.config/systemd/user/
```

- 6.2. 为 `webapp` 容器创建单元文件。使用 `--new` 选项，以便 systemd 在启动服务时创建容器并在停止服务时删除容器。

```bash
[contsvc@user] $ podman generate systemd --name webapp --files --new
/home/contsvc/.config/systemd/container-webapp.service
```

- 6.3. 停止并删除 `webapp` 容器。

```bash
[contsvc@server user]$ $ podman stop webapp
webapp
[contsvc@server user]$ $ podman rm webapp
7a96b8d1b3c7bb6b25907e8434ee2cc2cd47f9550439110fc6d4102914d00e6
[contsvc@server user]$ $ podman ps -a
```
