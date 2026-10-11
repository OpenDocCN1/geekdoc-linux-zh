
*列表 8-1：尝试访问 API 服务器上的默认 `/api` 路由*

啊，我们被锁在外面了。我们得到的响应并不令人意外。从 1.8 版本开始，Kubernetes 发布了角色基于访问控制（RBAC）的稳定版本，这是一种锁定对 API 服务器的访问以防止未经授权用户的

这个官僚式疯狂的最后一块拼图是 `kubelet`：一个在每个工作节点上运行的进程（不是 pod！），它会定期从 API 服务器拉取它应该运行的 pod 列表。`kubelet` 发现其主机应该再运行两个额外的容器，于是它通过容器运行时（通常是 Docker）启动它们。我们的 pod 最后终于活了过来。复杂？我就说嘛。但不可否认这种同步机制的美妙之处。尽管我们只涵盖了众多可能交互中的一种工作流，请放心，你应该能够跟上关于 Kube 的几乎每篇文章。我们甚至准备好进入下一步——因为，免得你忘了，我们在 MXR Ads 仍有一个真实的集群在等待着我们。

### 资源
- 关于桥接和桥接池的更多细节可在 Docker 文档中找到：https://docs.docker.com/network/bridge/
- 在 Amazon Elastic Kubernetes Service (EKS) 上的 Pod 直接插入 Elastic 网络接口，而不是使用桥接网络；详情请参阅 https://amzn.to/37Rfj5c。
- 有关 Kubernetes pod 到 pod 网络的更多信息，请参阅 http://bit.ly/3a0hJjX。
- 这是有关从外部访问集群的其他方式的概述：http://bit.ly/30aGqFU。
- 有关 etcd 的更多信息，请参阅 http://bit.ly/36MAjKr 和 http://bit.ly/2sds4bg。
- 通过未认证 API 入侵 Kubernetes 的内容可在 http://bit.ly/36NBk4S 找到。

## 8
## 肖申克的救赎：越狱

![](img/961e81aef23040d0fbe348f58c055860_141_0.png)

带着对 Kubernetes 的这一新理解，我们回到调查应用程序上的临时远程 shell，以收集信息、提升权限，并希望找到有关用户定位的有趣数据。

我们恢复对 `surveyapp` 容器的早期 shell 访问并查看环境变量：

```
shell> env

KUBERNETES_SERVICE_PORT_HTTPS=443

KUBERNETES_PORT_443_TCP_PORT=443

KUBERNETES_PORT_443_TCP=tcp://10.100.0.1:443
```

凭借我们的新知识，这些环境变量有了新的含义：`KUBERNETES_PORT_443_TCP` 必须指的是隐藏 API 服务器的集群 IP，即著名的 Kube 编排器。文档指出 API 遵循 OpenAPI 标准，因此我们可以使用臭名昭著的 `curl` 工具来访问默认的 `/api` 路由。`curl` 中的 `-L` 开关会跟随 HTTP 重定向，而 `-k` 开关则忽略 SSL 证书警告。我们在列表 8-1 中尝试一下。

```
shell> curl -Lk https://10.100.0.1/api

message: forbidden: User "system:anonymous" cannot get path "/api",

reason: Forbidden
```

*列表 8-1：尝试访问 API 服务器上的默认 `/api` 路由*

啊，我们被锁在外面了。我们得到的响应并不令人意外。从 1.8 版本开始，Kubernetes 发布了角色基于访问控制（RBAC）的稳定版本，这是一种锁定对 API 服务器的访问以防止未授权用户的

这个官僚式疯狂的最后一块拼图是 `kubelet`：一个在每个工作节点上运行的进程（不是 pod！），它会定期从 API 服务器拉取应运行的 pod 列表。`kubelet` 发现主机应再运行两个容器，于是通过容器运行时（通常是 Docker）启动它们。我们的 pod 终于活了。复杂？我就说嘛。但这种同步机制的美妙不可否认。尽管只涵盖了众多交互中的一种工作流，请放心，你应能跟上几乎所有关于 Kube 的文章。我们也准备进入下一步——因为别忘了，MXR Ads 仍有一个真实集群在等着我们。

