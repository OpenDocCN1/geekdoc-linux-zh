
*   **inspect：** 该参数在前文已有说明；选项 **--format** (-f) 允许从详细信息中访问特定数据。所需的格式为 **{{ .Category.Element}}**。**图 13.34** 展示了一些示例：

```bash
root@ubuntu:~$ docker inspect -f "{{ .Config.Hostname }}" web
c6812ed6469b
root@ubuntu:~$ docker inspect -f "{{ .NetworkSettings.IPAddress }}" web
172.17.0.2
root@ubuntu:~$ docker inspect -f "{{ .NetworkSettings.MacAddress }}" web
02:42:ac:11:00:02
root@ubuntu:~$ docker inspect -f "{{ .State.Status }}" web
running
```

![](img/863afa537de4eed7deb11978bfbfa90e_454_0.png)

*   默认情况下，当容器被移除时，容器内部的数据会丢失。可以在**容器**内部实现持久化存储。使用选项 **--volume** (-v)，可以指定服务器（**Docker 守护进程**正在运行的服务器）上的一个目录，该目录将被挂载到**容器**内部。**图 13.35** 展示了如何使用**主机**上的目录来存储容器将使用的 **HTML** 文件。

```bash
root@ubuntu:~$ mkdir /web/
root@ubuntu:~$ echo "File stored in the host" > /web/index.html
root@ubuntu:~$ docker run -dtiv /web:/usr/local/apache2/htdocs -p 8081:80 httpd
4ef4b6434ed1bf2ba80ca64f3d752fe8dd8d7d1e406511e11f7d940697d65a ea7f
root@ubuntu:~$ docker inspect -f "{{ .Mounts }}" 4ef4b6434ed1bf2
[{bind /web /usr/local/apache2/htdocs true private}]
root@ubuntu:~$ curl -s http://localhost:8081
File stored in the host
```

![](img/863afa537de4eed7deb11978bfbfa90e_454_1.png)

