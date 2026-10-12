
```
opc@portainer2 ~$ sudo docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
Unable to find image 'portainer-ce:latest' locally
latest: Pulling from portainer/portainer-ce
7222778261: Pull complete
96df13bef7: Pull complete
517116dbf2: Pull complete
a1a3d4c44f2: Pull complete
b62279b77: Pull complete
clcad9f5200f: Pull complete
8a7701fc2b: Pull complete
d6db8d4974: Pull complete
c6fd0bfc1c: Pull complete
88920068c61: Pull complete
4af700ef5f: Pull complete
Digest: sha256:98a561869fa3df0b6427113ea09629291f5c2fc557de39796
Status: Downloaded newer image for portainer-ce:latest
89b379c137ab4f6b3fd62118039fed674a7351a5fc038215a4a8b
```

Portainer 已安装，下一步运行 `docker ps` 查看正在运行的容器及其 Docker 状态。

| 容器 | 镜像 | 创建 | 状态 | 端口 | 名称 |
| --- | --- | --- | --- | --- | --- |
| 89b379c137ab | portainer/portainer-ce:latest | weeks ago | Up 2 minutes | 8000/tcp, 943/tcp, 0.0.0.0:9000/tcp, :::9000/tcp | portainer |

4. 一旦 Docker 安装且 `docker ps` 显示 Portainer 正在运行，我们必须确保 OCI 配置允许端口 9000 可见。为此我们需要通知 OCI 我们正在工作的虚拟云网络 `VCN` 以开放该端口。

### 网络 › 虚拟云网络 › vb-oci-test › 安全列表详情

![](img/110fa0d6324f93fff03cee639414d_471_0.png)

进入相应的安全列表后，我们需要创建一个如下截图所示的规则。

![](img/110fa0d6324f93fff03cee639414d_471_1.png)

### 入站规则

![](img/110fa0d6324f93fff03cee639414d_472_0.png)

图 13.20 – VCN 安全列表创建

| 源类型 | 源 CIDR | IP 协议 |
| :--- | :--- | :--- |
| CIDR | 0.0.0.0/0 | TCP |

规则创建后，我们可以在 OCI 外部看到该端口。

|  | 源 CIDR | 协议 | 优先级 | 范围 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 1 | 0.0.0.0/0 | TCP | All | 9000 | 端口 9000 的 TCP 流量 |

21 安全列表规则

我们可以打开浏览器并访问 Portainer UI。要访问 UI 需要两个项：VM 的公网 IP 和端口。以下截图显示端口 `9000`，IP 与我们使用 `ssh` 登录 VM 时使用的 IP 相同。

你也可以在 OCI 控制台上找到 IP。从 **Compute**（计算）菜单导航到 VM，然后进入 **Instance**（实例），这将带你进入 OCI 控制台菜单中的所有 VM。然后如截图所示复制 VM 的 IP 地址。

### 实例访问

你使用安全 Shell `SSH` 连接到运行中的 Linux 实例。你需要创建实例时使用的 SSH 密钥的私钥。

**公网 IP 地址：** `132.226.58.24`

**用户名：** `opc`

图 22 – VM 的 IP

* 一旦获得地址，打开浏览器并在表单 `https://<IP>:9000` 中输入该信息。在我们情况下，这是 `https://<IP>:9000`。

注意：如果遇到如下过期页面，可能需要刷新：

![](img/110fa0d6324f93fff03cee639414d_473_0.png)

### 新 Portainer 安装

出于安全考虑，你的 Portainer 实例超时。要重新启用 Portainer 实例，你需要重启 Portainer。更多信息请参阅我们的文档。

图 13.23 – Portainer 落地页

6. 为了刷新，你需要通过运行 `docker restart` 命令来重启：

```
opc@portainer ~}$ sudo docker restart portainer

portainer
```
