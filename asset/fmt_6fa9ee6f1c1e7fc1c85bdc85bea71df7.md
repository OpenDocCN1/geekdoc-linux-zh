
要启动 Kubernetes 交互式教程，请从浏览器中访问以下 URL：

```
https://kubernetes.io/docs/tutorials/basics
```

图 31.1 显示了 Kubernetes 基础教程的开始。此时，你可以按照提示完成教程。由于该教程启动了一个实时集群，你也可以使用该界面尝试其他命令。

# 第 31 章：使用 Kubernetes 部署容器应用程序

## 启动你的集群

以具有 `sudo` 权限的用户身份运行 `minikube start`。如果一切顺利，`minikube` 将会找到你的虚拟化管理程序并创建 `minikube` 控制平面。此时，你可以尝试在你的集群上执行一些 `kubectl` 命令并运行一些容器化应用程序。

## 安装 kubectl 命令

获取一个与你 `Minikube` 中 Kubernetes 版本保持在一个版本以内的 `kubectl` 命令版本。安装最新版本的 `kubectl` 和 `minikube` 应该可以解决这个问题。输入以下内容：

```bash
$ curl -LO https://storage.googleapis.com/kubernetes-release/release -s https://storage.googleapis.com/kubernetes-release/release/stable.txt | xargs /bin/linux/amd64/kubectl
$ mv kubectl /usr/local/bin/kubectl
$ chmod 755 /usr/local/bin/kubectl
```

严格来说，你不需要获取 `kubelet` 二进制文件，因为 `minikube` 已经内置了。例如，你只需要运行 `minikube get node`。但在其他环境中，你将 `kubectl` 作为独立的命令使用。

# 运行 Kubernetes 基础教程

Kubernetes 基础教程将带你通过一系列良好的命令来熟悉 Kubernetes：

https://kubernetes.io/docs/tutorials/kubernetes-basics/

以下内容将带你浏览 Kubernetes 教程页的前五个模块，请继续并启动 Minikube (`minikube start`)。如果你已经在笔记本电脑上运行的虚拟机中使用 Minikube，你仍然可以遵循此步骤。由于两者都使用 Minikube，步骤是相同的。

## 获取关于集群的信息

运行这些命令来获取关于你集群的基本信息：

### Minikube 版本

要查看你正在使用的 `minikube` 版本，输入以下内容：

```bash
$ minikube version
minikube version: v1.35.0
commit: dd5d320e41b5451cdcf3c0189bc4e1d38195866ed-dirty
```

### 集群信息

要查看 Kubernetes 主节点和 DNS 服务可 URL，输入以下内容：

```bash
$ kubectl cluster-info
Kubernetes control plane is running at https://localhost:36473
CoreDNS is running at https://localhost:36555/api/v1/namespaces/kube-system/services/kube-dns/proxy
```

### 列出节点信息

要查看运行的节点数量（Minikube 只有一个主节点）及其状态，输入以下内容：

```bash
$ kubectl get nodes
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   23m   v1.32.0
```

### 列出集群和客户端版本

要查看 `kubectl` 客户端和 Kubernetes 集群的版本（以确保它们彼此在一个版本以内），输入以下内容：

```bash
$ kubectl version
Client Version: v1.31.0
Kustomize Version: v5.4.2
Server Version: v1.32.0
```

> 为了进一步调试和诊断集群问题，请使用 `kubectl cluster-info dump`。

# 部署 Kubernetes 应用程序

在 Kubernetes 集群上运行许多容器化应用程序（以 pod 形式）被称为部署（deployment）。当创建一个部署时，将由 Kubernetes 集群确保请求的 pod 始终在运行。它通过以下操作实现这一点：

- 通过 API 服务器接受部署的创建
- 请求调度器在可用节点上运行每个 pod 中请求的容器
- 监控 pod 以确保它们按照请求继续运行
- 如果 pod 失败（例如，容器停止运行），则启动 pod 的新实例（在相同或不同节点上）

