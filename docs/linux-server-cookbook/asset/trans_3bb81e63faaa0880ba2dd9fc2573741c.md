

root@ubuntu:~# docker history ubuntuapache2:0.1
IMAGE     CREATED    CREATED BY      SIZE
f1715312940c 5 days ago /bin/sh -c #(nop)  CMD ["/bin/sh" -c"] /usr... 0B
14efd05a5ac0 5 days ago /bin/sh -c #(nop)  EXPOSE 80 0B
99dfd22d79d5 5 days ago /bin/sh -c #(nop)  COPY file:34aeb59838c5612... 10B
dd122fabfbfc 5 days ago /bin/sh -c echo "Image generated" > /var/ww... 16B
e456d9e2e1f3 5 days ago /bin/sh -c apt-get update && apt-get install... 147MB
cdb68b45541a 13 days ago /bin/sh -c #(nop)  CMD ["bash"] 0B
<missing> 13 days ago /bin/sh -c #(nop) ADD file:ba96f963b0bfd429a0... 77.8MB

*图 13.41：* 使用参数 history 的输出示例

生成的镜像将在本地可用，并且可以基于它创建容器。图 13.42 展示了一个示例：

root@ubuntu:~# docker images | head -2
REPOSITORY  TAG  IMAGE ID     CREATED  SIZE
ubuntuapache2  0.1  f1715312940c  4 minutes ago  225MB

root@ubuntu:~# docker run -dti -p 8888:80 ubuntuapache2:0.1
856cc9dfb66eaf9dd5400ba69a953a28a4d039ce798c5dc21fa6002ac703fb9b

root@ubuntu:~# curl http://localhost:8888/
Image generated

root@ubuntu:~# curl http://localhost:8888/test.html
Test file

*图 13.42：* 从生成的镜像创建容器的示例

Dockerfile 中可用的其他有用语句在表 13.2 中有描述：

| 语句 | 描述 |
| :--- | :--- |
| LABLE | 向镜像添加元数据。例如维护者、软件版本或其他任何信息。 |
| ADD | 向镜像中添加文件。与 COPY 的区别有两点：<br>• 如果指定的是目录，则只复制内容而不包括父目录。<br>• 如果要添加的文件是压缩文件，它将自动解压。 |
| ENTRYPOINT | 默认情况下，容器用于执行使用 /bin/sh 指定的命令。使用此语句可以更改此行为，将其他命令指定为入口点。 |
| VOLUME | 指定要创建以实现持久化存储的卷。 |
| USER | 指定用于执行 Dockerfile 中指定命令的用户。 |
| WORKDIR | 设置容器内的工作目录。 |
| ENV | 设置镜像内的环境变量。 |
| ARG | 指定可以使用 --build-args 选项接受的参数。 |
| HEALTHCHECK | 指定健康检查测试，以确保容器正常工作。 |

# *表 13.2：Dockerfile 中可用的语句*

