
需要更多功能吗，比如带有图形化输出的工具？有很多工具可用。其中一个著名的工具是 `Google` 的 `cAdvisor`。你可以将该工具本身作为 `Docker` 容器运行，如下：

```bash
docker run -d -p 8080:8080 --name cadvisor \
--volume=:/rootfs:ro \
--volume=:/var/run:/var/run:rw \
--volume=:/sys:/sys:ro \
--volume=:/lib/docker:/var/lib/docker:ro \
go/cadvisor:latest
```

一旦容器启动，你就可以通过服务器域名或 `IP` 的 `8080` 端口或你使用的任何端口访问 `UI`。`cAdvisor` 能够监控 `LXC` 和 `Docker` 容器。此外，它还可以报告主机系统资源。

### 更多...

有各种外部工具提供监控和故障排除服务。`Sysdig` 是一个类似的命令行工具，可用于监控 `Linux` 系统和容器。可以在 `https://github.com/draios/sysdig/wiki/Sysdig%20Examples` 查看一些使用 `sysdig` 的示例。

此外，请查看 `Sysdig Falcon`，这是一个支持容器的开源行为监控器。

### 另请

- `Docker` 运行时指标：`http://docs.docker.com/v1.8/articles/metrics/`

- `GitHub` 上的 `cAdvisor`：`https://github.com/google/cadvisor`

### 保护 `Docker` 容器

在本教程中，我们将学习可能稍微提高容器安全性的 `Docker` 配置。`Docker` 在最新的 `Linux` 内核中使用了一些高级功能，包括提供进程隔离的内核命名空间、控制资源分配的控制组以及运行非特权容器的内核能力用户命名空间。正如 `Docker` 文档页面所述，`Docker` 容器默认是非常安全的。

本教程涵盖了一些提高 `Docker` 安全性并减少 `Ubuntu` 主机以及 `Docker` 守护进程攻击面的基本步骤。

### 如何操作...

第一也是最常见的方法是使用软件的最新版本。确保你正在使用带有所有安全更新的最新 `Ubuntu` 版本，并且 `Docker` 版本是最新稳定版：

1. 使用以下命令升级你的 `Ubuntu` 主机：

   ```bash
   $ sudo apt-get update

   $ sudo apt-get upgrade
   ```

2. 如果你在安装时使用了 `Docker` 维护的仓库... ![](img/a6dbf7df749be83c0faae2334e970c0b_297_0.png)

### 容器操作

1. 通过 `docker logs`，你可以获取在容器内运行的应用程序日志。

它的用法类似于 `tail -f` 命令：

```bash
$ docker logs -f ubuntu
```

2. `Docker` 还会记录容器的状态变更事件。这些事件包括启动、停止、创建、杀死等。你可以通过 `docker events` 获取实时事件：

```bash
$ docker events
```

要获取过去的事件，请在 `docker events` 中使用 `--since` 参数：

```bash
$ docker events --since '2015-11-01'
```

3. 你也可以通过 `docker diff` 命令检查容器文件系统的变化，它将列出新添加 (`A`)、修改 (`C`) 或删除 (`D`) 的文件。

```bash
$ docker diff ubuntu
```

4. 另一个实用的命令是 `docker top`，它可以帮助查看容器内部。该命令显示容器内部运行的进程：

```bash
$ docker top ubuntu
```

### 原原理...

`Docker` 提供了各种内置命令来监控容器及其内部运行的进程。它使用了原生系统结构，如命名空间和控制组。大多数统计数据从原生系统收集。日志直接从运行进程中收集。

需要更多功能吗，比如带有图形化输出的工具？有很多工具可用。其中一个著名的工具是 `Google` 的 `cAdvisor`。你可以将该工具本身作为 `Docker` 容器运行，如下：

```bash
docker run -d -p 8080:8080 --name cadvisor \
--volume=:/rootfs:ro \
--volume=:/var/run:/var/run:rw \
--volume=:/sys:/sys:ro \
--volume=:/lib/docker:/var/lib/docker:ro \
go/cadvisor:latest
```