教程展示了如何从容器镜像创建一个简单部署的示例。在示例中，你为它指定了一个名称并标识了要使用的容器镜像。部署的其他设置将使用默认值。

### 创建部署

要启动部署名为 `kubernetes-bootcamp` 并拉取 `kubernetes-bootcamp` 的部署，输入以下内容：

```bash
$ kubectl create deployment kubernetes-bootcamp \
  --image=gcr.io/google-samples/kubernetes-bootcamp:v1
deployment.apps/kubernetes-bootcamp created
```

### 列出部署

要查看部署是否存在（并且请求了一个实例且运行了一个实例），输入以下内容：

```bash
$ kubectl get deployments
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   1/1     1            1           4m38s
```

### 描述部署

要查看有关部署的详情，输入以下内容：

```bash
$ kubectl describe deployments kubernetes-bootcamp
Name: kubernetes-bootcamp
Namespace: default
Replicas: 1 desired | 1 updated | 1 total | 1 available
0 unavailable
...
Pod Template:
  Labels: app=kubernetes-bootcamp
  Containers:
  kubernetes-bootcamp:
    Image: gcr.io/google-samples/kubernetes-bootcamp:v1
    Port: <none>
    Host Port: <none>
    Environment: <none>
    Mounts: <none>
  Volumes: <none>
```

在 `kubernetes-bootcamp` 部署中，注意它设置与部署关联的一个 pod 实例（副本）为可用。部署运行在当前命名空间中，称为 `default`。同样注意 `default` 没有挂载任何端口或卷。

# 获取部署的 pod 信息

通过部署，你可以请求关于 pod 的信息，并通过服务从虚拟机暴露 Kubernetes API，以便直接连接到 pod。

### 将 Kubernetes API 暴露到本地系统

要从 Minikube 中运行的 Kubernetes API 开启代理 (`kubectl proxy`)，输入以下内容：

```bash
$ kubectl proxy
```

### 查询 Kubernetes API

打开第二个终端，通过输入以下内容查询在 Minikube 上运行的 Kubernetes API：

```bash
$ curl http://localhost:8001/version
{
  "major": "1",
  "minor": "32",
  "gitVersion": "v1.32.0",
  "gitCommit": "70d3cc98aa821cd1fb125688902dbf53",
  "gitTree": "clean",
  "buildDate": "2024-12-11T17:59:15Z",
  "goVersion": "go1.23.3",
  "compiler": "gc",
}
```

### 获取 pod 的信息

通过输入以下内容查询在 Minikube 上运行的 Kubernetes API 以获取 pod 信息：

```bash
$ kubectl get pods
NAME                                 READY   STATUS    AGE
kubernetes-bootcamp-76856766-v7p2    1/1     Running   4m
```

### 连接到 pod

通过输入以下内容查看在部署中运行的 pod：

```bash
$ kubectl get pods
NAME                                 READY   STATUS    AGE
kubernetes-bootcamp-76856766-v7p2    1/1     Running   4m
```

### 查看日志

要查看 pod 内任何容器的日志，运行以下命令：

```bash
$ kubectl logs kubernetes-bootcamp-76856766-v7p2
2025-04-12T07:54:04
```

### 在 pod 上执行命令

使用 `kubectl exec` 在 pod 中运行命令。第一个命令运行 `env` 显示 pod 内部的环境变量，第二个命令在 pod 中打开一个 shell，你可以运行：

```bash
$ kubectl exec -it kubernetes-bootcamp-76856766-v7p2 -- env
PATH=/usr/local/bin:/usr/bin:/usr/bin:/bin
HOSTNAME=kubernetes-bootcamp-76856766-v7p2
KUBERNET_SERVICE_HOST=10.0.0.1
KUBERNET_SERVICE_PORT=443
```

```bash
$ kubectl exec -it kubernetes-bootcamp-76856766-v7p2 -- bash
root@kubernetes-bootcamp-76856766-v7p2# date
Sat Apr 12 07:58:00 2025
root@kubernetes-bootcamp-76856766-v7p2# exit
```