生成**镜像**后，可以将其发布到公共注册表，例如 [https://hub.docker.com](https://hub.docker.com) 或 [https://www.quay.io](https://www.quay.io)。可以创建免费账户用于个人使用并存储已创建的镜像。也有针对公司的其他计划。创建账户后，可以使用 **docker** 命令的 **login** 参数在发布所需的**镜像**之前执行登录操作。*图 13.43* 显示了登录 **Docker Hub** 的示例。

```
root@ubuntu:~# docker login docker.io
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: linuxservercb
Password:
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store
Login Succeeded
```

# *图 13.43：登录 Docker Hub 的示例*

登录成功后，需要按照目标存储库的正确格式对**镜像**进行*标记*。对于 **Docker Hub**，格式为 **docker.io/USERNAME/name:image:tag**。当**镜像**具有正确的名称后，**publish** 参数将上传并在存储库中创建该镜像。*图 13.44* 显示了标记和发布任务：

```
root@ubuntu:~# docker tag ubuntuapache2:0.1 docker.io/linuxservercb/ubuntuapache
root@ubuntu:~# docker push docker.io/linuxservercb/ubuntuapache
Using default tag: latest
The push refers to repository [docker.io/linuxservercb/ubuntuapache]
ddf96998d2d7: Pushed
0ff7c267b89e: Pushed
bcebf94eb56: Pushed
7ea4455e747e: Mounted from library/ubuntu
latest: digest: sha256:58557aced96f8d9371782e92ba6e418e15ea0992e4c83c8659f6f21cee
d26381 size: 1155
```

# *图 13.44：将镜像推送到 Docker Hub 的示例*

镜像发布后，该*镜像*将在 **Docker Hub** 门户中可用。由于该镜像未指定任何*镜像*标签，因此它在本地和*注册表*中都被标记为 *latest*。*图 13.45* 显示了已发布镜像的 **Docker Hub** 门户：

![](img/863afa537de4eed7deb11978bfbfa90e_460_0.png)

*图 13.45：Docker Hub 门户示例*

该镜像可以从另一个系统下载，如*图 13.46*所示。

```
[root@rhel ~]# docker pull linuxservercb/ubuntuapache
Using default tag: latest
latest: Pulling from linuxservercb/ubuntuapache
301a8b74f71f: Pull complete
ceabe2bc817b: Pull complete
ec49d2122720: Pull complete
76f631053f2e: Pull complete
Digest: sha256:58557aced96f8d93717829e2ba6418e15ea0992e4c83c8659f6f21cead26381
Status: Downloaded newer image for linuxservercb/ubuntuapache:latest
docker.io/linuxservercb/ubuntuapache:latest
```

*图 13.46：从公共存储库拉取镜像的输出示例*

与*容器*一样，*镜像*也可以通过检查来获取有关它的详细信息。使用参数 **image inspect**，后跟*镜像 ID*或名称，信息将显示在屏幕上。以下代码（截断）显示了之前下载的镜像的输出：

```
[
    {
      "Id":
      "sha256:f1715312940c0c43b4c5d7b01d78a4106d4532df429611fd993887da6de71
      584",
      "RepoTags": [
        "linuxservercb/ubuntuapache:latest"
      ],
      "RepoDigests": [
        "linuxservercb/ubuntuapache@sha256:58557aced96f8d937178
        29e2ba6e418e15ea0992e4c83c8659f6f21cead26381"
      ],
      (omitted)
      "Config" : {
        (omitted)
        "Cmd" : [
          "/bin/sh",
          "-c",
          "/usr/sbin/apache2ctl -D FOREGROUND"
        ],
        "Image":
        "sha256:14efd05a5ac026c330095be5c09f8bcfd0b6c82da8dc2853c7aaeaf4e
        9c1e19",
      },
      "Architecture" : "amd64",
      "OS" : "linux",
      "Size" : 225124187,
      "VirtualSize": 225124187,
      (omitted)
    },
    "RootFS" : {
      "Type": "layers",
      "Layers": [
        "sha256:7ea4455e747ead87d6cc1c4efaf3a79530a931a0856a9f9ce9ac2d8
        d45bd3c28",
        "sha256: bcebbf94eb56506a9f1f6bc38f5a6bbf1fc74d03af0cb44eb137ad6
        e107279fa",
        "sha256:0ff7c267b89e80ad4571a737758fa48f57a80cbddc52351bbab565c
        70b875c77",
        "sha256:ddf9698d2d70c418c2abe60746ff92b58dffdd16fa68d3fd4cdca
        9366c5a85"
      ]
    },
    (omitted)
  }
]
```

可以运行私有的**镜像注册表**，以便不全局发布生成的镜像。这通常是企业内部开发的自定义应用所必需的。运行私有**镜像注册表**有不同的替代方案；最流行且最简单的方式是使用 **Docker** 提供的**镜像**。该镜像的名称和版本为 **registry:2**。要在系统外部暴露它，需要使用 SSL 证书来接受来自远程源的连接。以下代码用于生成自签名证书：

```
openssl  req   -newkey rsa:4096 -nodes -sha256 -keyout certs/domain.key \ -addext  "subjectAltName = DNS:registry.example.com" \ -x509 -days 365 -out certs/domain.crt \ -subj "/C=ES/ST=Madrid/L=Madrid/O=example/OU=com/CN=registry.example.com"
```

使用 **docker** 及其参数 **run** 执行镜像注册表，使用镜像 **registry:2**。环境变量指定了证书的位置。

```
docker run -d --restart=always --name registry -v "$(pwd)"/certs:/certs \ -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt \ -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key \ -p 5000:5000 registry:2
```

要将**镜像**发布到专用的**镜像注册表**，必须指定服务器的 DNS 名称或 IP，后跟服务运行所在的端口。[图 13.47](#) 显示了如何标记和发布镜像：

![](img/863afa537de4eed7deb11978bfbfa90e_462_0.png)

*图 13.47：将镜像推送到本地注册表的示例*

非官方存储库应添加到文件 */etc/docker/daemon.json* 中。需要重启守护进程才能获取新配置。之后，可以从配置的注册表中发布和拉取镜像。

# Podman

