
在这里，使用 NGINX 开启 `compress` 的配置如下：

| 行 | 内容 |
| :--- | :--- |
| 45 | AddOutputFilterByType DEFLATE image/svg+xml |
| 46 | AddOutputFilterByType DEFLATE image/x-icon |
| 47 | AddOutputFilterByType DEFLATE text/css |
| 48 | AddOutputFilterByType DEFLATE text/html |
| 49 | AddOutputFilterByType DEFLATE text/javascript |
| 50 | AddOutputFilterByType DEFLATE text/plain |
| 51 | AddOutputFilterByType DEFLATE text/xml |
| 52 | </IfModule> |
| 53 | DocumentRoot `/var/www/html` |
| 54 | </VirtualHost> |

- 部署 Kubernetes 基础服务
- 在 Kubernetes 中安装 WordPress
- 需要记忆的 `kubectl` 命令

### 目标

在本章结束时，我们将从安装一个干净的 Ubuntu Server 开始。然后，我们将学习如何设置 Kubernetes 主节点（master node）。当 Kubernetes 主节点运行时，我们将添加一个新的 Ubuntu Server 作为 Kubernetes 工作节点（worker node）。此并开始向我们的 Kubernetes 集群中添加工作负载。

在本章结束时，你将能够设置自己的 Kubernetes 集群并将服务部署到集群中。一旦集群设置完成，我们将继续添加集群服务以使用该集群。我们将添加一个负载均衡器来接收进入集群的流量。我们还将添加工具，通过日志和指标来监控我们的集群。添加一个存储系统以使我们的工作负载能够利用磁盘资源。当核心系统安装完成后，我们就可以将工作负载添加到集群中，就像 WordPress 一样，进入我们的集群中。

最后，一旦工作负载运行，我们还将查看一些用于排查 Kubernetes 集群故障的基础命令。

### 在 Ubuntu 上安装 Kubernetes

有多种工具可以在 Ubuntu Server 上安装 Kubernetes。Ubuntu 也有它自己的工具。然而，在这里，我们将研究 `kubeadm`，这是 Kubernetes 用于设置 Kubernetes 集群的工具。

我们将从干净的 Ubuntu Server 安装开始并安装我们的组件。然后，我们将开始设置我们的主节点。

一旦主节点运行，我们将工作节点连接到主节点。

# 安装 Kubernetes 依赖

在主节点和工作节点上运行以下命令。在我们可以开始安装 Kubernetes 集群之前，它将在我们的 Ubuntu Server 上安装所需的包。这个小的 bash 脚本是一种确保我们的 Ubuntu 节点在开始之前已更新并具有正确软件包和设置的简单方法。这为我们构建 Kubernetes 集群提供了良好的基础。

以下命令在主节点和工作节点上运行：

- `echo "First lets update this box"`
- `apt-get update`
- `apt-get upgrade -y`
- `echo "Lets get docker"`
- `apt-get update`
- `apt-get install \`
- `apt-transport-https \`
- `ca-certificates \`
- `curl \`
- `gnupg \`
- `lsb-release -y`
- `echo "Setup cri-o"`
- `export OS=ubuntu_22.04`
- `export CRIO_VERSION=1.28`
- `echo "deb http://download.opensense.org/repositories/devel/kubic/libcontainers:stable/$OS/*" sudo tee /etc/apt/sources.list.d/kubic:libcontainers:stable.list`
- `echo "deb http://download.opensense.org/repositories/devel/kubic/libcontainers:stable/crio-o:$CRIO_VERSION/$OS/*" sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable:crio-o:$CRIO_VERSION-VERSION.list`
- `curl -L https://download.opensense.org/repositories/devel/kubic/libcontainers:stable:crio-o:$CRIO_VERSION/$OS/Release.key | sudo apt-key add -`
- `curl -L https://download.opensense.org/repositories/devel/kubic/libcontainers:/stable/$OS/Release.key | sudo apt-key add -`
- `apt update`
- `sudo apt install cri-o-runc -y`

