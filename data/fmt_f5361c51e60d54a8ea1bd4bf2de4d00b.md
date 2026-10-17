
Podman（Pod Manager 的缩写）采用了由 Kubernetes 引入的 Pod 模型。Pod 是容器，每个 Pod 都在同一服务器上运行独立的应用程序。例如，如果你想设置 Nextcloud，还需要一个服务器应用程序、一个数据库，以及如果你想从外部访问该服务，还需要一个反向代理。所有这些应用程序都在 Pod 中的独立容器中运行。这带来了一些好处，例如可以绑定到 Pod 的 `localhost` 地址，这意味着由于共享网络命名空间，Pod 中的所有容器都可以连接该地址。

在本文中，我将讨论 Podman 的优势，然后通过使用 Podman 设置 Nextcloud 的实际示例向您展示具体操作。

##### Podman 的优势

虽然 Docker 由守护程序集中控制，但 Podman 无需此类实例，并且无需 root 权限即可运行。得益于基于 Cgroups 2 [2] 的内核用户命名空间的使用，容器在普通用户的上下文中运行。然而，在容器内部，进程本身是以 root 权限运行的。在命名空间内，进程因此拥有与命名空间外部不同的权限和用户 ID。由于不受守护程序控制，Podman 容器可以作为 `systemd` 服务 [3] 包含，或使用 Cockpit 管理工具通过 GUI 进行控制（图 1）[4]。

照片来自 Unsplash 的 Axel Tyring

与 Docker 不同，Docker 中应用程序的各个组件运行在不同的容器中，而 Podman 将多个容器组合在一个 Pod 中；这反过来避免了网络问题。

在命令行上，Podman 的行为与 Docker 几乎相同，该软件在后台实现了 Docker 的命令。此外，Podman 可用于创建 Docker Registry 仓库的镜像。

为了使容器尽可能高效地利用资源，你可以使用 Buildah [5]，它允许你从头开始构建容器。特别是，Buildah 在希望镜像尽可能小的环境中非常有用。

如您所见，红帽公司通过 Podman 优雅地解决了其对 Docker 的依赖，同时提供了额外的功能。例如，Podman 4 带有新的 `podman image scp` 命令，允许您将镜像本地复制和远程服务器，而无需通过注册表绕道。

#### 安装

为了使用 Podman 设置一个简单的 Nextcloud 安装，我使用了 Fedora 36 搭配 Podman 4.0.2 以及 Debian “Sid”（Siduction）搭配 Podman 3.4.4。除了 Podman 的安装步骤外，说明是相同的。

在测试期间，我在 Proxmox 容器中运行 Fedora 36，而 Siduction 安装在笔记本电脑上。要在 Fedora 上安装 Podman，请键入：

```
sudo dnf install podman cockpit-podman
```

对于 Debian，请使用：

```
sudo apt install podman cockpit-podman
```

Debian 的说明应适用于 Debian Stable 及其衍生版本。使用较旧版本的 Podman 有时会导致行为偏差。

为了更好地集成容器和宿主环境，你需要额外安装 `toolbox` 实用工具 [6]。完成后，可以使用 `DNF` 在容器中安装包，可以直通 USB 设备，并且可以集成宿主的主目录（图 2）。

##### 配置

首先，你需要为要在 Podman 容器中创建的 Nextcloud 安装创建三个卷（列表 1）。在此上下文中，卷 [7] 充当 Podman 创建和管理存储设备，提供了在容器和宿主之间移动和编辑数据的能力。你可以预先使用 `podman volume` 命令创建卷，或者在设置容器时直接创建（图 3）。

接下来，通过键入以下内容创建一个新的网络：

```
podman network create nextcloud-net
```

并使用以下命令检查其属性：

```
podman network inspect nextcloud-net
```

现在是创建容器的时候了，从 MariaDB 数据库开始。作为替代方案，你可以集成 PostgreSQL，但 SQLite 不是 Nextcloud 的好选择。设置数据库容器的命令和规范在列表 2 中指定。

`podman run` 命令会弹出一个交互式 shell，你可以在其中定义数据库属性 [8]。确保你选择并记住 `<DB-User-Password>` 和 `<DB-Root-Password>`；你稍后需要它们。你可以通过键入 `podman container ls` 来检查这一切是否正常工作，它会显示正在运行的容器。

下一步是部署 Nextcloud。适用的原则与列表 3 中所示的相同。再次确保你运行 DB 容器中的 `<DB-User-Password>`，并替换 `<NC-Admin>` 和 `<NC-Password>` 变量。

设置好框架后，在你的 Web 浏览器中调用 `localhost:8080`。Nextcloud 23 将会显示 Hello，然后你可以

**列表 1：创建卷**

```
$ podman volume create nextcloud-app
$ podman volume create nextcloud-data
$ podman volume create nextcloud-db
```

**列表 2：容器中的 MariaDB**

```
podman run --detach \
--env MYSQL_DATABASE=nextcloud \
--env MYSQL_USER=nextcloud \
--env MYSQL_PASSWORD=<DB-User-Password> \
--env MYSQL_ROOT_PASSWORD=<DB-Root-Password> \
--volume nextcloud-db:/var/lib/mysql \
--network nextcloud-net \
--restart on-failure \
--name nextcloud-db \
docker.io:library/mariadb:10
```

**列表 3：部署 Nextcloud**

```
podman run --detach \
--env MYSQL_HOST=nextcloud-db.dns.podman \
--env MYSQL_DATABASE=nextcloud \
--env MYSQL_USER=nextcloud \
--env MYSQL_PASSWORD=DB-User-Password \
--env NEXTCLOUD_ADMIN_USER=<NC-Admin> \
--env NEXTCLOUD_ADMIN_PASSWORD=<NC-Password> \
--volume nextcloud-app:/var/www/html \
--volume nextcloud-data:/var/www/html/data \
--network nextcloud-net \
--restart on-failure \
--name nextcloud \
--publish 8080:80 \
docker.io:library/nextcloud:latest
```

**图 3：** 我们示例的 Nextcloud 项目由三个卷组成，可以使用简单的命令快速创建。卷通过允许在容器和宿主之间移动和编辑数据，增强了容器的灵活性。

![](img/b40e8bf6cf651f8eebf36f5265123095_52_0.png)

在 GUI 中继续安装。您也可以将环境参数写入文件，然后通过输入以下内容来包含该文件：

```
--env-file /path/to/<file>
```

#### 设置

此处描述的设置非常适合在家庭网络中使用 Nextcloud。在这种简单场景下，所有容器都在单个 pod 中运行。如果您想从家庭网络外部访问该 pod，则需要额外的容器。出于安全目的，可以通过 Traefik 代理实施 TLS 加密，也可使用 HTTPD、NGINX 或 Caddy 等工具实现。

如果您将 Podman 包含为 `systemd` 服务，可以通过额外指定 `label=10.containers.autoupdate=image` 并使用 `podman auto-update` [9] 来简化镜像更新。在创建容器时，使用

```
podman generate systemd --new
```

完成初步准备工作后，在您的浏览器上 `localhost:8080` 调用 Nextcloud，并以通常方式在那里完成安装（图 4）。可以在列表 4 中找到 Podman 三个最重要配置文件的路径。

**列表 4：Podman 配置**

- `/usr/share/containers/containers.conf`

- `/etc/containers/containers.conf`

- `${HOME}/.config/containers/containers.conf`

![](img/b40e8bf6cf651f8eebf36f5265123095_52_1.png)
