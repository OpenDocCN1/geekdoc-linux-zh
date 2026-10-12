
默认情况下，容器只能从主机（`Docker`守护进程运行时）内部访问。安装`Docker`时，会创建并默认使用私有网桥。默认配置的子网是`172.17.0.0`。图 13.13 显示了如何使用`http`镜像运行容器，该镜像包含`Apache`的默认实例。

```
root@ubuntu:~# docker run --name mywebview -di http
Unable to find image 'http:latest' locally
latest: Pulling from library/https
e999526091: Pull complete
e55c5c4d4cf4: Pull complete
d8c6be67efe: Pull complete
d50f83j3d3cb: Pull complete
e559e5308098: Pull complete
Digest: sha256:f99651b61395de5bf7fd8c9e741523322eb520a8e8832ef247fc80dbfc33
Status: Downloaded image for http:latest
c68122dc699ba3a0b3192f3192f31264e05047c39306087a0a4b29cf4071cb0c4
```

图 13.15：访问容器的示例

从公共仓库下载镜像并执行容器后，可以检查容器以获取分配的 IP，如图 13.16 所示：

```
root@ubuntu:~# docker inspect mywebserver | grep -m1 'IPAddress'
"IPAddress": "172.17.0.2",
root@ubuntu:~#
```

图 13.16：访问容器的示例

有了 IP，就可以访问运行`Docker`的主机。由于此容器是一个 Web 服务器，可以使用`curl`工具对其进行访问。图 13.17 显示了一个示例：

```
root@ubuntu:~# curl 172.17.0.2
<html><body><h1>It works!</h1></body></html>
root@ubuntu:~#
```

图 13.17：访问容器的示例

在许多在容器平台内执行的服务中，我们可能希望将该项暴露到外部。`docker`命令的`run`参数提供了两种暴露容器的选项：

- `--publish-all` (`-P`)：将所有暴露的端口发布到随机端口。
- `--publish` (`-p`)：手动指定要暴露到主机的端口列表。

使用第一个选项时，`Docker`将检查镜像中配置的待暴露端口，并为其分配一个随机端口。在图 13.18 所示的后续示例中，使用`publish-all`选项执行了一个使用`httpd`镜像的新容器：

```
root@ubuntu:~# docker run --publish-all --name mywebserver2 -d httpd
2630079f3a9b5f3dbb47791c4965b647e8d6d05fd2e388f8b3a89afc3
CONTAINER ID IMAGE COMMAND CREATED STATUS PORT
s2630079f3a9b5f3d httpd "httpd-foreground" 3 seconds ago 2 seconds 0.0.0.0.49153->80/tcp, :::49153->80/tcp mywebserver2
```

图 13.18：容器发布随机端口的示例

在前面的示例中，随机端口`49153`位于主机上，`IPv4`和`IPv6`将请求重定向到新创建名为`mywebserver2`容器的`80`端口。使用`curl`命令可以对其测试，如图 13.19 所示：

```
root@ubuntu:~# curl 192.168.122.43:49153
<html><h1>It works!</h1></body></html>
```

图 13.19：访问容器的示例

与选项`--publish` (`-p`)配合使用时，主机的端口也将用于重定向，且同样需要指定。共有三种格式可用，如表 13.1 所示。

| 格式 | 说明 |
| --- | --- |
| `host_port:container_port` | 将主机端口`host_port`重定向到容器端口`container_port`。服务器上所有可用的 IP 将在`host_port`上监听。 |
| `IP:host_port:port_container` | 与前述格式类似，但仅指定一个 IP，该 IP 将监听端口`host_port`。 |
| `IP::port_container` | 在此格式下，主机将使用相同的端口。例如，如果容器暴露`80`，则主机上也将使用相同的端口。 |

```bash
root@ubuntu:~# docker rename mywebview web
root@ubuntu:~# docker exec web grep ^Listen /usr/local/apache2/conf/httpd.conf
Listen 80
```

图 13.30: 在运行的容器中执行命令的示例

- 常用选项如下：
- `--detach` (`-d`)：在后台执行命令。
- `--interactive` (`-i`)：交互模式，用于引入命令。
- `--tty` (`-t`)：分配一个伪终端。

```
root@ubuntu:~# docker exec -ti /bin/bash
root@c6812ed649b:/usr/local/apache2# grep ^DocumentRoot conf/httpd.conf
DocumentRoot "/usr/local/apache2/htdocs"
root@c6812ed649b:/usr/local/apache2#
```

图 13.31: 访问容器的示例

- `export/import`: `export`参数可以对运行中或停止的容器进行备份，并生成一个包含内容的`tar`文件。请参考图 13.32。

```bash
root@ubuntu:~# docker export web -o web.tar
root@ubuntu:~# ls -lh web.tar
-rw-r--r-- 1 root 140M Oct 30 20:52 web.tar
```

图 13.32: 导出容器的示例

要创建一个容器，我们首先需要从备份创建一个镜像，然后使用该镜像创建容器。请参考图 13.33。

```bash
root@ubuntu:~# docker import web.myimage:0.1
sha256:350380393de853f54463772e60c6a8df6c2717c63e2e876662ebc3c4c51
root@ubuntu:~# docker run -ti myimage:0.1 /usr/local/apache2/bin/httpd -v
Server Version: Apache/2.4.4 (Linux)
Server built:
Oct 25 2022 03:59:05
```

图 13.33: 将容器导入为镜像的示例

- `inspect`: 此参数之前描述过，`--format` (`-f`) 选项允许从详细信息中访问特定数据。所需的格式为`{{ .Config.Hostname }} web {{ .Category }}`。图 13.34 显示了一些示例：

```bash
root@ubuntu:~# docker inspect -f "{{ .Config.Hostname }}" web
c6812ed649b
root@ubuntu:~# docker inspect -f "{{ .NetworkSettings.IPAddress }}" web
172.17.0.2
root@ubuntu:~# docker inspect -f "{{ .NetworkSettings.MacAddress }}" web
02:42:ac:11:00:02
root@ubuntu:~# docker inspect -f "{{ .State.Status }}" web
running
```

图 13.34: 检查容器的示例

- 默认情况下，当容器删除时，容器内部的数据将会丢失。容器内部可以实现持久化存储。使用`volume` (`-v`) 选项，可以指定运行`Docker`守护进程服务器上的一个目录，并将其挂载到容器内部。图 13.35 显示了如何使用目录来存储容器将使用的`HTML`文件。