*   命令 **docker** 具有 **volume** 参数，用于列出、创建和删除系统中的卷。**图 13.36** 展示了如何创建一个卷，该卷可以通过目录 **/var/lib/docker/volumes/** 进行访问，以及如何通过选项 **--volume** 指定将其挂载到容器上。

```bash
root@ubuntu:~$ docker volume create myweb
myweb
root@ubuntu:~$ echo "From vol" > /var/lib/docker/volumes/myweb/_data/index.html
root@ubuntu:~$ docker run -dtiv myweb:/usr/local/apache2/htdocs -p 8082:80 httpd
e06bfdcd80ab31af456fe217b8e10de5550bb24b800d5a4232dd0775c65a38
root@ubuntu:~$ curl -s http://localhost:8082
From vol
```

![](img/863afa537de4eed7deb11978bfbfa90e_454_2.png)

## Docker 服务器统计和事件

通过 **Docker 客户端**（命令 `docker`），可以获取 **Docker 守护进程**的使用统计信息。可以使用参数 `stats` 来获取正在运行的**容器**的统计数据、所有**容器**（`-a|all`）或指定容器列表的统计数据。`图 13.37` 展示了输出示例：

```text
root@ubuntu:~# docker stats --no-stream
CONTAINER ID    NAME    CPU %    MEM USAGE / LIMIT    MEM %    NET I/O
BLOCK I/O    PIDS
c6812ed6469b    web    0.00%    16.34MiB /  3.832GiB    0.42%    10.6kB / 626B
0B / 24.6kB    82
```

`图 13.37`：*使用参数 `stats` 的输出示例*

客户端还提供选项以可视化生成的事件或在实时查看服务器上正在发生的事情。使用的参数是 `events`，选项如下：

-   `--filter (-f)`：使用指定过滤器过滤输出。
-   `--since`：显示从指定日期开始的记录。
-   `--until`：显示直到指定日期的记录。

如果未指定选项，客户端将等待新事件出现，并将其显示在屏幕上。选项 `--filter (-f)` 允许不同的过滤器，最常见的包括：

-   `container=container`：按容器（名称或标识符）过滤。
-   `event=action`：按事件类型过滤。
-   `image=image`：按镜像（名称或标识符）过滤。
-   `label=key or label=value`：按标签过滤。
-   `type=[container | image | volume | network | daemon]`：按生成事件的对象的类型过滤。
-   `volume=volume`：按卷（名称或标识符）过滤。
-   `network=network`：按内部 **Docker** 网络（名称或标识符）过滤。
-   `daemon=service`：按服务（名称或标识符）过滤。

`图 13.38` 展示了针对特定时段以及与 `image` 相关的任务进行过滤的示例，显示了前文描述的导入镜像示例。

```text
root@ubuntu:~# docker events --since '2022-10-30T20:56:37' --filter type=image
2022-10-30T20:56:37.602250603Z     image tag sha256:3508309e393de8538254463727e6e60ca8fdcd62717c63e2e876662ebc3c4c51    (name=myweb:0.1)
2022-10-30T20:56:37.602284773Z     image import sha256:3508309e393de8538254463727e6e60ca8fdcd62717c63e2e876662ebc3c4c51    (name=sha256:3508309e393de8538254463727e6e60ca8fdcd62717c63e2e876662ebc3c4c51)
```

> 图 13.38：使用参数 events 的输出示例

## 镜像仓库

Docker 允许创建自定义镜像并将其发布到私有或公共镜像仓库。镜像可以存储在本地，以便发布到仓库。镜像具有名称和标签。标签有助于指定应用程序或基础系统的版本，例如 httpd:2.4 或 ubuntu:22.04。标签还可以指定字符串以指示基于名称的版本，例如 ubuntu:jammy 或 ubuntu:latest（始终使用 Ubuntu 可用的最新镜像）。在创建镜像时，用户可以无限制地指定所需的标签。

生成镜像主要有以下两种选项：

-   **将容器转换为镜像：** 这种生成方式是手动任务，需要配置容器。这是不太推荐的选项。使用 Docker 客户端时，有以下两种可用选项：
    -   使用前文描述的 export 和 import 参数。
    -   使用 commit 和 tag 参数。图 13.39 展示了一个示例：
        ```text
        root@ubuntu:~# docker commit mywebserver3
        sha256:619992f21a8ebcdda4cef9ee2d6e20b0139092268f39cf9f19dd393e83f20d4d
        root@ubuntu:~# docker tag 619992f21a8e imagewebserver3:0.1
        root@ubuntu:~# docker images | head -2
        REPOSITORY TAG IMAGE ID CREATED SIZE
        imagewebserver3 0.1 619992f21a8e 20 seconds ago 145MB
        ```
    -   图 13.39：使用 commit 参数的示例
-   **使用模板：** 通常命名为 Dockerfile 的文件用作 Docker 命令 build 参数的参考。

以下是一个 Dockerfile 的示例：

```dockerfile
FROM ubuntu:latest
RUN apt-get update && apt-get install -y apache2
RUN echo "Image generated" > /var/www/html/index.html
COPY test.html /var/www/html/test.html
EXPOSE 80
CMD /usr/sbin/apache2ctl -D FOREGROUND
```

前一个示例中使用的指令如下：

-   **FROM：** 指示要配置的基础镜像。有效的 Dockerfile 必须以此指令开始。
-   **RUN：** 在基础镜像内部执行命令。每个 **RUN** 为镜像生成一个*层*；建议将它们分组并减少此类指令的数量。
-   **COPY：** 将文件复制到基础镜像内部。文件需要相对于 **Dockerfile** 所在的目录。
-   **EXPOSE：** 指定当使用此镜像的容器使用选项 **--publish-all** (-P) 时，将暴露哪个端口或哪些端口。
-   **CMD：** 当容器启动并使用此镜像时执行的默认命令。

要从 **Dockerfile** 模板构建**镜像**，使用带有 **build** 参数的 **docker** 命令。指定目标镜像名称和*标签*的选项是 **--tag** (-t)。参数 **build** 需要一个包含 **Dockerfile** 的上下文目录。**图 13.40** 展示了上一个示例的构建过程：

```text
root@ubuntu:~# docker build /root/ubuntuapache2/ -t ubuntuapache2:0.1
Sending build context to Docker daemon 3.072kB
Step 1/6 : FROM ubuntu:latest
---> cdb68b455a14
Step 2/6 : RUN apt-get update && apt-get install -y apache2
---> Using cache
---> e456d9e2e1f3
Step 3/6 : RUN echo "Image generated" > /var/www/html/index.html
---> Using cache
---> dd122fabfbfc
Step 4/6 : COPY test.html /var/www/html/test.html
---> Using cache
---> 99dfd22d79d5
Step 5/6 : EXPOSE 80
---> Using cache
---> 14efd05a5ac0
Step 6/6 : CMD /usr/sbin/apache2ctl -D FOREGROUND
---> Running in 50b7a218682d
Removing intermediate container 50b7a218682d
---> f1715312940c
Successfully built f1715312940c
Successfully tagged ubuntuapache2:0.1
```

图 13.40：构建新镜像的示例

参数 **history** 后跟一个镜像，将显示每一层及其执行的任务。**图 13.41** 展示了使用之前构建的镜像的示例。