一旦容器启动，你就可以通过服务器域名或 `IP` 的 `8080` 端口或你使用的任何端口访问 `UI`。`cAdvisor` 能够监控 `LXC` 和 `Docker` 容器。此外，它还可以报告主机系统资源。

### 更多...

有各种外部工具提供监控和故障排除服务。`Sysdig` 是一个类似的命令行工具，可用于监控 `Linux` 系统和容器。可以在 `https://github.com/draios/sysdig/wiki/Sysdig%20Examples` 查看一些使用 `sysdig` 的示例。

此外，请查看 `Sysdig Falcon`，这是一个支持容器的开源行为监控器。

### 另请

- `Docker` 运行时指标：`http://docs.docker.com/v1.8/articles/metrics/`

- `GitHub` 上的 `cAdvisor`：`https://github.com/google/cadvisor`

### 保护 `Docker` 容器

在本教程中，我们将学习可能稍微提高容器安全性的 `Docker` 配置。`Docker` 在最新的 `Linux` 内核中使用了一些高级功能，包括提供进程隔离的内核命名空间、控制资源分配的控制组以及运行非特权容器的内核能力用户命名空间。正如 `Docker` 文档页面所述，`Docker` 容器默认是非常安全的。

本教程涵盖了一些提高 `Docker` 安全性并减少 `Ubuntu` 主机以及 `Docker` 守护进程攻击面的基本步骤。

### 如何操作...

第一也是最常见的方法是使用软件的最新版本。确保你正在使用带有所有安全更新的最新 `Ubuntu` 版本，并且 `Docker` 版本是最新稳定版：

1. 使用以下命令升级你的 `Ubuntu` 主机：

   ```bash
   $ sudo apt-get update

   $ sudo apt-get upgrade
   ```

2. 如果你在安装时使用了 `Docker` 维护的仓库... ![](img/a6dbf7df749be83c0faae2334e970c0b_297_0.png)

### 容器操作

1. 通过 `docker logs`，你可以获取在容器内运行的应用程序日志。

它的用法类似于 `tail -f` 命令：

```bash
$ docker logs -f ubuntu
```

2. `Docker` 还会记录容器的状态变更事件。这些事件包括启动、停止、创建、杀死等。你可以通过 `docker events` 获取实时事件：

```bash
$ docker events
```

要获取过去的事件，请在 `docker events` 中使用 `--since` 参数：

```bash
$ docker events --since '2015-11-01'
```

3. 你也可以通过 `docker diff` 命令检查容器文件系统的变化，它将列出新添加 (`A`)、修改 (`C`) 或删除 (`D`) 的文件。

```bash
$ docker diff ubuntu
```

4. 另一个实用的命令是 `docker top`，它可以帮助查看容器内部。该命令显示容器内部运行的进程：

```bash
$ docker top ubuntu
```

### 原原理...

`Docker` 提供了各种内置命令来监控容器及其内部运行的进程。它使用了原生系统结构，如命名空间和控制组。大多数统计数据从原生系统收集。日志直接从运行进程中收集。

需要更多功能吗，比如带有图形化输出的工具？有很多工具可用。其中一个著名的工具是 `Google` 的 `cAdvisor`。你可以将该工具本身作为 `Docker` 容器运行，如下：

```bash
docker run -d -p 8080:8080 --name cadvisor \
--volume=:/rootfs:ro \
--volume=:/var/run:/var/run:rw \
--volume=:/sys:/sys:ro \
--volume=:/lib/docker:/var/lib/docker:ro \
go/cadvisor:latest
```

一旦容器启动，你就可以通过服务器域名或 `IP` 的 `8080` 端口或你使用的任何端口访问 `UI`。`cAdvisor` 能够监控 `LXC` 和 `Docker` 容器。此外，它还可以报告主机系统资源。

1. `Ampache` 的 `Web` 设置将配置配置保存在 `config` 目录下。它需要该目录的写权限：