### 资源
- 关于桥接和桥接池的更多细节可在 Docker 文档中找到：https://docs.docker.com/network/bridge/
- 在 Amazon Elastic Kubernetes Service (EKS) 上的 Pod 直接接入 Elastic 网络接口，而非使用桥接网络；详情见 https://amzn.to/37Rfj5c。
- 有关 Kubernetes pod 到 pod 网络，请参阅 http://bit.ly/3a0hJjX。
- 从外部访问集群的其他方式概述：http://bit.ly/30aGqFU。
- 有关 etcd 的更多信息，请参阅 http://bit.ly/36MAjKr 和 http://bit.ly/2sds4bg。
- 通过未认证 API 入侵 Kubernetes 详见 http://bit.ly/36NBk4S。

## 8
## 肖申克的救赎：越狱

![](img/961e81aef23040d0fbe348f58c055860_141_0.png)

带着对 Kubernetes 的新理解，我们回到调查应用上的临时远程 shell，收集信息、提升权限，并希望找到用户定位的有趣数据。

我们恢复对 `surveyapp` 容器的早期 shell 访问并查看环境变量：

```
shell> env

KUBERNETES_SERVICE_PORT_HTTPS=443

KUBERNETES_PORT_443_TCP_PORT=443

KUBERNETES_PORT_443_TCP=tcp://10.100.0.1:443
```

凭借新知识，这些环境变量有了新含义：`KUBERNETES_PORT_443_TCP` 必须指向隐藏 API 服务器的集群 IP，即著名的 Kube 编排器。文档指出 API 遵循 OpenAPI 标准，可用臭名昭著的 `curl` 工具访问默认 `/api` 路由。`curl` 的 `-L` 开关会跟随 HTTP 重定向，`-k` 开关忽略 SSL 证书警告。我们在列表 8-1 中尝试。

```
shell> curl -Lk https://10.100.0.1/api

message: forbidden: User "system:anonymous" cannot get path "/api",

reason: Forbidden
```

*列表 8-1：尝试访问 API 服务器上的默认 `/api` 路由*

啊，我们被锁在外面了。响应并不意外。从 1.8 版本起，Kubernetes 发布了稳定的角色基于访问控制 RBAC，用于锁定 API 服务器对未授权用户的访问。即使监听在 8080 端口的“不安全”API 也仅限 localhost：

```
shell> curl -L http://10.100.0.1:8080

(timeout)
```

为绕过此限制，我们将更仔细地查看 Kubernetes RBAC 系统。

## Kube 中的 RBAC

Kubernetes RBAC 采用相当标准的实现。管理员可为人工操作员创建用户账户，或可分配给 pod 的服务账户。每个用户或服务账户再绑定到一个角色，该角色对 pod、节点、secret 等资源拥有 get、list、change 等特定权限。主体（用户或服务账户）与角色的关联称为绑定。

> NOTE Kubernetes 中的 `secret` 是存储在 `etcd` 数据库中并受访问控制的敏感数据片段。它提供了一种替代方案，避免在 pod 清单中硬编码密码。`secret` 在运行时通过环境变量或挂载的文件系统注入。

服务账户、角色及其绑定与其它 Kube 资源一样，均定义在存储于 `etcd` 数据库的清单文件中。服务账户的定义类似列表 8-2。

```
# define a service account

apiVersion: v1

kind: ServiceAccount  # deploy a service account

metadata:

  name: metrics-ro  # service account's name

--

# Bind metrics-ro account to cluster admin role

apiVersion: rbac.authorization.k8s.io/v1

kind: ClusterRoleBinding

metadata:

  name: manager-binding # binding's name

subjects:

- kind: ServiceAccount

  name: metrics-ro  # service account's name

  apiGroup: ""

roleRef:

  kind: ClusterRole
```
