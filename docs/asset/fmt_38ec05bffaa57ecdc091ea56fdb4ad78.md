
`[user@host ~]$ podman exec -it client01 ping -c 3 10.87.0.3 | grep 'packet loss'`

3 packets transmitted, 3 received, 0% loss, time 2054ms

```
> 参考文献
`podman(1)`, `podman-exec(1)`, `podman-info(1)`, `podman-network(1)`, `podman-network-create(1)`, `podman-network-inspect(1)`, `podman-network-ls(1)`, `podman-port(1)`, `podman-run(1)`, and `podman-unshare(1)` man pages
更多信息，请参阅《Red Hat Enterprise Linux 9 上的构建、运行和管理 Linux 容器》指南中的“处理容器”部分，网址为 https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html-simple/building_running_and_managing_containers/assembling_working-with-containers_building-running-and-managing-containers

## 引导练习

# 管理容器存储和网络资源

在此练习中，你将在创建容器期间向容器传递环境变量，为容器挂载持久化存储，创建并连接多个容器网络，并从宿主机暴露容器端口。

## 学习目标

- 创建容器网络并将其连接到容器。
- 故障排除故障的容器。
- 在创建期间向容器传递环境变量。
- 为容器创建并挂载持久化存储。
- 将宿主机端口映射到容器内部端口。

### 在开始之前

作为工作站机器上的 `student` 用户，使用 `lab` 命令为你的练习准备系统。

此命令将准备你的环境并确保所有所需的资源均可用。

```
[student@workstation ~$] lab start containers-resources \
```

## 指令

- 1. 以 `student` 用户身份登录 `servera`。

```
[student@workstation ~$] ssh student@servera
--output omitted.
[student@servera ~$]
```

- 2. 创建前端 容器网络。创建 db_subnet 和 db_01 容器并将它们连接到前端 网络。

- 1. 使用 `pod network create` 命令的 `--subnet` 和 `--gateway` 选项创建一个子网段为 10.89.1.0/24、网关为 10.89.1.1 的 frontend 网络。

```
[student@servera ~$] pod network create --subnet 10.89.1.0/24 \
--gateway 10.89.1.1 frontend
frontend
```

- 2. 登录到 registry.lab.example.com 注册表。

```
$studentserver~$ podman login registry.lab.example.com
Username: admin
Password: redhat321
Login Succeeded!
```

- 2.3. 创建连接到 frontend 网络的客户端容器。将容器内的 `/etc/yum.repos` DNF 目录挂载到 `/etc/yum.repos` 以添加包安装功能。

```
$studentserver~$ podman run -d --name db_client \
--network frontend \
-v /etc/yum.repos:/etc/yum.repos \
registry.lab.example.com/ubi9-beta/ubi \
sleep infinity
02ed0fd7e39z2abe4b73ea3c25ec6b7ef95d16af9cedd50d688f997a663ba6c15
```

- 2.4. 创建连接到 frontend 网络的 db_01 容器。

```
$studentserver~$ podman run -d --name db_01 --network frontend \
registry.lab.example.com/rhel8/mariadb-db-105
3e76ea7ae6ea4571815a2916b52eba5e9c8ef03a26998d8be2736b8b45bab05
```

- 2.5. 查看所有容器。

```
$studentserver~$ podman ps -a
CREATED IMAGE STATUS PORTS COMMAND
02ed0fd7e39z2abe4b73ea3c25ec6b7ef95d16af9cedd50d688f997a663ba6c15 registry.lab.example.com/ubi9-latest sleep infinity 56 seconds ago Up 56 seconds db_client
3e76ea7ae6ea4571815a2916b52eba5e9c8ef03a26998d8be2736bb8b45bab05 registry.lab.example.com/rhel8/mariadb-db-105 mysqld 1 second ago Exited (1) db_01
```

- 3. 故障排除 db_01 容器并确定它未运行的原因。

  - 3.1. 查看 db_01 的日志并确定它未运行的原因。

```
$studentserver~$ podman logs db_01
output omitted...
  You must指定以下环境变量:
  MYSQL_USER
  MYSQL_PASSWORD
  MYSQL_DATABASE
```

  - 3.2. 删除 db_01 容器并使用所需的环境变量重新创建它。

```
[student@servera] podman rm db_01
3e76ea7ae6ea4571815a2916b52eba5e9c8ef03a26998d8be2736bb8b45bab05
```

```
[student@servera] podman run -d --name db_01 --network frontend \
registry.lab.example.com/rhel8/mariadb-db-105
-e MYSQL_USER=admin \
-e MYSQL_PASSWORD=redhat321 \
-e MYSQL_DATABASE=db_net
```

- 3.3. 查看所有容器。

```
$studentserver~$ podman ps -a
```

# 容器

```
[student@workstation]$ mysql -u dev1 -p h server --port 1306 \
devb -e 'SHOW TABLES';
Enter password: devpass
+----
| Tables_in_devdb |
+-----+
| crucial_data |
+-----+
```

- 5. 创建一个名为 backend 的第二个容器网络，并将 backend 网络连接到 db_client 和 db_01 容器。测试容器11. 容器之间的网络连通性和 DNS 解析。

5.1. 创建具有 10.90.0.0/24 子网和 10.90.0.1 网关的 `backend` 网络。

```
[student@server]$ podman network create --subnet 10.90.0.0/24 \
gateway 10.90.0.1 backend
```

5.2. 将 `backend` 容器网络连接到 `db_client` 和 `db_01` 容器。

```
[student@server]$ podman network connect backend db_client \
[student@server]$ podman network connect backend db_01
```

5.3. 获取 `db_01` 容器的 IP 地址。

```
[student@server]$ podman inspect db_01 \
...output omitted...\
  "Networks": {
    "backend": {
      "EndpointID": "",
      "Gateway": "10.90.0.1",
      "IPAddress": "10.90.0.3",
    ...output omitted...\
```