```
echo "Setup kubeadm"
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
br_netfilter
EOF

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sudo sysctl --system
```

```
apt-get update
apt-get install -y apt-transport-https ca-certificates curl
curl -fSL https://pkgs.k8s.io/core:/stable/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable/v1.28/deb //' | sudo tee /etc/apt/sources.list.d/kubernetes.list
apt-get update
apt-get install -y kubelet kubeadm
apt-mark hold kubelet kubeadm
```

同样，在我们的主节点上，安装 `kubectl` cli。`kubectl` 将是我们用来控制集群的命令。在主节点上安装它，如果你想从计算机连接到集群，请运行以下命令：

Kubernetes 无法在启用 `swap` 的情况下运行，因此我们需要禁用 `swap`。运行以下命令：`swapoff -a`

为了使其持久化，打开文件 `/etc/fstab` 并注释掉所示的 `swap` 行：

```
root@worker1:cat /etc/fstab
# /etc/fstab: 静态文件系统信息
# 使用 'blkid' 打印设备的唯一标识符；这可以配合 UUID= 使用是一种更稳健的设备命名方法，即使在添加和删除磁盘也能工作。查看 fstab(5)。
# <file> <mount point> <type>
```

| 32. | [https://kubernetes.io/docs/concepts/cluster-administration/addons/] |
| 33. | |
| 34. | 然后你可以通过在每个节点上以 root 身份运行以下命令加入任意数量的节点： |
| 35. | |
| 36. | `kubeadm join 192.168.122.162:6443 --token s139j1.2zdneeaeb6d8e7u \` |
| 37. | `--discovery-token-ca-cert-hash sha256:29d849da533a16d55ee447b02534135eee998d674e8f73a8bd98c0d2dbcf2` |

现在，我们的 Kubernetes 主节点已经设置就绪。我们现在可以在 worker 节点上运行 `join` 命令将其添加到集群。可以通过运行以下代码来实现：

```
root@k8worker1:/etc# kubeadm join 192.168.122.162:6443 --token en80jxkg.nc73dumshya6616t --socket=/var/run/crio/crio.sock --discovery-token-ca-cert-hash sha256:6a0886192f3c308cd78fc33622aefe7e9692626e09dbb0b1888d49e8feb2
W1106 20:52:36.423681 9268 initconfiguration.go:120] 使用不带 URL 方案的 cri 端点已弃用，未来可能会导致 kubelet 错误。自动在 "criSocket with value /var/run/crio/crio.sock" 前面添加 "scheme"。请更新您的配置！
[preflight] 正在运行预检检查
[preflight] 正在从集群读取配置...
[preflight] 提示：你可以通过 `kubectl -n be-system cm kubeadm-config -o yaml` 查看此配置文件
[kubelet-start] 正在将 kubelet 配置写入文件 "/var/lib/kubelet/config.yaml"
[kubelet-start] 正在将带有标记的 kubelet 环境文件写入文件 "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] 正在启动 kubelet
[kubelet-start] 等待 kubelet 执行 TLS Bootstrap p...
此节点已加入集群：
* 证书签名请求已发送到 apiserver 并收到了响应。
* Kubelet 已获新的安全连接详情。
在控制平面上运行 'kubectl get nodes' 查看此节点已加入集群。
root@k8sworker:/etc#
```

`join` token 有一段时间有效期，但如果你以后想添加更多节点，可以轻松创建一个新 token。

要访问您的集群，我们需要一个带有 URL 和证书的配置来授予访问。`Kubeadmin` 已经为我们生成了，我们可以使用以下命令使用：

```
export KUBECONFIG=/etc/kubernetes/admin.conf
```

你可以将此文件复制到电脑，然后在那里运行 `kubectl` 命令。这是您应该妥善保存的 admin token。在 Kubernetes 中有很多方法创建用户和角色，但我们只使用 admin token。如下代码所示，我们添加了配置并请求 Kubernetes API 来确定哪些节点已连接。以下代码显示了如何设置对 Kubernetes 集群的访问：
