
Untagged `localhost/python36:1.0`

Untagged `registry.lab.example.com/ubi8/python-38:latest`

Deleted `registry.lab.example.com/ubi8/ubi`

Deleted: `80e8c6195925bea5fe3b2ada7a54f1e567393db847276bc625d5f9810e9eb499`

Deleted: `219e43fff096f1d2e184f674c6641113534dd5cbe2699ff1dbffb57b1f81d89a`

Deleted: `67c1c3cb4b2984ae23387eb5ba9a68e9e267cb7ffcc802283d3bc866f632161`

## 结束

在工作站上，切换学生用户主目录并使用 `lab` 命令完成本次练习。这一步非常重要，因为它可以确保之前练习的资源不会影响后续的练习。

```
[student@workstation ~]$ lab finish containers-deploy
```

# 管理容器存储和网络资源

## 目标

通过共享容器主机的存储为容器数据提供持久存储，并配置容器网络。

## 管理容器资源

你可以选择运行一个简单的进程并退出。你也可以配置容器持续运行服务，例如数据库服务器。在这种情况下，你可能考虑为容器添加更多资源，例如持久化存储或针对其他容器的 DNS 解析。

你可以使用不同的策略为容器配置持久化存储。在企业级容器平台（如 Red Hat OpenShift）中，你可以使用复杂的存储解决方案，在无需底层基础设施的情况下为容器提供存储。

对于仅使用单个容器主机且不需要扩展的小型部署，你可以通过创建一个挂载到运行中容器的目录，从容器主机上创建持久化存储。

当容器（如 Web 服务器或数据库服务器）为容器主机之外的客户端提供内容时，你需要在本地机器通过适当的防火墙配置允许端口 `3306` 流量。你可以配置*端口映射*来启用与容器的通信。通过端口映射，指向容器主机的请求将转发到容器内部的端口。

为了涵盖本章的主题，请想象以下场景。

作为系统管理员，你的任务是创建一个基于 MariaDB 的 `db01` 容器数据库，使用本地机器通过适当的防火墙配置允许端口 `3306` 流量。`db01` 容器必须使用具有适当 SELinux 上文的持久化存储。添加适当的网络配置，以便 `client01` 容器可以通过 DNS 与 `db01` 容器通信。

## 容器的环境变量

某些镜像允许在创建时传递环境变量来自定义容器。你可以使用环境变量对容器进行参数化，以适应你的环境，而无需创建自己的自定义镜像。通常，你不会修改容器镜像，因为这会给镜像增加层，可能更难以维护。

你使用 `podman run -d registry.lab.example.com/rhel8/mariadb-105` 命令运行一个容器化数据库，但你发现容器启动失败。

# 第 11 章 | 运行容器

```
[user@host ~]$ podman run -d registry.lab.com/rhel8/mariadb-105 --name db01

20751a03898f147a64b0e5c7c57465248595026121794456d26c94c435

[user@host ~]$ podman ps -a

CONTAINER ID IMAGE PORTS NAMES

CREATED STATUS

20751a03898f registry.lab.com/rhel8/mariadb-105:latest run-mysqld

29 seconds Exited (1) 29 seconds ago db01
```

你可以使用 `podman container logs` 来调查容器状态的原因。

```
[user@host ~]$ podman container logs db01

... 输出已省略。

你必须指定以下环境变量：

MYSQL_USER (regex: '^[a-zA-Z0-9_!]*$')

MYSQL_PASSWORD (regex: '^[a-zA-Z0-9_!#\$%&()<>,.;:||]+$')

MYSQL_DATABASE (regex: '^[a-zA-Z0-9_]*$')

或者提供：

MYSQL_ROOT_PASSWORD (regex: '^[a-zA-Z0-9_!#\$%&()<>,.;:||]+]+$')

... 输出已省略。
```

从前面的输出中，你确定容器没有运行，是因为没有向容器传递必需的环境。因此，你检查了 `mariadb-container` 以获取更多关于用于自定义容器的环境变量信息。

```
[user@host ~]$ skope inspect docker://registry.lab.com/rhel8/mariadb-105

... 输出已省略。

"name": "rhel8/mariadb-105",

"release": "40.167451927",

"summary": "MariaDB 10.5 SQL数据库服务器",

"url": "https://access.redhat.com/containers/#registry.access.redhat.com/rhel8/mariadb-105/"

"images":[{"tag": "40.167451927",

"command": "podman run -p 3306:3306 rhel8/mariadb-105 MYSQL_USER=mysql MYSQL_PASSWORD -e MYSQL_DATABASE=db",

"vcs-ref": "c84193b96a11e17ada62d779db440e0fed7a6",

"vcs-type": "git",

"vendor": "Red Hat, Inc."}],

... 输出已省略。
```

输出中的用法标签提供了如何运行镜像的示例。`url` 标签指向 Red Hat Container Catalog 中的一个页面，其中描述了环境变量以及关于如何使用容器镜像的其他信息。

该镜像的文档显示容器使用 `3306` 端口用于数据库服务。它还显示可以使用以下环境变量配置数据库服务：

## mariadb 镜像的环境变量

| 变量 | 说明 |
| --- | --- |
| `MYSQL_USER` | 要创建的 MySQL 账户的用户名 |
| `MYSQL_PASSWORD` | 用户账户密码 |
| `MYSQL_DATABASE` | 数据库名称 |
| `MYSQL_ROOT_PASSWORD` | root 账户密码 |

在检查环境变量后，你使用 `podman run -d` 来验证它们是否工作。

```
[user@host ~]$ podman run -d --name db01 \
  MYSQL_USER=mysql MYSQL_PASSWORD \
  - MYSQL_DATABASE=db \
  registry.lab.com/rhel8/mariadb-105
```

## 持久化存储

默认情况下，容器存储是临时的，数据在容器删除后会丢失。为了持久化数据，你必须使用持久化存储。常用的方法：

- Volumes（卷）：由容器引擎管理。
- Bind mounts（绑定挂载）：将主机上的文件或目录挂载到容器。
- tmpfs：存储在内存中。

对于仅使用单个容器主机且不需要扩展的小型部署，你可以通过创建一个挂载到运行中容器的目录，从容器主机上创建持久化存储。

当容器（如 Web 服务器或数据库服务器）为容器主机之外的客户端提供内容时，你需要在本地机器通过适当的防火墙配置允许端口 `3306` 流量。你可以配置*端口映射*来启用与容器的通信。通过端口映射，指向容器主机的请求将转发到容器内部的端口。

为了涵盖本章的主题，请想象以下场景。

作为系统管理员，你的任务是创建一个基于 MariaDB 的 `db01` 容器数据库，使用本地机器通过适当的防火墙配置允许端口 `3306` 流量。`db01` 容器必须使用具有适当 SELinux 上文的持久化存储。添加适当的网络配置，以便 `client01` 容器可以通过 DNS 与 `db01` 容器通信。

# 第1章 | 运行容器

```bash
[user@]$ podman container logs db01

output omitted...

--> 16:41:25 Initializing database ...
--> 16:41:25 Running mysql_install_db ...
mkdir: cannot create directory '/var/lib/mysql/data': Permission denied
Fatal error Can't create database '/var/lib/mysql/data'
```