# 第六部分：与云计算交互

## 使用 Kubernetes 暴露服务

在这些过程中，为了暴露 `kubernetes-bootcamp` pod，使其能够从运行它的工作节点的外部 IP 地址进行访问，你可以创建一个 `NodePort` 服务。以下是实现方法之一：

### 检查 pod 是否正在运行

输入以下命令查看 `kubernetes-bootcamp` pod 是否正在运行：

```bash
$ kubectl get pods
NAME                                 READY   STATUS    RESTARTS   AGE
kubernetes-bootcamp-9bc5d8d6-7g6dr   1/1     Running   0          26m
```

### 检查服务

输入以下命令查看默认命名空间中的服务。请注意，只有 `kubernetes` 服务是可用的，目前没有在集群外暴露 `kubernetes-bootcamp` pod 的服务：

```bash
$ kubectl get services
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   31m
```

### 创建一个服务

创建一个使用 `NodePort` 的服务，以便通过特定端口号（8080）的 IP 地址访问 pod。例如，以下命令：

```bash
$ kubectl expose deployment/kubernetes-bootcamp --type=NodePort --port 8080
service/kubernetes-bootcamp exposed
```

### 查看新服务

输入以下命令查看宿主机上可用服务的 IP 地址（10.96.66.230）和端口号（8080）：

```bash
$ kubectl get services
NAME                  TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes            ClusterIP  10.96.0.1      <none>        443/TCP          33m
kubernetes-bootcamp   NodePort   10.96.66.230   <none>        8080:30128/TCP   5s
```

```bash
$ kubectl describe service/kubernetes-bootcamp
Name: kubernetes-bootcamp
Namespace: default
Labels: app=kubernetes-bootcamp
Annotations: <none>
Selector: app=kubernetes-bootcamp
Type: NodePort
IP Family Policy: SingleStack
IP Families:
IP: 10.106.58.189
IPs: 10.106.58.189
Port: <unset> 8080/TCP
TargetPort: <unset> 30128/TCP
```

### 获取分配的节点端口

要获取分配给服务的端口并将 `$NODE_PORT` 变量设置为该值，请输入以下命令：

```bash
$ NODE_PORT=$(kubectl get services/kubernetes-bootcamp \
-o go-template='{{(index .spec.ports 0).nodePort}}')

$ echo NODE_PORT=$NODE_PORT
NODE_PORT=30000
```

### 访问服务

要检查是否可以通过 `NodePort` 访问服务，请使用以下 `curl` 命令（使用你 minikube 实例的 IP 地址）：

```bash
$ curl $(minikube ip) $NODE_PORT
Running on: kubernetes-bootcamp-9bc58d867
```

## 为服务打标签

标签（Labels）提供了对 Kubernetes 中 pod、节点或其他对象分组的方法。使用标签，你可以执行诸如确保只有带有特定标签的 pod 运行在选定节点上的操作。你可以通过标签识别 pod，以便找到并对其进行操作。标签以键/值对的形式设置。使用此过程为现有服务添加标签。

### 检查 pod 的标签

`kubernetes-bootcamp` 是分配给该 pod 的唯一标签。为了确认这一点，请输入以下命令：

```bash
$ kubectl describe deployment kubernetes-bootcamp
Name:
Namespace: default
CreationTimestamp: Sat, 12 Apr 2025 03:39:50 -0400
Labels: app=kubernetes-bootcamp
Annotations: deployment.kubernetes.io/revision:1
...
```

### 为 pod 添加另一个标签 (v1)

获取 pod 的名称并将其作为新标签添加：

```bash
$ POD_NAME=$(kubectl get pods -o go-template --template='{{range .items}}{{.metadata.name}}{{end}}')
$ kubectl label pod $POD_NAME version=v1
pod/kubernetes-bootcamp-9bc58d867-76dr labeled
```

### 检查并使用标签

检查 `version=v1` 标签是否已分配给 pod，然后使用该标签列出 pod 的信息：
