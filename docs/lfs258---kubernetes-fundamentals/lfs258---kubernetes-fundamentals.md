
# FS258 - Kubernetes 入门指南

如果对此处材料的适当和公平使用有任何疑问，请联系：

ntraining@linuxfoundation.org

# 第 1 章：引言

![](img/7b8a27c9e8a5a4b2faa64ee2b38e8e6d_6_0.png)

## 1.1 实验

### 练习 1.1：配置系统使用 `sudo`

除非绝对必要，否则运行 root shell 是非常危险的：一次拼写错误或其他错误都可能导致严重的（甚至是致命的）损害。

合理的做法是配置系统，通过使用 `sudo` 机制允许单个命令以超级用户权限运行。通过 `sudo`，用户只需要知道自己的密码，而永远不需要知道 root 密码。

如果你使用的是 Ubuntu 等发行版，你可能不需要通过此实验来为课程正确配置 `sudo`。但是，你应该确保自己理解了这一过程。

要检查系统是否已配置允许你正在运行的用户运行 `sudo`，只需执行一个简单的命令：

```
$ sudo ls
```

系统会提示你输入用户密码，然后命令应该执行。如果如果没有，你会收到一条错误消息，此时你需要执行以下步骤。

通过输入 `su` 启动 root shell，然后给出 root 密码而不是你的用户密码。

在所有最近的 Linux 系统中，你都应该导航到 `/etc/sudo.d` 子目录并创建一个文件，文件名通常是想要授予 `sudo` 访问权限的用户名。然而，这种约定并不是必须，因为 `sudo` 会根据需要扫描此目录下的所有文件。该文件可以简单包含：

```
student ALL=(ALL) ALL
```

如果用户是 `student`。

一种较旧的做法（显然仍然有效）是在 `/etc/sudoers` 文件的末尾添加一行。最好使用 `visudo` 程序来这样做，它会确保你在编辑使用了正确的语法。

你可能需要通过输入以下命令对文件设置正确的权限：

```
$ chmod 440 /etc/sudoers.student
```

（注意：Linux 发行版可能要求权限设为 400 而不是 440。）

完成这些步骤后，输入 `exit` 退出 root shell，然后再次尝试。

管理员有许多配置 `sudo` 的其他方法，包括仅为某些用户指定权限、限制搜索路径等。`/etc/sudoers` 文件有非常详细的文档。

然而，我们非常建议你进行另一项设置，即使你的系统已经配置了 `sudo`。大多数发行版为普通用户和 root 用户设置了不同的可执行文件路径。特别是 `/sbin` 和 `/usr/bin` 目录不会被搜索，因为它继承的是用户的 `PATH`，而不是完整的 root 用户用户路径。

因此，在课程中，我们必须不断提醒你许多系统管理工具的完整路径；任何安全增强可能都不值得花额外的时间去输入和查找这些程序所在的目录。因此，我们建议你在家目录下的 `.bashrc` 文件中添加以下行：

```
PATH=$PATH:/usr/sbin:/sbin
```

如果你注销并重新登录（不需要重启），此设置将完全生效。

# 第 2 章：Kubernetes 基础

![](img/7b8a27c9e8a5a4b2faa64ee2b38e8e6d_8_0.png)

## 2.1 实验

### 练习 2.1：查看在线资源

#### 访问 `kubernetes.io`

对于这样一个变化如此迅速的项目，跟踪更新至关重要。查找当前版本文档的主要地方是 <https://kubernetes.io/>。

1. 打开浏览器访问 <https://kubernetes.io/> 网站。
2. 在右上角，使用下拉菜单访问可用版本。它会显示类似 v1.2 的内容。
3. 选择“Documentation”（文档）顶层链接。页面左侧的链接有助于导航。
4. 在时间允许的情况下，浏览其他子页面，如 SETUP（设置）、CONCEPTS（概念）和 TASKS（任务），以熟悉其布局。

#### 跟踪 Kubernetes 问题（Issues）

每天有数百、甚至可能数千人正致力于 Kubernetes。由于有这么多人并行工作，你有很好的资源可以查看其他人是否也遇到了类似的停机。源代码以及功能和问题跟踪目前都在 `github.com` 上。

1. 要查看主页，使用浏览器访问 <https://github.com/kubernetes/kubernetes/>。
2. 点击不同的子目录并访问可用的基本信息。
3. 将你的 URL 指向 <https://github.com/kubernetes/kubernetes/issues>。你应该看到一系列问题、功能请求和支持交流。
4. 在搜索框中，你可能会看到一些现有文本，如 `is:issue is:open`，这允许你过滤你想要的信息类型。追加搜索字符串读取：`-is:issue is:open label:kind/bug`，然后按回车。
5. 你现在应该可以看到按日期倒序排列的 bug。问题顶部的菜单区域允许你按作者、标签、项目、里程碑、分配者查看条目。花点时间查看其他选择标准。
6. 有时你可能想排除某种输出。再次更新 URL，但在 label 前加一个减号，例如：`-is:issue is:open -label:kind/bug`。现在你可以看到除了 bug 报告以外的所有内容。
7. 利用剩余时间探索该页面。

# 第 3 章：安装与配置

![](img/7b8a27c9e8a5a4b2faa64ee2b38e8e6d_10_0.png)

## 3.1 实验

### 练习 3.1：安装 Kubernetes

#### 概述

不同的供应商提供了几种 Kubernetes 安装工具。在实验中，我们将学习使用 `kubeadm`。作为一个社区支持的独立工具，它计划成为构建 Kubernetes 集群的主要方法。

实验是使用运行在 Google Cloud Platform (GCP) 上的 Ubuntu 实例编写的。它们被设计为与供应商无关，因此可以在 AWS、本地硬件或虚拟化内部运行，为你提供最大的灵活性和选择。每个平台都有不同的访问方法和考虑因素。截至 v1.12.1，VirtualBox 的最小（尽可能小）尺寸是：主节点需要 2vCPU/1G 内存的最小 OS，工作节点需要 1vCPU/1G 内存的最小 OS。

如果你拥有自己的设备，你需要禁用交换分区（swap）。可能还有其他要求在使用 `kubeadm` 命令时会以警告或错误的形式显示。大多数命令作为普通用户运行，但有些命令需要 root 权限。例如，请如 AWS 示例所示使用 `sudo` 权限；如果不使用 Linux 或 Mac，你需要使用如本地终端或 PuTTY 等 SSH 客户端。你可以从 <www.putty.org> 下载 PuTTY。你还需要一个 `.pem` 或 `.ppk` 文件来访问节点。每个云提供商都有下载或创建此文件的流程。参加现场导师培训的学员将在课程期间获得该文件。

在练习中，我们将在单节点上安装 Kubernetes，然后扩展集群，添加更多计算资源。两个节点使用相同的大小，提供 2 个 vCPU 和 5G 内存。可以使用较小的节点，但运行速度会较慢。

各种练习将使用 YAML 文件，这些文件包含在文中。鼓励你尽可能编写文件，因为 YAML 的语法对空格缩进有要求，这是需要学习的。重要提示：在你的 YAML 文件中不要使用空格，仅使用缩进。

如果你使用 PDF 复制粘贴后，单引号无法正确通过吗？它会粘贴为反引号。你需要手动修改它。

如果你使用 PDF 复制粘贴……

### 实验步骤

5. 为软件包添加 GPG 密钥。该命令跨越三行。在输入时你可以省略反斜杠。`OK` 是预期的输出，而不是命令的一部分。

```
root@lfs458-node-1a0:~# curl -s \
https://packages.cloud.google.com/apt/doc/apt-key.gpg \
  | apt-key add -
OK
```

6. 使用新仓库更新，这将下载新的仓库信息。

```
root@lfs458-node-1a0:~# apt-get update
<输出已省略>
```

7. 安装软件。这里有定期发布，你可以通过在命令行中输出等号和版本信息来获取最新版本。新的历史记录有多个处更改，并且有少几个良好的错误。

```
root@lfs458-node-1a0:~# apt-get install -y \
kubeads=1.21.0-0 kubelet=1.21.0-0 kubeadm=1.21.0-0
<输出已省略>
```

8. 决定为容器网络接口 (CNI) 使用哪种 pod 网络，应该考虑集群的预期需求。每个集群有多个网络，CNI-Genus 项目正试图改变这一点。

网络可能还使用从容器到容器、pod 到 pod、pod 到服务以及外部到服务的通信。由于 Docker 使用宿主机网络，`docker2` 虚拟桥接器和 `veth` 接口需要位于在同一台主机上才能进行通信。

我们使用 Calico 作为网络插件，它允许我们在当前使用网络策略（Network Policies）。Calico 默认不部署 DNS。Calico 的 3.3 版本有多个带有 RBAC 的配置策略。使用配置文件。一旦为 calico 预期的 IPv4 范围下载后到。

每个文件的短 URL，更长的 URL 可以在此处找到：<https://docs.projectcalico.org/v3.3/getting-started/kubernetes/hosted/rbac-kdd.yaml> 和 <https://docs.projectcalico.org/v3.3/getting-started/kubernetes/installed/hosted/datastore/calico-networking/1.7/calico.yaml>

```
root@lfs458-node-1a0:~# wget https://tinyurl.com/yb4xburn \
-O rbac-kdd.yaml
root@lfs459-node-1a0:~# wget https://tinyurl.com/y81vc9g \
-O calico.yaml
```

9. 用于解析文件路径。查找集群预期的 IPv4 pod。此文件中有很多配置设置。花点时间查看整个文件。`CALICO_IPV4_POOL_CIDR` 必须与下一步中 `kubeadm init` 给出的值匹配，无论该值是什么。

```
root@lfs458-node-1a0:~# less calico.yaml

 配置从从中选择 Pod IPs 的 IP 池。
  name: CALICO_IPV4_POOL_CIDR
  value: "192.168.0.0/16"
```

10. 初始化主节点。逐行读取输出。预计输出随着软件的成熟而变化。有以非 root 用户运行的结束配置。token 在上面提到。此信息稍后可以通过 `kubeadm token list` 找到。这允许你为集群创建一个网络 pod，这将是我们的下一步。将下一个命令传递给 `kubeadm`，在上一步找到的配置文件中设置 Calico。请注意：后续某些命令的输出将不完整。在继续输入之前请阅读下一步。

```
root@lfs458-node-1a0:~# kubeadm init --pod-network-cidr 192.168.0.0/16
```

# 第 3 章：安装与配置

```
[init] 正在使用 Kubernetes 版本: v1.12.1
[preflight] 正在运行预检
[preflight/images] 正在拉取设置 Kubernetes 集群所需的镜像
[preflight/images] 这可能需要一或两分钟，取决于 你的互联网连接速度
```

<输出已省略>

你的 Kubernetes 主 节点已成功初始化。

要启动你的集群，你需要以普通用户身份运行以下命令：

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

你现在应该向集群部署一个 pod 网络。运行 `kubectl apply -f [podnetwork.yaml]` 并使用列在下面的选项之一：

<https://kubernetes.io/docs/concepts/cluster-administration/addons/>

你现在可以通过在每个节点上作为 root 运行以下命令加入任意数量的机器：

```
kubectl join 10.128.0.4:6443 --token rdnhok.6b8mb61gesunanh
--discovery-token=ca-cert-bash
sha256:66350d154fc0c169b5bb5fd0c54b2764281695e356d879d55e95542f77
```

11. 正如方向中建议的，允许非 root 用户访问集群。在复制后查看文件。

```
root@lfs458-node-1a0:~# exit
root@lfs458-node-1a0:~# sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
root@lfs458-node-1a0:~# sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

```
root@lfs458-node-1a0:~# less ~/.bash
```

12. 将插件应用到集群。一旦复制后，非 root 用户访问。

```
root@lfs458-node-1a0:~# kubectl apply -f rbac-kdd.yaml
root@lfs458-node-1a0:~# kubectl apply -f calico.yaml
```

13. 当 `kubectl` 命令有许多短名称时，我们将通过添加到 `.bashrc` 来启用补全。使其持久化。

```bash
student@lfs458-node-1a~$ echo "source <(kubectl completion)" >> ~/.bashrc
```

14. 通过描述节点进行测试。输入命令的前三个字母 `Tab`。补全默认。

```bash
student@lfs458-node-1a~$ source ~/.bashrc
student@lfs458-node-1a~$ kubectl get<Tab>
```

## 3.1 实验室

（注：此处由于原文重复，已按要求处理）

# 第 3 章：安装与配置

### 实验步骤

4. 只有当令牌（token）过期时，你才能创建一个新的令牌作为加入命令的一部分。

```
student@lfs458-node-1a0a~$ sudo kubeadm token create
27ee4.66ff60318da929
```

5. 从 v1.9 开始，你应该从主节点创建一个发现令牌 CA 证书哈希（Discovery Token CA Cert Hash），以确保安全地加入集群。在主节点或任何你拥有 CA 文件的地方运行。你将得到一个长字符串。

```
student@lfs458-node-1a0a~$ openssl x509 -pubkey \
-in /etc/kubernetes/pki/ca.crt | openssl rsa \
-outform der 2>/dev/null | openssl dgst \
-sha256 -hex | /dev/null \
6d54167b05d62e52fa543d90e7e65f376994c3483436683f2a18673e5d2a1b0
```

6. 使用上述令牌和哈希值（`<hash>`）来加入集群节点。使用主节点的私有 IP 地址和端口 6443。主节点上执行 `kubeadm init` 的输出也在此处，它应该仍然可用。

```
root@lfs458-worker:$ kubeadm join \
--token 27ee4.66ff6031da929 \
10.12.0.2:6443 \
--discovery-token-ca-hash \
sha256:6d54167b05d62e52fa543d90e7e65f376994c3483436683f2a18673e5d2a1b0
```

```
[preflight] Running pre-flight checks
[WARNING] FileCreating:kubectl not found in system
[discovery] Trying to connect to API Server "10.142.0.2:6443"
[discovery] Created cluster-info discovery client, requesting info from "https://10.142.0.2:6443"
[discovery] Requesting info from "https://10.142.0.2:6443" to validate TLS against the public key
[discovery] Cluster info signature and contents are valid and TLS certificate validates against pinned roots, will use API Server "10.142.0.2:6443"
[discovery] Successfully established connection with API Server
```

- 该节点已加入集群。
- 证书签名请求已发送到主节点并收到了响应。
- Kubelet 已获知新的连接详情。在主节点上运行 `kubectl get nodes` 来查看该节点加入集群的情况。

7. 尝试在服务器上运行 `kubectl` 命令。如果你在本地的 `.kube/config` 文件没有证书或身份密钥。



## 练习 3.3: 完成集群设置

1. 查看集群节点。状态从 `NotReady` 变为 `Ready` 可能需要一两分钟。可以使用 `NAME` 字段查看详情。你的节点名称会不同。注意主节点显示为 `NotReady`，这是由于污点（taint）导致的。

LFS258: 2018-11-13 © Copyright the Linux Foundation. 保所有.

## 3.1. 实验

```
student@lfs458-node-10a:# kubectl get node
NAME STATUS ROLES AGE VERSION
lfs458-node-10a NotReady master 10m  v1.12.1
lfs458-worker Ready    <none> 32s  v1.12.1
```

2. 查看节点的详情。逐行查看资源及其当前状态。查看污点（Taints）的状态。出于安全考虑，主节点默认不会在线拉取。花点时间阅读输出的每一行，如果你发现状态为 `False`，某些可能是错误。

```
student@lfs458-node-10a:# kubectl describe node lfs458-node-10a
Name:
master
Labels:
beta.kubernetes.io/arch=amd64
beta.kubernetes.io/os=linux
kubernetes.io:hostname=lfs458-node-10a
node.kubernetes.io/master=
Annotations:
node.kubernetes.io/in/cri=/var/run/dockershim.sock
node.alpha.kubernetes.io/ti=0
volumes.kubernetes.io/controller-managed-attach-detach=true
CreationTimestamp: Sun, Jun 29 2018 21:32:00
Taints:
node.kubernetes.io/master:NoSchedule
```

3. 允许主节点运行非基础设施节点。主节点出于安全和性能原因带有污点。将在训练环境中使用该节点，但在生产环境中可以过此步骤。移除末尾的减号（−），这是移除它的语法。在得到“未找到”错误之前，第二个节点没有污点。

```
student@lfs458-node-10a:# kubectl describe node | grep -i taint
Taints:
node.kubernetes.io/master:NoSchedule
Taints:
<none>
```

```
student@lfs458-node-10a:# kubectl taint nodes \
--all node.kubernetes.io/master-
node/lfs458-node-10a untainted
error: taint "node.kubernetes.io/master" not found
```

4. 现在主节点可以执行任何节点，我们可能会发现一个新的污点。v1.12.0 的这种行为需要启用新节点。如果存在污点，将其移除。调度器部署剩余节点可能需要一两分钟。

```
student@lfs458-node-10a:# kubectl describe node | grep -i taint
Taints:
node.kubernetes.io/not-ready
Taints:
<none>
```

5. v1.12.1 的另一个“未记录”的特性是污点移除第一次运行时不起作用。检查污点是否已被移除。在它真正消失之前，可能需要移除两次或三次。在再次尝试移除污点之前等待60秒。

```
student@lfs458-node-10a:# kubectl describe node | grep -i taint
Taints:
node.kubernetes.io/not-ready:NoSchedule
Taints:
<none>
```

```
student@lfs458-node-10a:# kubectl taint nodes \
--all node.kubernetes.io/not-ready-
node/lfs458-node-10a untainted
error: taint "node.kubernetes.io/not-ready" not found
```

6. 使用上述令牌和哈希值（`<hash>`）来加入集群节点。使用主节点的私有 IP 地址和端口 6443。主节点上执行 `kubeadm init` 的输出也在此处，它应该仍然可用。

7. 尝试在服务器上运行 `kubectl` 命令。如果你在本地的 `.kube/config` 文件没有证书或身份密钥。

```
root@lfs458-worker:$ kubectl get nodes
The connection to the server localhost:8080 was refused
- did you specify the right host or port?
```

```
student@lfs458-worker:$ ls -l .kube
ls: cannot access '.kube': No such file or directory
```

## 练习 3.4: 部署示例应用程序

1. 使用 nginx 镜像创建一个部署。这将启动一个 pod。

```
student@lfs458-node-10a:# kubectl create deployment nginx --image=nginx
deployment.nginx created
```

2. 检查部署和 pod 的状态，直到它们运行。

```
student@lfs458-node-10a:# kubectl get pods
```

3. 将部署伸缩到 3 个副本。

```
student@lfs458-node-10a:# kubectl scale deployment nginx --replicas=3
```

4. 将部署暴露为 NodePort。

```
student@lfs458-node-10a:# kubectl expose deployment nginx --port=80 --type=NodePort
```

5. 获取分配给服务的端口号。

```
student@lfs458-node-10a:# kubectl get service
```

6. 使用节点 IP 和端口通过浏览器访问应用程序。

7. 删除部署和。

```
student@lfs458-node-10a:# kubectl delete deployment nginx
student@lfs458-node-10a:# kubectl delete service nginx
```

8. 查看本次迭代的 yaml 输出并将其与第一次进行比较。我们在新文件中添加了时间戳、资源版本（resource version）和 uid。这些是每个资源生成的，因此我们需要从 yaml 文件删除它们以避免冲突或错误信息。状态（status）也不是硬编码的。

```
$student@1fs458-node-1a0$: $ kubectl deploy nginx -o yaml > second.yaml
<output_omitted>
```

```
$student@1fs458-node-1a0$: $ diff first.yaml second.yaml
<output_omitted>
```

9. 既然我们已经处理了原始输出，现在我们来探索生成 YAML 或 JSON 的其他方法。使用 `--dry-run` 选项并验证创建的内容。唯一的 deployment 应该显示我们之前删除的信息。

```
$student@1fs458-node-1a0$: kubectl create deployment two --image=nginx --dry-run -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    run: two
    name: two
spec:
<output_omitted>
```

```
$student@1fs458-node-1a0$: $ kubectl get deployment AVAILABLE AGE
NAME    DESIRED CURRENT UP-TO-DATE
nginx   1        1            1             7m
```

10. 现有对象可以用准备即用的 YAML 输出进行查看。查看现有的 deployment。注意 `--export` 选项还有更多细节。

```
$student@1fs458-node-1a0$: $ kubectl get deployments nginx --export -o yaml
apiVersion: extensions/v1beta
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
  creationTimestamp: null
  generation: 1
  labels:
    run: nginx
<output_omitted>
```

11. 输出也可以以 JSON 输出的形式查看。

```
$student@1fs458-node-1a0$: kubectl get deploy nginx -o json
{
  "apiVersion": "extensions/v1beta",
  "kind": "Deployment",
  "metadata": {
    "annotations": {
      "deployment.kubernetes.io/revision": "1"
    }
  },
<output_omitted>
```

12. 新的 deployment 容器是一个轻量级 Web 服务器。我们需要创建一个 service 来查看默认欢迎页面。首先查看帮助输出。注意在章节中间部分大约有几个示例。

```
$student@1fs458-node-1a0$: $ kubectl expose -h
<output_omitted>
```

13. 现在访问 Web 服务器。由于我们没有声明要使用的端口，你将收到一个错误。

```
student@lfs458-node-la0a~$ kubectl expose deployment/nginx
error: couldn't find port via --port flag or introspection
See kubectl expose -h for help and examples.
```

14. 依若要更改集群中的现有配置，可以使用 `edit` 或 `patch` 子命令进行非破坏性更新。集群会对先前的、当前的和提供的输入进行三方合并，以确定要做的修改。未提及的字段不受影响。`edit` 函数执行一次编辑，然后打开编辑器，之后你可以使用带有 JSON patch、merge 或战略 merge 功能的 API 请求。

如果配置已更改，它将被缓存直到被察觉，然后可以使用 `replace --force` 选项进行破坏性更新。这会删除并重新创建资源。

编辑该文件。找到容器名称（大约在第31行左右），并按所示添加端口。

```
student@lfs458-node-la0a~$ vim first.yaml
spec:
  containers:
    image: nginx
    imagePullPolicy: Always
    name: nginx
    ports:
      - containerPort: 80  # 添加这些
        protocol: TCP      # 这里的行
    resources: {}         # 几行
```

15. 由于我们所创建的更改，我们将使用 `replace` 来终止并创建一个新的 deployment。

```
student@lfs458-node-la0a~$ kubectl replace -f first.yaml
deployment.extensions/nginx replaced
```

16. 查看 Pod 和 Deployment。AGE 显示 pod 已被重新创建。

```
student@lfs458-node-la0a~$ kubectl get deploy,pod
NAME                    DESIRED CURRENT   UP-TO-DATE AVAILABLE AGE
deployment.extensions/nginx                               2m4s
pod/nginx-f7cbc4b4d9-18cl1 READY STATUS   RESTARTS AGE
                       1/1       Running     0s
```

17. 再次暴露原因。这次应该可以工作了。

```
student@lfs458-node-la0a~$ kubectl expose deployment/nginx
service/nginx exposed
```

18. 验证你的配置。查看服务信息，然后查看 endpoint 信息。Cluster IP 不是当前的 endpoint。注意当前的 IP。下方的示例是 `10.244.1.1:99`。在接下来的几次测试中使用此信息。

```
student@lfs458-node-la0a~$ kubectl get svc nginx
NAME       TYPE     EXTERNAL-IP   PORT(S)   AGE
nginx      ClusterIP  10.100.61.222  <none>     80/TCP    3m
student@lfs458-node-la0a~$ kubectl get ep nginx
NAME       POINTS   AGE
nginx      10.244.1.1:99   4m
```

19. 确定运行在哪个容器。进入该节点并使用 `tcpdump` 查看 `tun0` 接口上的流量（零接口，即第二个容器接口）。你可能在以 cal 开头加某些名称的接口上看到它。在下一步运行 `curl` 时留出该命令。你会看到几条消息来回传输，包括 `HTTP: HTTP/1.1 200 OK` 以及对相同序列的响应。

## 第3章. 安装与配置

```
student@lfs458-node-1a0a~$ kubectl describe pod nginx-7cbc4b4dc-d27xv \
  grep Node:
Node: lfs458-worker/10.128.5
```

20. 再次暴露原因。这次应该可以工作。注意 `--export` 选项有更多详细。

```
student@lfs458-node-1a0a~$ kubectl describe pod nginx-7cbc4b4dc-d27xv \
  grep Node:
Node: lfs458-worker/10.128.5
```



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```



```bash
student@lfs458-node-la0a~$ kubectl get pods -n low-usage-limit
NAME                             READY  STATUS    RESTARTS AGE
limited-hog-255609208-wnnpv      1/1     Running   0         3m
```

8. 查看详情。你会注意到它继承了整个命名空间的设置。如果你先创建命名空间，补全功能应该是可以工作的。

```bash
student@lfs458-node-la0a~$ kubectl -n low-usage-limit get pod limited-hog-255609208-wnnpv -o yaml
<output_metadata>
spec:
  containers:
    - image: vish/stress
      imagePullPolicy: Always
      name: stress
      resources:
        limits:
          cpu: "1"
          memory: 500Mi
        requests:
          memory: 100Mi
      terminationMessage: /dev/termination-log
<output_metadata>
```

9. 复制并编辑全局文件的配置文件。添加 `namespace:` 行，以便新的部署将位于 `low-usage-limit` 命名空间。

```yaml
student@lfs458-node-la0a~$ cp hog.yaml hog2.yaml
...
labels:
  app: hog
  name: hog
  namespace: low-usage-limit  # < 添加此行
selfLink: /apis/extensions/v1/namespaces/default/deployments/hog
spec:
...
```

LFS258: V.2018-11-13 © Copyright the Linux Foundation 2018. 版权所有。

# 第 4 章 KERNETES 架构

10. 打开外部会话，以便在每个会话中都有运行的任务。当创建新部署时，它可能会被调度到没有任何压力的节点上。

创建部署。

```bash
$ student@lfs458-node-1ia0a:~$ kubectl create -f hog2.yaml
deployment.extensions/hog created
```

11. 查看部署。有两个同名的部署，但在不同的命名空间中。你可能还会发现 `calico-hypo` 部署有 pod，但没有任何请求。任何小型集群都不需要通过此 ViewController 拥有 Calico pod。

```text
$ student@lfs458-node-1ia0a:~$ kubectl get deployments --all-namespaces
NAMESPACE NAME DESIRED UP-TO-DATE AVAILABLE AGE
default hog 1 1 45m
kube-system calico-hypo 0 0 0h
kube-system coredns 2 2 8h
low-usage-limit hog 1 1 13s
low-usage-limit hog 1 1 5m
```

12. 查看其他终端中运行的输出。你应该发现两个部署使用的资源大约相同，每个部署各占一个。对于每个部署，你将看到来自一个节点的以下行，这表明在具有 8 核心的系统上运行时，使用了一个处理器和大约 12% 的内存。

```text
25128 root 20 0 958532 954672 3180 R 100.0 11.7 05:22:27 stress
24875 root 20 0 958532 954800 3180 R 100.3 11.7 41:04:29 stress
```

13. 删除 hogs 以恢复资源。

```bash
$ student@lfs458-node-1ia0a:~$ kubectl delete low-usage-limit deployment hog
deployment.extensions/"hog" deleted

$ student@lfs458-node-1ia0a:~$ kubectl delete deployment hog
deployment.extensions/"hog" deleted
```

## 练习 4.3：更复杂的部署

我们现在将部署一个复杂的演示来测试集群。完成后，它将是一个 `sock-shop` 站点。提供的短 URL 是：https://raw.githubusercontent.com/microservices-demo/microservices-demo/master/deploy/complex-demo.yaml

1. 使用预先制作的 YAML 文件部署。

```bash
$ student@lfs458-node-1ia0a:~$ wget https://raw.githubusercontent.com/microservices-demo/microservices-demo/master/deploy/complex-demo.yaml -O complex-demo.yaml
Resolving tinymin.com (tinymin.com). 104.20.218.42,104.20.219.42.
Connecting to tinymin.com (tinymin.com).104.20.218.42... connected.
HTTP request sent, awaiting response: 301
Permanently: https://raw.githubusercontent.com/microservices-demo/microservices-demo/master/deploy/complex-demo.yaml
2017-11-02 16:54:27
Resolving raw.githubusercontent.com (raw.githubusercontent.com).151.101.5...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com).151.101.5...
HTTP request sent, awaiting response: 200 OK
<output_omitted>
```

2. 在文件中找到预期的命名空间。应该是 `sock-shop`。还要注意一起工作的各种容器，你可以通过参数可以看到这些 pod 设置。LFS258: V.2018-11-13 © The Linux Foundation 2018. 版权所有。

## 4.1. 实验室

```yaml
student@lfs458-node-la0a~$ less complex-demo.yaml
apiVersion: extensions/v1
kind: Deployment
metadata:
  name: carts-db
  labels:
    name: carts-db
    namespace: sock-shop
spec:
  replicas: 1
<output_omitted>
```

3. 创建命名空间并验证其已创建。

```bash
student@lfs458-node-la0a~$ kubectl create namespace sock-shop
student@lfs458-node-la0a~$ kubectl get namespace
NAME          STATUS    AGE
default       Active    35m
kube-system   Active    35m
low-usage-limit Active    26m
sock-shop     Active    5s
```

4. 查看镜像。

```bash
student@lfs458-node-la0a~$ grep image complex-demo.yaml
image: weave/carts:0.4.8
image: weave/catalogue-db:0.5
image: weave/front-end:0.12
image: mongo
```

5. 使用 YAML 文件创建新的购物网站。使用你创建的命名空间。现在部署了我们看到的。

```bash
student@lfs458-node-la0a~$ kubectl apply -n sock-shop -f complex-demo.yaml
deployment "carts-db" created
service "carts-db" created
service "carts" created
<output_omitted>
```

6. 使用命名空间作为命令的基础。第一个命令显示没有 pod。必须传递命名空间参数。在你运行时，某些容器可能尚未完全部署。

```bash
student@lfs458-node-la0a~$ kubectl get pods
student@lfs458-node-la0a~$ kubectl -n sock-shop get pods
NAME                    STATUS    RESTARTS  AGE
carts-db-255609208-c4v   Running   0         7m
catalogue-db-255609208-t9j   Running   0         7m
front-end-255609208-f5c   Running   0         7m
mongo-255609208-g6k       Running   0         7m
payment-255609208-c21   Running   0         7m
queue-master-255609208-q7t Running   0         7m
rabbitmq-255609208-vz     Running   0         7m
shipping-255609208-q7z   Running   0         7m
user-255609208-x4f       Running   0         7m
user-db-255609208-w2z    Running   0         7m
```

7. 验证端口很容易。使用节点的 IP 地址（不是从提示中派出的那个）查看页面。外部 IP 未配置。首先使用端口 80，然后等待端口 30001 直到你看到列。

```bash
student@lfs458-node-i0a~$ get svc -n sock
NAME             TYPE        CLUSTERIP     EXTERNAL-IP   PORT           AGE
carts            ClusterIP   100.96.15.48  None          80             7s
carts-db         ClusterIP   100.96.20.73  None          27017         7s
catalogue         ClusterIP   100.96.8.203  None          80             7s
catalogue-db     ClusterIP   100.96.151.94 None          27017         7s
front-end         NodePort    100.96.151.255 80:30001/TCP   7s
mongo             ClusterIP   100.96.151.255 None          27017         7s
payment           NodePort    100.96.151.255 80:30002/TCP   7s
queue-master     ClusterIP   100.96.151.255 None          27017         7s
rabbitmq         NodePort    100.96.151.255 80:30003/TCP   7s
shipping         NodePort    100.96.151.255 80:30004/TCP   7s
user             NodePort    100.96.151.255 80:30005/TCP   7s
user-db          ClusterIP   100.96.151.255 None          27017         7s
```

# 第 4 章 KERNETES 架构

8. 检查运行的部署。你会发现两个部署使用的资源大约相同，每个部署各占一个。对于每个部署，你将看到来自一个节点的以下行，这表明在具有 8 核心的系统上运行时，使用了一个处理器和大约 12% 的内存。

```text
25128 root 20 0 958532 954672 3180 R 100.0 11.7 05:22:27 stress
24875 root 20 0 958532 954800 3180 R 100.3 11.7 41:04:29 stress
```

9. 删除 hogs 以恢复资源。

```bash
$ student@lfs458-node-1ia0a:~$ kubectl delete low-usage-limit deployment hog
deployment.extensions/"hog" deleted

$ student@lfs458-node-1ia0a:~$ kubectl delete deployment hog
deployment.extensions/"hog" deleted
```

10. 打开外部会话，以便在每个会话中都有运行的任务。当创建新部署时，它可能会被调度到没有任何压力的节点上。

创建部署。

```bash
$ student@lfs458-node-1ia0a:~$ kubectl create -f hog2.yaml
deployment.extensions/hog created
```

11. 查看部署。有两个同名的部署，但在不同的命名空间中。你可能还会发现 `calico-hypo` 部署有 pod，但没有任何请求。任何小型集群都不需要通过此 ViewController 拥有 Calico pod。

```bash
$ student@lfs458-node-1ia0a:~$ kubectl get deployments --all-namespaces
NAMESPACE NAME DESIRED UP-TO-DATE AVAILABLE AGE
default hog 1 1 45m
kube-system calico-hypo 0 0 0h
kube-system coredns 2 2 8h
low-usage-limit hog 1 1 13s
low-usage-limit hog 1 1 5m
```

12. 查看其他终端中运行的输出。你应该发现两个部署使用的资源大约相同，每个部署各占一个。对于每个部署，你将看到来自一个节点的以下行，这表明在具有 8 核心的系统上运行时，使用了一个处理器和大约 12% 的内存。

```text
25128 root 20 0 958532 954672 3180 R 100.0 11.7 05:22:27 stress
24875 root 20 0 958532 954800 3180 R 100.3 11.7 41:04:29 stress
```

13. 删除 hogs 以恢复资源。

```bash
$ student@lfs458-node-1ia0a:~$ kubectl delete low-usage-limit deployment hog
deployment.extensions/"hog" deleted

$ student@lfs458-node-1ia0a:~$ kubectl delete deployment hog
deployment.extensions/"hog" deleted
```

## 4.1. 实验室

```bash
student@lfs48-worker:~$ sudo docker ps | wc -l
30
```

11. 为了进行维护，我们需要将容器从某个节点移走并防止新容器部署。实现此点的方法之一是 `drain`（驱逐）或 `cordon`（隔离）。目前不会影响 DaemonSets，我们将在未来详细讨论。通过获取节点列表，你的节点名称将有所不同。

```bash
student@lfs48-node-l40a:~$ kubectl get nodes
NAME STATUS ROLES AGE VERSION
lfs48-worker Ready <none> 3h v1.12.1
lfs48-node-l40a Ready master 3h v1.12.1
```

12. 如果要修改你的节点，请使用 `node drain` 来驱逐 pod。某些资源可能无法驱逐，除了一个不会影响后续操作的错误。请注意，错误信息包含了 `abort` 命令，说明 `drain` 未执行。在节点检查它，运行的容器数量将相同，但会显示一个新的污点（taint），阻止调度器分配新的 pod。

```bash
student@lfs48-node-l40a:~$ kubectl drain lfs48-worker
node/lfs48-node-l40a
error: unable to drain "lfs48-worker", aborting command...
```

有待待驱逐的：

`lfs48-worker`



`error: unable to drain (use --ignore-daemonsets to ignore):`

`calico-node-vmn7`, `kube-proxy-rjjls`

```bash
student@lfs48-node-l40a:~$ kubectl describe node | grep -i taint
Taints:
<none>
node.kubernetes/unschedulable:NoSchedule
```

13. 如错误所示，我们可以对未与我们的节点连接的容器使用`--ignore-daemonsets`。当我们使用该命令时，会在节点末尾发现一个新的错误。节点将继续保持相同数量的 pod 和容器。

```bash
student@lfs48-node-l40a:~$ kubectl drain lfs48-worker --ignore-daemonsets
node/lfs48-worker
error: unable to drain node "lfs48-worker", aborting command...
```

有待待驱逐的：

`lfs48-worker`

`error: pods with local storage (use --delete-local-data to override):`

`cards-5574f7c5679ffkq2`, `cards-db-55c5f849e-v72d8`, `orders-7b69bf5686-vtcdkn`

14. 再次运行命令。此输出将显示节点是否已准备好驱逐 pod。所有非 daemonset 的 pod 都将保留。节点显示在两行。你可以复制冲突内容并在单行中输入命令。

```bash
student@lfs48-node-l40a:~$ kubectl drain lfs48-worker \
--ignore-daemonsets --delete-local-data
node/lfs48-worker already cordoned
WARNING: Ignoring DaemonSet-managed pods: calico-node-vmn7, kube-proxy-rjjls; Deleting pods with local storage:
pods/cards-db-55c5f849e-b4v2 evicted
pods/orders-db-7b69bf568-zr1 evicted
pods/calico-node-db6ff5bbf2-ze7 evicted
pods/catalogue-5764fd6d-86kv96 evicted
pods/orders-7b69bf568b-t2z1 evicted
pods/front-end-f99fbbc9c-v24qp evicted
pods/cards-5571fc5679-c77p evicted
```

15. 如果你想取消第二个工作节点（worker node），你会发现那里的 pod 和容器比之前少。这些 pod 只能通过我们将在章节中讨论的特殊方式进行驱逐。

`LFS258:2018-11-13 © Copyright Linux Foundation 2018. All rights reserved.`

```bash
student@lfs458-worker:$ sudo docker ps | wc -l
6
```

16. 更新节点污点，使调度器再次使用该节点。验证在仅当部署 pod 时没有节点被调度器移动到工作节点。

```bash
student@lfs458-node-ia0a:$ kubectl cordon lfs458-worker
node/lfs458-worker uncorcorded
```

```bash
student@lfs458-node-ia0a:$ kubectl describe node | grep -i taint
Taints:
<none>
<none>
```

```bash
student@lfs458-worker:$ sudo docker ps | wc -l
6
```

17. 清理你的 sock set，让我们看看 pod 和 deployment 之间的一些区别。从 sock-shop 命名空间运行的 pod 列表开始。

```bash
student@lfs458-node-ia0a:$ kubectl -n sock-shop get pod
```

| NAME | READY | STATUS | RESTARTS | AGE |
|---|---|---|---|---|
| carts-db-54905638-tw6zz | 1/1 | Running | 0 | 6h |
| catalogue-423903682-sp5kt | 1/1 | Running | 0 | 6h |
| <output_omitted> | | | | |

18. 使用 pod 删除一个松散的 pod。

```bash
student@lfs458-node-ia0a:$ kubectl -n sock-shop delete pod
catalogue-423903682-sp5kt catalogue-db-18469424-zhqvk \
front-end-233748189
```

19. 正如错误所示，我们可以使用`--ignore-daemonsets`处理未与我们连接的容器。

20. 让我们让我们查看 sock-shop 命名空间中运行的 pod 列表。

```bash
student@lfs458-node-ia0a:$ kubectl -n sock-shop get pod
```

| NAME | READY | STATUS | RESTARTS | AGE |
|---|---|---|---|---|
| carts-db-54905638-tw6zz | 1/1 | Running | 0 | 6h |
| catalogue-423903682-sp5kt | 1/1 | Running | 0 | 6h |
| <output_omitted> | | | | |

18. 使用 pod 删除一个松散的 pod。

```bash
student@lfs458-node-ia0a:$ kubectl -n sock-shop delete pod
catalogue-423903682-sp5kt catalogue-db-18469424-zhqvk \
front-end-233748189
```

19. 正如错误所示，我们可以使用`--ignore-daemonsets`处理未与我们连接的容器。当我们使用该命令时，会在节点末尾发现一个新的错误。节点将继续保持相同数量的 pod 和容器。

20. 再次运行命令。此输出将显示节点是否已准备好驱逐 pod。所有非 daemonset 的 pod 都将保留。节点显示在两行。你可以复制冲突内容并在单行中输入命令。

```bash
student@lfs458-node-l40a:~$ kubectl drain lfs48-worker \
--ignore-daemonsets --delete-local-data
node/lfs48-worker already cordoned
WARNING: Ignoring DaemonSet-managed pods: calico-node-vmn7, kube-proxy-rjjls; Deleting pods with local storage:
pods/cards-db-55c5f849e-b4v2 evicted
pods/orders-db-7b69bf568-zr1 evicted
pods/calico-node-db6ff5bbf2-ze7 evicted
pods/catalogue-5764fd6d-86kv96 evicted
pods/orders-7b69bf568b-t2z1 evicted
pods/front-end-f99fbbc9c-v24qp evicted
pods/cards-5571fc5679-c77p evicted
```

15. 如果你想取消第二个工作节点（worker node），你会发现那里的 pod 和容器比之前少。这些 pod 只能通过我们将在章节中讨论的特殊方式进行驱逐。

`LFS258:2018-11-13 © Copyright Linux Foundation 2018. All rights reserved.`

```bash
student@lfs458-worker:$ sudo docker ps | wc -l
6
```

16. 更新节点污点，使调度器再次使用该节点。验证在仅当部署 pod 时，没有节点被调度器移动到工作节点。

```bash
student@lfs458-node-ia0a:$ kubectl cordon lfs458-worker
node/lfs458-worker uncorcorded
```

```bash
student@lfs458-node-ia0a:$ kubectl describe node | grep -i taint
Taints:
<none>
<none>
```

```bash
student@lfs458-worker:$ sudo docker ps | wc -l
6
```

17. 清理你的 sock set，让我们看看 pod 和 deployment 之间的一些区别。从 sock-shop 命名空间运行的 pod 列表开始。

```bash
student@lfs458-node-ia0a:$ kubectl -n sock-shop get pod
```

| NAME | READY | STATUS | RESTARTS | AGE |
|---|---|---|---|---|
| carts-db-54905638-tw6zz | 1/1 | Running | 0 | 6h |
| catalogue-423903682-sp5kt | 1/1 | Running | 0 | 6h |
| <output_omitted> | | | | |

18. 使用 pod 删除一个松散的 pod。

```bash
student@lfs458-node-ia0a:$ kubectl -n sock-shop delete pod
catalogue-423903682-sp5kt catalogue-db-18469424-zhqvk \
front-end-233748189
```

19. 正如错误所示，我们可以使用`--ignore-daemonsets`处理未与我们连接的容器。当我们使用该命令时，会在节点末尾发现一个新的错误。节点将继续保持相同数量的 pod 和容器。

20. 再次运行命令。此输出将显示节点是否已准备好驱逐 pod。所有非 daemonset 的 pod 都将保留。节点显示在两行。你可以复制冲突内容并在单行中输入命令。

```bash
student@lfs458-node-l40a:~$ kubectl drain lfs48-worker \
--ignore-daemonsets --delete-local-data
node/lfs48-worker already cordoned
WARNING: Ignoring DaemonSet-managed pods: calico-node-vmn7, kube-proxy-rjjls; Deleting pods with local storage:
pods/cards-db-55c5f849e-b4v2 evicted
pods/orders-db-7b69bf568-zr1 evicted
pods/calico-node-db6ff5bbf2-ze7 evicted
pods/catalogue-5764fd6d-86kv96 evicted
pods/orders-7b69bf568b-t2z1 evicted
pods/front-end-f99fbbc9c-v24qp evicted
pods/cards-5571fc5679-c77p evicted
```

15. 如果你想取消第二个工作节点（worker node），你会发现那里的 pod 和容器比之前少。这些 pod 只能通过我们将在章节中讨论的特殊方式进行驱逐。

`LFS258:2018-11-13 © Copyright Linux Foundation 2018. All rights reserved.`

```bash
student@lfs458-worker:$ sudo docker ps | wc -l
6
```

16. 更新节点污点，使调度器再次使用该节点。验证在仅当部署 pod 时，没有节点被调度器移动到工作节点。

```bash
student@lfs458-node-ia0a:$ kubectl cordon lfs458-worker
node/lfs458-worker uncorcorded
```

```bash
student@lfs458-node-ia0a:$ kubectl describe node | grep -i taint
Taints:
<none>
<none>
```

```bash
student@lfs458-worker:$ sudo docker ps | wc -l
6
```

17. 清理你的 sock set，让我们看看 pod 和 deployment 之间的一些区别。从 sock-shop 命名空间运行的 pod 列表开始。

```bash
student@lfs458-node-ia0a:$ kubectl -n sock-shop get pod
```

| NAME | READY | STATUS | RESTARTS | AGE |
|---|---|---|---|---|
| carts-db-54905638-tw6zz | 1/1 | Running | 0 | 6h |
| catalogue-423903682-sp5kt | 1/1 | Running | 0 | 6h |
| <output_omitted> | | | | |

18. 使用 pod 删除一个松散的 pod。

```bash
student@lfs458-node-ia0a:$ kubectl -n sock-shop delete pod
catalogue-423903682-sp5kt catalogue-db-18469424-zhqvk \
front-end-233748189
```

19. 正如错误所示，我们可以使用`--ignore-daemonsets`处理未与我们连接的容器。当我们使用该命令时，会在节点末尾发现一个新的错误。节点将继续保持相同数量的 pod 和容器。

20. 再次运行命令。此输出将显示节点是否已准备好驱逐 pod。所有非 daemonset 的 pod 都将保留。节点显示在两行。你可以复制冲突内容并在单行中输入命令。

```bash
student@lfs458-node-l40a:~$ kubectl drain lfs48-worker \
--ignore-daemonsets --delete-local-data
node/lfs48-worker already cordoned
WARNING: Ignoring DaemonSet-managed pods: calico-node-vmn7, kube-proxy-rjjls; Deleting pods with local storage:
pods/cards-db-55c5f849e-b4v2 evicted
pods/orders-db-7b69bf568-zr1 evicted
pods/calico-node-db6ff5bbf2-ze7 evicted
pods/catalogue-5764fd6d-86kv96 evicted
pods/orders-7b69bf568b-t2z1 evicted
pods/front-end-f99fbbc9c-v24qp evicted
pods/cards-5571fc5679-c77p evicted
```

15. 如果你想取消第二个工作节点（worker node），你会发现那里的 pod 和容器比之前少。这些 pod 只能通过我们将在章节中讨论的特殊方式进行驱逐。

`LFS258:2018-11-13 © Copyright Linux Foundation 2018. All rights reserved.`

```bash
student@lfs458-worker:$ sudo docker ps | wc -l
6
```

16. 更新节点污点，使调度器再次使用该节点。验证在仅当部署 pod 时，没有节点被调度器移动到工作节点。

```bash
student@lfs458-node-ia0a:$ kubectl cordon lfs458-worker
node/lfs458-worker uncorcorded
```

```bash
student@lfs458-node-ia0a:$ kubectl describe node | grep -i taint
Taints:
<none>
<none>
```

```bash
student@lfs458-worker:$ sudo docker ps | wc -l
6
```

17. 清理你的 sock set，让我们看看 pod 和 deployment 之间的一些区别。从 sock-shop 命名空间运行的 pod 列表开始。

```bash
student@lfs458-node-ia0a:$ kubectl -n sock-shop get pod
```

| NAME | READY | STATUS | RESTARTS | AGE |
|---|---|---|---|---|
| carts-db-54905638-tw6zz | 1/1 | Running | 0 | 6h |
| catalogue-423903682-sp5kt | 1/1 | Running | 0 | 6h |



| `<output_omitted>` | | | | |

18. 使用 `pod` 删除一个松散的 `pod`。

```bash
student@lfs458-node-ia0a:$ kubectl -n sock-shop delete pod
catalogue-423903682-sp5kt catalogue-db-18469424-zhqvk \
front-end-233748189
```

19. 正如错误所示，我们可以使用 `--ignore-daemonsets` 处理未与我们连接的容器。当我们使用该命令时，会在节点末尾发现一个新的错误。节点将继续保持相同数量的 `pod` 和容器。

20. 再次运行命令。此输出将显示节点是否已准备好驱逐 `pod`。所有非 `daemonset` 的 `pod` 都将保留。节点显示在两行。你可以复制冲突内容并在单行中输入命令。

- 4. 视图将找到这些包含各种 `kubernetes` 配置信息的目录。

# 第 5 章 API 与访问

```
student@lfs458-node-1a0$:~/kube/cache/discovery/10.128.0.3:6443 ls
admissionregistration.k8s.io  batch  policy
apiek8s.io  certificates.k8s.io  rbac.authorization.k8s.io
apireistration.k8s.io  coordination.k8s.io  scheduling.k8s.io
apps  crd.projectcalico.org  servergroups  json
authentication.k8s.io  events.k8s.io  storage.k8s.io
authorization.k8s.io  extensions  v1/autoscaling  networking.k8s.io
```

- 5. 使用 `list` 命令显示输出。提示符已修改，以便在页面上看起来更好。

```
student@lfs458-node-1a0$:../10.128.0.3:6443$ find
./events.k8s.io
./events.k8s.io/v1beta
./events.k8s.io/v1beta/resources.json
./apps
./apps/v1
./apps/v1/resources.json
./apps/v1beta
./apps/v1beta/resources.json
<output_omitted>
```

- 6. 查看版本 1 API 中的对象列表。对于每个对象，你可以像下面的示例所示查看该对象的视图或操作。注意提示符已截断以适应单行显示。其中一些是具有标准 HTTP 动词的 HTTP 请求。

```
student@lfs458-node-1a0$: python -m json v1/resources.json
{
  "apiVersion": "v1",
  "version": "v1",
  "kind": "APIResourceList",
  "resources": [
    {
      "kind": "Binding",
      "name": "bindings",
      "namespaced": true,
      "singularName": "",
      "verbs": [
        "create"
      ]
    }
  ]
}
<output_omitted>
```

- 7. 一些对象具有 `shortNames`，这使得命令行变得简单得多。找到 `shortName` 端点。

```
student@lfs458-node-1a0$: python -m json v1/resources.json | less
{
  "kind": "Endpoints",
  "name": "endpoints",
  "namespaced": true,
  "shortNames": [
    "ep"
  ],
  "singularName": "",
  "verbs": [
    "create",
    "delete"
  ]
}
```

- 8. 使用 `shortName` 查看端点。它应该与上一个命令的输出匹配。Linux Foundation 2018 版留所有。

### 5.1 实验

```
student@lfs458-node-1a0$: kubectl get ep
ENDPOINTS  AGE
kubernetes  10.128.0.3:6443
```

- 9. 我们可以看到版本 1 中有 37 个对象。

```
student@lfs458-node-1a0$: python -m json v1/resources.json | grep kind
"kind": "APIResourceList",
"kind": "Binding",
"kind": "ComponentStatus",
"kind": "ConfigMap",
"kind": "Endpoints",
<output_omitted>
```

- 10. 查看另一个文件，我们发现一个没有。

```
student@lfs458-node-1a0$: python -m json \
apps/v1beta/resources.json | grep kind
"kind": "APIResourceList",
"kind": "ControllerRevision",
"kind": "Deployment",
<output_omitted>
```

- 11. 删除 `curlpod` 以收回系统资源。

```
student@lfs458-node-1a0$: kubectl delete pod curlpod
pod "curlpod" deleted
```

- 12. 时间允许的话查看此目录下的其他文件。

# 第 6 章

## API 对象

### 6.1 实验

### 练习 6.1：RESTful API 访问

### 概述

我们将继续探索访问集群控制平面的方法。在安全章节中，我们将讨论有几种身份验证方法，其中一种是使用 Bearer令牌。我们将使用其中一个，然后部署一个本地代理服务器，以便在应用程序级别访问 Kubernetes API。

### RESTful API 访问

我们使用 `curl` 命令以不安全的方式向集群发出 API 请求。一旦我们知道了 IP 地址、端口以及令牌（`token`），我们就可以以 RESTful 方式检索集群数据。默认情况下，大多数信息都是限制的，但身份验证策略的更改可能允许更多访问权限。

- 1. 首先，我们需要知道 API 服务器节点副本的 IP 和端口。系统通常会运行一个这样的实例。使用 `kubectl config view` 获取集群的整体配置，并找到 `server` 条目。这将为我们提供 IP 和端口。

```
student@e1fa65-node-1a0:~$ kubectl config view
apiVersion: v1
clusters:
  cluster:
    certificate-authority-data: REDACTED
    server: https://10.128.0.3:6443
  name: kubernetes
<output_omitted>
```

- 2. 我们需要找到 bearer令牌。这是一个默认令牌。查看集群中的令牌列表，首先是 `default` 命名空间。集群中的每个控制器都会有一个 `secret`。

```
student@lfs458-node-1a0$: kubectl get secrets --all-namespaces
NAMESPACE    NAME                  TYPE
default      default-token-jdqp7  kubernetes.io/service-account-token
kube-public  default-token-b2pr   kubernetes.io/service-account-token
kube-system  attach-token-ck     kubernetes.io/service-account-token
kube-system  bootstrap-token-wpx6  kubernetes.io/service-account-token
student@lfs458-node-1a0$: kubectl get secrets NAME  AGE
default      default-token-jdqp7  kubernetes.io/service-account-token
```

- 3. 查看 `secret` 的详情。我们需要输出中的信息。

```
student@lfs458-node-1a0$: kubectl describe secret default-token-jdqp7
Namespace: default
Labels:
  kubernetes.io/service-account: default
Data:
  token: <base64-encoded>
```

- 4. 使用你的令牌复制，或使用 `awk` 保存从第一个到最后一个名为 `token` 的数据。你的数据将会有不同。

```
student@lfs458-node-1a0$: kubectl describe secret default-token-jdqp7 | grep token | cut -d '
```

- 5. 测试是否从你的集群获取基本 API 信息。我们将传递服务器名称和端口，使用 `-k` 选项避免使用证书。

```
student@lfs458-node-1a0$: curl http://10.128.0.3:6443/api \
--header "Authorization: Bearer $token" -k
{
  "kind": "APIVersion",
  "versions": [
    "v1"
  ],
  "serverAddress": [
    "clientCID": "0.0.0.0/",
    "serverAddress": "10.128.0.3:6443"
  ]
}
<output_omitted>
```

- 6. 尝试相同的命令，但调用 API `v1`。

```
student@lfs458-node-1a0$: curl http://10.128.0.3:6443/api/v1 \
--header "Authorization: Bearer $token" -k
<output_omitted>
```

- 7. 尝试获取命名空间列表。这应该返回一个错误。它显示我们的请求被 `system:serviceaccount` 看到，它没有在集群列出命名空间的 RBAC 权限。

```
student@lfs458-node-1a0$: curl https://10.128.0.3:6443/api/v1/namespaces \
--header "Authorization: Bearer $token" -k
<output_omitted>
{"message": "namespaces is forbidden: User \"system:serviceaccount:...}
<output_omitted>
```

- 8. `Pod` 也使用包含的证书来验证 API。证书自动对 `/var/run/secrets/kubernetes.io/serviceaccount/` 下的 `Pod` 可用。如果你使用令牌文件，它与 `$token` 变量相同。`-i` 标志创建一个 `busybox` 容器的终端会。一旦容器重启，`pod` 将显示为：

```
student@lfs458-node-1a0$: kubectl run -i -t busybox --image=busybox \
--restart=Never
# ls /var/run/secrets/kubernetes.io/serviceaccount/
# namespace token
# exit
```

## 6.2：使用代理

与 API 交互的另一种方法是通过代理。代理可以从节点运行或通过使用 `sidecar` 在 `Pod` 内运行。在后续步骤中，我们将向环回地址部署代理。我们将使用 `curl` 访问 API 服务器。如果 `curl` 请求有效但在集群外无效，则我们将问题缩小到 API 摄取过程之后的身份验证和授权问题。

- 1. 开始启动代理。它默认在前台运行。你可以选择几个选项。从查看输出开始。

```
student@lfs458-node-1a0$: kubectl proxy -b
在 localhost 和同样通过指定的 HTTP 路径提供静态内容之间创建代理服务器或应用程序网关。所有输入数据都通过一个端口进入，并根据与静态路径匹配的路径转发到远程 kubernetes API 服务器端口。
```

```
示例:
# 要代理所有 kubernetes 而不包含其他，使用：

$ kubectl proxy --api-prefix/
<output_omitted>
```

- 2. 启动代理设置 API 前缀，并将其放入后台。你可能需要回车来查看提示符。

```
student@lfs458-node-1a0$: kubectl proxy --api-prefix=/ & 
[1] 22500
Starting to serve on 127.0.0.1:8001
```

- 3. 现在使用 `curl` 命令，但指向代理显示的 IP 和端口。输出应该与另一个相同，但格式可能不同。

```
student@lfs458-node-1a0$: curl http://127.0.0.1:8001/api/v1/namespaces
--header "Authorization: Bearer $token" -k
<output_omitted>
```

- 4. 调用 API 获取命名空间。该命令在上一部分由于权限问题不起作用，但现在由于代理代表你进行请求，它应该可以工作了。

```
student@lfs458-node-1a0$: curl http://127.0.0.1:8001/api/v1/namespaces
{
  "kind": "NamespaceList",
  "apiVersion": "v1",
  "metadata": {
    "selfLink": "/api/v1/namespaces",
    "resourceVersion": "86902"
  },
  <output_omitted>
}
```

## 6.3：处理任务

虽然 API 对象被部署后可以持续可用，但某些对象我们可能希望定期运行特定次数，例如 `CronJob`。

### 创建作业

1. 创建一个作业，它将运行一个睡眠三秒的容器。

```bash
student@lfs458-node-1a0a~$ vim job.yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: sleepy
spec:
  template:
    spec:
      containers:
      - name: resting
image: busybox
        command: ["/bin/sleep"]
        args: ["3"]
      restartPolicy: Never
```

2. 创建该作业，然后验证详情。示例中的检查显示作业运行了三秒钟，完成后完成后再次检查。你可能会根据打字快慢看到不同的输出。

```
student@lfs458-node-1a0a~$ kubectl create -f job.yaml
job.batch/sleepy created
```

```
student@lfs458-node-1a0a~$ kubectl get job
NAMECOMPLETIONS DURATION AGE
sleepy 0/1           3s           3s
```

```
student@lfs458-node-1a0a~$ kubectl describe job.sleepy
Name:
  sleepy
Namespace:
  default
Selector:
  controller-id=c2c49125-d0fb-11e8-947a-4210a80002
Labels:
  controller-id=c2c49125-d0fb-11e8-947a-4210a80002
  job-name=sleepy
Annotations:
  <none>
Parallelism:
  1
Completions:
  1
Start Time:
  Tue, 16 Oct 2018 04:22:50 +0000
Completed At:
  Tue, 16 Oct 2018 04:22:55 +0000
Duration:
  5s
Pods Status: 0 Running / 1 Succeeded / 0 Failed
<output-committed>
```

```
student@lfs458-node-1a0a~$ kubectl get jobs
NAMECOMPLETIONS DURATION AGE
sleepy 1/1           5s           17s
```

3. 查看作业的配置。我们可以使用三个参数来影响作业的运行方式。使用 `--yaml` 查看这些参数。我们可以看到 `backoffLimit`、`completions` 和 `parallelism`。接下来我们将添加所有参数。



```
student@lfs458-node-1a0a~$ kubectl get jobs.batch.sleepy -o yaml
<output-committed>
uid: c2c3a80d-d0fc-11e8-947a-4210a8000200
spec:
  backoffLimit: 6
  completions: 1
  parallelism: 1
selector:
    matchLabels:
<output-committed>
```

## 6.1. 实验

4. 当作业状态持续持续时，删除该作业。

```bash
student@lfs458-node-1a0a~$ kubectl delete jobs.batch sleepy
job.batch "sleepy" deleted
```

5. 编辑 YAML 并添加 `completions` 参数并设置为 5。

```bash
student@lfs458-node-1a0a~$ vim job.yaml
<output_omitted>
metadata:
  name: sleepy
spec:
  completions: 5  #--添加行
  template:
    spec:
      containers:
        <output_omitted>
```

6. 创建作业。当你查看作业时，`COMPLETIONS` 从 0/5 开始计数。

```
student@lfs458-node-1a0a~$ kubectl create -f job.yaml
job.batch/sleepy created
```

```
student@lfs458-node-1a0a~$ kubectl get jobs.batch
NAME COMPLETIONS DURATION AGE
sleepy 0/5 5s 5s
```

7. 查看对应的 pod。输出可能会根据打字速度而不同。

```
student@lfs458-node-1a0a~$ kubectl get pods
NAME READY RESTARTS AGE
sleepy-z25hn 0/1 Completed 0 8s
sleepy-zd6692 1/1 Running 0 3s
<output_omitted>
```

8. 最终所有作业都已完成。验证该作业。

```
student@lfs458-node-1a0a~$ kubectl get jobs
NAME COMPLETIONS DURATION AGE
sleepy 5/5 26s 10m
```

```
student@lfs458-node-1a0a~$ kubectl delete jobs.batch sleepy
job.batch "sleepy" deleted
```

9. 再次编辑 YAML。在 `parallelism` 中添加此：将其设置为 2，以便一次部署两个 pod。

```
student@lfs458-node-1a0a~$ get job.yaml
<output_omitted>
metadata:
  name: sleepy
spec:
  completions: 5
  parallelism: 2 #--添加此行
  template:
    spec:
      <output_omitted>
```

10. 创建作业。你应该看到 pod 两个两个部署，直到所有五个都完成。

```
student@lfs458-node-1a0a~$ kubectl create -f job.yaml
job.batch/sleepy created
```

```
student@lfs458-node-1a0a~$ kubectl get pods
NAME READY STATUS RESTARTS AGE
```

## 第6章. API 对象

| 名称 | Ready | 状态 | 重启 | Age |
| :--- | :--- | :--- | :--- | :--- |
| sleepy-8xwpc | 1/1 | Running | 0 | 5s |
| sleepy-xjqnf | 1/1 | Running | 0 | 5s |

```
student@if458-node-1a0a$: kubectl get jobs
NAME COMPLETIONS DURATION AGE
sleepy 3/5 11s 11s
```

11. 一个在指定秒数后让作业睡眠的参数。将 `activeDeadlineSeconds` 设置为 15。作业和 pod 将运行 15 秒后结束。我们还增加了 `sleep` 参数到，以确保不会自动过期。

```bash
student@if458-node-1a0a$: vim yaml
<output_committed>
pletions: 5
parallelism: 2
activeDeadlineSeconds: 15 <-- 添加此行
template:
 spec:
  containers:
    name: resting
    image: busybox
    args: ["/bin/sleep"] <-- 修改此行
<output_committed>
```

12. 删除并重建作业。如果它运行了 15 秒，通常为 3/5，然后持续没有

```bash
student@if458-node-1a0a$: kubectl delete jobs.batch sleepy
job.batch "sleepy" deleted
```

```
student@if458-node-1a0a$: kubectl create -f job.yaml
job.batch/sleepy created
```

```
student@if458-node-1a0a$: kubectl get jobs
NAME COMPLETIONS DURATION AGE
sleepy 1/5 6s 6s
```

```
student@if458-node-1a0a$: kubectl get jobs
NAME COMPLETIONS DURATION AGE
sleepy 3/5 11s 11s
```

13. 查看 YAML 中 Status 部分的消息。

```
student@if458-node-1a0a$: kubectl get job.sleepy -o yaml
<output_committed>
status:
  conditions:
  - lastTransitionTime: Tue, 16 Oct 2018 04:22:45 +0000
    message: Job active longer than specified deadline
    reason: DeadlineExceeded
    status: True
    type: Failed
  startTime: Tue, 16 Oct 2018 04:22:44 +0000
  completedAt: Tue, 16 Oct 2018 04:22:59 +0000
  failed: 
```

14. 删除该作业。

```bash
student@if458-node-1a0a$: kubectl delete jobs.batch sleepy
job.batch "sleepy" deleted
```

# 第 7 章

## 使用 Deployment 管理状态

![](img/7b8a27c9e8a5a4b2faa64ee2b38e8e6d_50_0.png)

### 7.1 实验

### 练习 7.1：使用 ReplicaSets

### 概述

理解和管理容器的状态是 Kubernetes 的核心任务。在本次实验中，我们将首先探索用于管理容器组的 API 对象。随着 Kubernetes 的成熟，可用对象发生了变化，因此使用的版本将决定哪些对象可用。我们的第一个对象是 ReplicaSet，它不包含 Deployment 中那些较新的管理功能。Deployment 会替你管理 ReplicaSets。我们还将与另一个名为 DaemonSet 的对象一起，它可以确保在新添加的节点上运行一个容器。

然后，我们将更新容器中的软件，查看修订历史，并回滚到之前的版本。

### 使用 ReplicaSets

ReplicaSet 是复制控制器（Replication Controller）的下一代产品，其区别仅在于支持的选择器（selectors）。现在使用 ReplicaSet 的唯一理由是你不需要更新容器软件，或者你需要典型流程无法处理的更新编排。

1. 查看你当前的 ReplicaSets。如果你在之前的实验结束时删除了资源，在默认命名空间中应该没有任何报告。

2. 为简单的 ReplicaSet 创建一个 YAML 文件。`apiVersion` 取决于你使用的 Kubernetes 版本。1.8 及更高版本将使用 `apps/beta1`，然后可能是现在的 `apps/beta2`，然后可能是稳定的 `apps/v1`。我们将使用较旧版本的 nginx，然后在实验稍后将其更新到新版本。

```
student@lfs458-node-1a0a~$ kubectl get rs
No resources found.
```

```
student@lfs458-node-1a0a~$ kubectl apply -f yaml
```

```yaml
apiVersion: extensions/v1beta1
kind: ReplicaSet
metadata:
  name: rs-one
spec:
  replicas: 2
  template:
    metadata:
      labels:
        system: ReplicaOne
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

3. 创建 ReplicaSet：

```
student@lfs458-node-104a:~$ kubectl create -f rs.yaml
replicaset.extensions/rs-one created
```

4. 查看新的 ReplicaSet：

```
student@lfs458-node-104a:~$ kubectl describe rs rs-one
Name:
  rs-one
Namespace:
  default
Selector:
  system=ReplicaOne
Labels:
  system=ReplicaOne
Annotations:
  <>
Replicas:
  2 / 2 desired
Pods Status:
  2 Running / 0 Waiting / 0 Failed
Pod Template:
  Labels:
    system=ReplicaOne
  Containers:
  nginx:
    Image:
      nginx:1.7.9
    Port:
      80/TCP
    Environment:
      <>
    Mounts:
      <>
  Volumes:
      <>
Events:
  <>
```

5. 查看 ReplicaSet。从 yaml 文件来看应该有两个 Pod。你可能会看到一个 Completed byyesha，它会被清理。

```
student@lfs458-node-104a:~$ kubectl get pods
NAME             READY   STATUS    AGE
rs-one-2p99x      1/1     Running   5s
rs-one-3c6pb      1/1     Running   5s
```

6. 现在我们删除 ReplicaSet，但不删除 Pod。

```
student@lfs458-node-104a:~$ kubectl delete rs rs-one --cascade=false
replicaset.extensions "rs-one" deleted
```

查看 ReplicaSet 和 Pods：

```
student@lfs458-node-104a:~$ kubectl describe rs rs-one
Error from server (NotFound): replicasets.extensions "rs-one" not found
```

```
student@lfs458-node-104a:~$ kubectl get pods
```

### 7.1. 实验

| NAME | STATUS | RESTARTS | AGE |
| :--- | :--- | :--- | :--- |
| rs-one-2p9x4 | 1/1 Running | 0 | 7m |
| rs-one-3c6pb | 1/1 Running | 0 | 7m |

8. 创建 ReplicaSet，只要我们不更改选择器字段，新的 ReplicaSet 应该获得所有权。Pod 软件无法通过这种方式更新。

```
student@lfs458-node-ia0a:~$ kubectl create -f rs.yaml
replicaset.extensions/rs-one created
```

9. 查看 ReplicaSet 和 Pods 的年龄：

```
student@lfs458-node-ia0a:~$ kubectl get rs
NAME DESIRED CURRENT READY AGE
rs-one 2 2 4s
```

```
student@lfs458-node-ia0a:~$ kubectl get pods
NAME READY STATUS RESTARTS AGE
rs-one-2p9x4 1/1 Running 0 8m
rs-one-3c6pb 1/1 Running 0 8m
```

10. 我们将从其 ReplicaSet 中添加一个 Pod。首先给 Pod 标记标签。我们将 `system-parameter` 修改为 `IsolatedPod`。

```
student@lfs458-node-ia0a:~$ kubectl edit pod rs-one-3c6pb
...
labels:
  system: IsolatedPod # Change from ReplicaOne
  name: rs-one-3c6pb
...
```

11. 查看 ReplicaSet 中 pod 的数量。你应该看到两个正在运行。

```
student@lfs458-node-ia0a:~$ kubectl get rs
NAME DESIRED CURRENT READY AGE
rs-one 2 2 4m
```

12. 查看带有 `system` 标签键的 pods。你应该注意到有三个，其中一个比其他的新的。ReplicaSet 被创建用来替换你的，替换了我们创建的那个 Pod。

```
student@lfs458-node-ia0a:~$ kubectl get pod -L system
NAME READY STATUS RESTARTS AGE SYSTEM
rs-one-3c6pb 1/1 Running 0 5m IsolatedPod
rs-one-2p9x4 1/1 Running 0 7m ReplicaOne
rs-one-3c6pb 1/1 Running 0 7m ReplicaOne
```

13. 删除 ReplicaSet，但保留 Pods。

```
student@lfs458-node-ia0a:~$ kubectl delete rs rs-one --cascade=false
replicaset.extensions "rs-one" deleted
```

查看 ReplicaSet 和 Pods：

```
student@lfs458-node-ia0a:~$ kubectl describe rs rs-one
Error from server (NotFound): replicasets.extensions "rs-one" not found
```

```
student@lfs458-node-ia0a:~$ kubectl get pods
```

14. 再次查看 ReplicaSet。它看到正在运行的 Pod。

```
student@lfs458-node-ia0a:~$ kubectl get pods
NAME READY STATUS
AGE
rs-one-2p9x4 1/1 Running 0 8m
rs-one-3c6pb 1/1 Running 0 8m
```

15. 查看 ReplicaSet。 Pods

```。

```

fs555----0

kubectl.extensions

rs-one 

 2 4s

```



# 第 7 章：通过部署管理状态

挂载：<none>
卷：<none>

```
student@lfs458-node-10a:~$ kubectl rollout history ds ds-one --revision=2
```

```
Image: nginx:1.8.1-alpine
```

8. 使用 `kubectl rollout` 将 DaemonSet 更改到早期的版本。由于我们仍然使用 `OnDelete`（删除时）策略，Pods 不应发生任何变化。

```
student@lfs458-node-10a:~$ kubectl undo ds-one --to-revision=1
daemonset.extensions/ds-one rolled back
```



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```



```bash
student@ef458-node-la0a:~$ kubectl create -f simpleshell.yaml

pod/shell-demo created
```

```bash
student@ef458-node-la0a:~$ kubectl exec -it shell-demo \
  --bin/bash -c 'env' \
  --shell-demo

HOSTNAME=13.6.0.1-14-stretch
NGINX_VERSION=1.13.6-1stretch
black=
known as key
favorite=blue

<output_omitted>
```

```bash
student@ef458-node-la0a:~$ kubectl delete pod shell-demo

pod "shell-demo" deleted
```

### 7. 从 YAML 文件创建 ConfigMap

ConfigMap 也可以从 YAML 文件创建。创建一个包含几个描述汽车参数的 ConfigMap。

```bash
student@if8s458-node-10a:~$ vim car-map.yaml

apiVersion: v1
kind: ConfigMap
metadata:
  name: fast-car
namespace: default
data:
  car.make: Ford
  car.model: Mustang
  car.trim: Shelby
```

### 8. 创建 ConfigMap 并验证设置

```bash
student@if8s458-node-10a:~$ kubectl create -f car-map.yaml

configmap/fast-car created
```

```bash
student@if8s458-node-10a:~$ kubectl get configmap fast-car -o yaml

apiVersion: v1
data:
  car.make: Ford
  car.model: Mustang
  car.trim: Shelby
kind: ConfigMap

output: omitted:
```

### 9. 将 ConfigMap 以挂载卷的形式提供给 Pod

我们现在将把 ConfigMap 以挂载卷的形式提供给 Pod。你可以注释掉之前的环境变量设置并添加新的段。`containers:` 和 `volumes:` 条目对应的缩进空格数相同。

```bash
student@if8s458-node-10a:~$ vim simpleshell.yaml

<output_omitted>

spec:
  containers:
    - name: nginx
      image: nginx
      volumeMount:
        - name: car-vol
          mountPath: /etc/cars
  volumes:
    - name: car-vol
      configMap:
        name: fast-car
```

### 10. 创建 Pod 并验证卷

创建 Pod，验证卷是否存在以及内容。由于缺少换行符，你的下一个提示可能在同一行。

```bash
student@if8s458-node-10a:~$ kubectl create -f simpleshell.yaml

pod "shell-demo" created
```

```bash
student@if8s458-node-10a:~$ kubectl exec -it shell-demo \
  --bin/bash -c 'df -'

/dev/sda 20G 4.7G 25
```

```bash
student@if8s458-node-10a:~$ kubectl exec -it shell-demo \
  --bin/bash -c 'ls /etc/cars'
```

### 11. 删除 Pod 和 ConfigMap

```bash
student@if8s458-node-10a:~$ kubectl delete pod shell-demo

pod "shell-demo" deleted
```

```bash
student@if8s458-node-10a:~$ kubectl delete configmap fast-car

configmap "fast-car" deleted
```

## 9.2：创建持久化卷（PV）

我们将在节点上创建一个持久化卷。

### 1. 确定 PV 当前是否存在

```bash
student@ef458-node-la0a:~$ kubectl get pv

No resources found.
```

### 2. 为新的 PV 创建 YAML 文件

```bash
student@ef458-node-la0a:~$ vim pv.yaml

apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-example
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: /mnt/data
```

### 3. 编辑 PV 以匹配目录

```bash
student@ef458-node-la0a:~$ vim pv.yaml

# (编辑内容)
```

### 4. 查看 PV 的状态

查看 PV 的状态，确定它是否被使用。

```bash
student@ef458-node-la0a:~$ kubectl get pv
```

### 5. 测试持久化卷

```bash
student@ef458-node-la0a:~$ kubectl create -f pv.yaml

persistentvolume/pv-example created
```

### 6. 返回主节点

## 9.1. 实验室

```bash
student@lfs458-node-laa0a:~$ cp first.yaml nfs-pod.yaml
```

```bash
student@lfs458-node-laa0a:~$ vim nfs-pod.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
    generation: 1
  labels:
    run: nginx
  name: nginx-nfs
  namespace: default
  resourceVersion: "1411"
spec:
  replicas: 1
  selector:
    matchLabels:
      run: nginx
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        run: nginx
    spec:
      containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
        volumeMounts:
        - name: nfs-vol
          mountPath: /opt
        ports:
        - containerPort: 80
          protocol: TCP
      resources:
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
volumes:
- name: nfs-vol
  persistentVolumeClaim:
    claimName: pvc-claim
dnPolicy: ClusterFirst
  restartPolicy: Always
schedulerName: default-scheduler
securityContext: {}
  terminationGracePeriodSeconds: 30
```

### 6. 使用新编辑的文件创建 Pod

```bash
student@lfs458-node-laa0a:~$ kubectl create -f nfs-pod.yaml

deployment.apps/nginx-nfs created
```

### 7. 查看 Pod 的详细信息

你可能会看到 daemon pods 正在运行。

```bash
student@lfs458-node-1oa0:~$ kubectl get pods

NAME                             STATUS    RESTARTS AGE
nginx-nfs-1054079768-s8g28      Running   1        0 3m
```

```bash
student@lfs458-node-1oa0:~$ kubectl describe pod nginx-nfs-1054079768-s8g28

Name:               nginx-nfs-1054079768-s8g28
Namespace:          default
Node:               ifs458-worker/10.128.0.5
```

```text
<output_omitted>
Mounts:
  /opt from nfs-vol (rw)
```

```text
<output_omitted>
Volumes:
  nfs-vol:
    Type:               PersistentVolumeClaim (a reference to a PersistentV...
    ClaimName:          pvc-one
    ReadOnly:           false
```

### 8. 查看 PVC 的状态

PVC 应该显示为 `bound`（已绑定）。

```bash
student@lfs458-node-1oa0:~$ kubectl get pvc

NAME     STATUS  CAPACITY  ACCESS MODES  STORAGECLASS  AGE
pvc-one  Bound   pvvol-1   1Gi           RW             2m
```

### 练习 9.4：使用 ResourceQuota 限制 PVC 数量和使用

云存储的灵活性要求限制用户之间的消耗。我们将使用 ResourceQuota 对象来限制总消耗以及持久化卷声明（persistent volume claims）的数量。

#### 1. 删除用于 NFS 的部署、PV 和 PVC

```bash
student@lfs458-node-1oa0:~$ kubectl delete nginx-nfs

deployment.apps/"nginx-nfs" deleted
```

```bash
student@lfs458-node-1oa0:~$ kubectl delete pvc-one

persistentvolumeclaim "pvc-one" deleted
```

```bash
student@lfs458-node-1oa0:~$ kubectl delete pv pvvol-1

persistentvolume "pvvol-1" deleted
```

#### 2. 为 ResourceQuota 对象创建 YAML 文件

设置存储限制，以限制总量为 `500Mi` 的声明。

```bash
student@lfs458-node-1oa0:~$ vim storage-quota.yaml
```

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: storagequota
spec:
  hard:
    persistentvolumeclaims: "10"
    requests.storage: "500Mi"
```

![](img/7b8a27c9e8a5a4b2faa64ee2b38e8e6d_71_0.png)

#### 3. 创建新的命名空间 `small`

创建一个新的 namespace `small`。在设置新配额之前查看命名空间信息。可以使用带有双横杠 `--namespace` 的长名或别名作为资源名称。

```bash
student@lfs458-node-la0a~$ kubectl create namespace small

namespace/small created
```

```bash
student@lfs458-node-la0a~$ kubectl describe ns small

Name:
  small
Labels:
  <none>
Annotations:
  <none>
Status:
  Active

No resource quota.
```

No resource limits.

#### 4. 在 `small` 命名空间创建新的 PV 和 PVC

```bash
student@lfs458-node-la0a~$ kubectl create -f pvol.yaml -n small

persistentvolume/pvvol-1 created
```

```bash
student@lfs458-node-la0a~$ kubectl create -f pvc.yaml -n small

ppersistentvolumeclaim/pvc-one created
```

#### 5. 创建新的资源配额

创建新的资源配额，将其放在低使用率命名空间内。

```bash
student@lfs458-node-la0a~$ kubectl create -f storage-quota.yaml \
  n small

resourcequota/storage-quota created
```

#### 6. 验证 `small` 命名空间是否有配额

将输出与上述相同命令进行比较。

```bash
student@lfs458-node-la0a~$ kubectl describe ns small

Name:
  small
Labels:
  <none>
Annotations:
  <none>
Status:
  Active
```

| Resource Quotas | | storagequota |
| --- | --- | --- |
| persistentvolumeclaims | 1 | 10 |
| requests.storage | 200Mi | 500Mi |

No resource limits.

#### 7. 从 `nfs-pod.yaml` 文件中删除命名空间行

应该在第 11 行左右。这将允许你在命令行上传递其他命名空间。

```bash
student@lfs458-node-la0a~$ vim nfs-pod.yaml
```

#### 8. 创建容器

```bash
student@lfs458-node-la0a~$ kubectl create -f nfs-pod.yaml \
  n small

deployment.apps/nginx-nfs created
```

#### 9. 确定部署是否有一个运行的 Pod

# 第 9 章 卷与数据

```bash
student@lfs458-node-laa0a:~$ cp first.yaml nfs-pod.yaml
```

```bash
student@lfs458-node-laa0a:~$ vim nfs-pod.yaml
```



# 第 9 章 卷与数据

```bash
student@lfs458-node-laa0a:~$ cp first.yaml nfs-pod.yaml
```

```bash
student@lfs458-node-laa0a:~$ vim nfs-pod.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
    generation: 1
  labels:
    run: nginx
  name: nginx-nfs
  namespace: default
  resourceVersion: "1411"
spec:
  replicas: 1
  selector:
    matchLabels:
      run: nginx
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        run: nginx
    spec:
      containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
        volumeMounts:
        - name: nfs-vol
          mountPath: /opt
        ports:
        - containerPort: 80
          protocol: TCP
      resources:
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
volumes:
- name: nfs-vol
  persistentVolumeClaim:
    claimName: pvc-claim
dnPolicy: ClusterFirst
  restartPolicy: Always
schedulerName: default-scheduler
securityContext: {}
  terminationGracePeriodSeconds: 30
```

6. 使用新编辑的文件创建 pod。

```bash
student@lfs458-node-laa0a:~$ kubectl create -f nfs-pod.yaml
deployment.apps/nginx-nfs created
```

7. 查看 pod 的详细信息。你可能会看到 daemon pods 正在运行。

```bash
student@lfs458-node-1oa0:~$ kubectl get pods
NAME                             STATUS RESTARTS AGE
nginx-nfs-1054079768-s8g28      Running   1      0 3m
```

```bash
student@lfs458-node-1oa0:~$ kubectl describe pod nginx-nfs-1054079768-s8g28
Name:               nginx-nfs-1054079768-s8g28
Namespace:          default
Node:               ifs458-worker/10.128.0.5
```

```
<output_omitted>
Mounts:
  /opt from nfs-vol (rw)
```

```
<output_omitted>
Volumes:
  nfs-vol:
    Type:               PersistentVolumeClaim (a reference to a PersistentV...
    ClaimName:         pvc-one
    ReadOnly:           false
```

8. 查看 PVC 的状态。它应该显示为 bound（已绑定）。

```bash
student@lfs458-node-1oa0:~$ kubectl get pvc
NAME             STATUS CAPACITY ACCESS MODES STORAGECLASS AGE
pvc-one           Bound   pvvol-1  1Gi       RW                    2m
```

### 练习 9.4：使用 ResourceQuota 限制 PVC 数量和使用

云存储的灵活性要求限制用户之间的消耗。我们将使用 ResourceQuota 对象来限制总消耗以及持久化卷声明（persistent volume claims）的数量。

- 1. 通过开始我们创建的用于 NFS 的部署、pv 和 pvc。

```bash
student@lfs458-node-1oa0:~$ kubectl delete nginx-nfs
deployment.apps/"nginx-nfs" deleted
```

```bash
student@lfs458-node-1oa0:~$ kubectl delete pvc-one
persistentvolumeclaim "pvc-one" deleted
```

```bash
student@lfs458-node-1oa0:~$ kubectl delete pv pvvol-1
persistentvolume "pvvol-1" deleted
```

- 2. 为 ResourceQuota 对象创建一个 yaml 文件。设置存储限制，以限制总量为 500Mi 的声明。

```bash
student@lfs458-node-1oa0:~$ vim storage-quota.yaml
```

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: storagequota
spec:
  hard:
    persistentvolumeclaims: "10"
    requests.storage: "500Mi"
```

![](img/7b8a27c9e8a5a4b2faa64ee2b38e8e6d_71_0.png)

3. 创建一个新的 namespace small。在设置新配额之前查看命名空间信息。可以使用带有双横杠 `--namespace` 的长名或别名作为资源名称。

```bash
student@lfs458-node-la0a~$ kubectl create namespace small
namespace/small created
```

```bash
student@lfs458-node-la0a~$ kubectl describe ns small
Name:
  small
Labels:
  <none>
Annotations:
  <none>
Status:
  Active

No resource quota.
```

No resource limits.

4. 在 small 命名空间创建一个新的 pv 和 pvc。

```bash
student@lfs458-node-la0a~$ kubectl create -f pvol.yaml -n small
persistentvolume/pvvol-1 created
```

```bash
student@lfs458-node-la0a~$ kubectl create -f pvc.yaml -n small
ppersistentvolumeclaim/pvc-one created
```

5. 创建新的资源配额，将其放在低使用率命名空间内。

```bash
student@lfs458-node-la0a~$ kubectl create -f storage-quota.yaml \
  n small
resourcequota/storage-quota created
```

6. 验证 small 命名空间是否配配额。将输出与上述相同命令进行比较。

```bash
student@lfs458-node-la0a~$ kubectl describe ns small
Name:
  small
Labels:
  <none>
Annotations:
  <none>
Status:
  Active
```

| Resource Quotas | | storagequota |

| --- | --- | --- |

| persistentvolumeclaims | 1 | 10 |

| requests.storage | 200Mi | 500Mi |

No resource limits.

7. 从 nfs-pod.yaml 文件中删除命名空间行。应该在第 11 行左右。这将允许你在命令行上传递其他命名空间。

```bash
student@lfs458-node-la0a~$ vim nfs-pod.yaml
```

8. 创建容器。

```bash
student@lfs458-node-la0a~$ kubectl create -f nfs-pod.yaml \
  n small
deployment.apps/nginx-nfs created
```

9. 确定部署是否有一个运行的 pod。



6. 验证`small`命名空间是否配配额。将输出与上述相同命令进行比较。

```bash
student@lfs458-node-la0a~$ kubectl describe ns small
Name:
  small
Labels:
  <none>
Annotations:
  <none>
Status:
  Active
```

| Resource Quotas | | storagequota |

| --- | --- | --- |

| persistentvolumeclaims | 1 | 10 |

| requests.storage | 200Mi | 500Mi |

No resource limits.

7. 从`nfs-pod.yaml`文件中删除命名空间行。应该在第 11 行左右。这将允许你在命令行上传递其他命名空间。

```bash
student@lfs458-node-la0a~$ vim nfs-pod.yaml
```

8. 创建容器。

```bash
student@lfs458-node-la0a~$ kubectl create -f nfs-pod.yaml \
  n small
deployment.apps/nginx-nfs created
```

9. 确定部署是否有一个运行的 pod。

# 第 9 章 卷与数据

```bash
student@lfs458-node-laa0a:~$ cp first.yaml nfs-pod.yaml
```

```bash
student@lfs458-node-laa0a:~$ vim nfs-pod.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
    generation: 1
  labels:
    run: nginx
  name: nginx-nfs
  namespace: default
  resourceVersion: "1411"
spec:
  replicas: 1
  selector:
    matchLabels:
      run: nginx
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        run: nginx
    spec:
      containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
        volumeMounts:
        - name: nfs-vol
          mountPath: /opt
        ports:
        - containerPort: 80
          protocol: TCP
      resources:
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
volumes:
- name: nfs-vol
  persistentVolumeClaim:
    claimName: pvc-claim
dnPolicy: ClusterFirst
  restartPolicy: Always
schedulerName: default-scheduler
securityContext: {}
  terminationGracePeriodSeconds: 30
```

19. 我们使用`kubectl patch`将保留策略更改为`Delete`。之前的 yaml 输出可以帮助获取正确的语法。

```bash
student@lfs458-node-1oa0$: kubectl patch pv pvvol-1 -p \
  '{"persistentVolumeReclaimPolicy": "Delete"}'
  persistentvolume/pvvol-1 patched
```

```bash
student@lfs458-node-1oa0$: kubectl get pv/pvvol-1
| NAME | CAPACITY | AGE | RECLAIMPOLICY | CLAIM | STORAGECLASS | REASON |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| pvvol-1 | 1Gi | 2m | Delete | Available | RW | |
```

20. 查看当前的配额。

```bash
student@lfs458-node-1oa0$: kubectl describe ns small
requests.storage 0 500Mi
```

21. 再次创建 pvc。在没有 pod 运行的情况下，注意资源的使用情况。

```bash
student@lfs458-node-1oa0$: kubectl -n small create -f pvc.yaml
  persistentvolumeclaim/pvc-one created
student@lfs458-node-1oa0$: kubectl describe ns small
requests.storage 200Mi 500Mi
```

22. 从命名空间中删除现有配额。

```bash
student@lfs458-node-1oa0$: kubectl -n small get resourcequota
NAME          CREATED                               AT
storagequota  2018-08-01T04:10:02Z
student@lfs458-node-1oa0$: kubectl -n small delete resourcequota
resourcequota/storage deleted
```

23. 编辑`storage-quota.yaml`并将容量降低到 100Mi。

```bash
student@lfs458-node-1oa0$: vim storage-quota.yaml
requests.storage: "100Mi",
```

24. 创建并验证新配额。注意硬限制已超出。

```bash
student@lfs458-node-1oa0$: kubectl create -f storage-quota.yaml -n small
  resourcequota/storage created
student@lfs458-node-1oa0$: kubectl describe ns small
persistentvolumeclaims 1
requests.storage 200Mi 100Mi
```

25. 再次创建部署。查看部署。注意没有错误。

## 9.1. 实验

```bash
student@lfs458-node-1oa0$: kubectl create -f nginx.yaml -n small
  deployment.apps/nginx-nfs created
student@lfs458-node-1oa0$: kubectl -n small describe deployment/nginx-nfs
Name: nginx-nfs
Namespace: small
<itted>
```

26. 检查 pods 以查看它们是否正在运行。

```bash
student@lfs458-node-1oa0$: kubectl -n small get pods
| NAME | READY | STATUS | RESTARTS | AGE |
| :--- | :--- | :--- | :--- | :--- |
| nginx-nfs | 1/1 | Running | 0 | 58s |
```

27. 既然我们甚至没有硬配额就能部署 pod，让我们测试一下存储删除是否发生。删除持久卷声明。

```bash
student@lfs458-node-1oa0$: kubectl -n small delete deployment-nfs
  deployment.extensions/nginx-nfs deleted
student@lfs458-node-1oa0$: kubectl -n small delete pvc/pvc-one
  persistentvolumeclaim/pvc-one deleted
```

28. 查看持久卷。你会看到它被删除，但失败了。如果你仔细观察，会发现错误是缺少 NFS 的删除器。其他协议都有。

```bash
student@lfs458-node-1oa0$: kubectl -n small get pv
| NAME | CAPACITY | RECLAIMPOLICY | STATUS | CLAIM | STORAGECLASS | AGE |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| pvvol-1 | 1Gi | | Failed | small/pvc-one | | 20m |
```

29. 确保部署、pod 和 pv 都已删除。

```bash
student@lfs458-node-1oa0$: kubectl delete pv/pvvol-1
  persistentvolume/pvvol-1 deleted
```

30. 编辑持久卷 YAML 文件并将`persistentVolumeReclaimPolicy:`改为`Recycle`。

```bash
student@lfs458-node-1oa0$: vim PV.yaml
...
persistentVolumeReclaimPolicy: Recycle
...
```

31. 向命名空间中添加 LimitRange 并再次创建持久卷和持久卷声明。我们可以使用之前使用的 LimitRange。

```bash
student@lfs458-node-1oa0$: kubectl -n small -f low-resource-range.yaml
  limitrange/low-resource-range created
```

32. 查看命名空间的限制。应该能看到配额和资源限制。

```bash
student@lfs458-node-1oa0$: kubectl describe ns small
<itted>
Resource Limits:
| Type | Resource | Max | Default Request | Default Limit |
| :--- | :--- | :--- | :--- | :--- |
| Container | cpu | 500Mi | 1 | 500Mi |
| Container | memory | 100Mi | | 500Mi |
```

# 第 9 章 卷与数据

33. 创建持久卷声明。查看资源。Reclaim Policy 为 Recycle。

```bash
student@lfs458-node-1oa0$: kubectl -n small -f PV.yaml
  persistentvolume/pvvol-1 created
student@lfs458-node-1oa0$: kubectl get pv
| NAME | CAPACITY | ACCESS MODES | RECLAIM POLICY | STATUS |
| :--- | :--- | :--- | :--- | :--- |
| pvvol-1 | 1Gi | RWX | Recycle | Available |
```

34. 尝试创建持久卷声明。只有在资源限制生效时才会触发配额。

```bash
student@lfs458-node-1oa0$: kubectl -n create -f pvc.yaml
Error from server (Forbidden): error when creating "pvc.yaml":
persistentvolumeclaims/pvc-one is forbidden: exceeded quota: requested.storage=200Mi, used:storage=0, limited:storage=100Mi
```

35. 修改 resourcequota 将 requests 增加到 500Mi。

```yaml
spec:
hard:
  persistentvolumeclaims: "10"
  requests.storage: 500Mi
status:
```

36. 创建 pvc。现在应该可以了。然后创建部署。

```bash
student@lfs458-node-1oa0$: kubectl -n small -f pvc.yaml
  persistentvolumeclaims/pvc-one created
student@lfs458-node-1oa0$: kubectl -n small -f nginx-pod.yaml
  deployment.apps/nginx-nfs created
```

37. 查看命名空间。

```bash
student@lfs458-node-1oa0$: kubectl -n small describe
<itted>
```

38. 删除部署。查看 pv 和 pvc 的状态。

```bash
student@lfs458-node-1oa0$: kubectl -n small delete nginx-nfs
  deployment.extensions/nginx-nfs deleted
student@lfs458-node-1oa0$: kubectl -n small get
| NAME | STATUS | CAPACITY | ACCESS MODES | STORAGECLASS | AGE |
| :--- | :--- | :--- | :--- | :--- | :--- |
| pvvol-1 | Bound | 1Gi | RWX | | 7m |
```

39. 删除 pvc 并检查 pv 的状态。应该显示：

```bash
student@lfs458-node-1oa0$: kubectl -n small delete pvc-one
  persistentvolumeclaims/pvc-one deleted
student@lfs458-node-1oa0$: kubectl -n small get
| NAME | CAPACITY | ACCESS MODES | RECLAIM POLICY | STATUS | CLAIM |
| :--- | :--- | :--- | :--- | :--- | :--- |
| pvvol-1 | 1Gi | RWX | Recycle | Available |
```

40. 删除 pv 以及实验期间创建的任何资源。

```bash
student@lfs458-node-1oa0$: kubectl delete pv pvvol-1
  persistentvolume/pvvol-1 deleted
```

# 第 10 章

# Ingress.io

### 10.1 实验

### 练习 10.1：高级服务暴露

### 配置 Ingress Controller

对于这样一个更新快速的项目，跟踪更新非常重要。查找文档的主要地方是 https://kubernetes.io/。

- 如果你有大量的服务需要暴露到集群之外，或者要在主机节点上暴露低位端口，你可以部署 ingress 控制器或服务网格。nginx 和 G 有 Kubernetes.io 支持的控制器，目前 Traefik ingress 控制器更容易安装。

```bash
student@lfs458-node-1oa0$: create deployment secondapp --image=nginx
```

- 找到部署当前使用的标签。我们将使用它们将来自 ingress 控制器的流量绑定到正确的服务。

```bash
student@lfs458-node-1oa0$: kubectl get deployments secondapp -o yaml | grep label -A2
labels:
  app: secondapp
  name: secondapp
```

- 将新服务器作为 NodePort 暴露。

```bash
student@lfs458-node-1oa0$: kubectl expose deployment secondapp --type=NodePort --port=80
```

4. 由于我们配置了 RBAC，我们需要声明控制器能够处理所有必要的端口、端点和资源。创建一个 YAML 文件来声明 clusterrole 和 clusterrolebinding。



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```



`secondary-8f756cd9dc5-2qx9` 1/1 Running 0 43m

`thirdparty-7c9c5bbdd-2fqqr` 1/1 Running 0 20m

```bash
student@lfs458-node-1oaa:$ kubectl create -f vip.yaml
pod/vip created
```

10. 确定新容器部署在何处。它们应该分布得更均匀。

```bash
student@lfs458-node-1oaa:$ sudo docker ps | wc -l
24

student@lfs458-worker:$ sudo docker ps | wc -l
19
```

11. 为其他用户创建另一个文件。将名称从 `vip` 更改为 `others`，并取消 `nodeSelector` 行的注释。

```bash
student@lfs458-node-1oaa:$ cp vip.yaml other.yaml
student@lfs458-node-1oaa:$ sed -i 's/vip/other/g' other.yaml
```

```bash
student@lfs458-node-1a0a:~$ vim other.yaml
```

```yaml
nodeSelector:
  status: other
```

12. 创建其他容器。确定它们部署在哪里。

```bash
student@lfs458-node-1a0a:~$ kubectl create -f other.yaml
pod/created
```

```bash
student@lfs458-node-1a0a:~$ sudo docker ps | wc -l
24
```

```bash
student@lfs458-worker:~$ sudo docker ps | wc -l
24
```

13. 关闭两个 pod 并验证它们。应该只能找到我们之前的 pod。

```bash
student@lfs458-node-1a0a:~$ kubectl delete pods vip other
pod "vip"
pod "other" deleted
```

```bash
student@lfs458-node-1a0a:~$ kubectl get pods
NAME                READY STATUS AGE
s-one-bd4qt         1/1 Running 0 153m
d-one-t2t7z         1/1 Running 0 166m
secondapp-8576c5d5c-2q9x 1/1 Running 0 51m
thirdparty-7c9b56bfdd-2q5pr 1/1 Running 0 28m
```

### 练习 11：使用污点（Taints）控制 Pod 部署

使用污点来管理 pod 的部署或允许运行。在为一组节点分配污点时，你可能还想限制节点的使用或完全驱逐 pod。使用污点是实现这一目标的方法。你可能记得主节点有一个 `NoSchedule` 污点。我们将使用三种污点来限制或移除 pod。

1. 验证主节点和备节点运行的容器数量最少。

```bash
student@lfs458-node-1a0a:~$ kubectl delete deployment secondapp \
thirdparty
deployment.extensions "secondapp" deleted
deployment.extensions "thirdparty" deleted
```

2. 通过创建一个 YAML 文件创建一个部署八个 nginx 容器的部署。

```bash
student@lfs458-node-1a0a:~$ vim apps/v1beta
```

```yaml
apiVersion: apps/v1beta
kind: Deployment
metadata:
  name: taint-deployment
spec:
  replicas: 8
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:1.7.9
          ports:
            containerPort: 80
```

3. 将文件应用到部署。

```bash
student@lfs458-node-1a0a~$ sudo kubectl apply -f taint.yaml
deployment.apps/taint-deployment created
```

4. 确定容器运行在哪里。在下面的示例中，三个被部署在主节点和第二个节点上。请记住还会创建一些管理容器。数字可能会略有不同。

```bash
student@lfs458-node-1a0a~$ sudo docker ps | grep nginx
001cbe5d1fe7  nginx@sha256:e3456c851a52494c3e..
  <output_omitted>
```

```bash
student@lfs458-node-1a0a~$ sudo docker ps | wc -l
28

student@lfs458-worker~$ sudo docker ps | wc -l
26
```

5. 删除部署。验证容器已消失。

```bash
student@lfs458-node-1a0a~$ kubectl delete deployment taint-deployment
deployment.apps/taint-deployment deleted

student@lfs458-node-1a0a~$ sudo docker ps | wc -l
24
```

### 11.1 实验

```bash
student@lfs48-worker:~$ sudo docker ps wc -l
6
```

13. 除了对节点设置污点（taint）外，你还可以设置排空（drain）。查看状态，然后销毁现有的部署（deployment）。注意，状态报告显示由 DaemonSet 管理，尽管它不会允许容器执行。还要注意，正如我们在较早的实验中看到的，输出中提到的受 DaemonSet 管理的节点在默认情况下不受影响的。这次，我们将仔细观察在对节点和 pod 设置污点时会发生什么。

现有的容器会被移动，但不会创建新容器。你可能会收到错误：`unreal: unable to drain node "your node", aborting command...`

```bash
student@lfs48-node-ia0a:~$ kubectl get nodes
NAME STATUS ROLES AGE VERSION
lfs48-node-ia0a Ready master 2d v1.12.1
lfs48-worker Ready <none> 2d v1.12.1
```

```bash
student@lfs48-node-ia0a:~$ kubectl delete lfs48-worker
node/lfs48-worker cordoned
error: DaemonSet-managed pods (--ignore=daemonsets to ignore): kube-fannel-ds-fx3x, kube-proxy-q2q4k
```

14. 验证节点状态。它应该指示将不再有新的 Pod 被调度。

```bash
student@lfs48-node-ia0a:~$ kubectl get nodes
NAME STATUS ROLES AGE VERSION
lfs48-node-ia0a Ready master 2d v1.12.1
lfs48-worker Ready,SchedulingDisabled <none> 2d v1.12.1
```

15. 删除以重新部署当前的 pod。

```bash
student@lfs48-node-ia0a:~$ kubectl delete deployment taint-deployment
deployment.extensions/taint-deployment deleted
```

16. 创建部署并确定容器被部署在何处。

```bash
student@lfs48-node-ia0a:~$ kubectl apply -f taint.yaml
deployment.apps/taint-deployment created
```

```bash
student@lfs48-node-ia0a:~$ sudo docker ps wc -l
44
```

17. 返回状态界面，然后销毁并创建部署。容器应该分布在各个节点上。通过移除节点的封锁（cordon）。

```bash
student@lfs48-node-ia0a:~$ kubectl uncord lfs48-worker
node/lfs48-worker uncordoned
```

```bash
student@lfs48-node-ia0a:~$ kubectl get nodes
NAME STATUS ROLES AGE VERSION
lfs48-node-ia0a Ready master 2d v1.12.1
lfs48-worker Ready <none> 2d v1.12.1
```

18. 删除并重建部署。

```bash
student@lfs48-node-ia0a:~$ kubectl delete deployment taint-deployment
deployment.extensions/taint-deployment deleted
```

```bash
student@lfs48-node-ia0a:~$ kubectl apply -f taint.yaml
deployment.apps/taint-deployment created
```

19. 再次查看 `docker ps` 的输出。两个节点部署的容器数量应该几乎相同。由于角色原因，master 节点会多几个。

20. 最后删除部署以释放资源。

```bash
student@lfs458-node-1a0a:~$ kubectl delete deployment taint-deployment deployment.extensions "taint-deployment" deleted
```

# 第 12 章 日志记录与故障排除

### 12.1 实验

### 练习 12.1：回顾日志文件位置

### 概述

除了各种日志文件和命令输出外，你还可以使用 `journalctl` 从节点的角度查看日志。我们将查看日志文件的常见位置，然后是查看容器日志的命令。还有其他日志选项，例如使用专门的 `sidecar` 容器来加载 pod 中另一个容器的日志。

Kubernetes 尚未支持全集群日志。通常使用外部软件，例如 `Fluentd`（它是 https://fluentd.org/ 的一部分，它是 Kubernetes 的另一个 CNCF 成员项目）。

### 回顾日志文件位置

快速查看以下日志文件和网站。随着服务器进程从节点级移动到容器中运行，日志也随之移动。

1. 如果使用基于 `systemd` 的 Kubernetes 集群来查看 `kubelet`（本地 Kubernetes 代理）的节点级，每个节点的内容不同，因为这是节点特定的。

```bash
student@ifs468-node-1ao0$: journalctl -u kubectl | less
<output_omitted>
```

2. 主要 Kubernetes 进程现在运行在容器中。你可以从容器或节点的角度查看它们。使用 `find` 命令定位 `kube-apiserver` 日志。你的输出将不同，但会很长。一旦定位到文件，使用 `diff` 工具进行比较。应该没有差异，因为它们是 `/var/log/pods/` 的符号链接。如果你跟随链接，日志文件是唯一的。

```bash
student8if458-node-10a$: sudo less -f /var/log/containers/kube-apiserver-u16-12-1dc3b8-system-kube-apiserver-edoa7079382cd32c5f48b461925d1b52033a.log
/var/log/containers/kube-apiserver-u16-12-1dc3b8-system-kube-apiserver-edoa7079382cd32c5f48b461925d1b552033a.log

student8if458-node-10a$: sudo less /var/log/containers/kube-apiserver-u16-12-1dc3b8-system-kube-apiserver-edoa7079382cd32c5f48b461925d1b552033a.log
<output ended>
```

3. 取一个文件。
4. 在 `/var/log` 中搜索 `kube-dns`, `kube-proxy` 的其他日志项。
5. 如果不是使用 systemd 的 Kubernetes 集群，可以查看 master 节点上的文件：
   - `/var/log/kube-apiserver.log` 负责 API
   - `/var/log/kube-scheduler.log` 负责做决策
   - `/var/log/kube-controller-manager.log` 负责副本
6. `/var/log/containers` 各种容器日志
7. `/var/log/pods/` 当前 Pod 的文件
8. Worker 节点（非 systemd）：
   - `/var/log/kubelet.log` 负责节点上的容器
   - `/var/log/kube-proxy.log` 负责服务均衡
9. 更多阅读：https://kubernetes.io/tasks/debug-application-cluster/debug-service/ 和 https://kubernetes.io/tasks/debug-application-cluster/determine-pod-failure/

### 查看输出

可以使用 `kubectl` 命令查看容器状态。如果没有标准输出，看不到任何内容。此外，如果容器被销毁，可以看到日志。

1. 查看集群中的 Pod。查看所有命名空间中的 Pod：

| NAMES | READY | RESTARTS | AGE |
| :--- | :--- | :--- | :--- |
| `default-one-q27c` | 1/1 | 0 | 3h |
| `default-one-z31ra` | 1/1 | 0 | 3h |
| `kube-system-etcd-f458-node-10a` | 1/1 | 2 | 9h |
| `kube-system-kube-apiserver-lfs48-node-1aa` | 1/1 | 2 | 9h |
| `kube-system-kube-controller-manager-lfs48-node-1aa` | 1/1 | 2 | 9h |
| `kube-system-kube-dns-24252768-w0x` | 3/3 | 6 | 9h |
| `kube-system-kube-scheduler-lfs48-node-1aa` | 1/1 | 2 | 9h |

2. 查看与各种基础设施相关的日志。使用 Tab 获取列表并选择。然后你可以输入 pod 名称并按 Tab 补全。

```bash
student@lfs48-node-1aa~$ kubectl -n kube-system logs <Tab><Tab>
calico-etcd-n6h2q
etcd-lfs48-1-11-update-cm35
calico-controllers-7488b667-97d4ae
kube-apiserver-lfs48-1-11-update-cm35
calico-node-6j8hc
kube-controller-manager-lfs48-1-11-update-cm35
calico-node-dg9f8
kube-proxy-88mff
coredns-78fcdf689-7ffp9
kube-proxy-vf5dr
coredns-78fcdf689-g6k99
kube-scheduler-lfs48-1-11-update-cm35
```

```bash
student@lfs48-node-1aa~$ kubectl -n kube-system logs \
kube-apiserver-lfs48-1-11-update-cm35
Flag --insecure-port has been deprecated, This flag will
in a future version.
OT029 21:29:23.026394 1 server.go:[73] external host
was not specified, using 10.128.0.2
OT029 21:29:23.026394 1 server.go:[145] Version: v1.11.1
OT029 21:29:23.784000 1 plugins.go:[158] Loaded 8 mutating
admission controller() successfully in the following order:
```



`NamespaceLifecycle`、`LimitRange`、`ServiceAccount`、`NodeRestriction`、`Priority`、`DefaultTolerationSeconds`、`DefaultStorageClass`、`MutatingAdmissionWebhook`。

`OT029 21:29:23.784000 1 plugins.go:[161] Loaded 6 validating admission controller() successfully in the following order: LimitRange, ServiceAccount, Priority, PersistentVolumeResize, ValidatingAdmissionWebhook, ResourceQuota.`

## 第 13 章 自定义资源定义 (Custom Resource Definition)

### 13.1 实验

#### 练习 13.1：创建一个自定义资源定义

##### 概述

`ThirdPartyResource` 不再包含在 v1.8 版本的 API 中，使用它将返回验证错误。如果您从之前的版本升级到 Kubernetes v1.7，您将需要将它们转换为自定义资源 (CRD)。新资源通常需要一个控制器（controller）来管理。创建控制器的范围超出了本课程的范围，基本上它是一个监听循环（watch-loop），通过比较 spec 文件与当前状态并进行更改，直到状态匹配为止。关于创建控制器的良好讨论，可以在此处找到：https://coreos.com/blog/introducing-operators.html。

##### 创建自定义资源定义

我们将创建一个简单的 CRD，但不包含任何特定操作。只需找到被摄入 API 并响应命令的对象就足够了。

1. 我们创建一个新的 YAML 文件。

```
student@lfs45-node-la0a:~$ vim crd.yaml
```

```yaml
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: crontabs.training.lfs45.com
  # 此名称必须与下面的名称匹配。
  # <plural>.<group> 语法
spec:
  scope: Cluster # 也可以是 Namespaced
  group: training.lfs45.com
```

2. 将新资源添加到集群中。

```yaml
version: v1
names:
  kind: CronTab          # 资源清单通常使用大驼峰命名法
  plural: crontabs      # 在 URL 中显示
  singular: crontab     # CLI 别名的短名
  shortNames:
    - ct               # CLI 短名
```

```
student@lfs458-node-1ia0a$ kubectl create -f crd.yaml
customresourcedefinition.apiextensions.k8s.io/crontabs.training.lfs458.com created
```

3. 查看并描述资源。`describe` 的输出与我们目前为止看到的其他对象不同。

```
student@lfs458-node-1ia0a$ kubectl get crd
NAME                                            CREATED
crontabs.training.lfs458.com   2018-08-03T05:25:20Z
```

```
student@lfs458-node-1ia0a$ kubectl describe crd crontab<Tab>
Name:              crontabs.training.lfs458.com
Namespace:
Labels:            <none>
Annotations:       <none>
API Version:       apiextensions.k8s.io/v1
Kind:               CustomResourceDefinition
<output_omitted>
```

4. 现在我们有了一个 API 资源，可以创建一个新类型的对象。在这种情况下，它是一个类似于 crontab 的镜像，它尚不存在，但用于演示。

```yaml
apiVersion: "training.lfs458.com/v1"
  # 这来自新 CRD 的组和版本
kind: CronTab
  # 来自新 CRD 的 kind
metadata:
  name: new-cron-object
spec:
  cronSpec: "*/5 * * *"
  image: some-cron-image
  # 不存在
```

5. 使用短名和长名创建新对象和资源。

```
student@lfs458-node-1ia0a$ kubectl create -f new-crontab.yaml
crontab.training.lfs458.com/new-cron-object created
```

```
student@lfs458-node-1ia0a$ kubectl get CronTab
NAME             AGE
new-cron-object   22s
```

```
student@lfs458-node-1ia0a$ kubectl get ct
NAME             AGE
new-cron-object   29s
```

```
student@lfs458-node-1ia0a$ kubectl describe ct
```

#### 13.1. 实验

```
Name: new-object
Namespace: <none>
Labels: <output_omitted>
Spec:
Cron Spec: */5 * * * *
Image: some-cron-image
Events: <none>
```

6. 清理资源，我们将删除该 CRD。这应该也会删除所有使用它的端点和对象。

```
student@lfs458-node-la0a:~ kubectl delete -f crd.yaml
customresourcedefinition.apiextensions.k8s.io "crontabs.training.lfs458.com" deleted
```

```
student@lfs458-node-la0a:~ kubectl get ct
Error from server (NotFound): Unable to list "crontabs": the server
could not find the requested resource
(get crontabs.training.lfs458.com)
```

## 第 14 章 Kubernetes 联邦 (Federation)

### 14.1 实验

本章没有需要完成的实验。

## 第 15 章 Helm

### 15.1 实验

#### 练习 15.1：使用 Helm 和 Charts

##### 概述

Helm 允许轻松部署复杂的配置。这对于供应商单步部署多部分应用程序可能非常方便。通过使用 Chart（或模板文件），可以声明所需的组件及其关系。本地代理（如 Tiller）会代表你创建对象。实际上是它的编排工具。安装 Helm 的方法有几种。最新版本可能需要从源码编译。安装后，我们将部署一个 Chart，它将配置我们的集群。

##### 安装 Helm

1. 在主节点上使用 `wget` 下载压缩文件。下面的 URL 用于：https://storage.googleapis.com/kubernetes-helm/helm-v2.7.0-linux-amd64.gz

```
student@lfs458-node-la0a~$ wget https://storage.googleapis.com/kubernetes-helm/helm-v2.7.0-linux-amd64.gz
[output omitted]
100%[=================>] 11.6MB/s    0.1s 2018-08-03 05:34:56 (117 MB/s) saved
```

2. 解压并扩展文件：

```
student@lfs458-node-1ia0a$ tar -xvf helm-v2.7.0-linux-amd64.gz
```

*(注：此处根据上下文补全了可能的命令 `tar -xvf`)*

```
student@lfs458-node-1ia0a~$ tar -xvf helm-v2.7.0-linux-amd64.gz
helm-v2.7.0-linux-amd64/
```

3. 将二进制文件复制到 `/usr/local/bin`。

```
student@lfs458-node-1ia0a$ sudo cp helm-v2.7.0-linux-amd64/helm /usr/local/bin/
```

4. 检查权限。

```
student@lfs458-node-1ia0a$ ls -l /usr/local/bin/helm
```

5. 初始化 Tiller。

```
student@lfs458-node-1ia0a$ helm init
```

6. 为 kube-system 空间创建服务账户。

```
student@lfs458-node-1ia0a$ kubectl create serviceaccount tiller -n kube-system
```

7. 为 Tiller 绑定角色。

```
student@lfs458-node-1ia0a$ kubectl create clusterbinding tiller-admin \
  --role=cluster-admin \
  --serviceaccount=kube-system:tiller
```

8. 更新 `cluster-admin` 绑定以授予 Tiller 权限。

```
student@lfs458-node-1ia0a$ kubectl edit clusterrolebinding tiller-admin
```

9. 检查 kube-system 空间中的 Tiller 状态。

```
student@lfs458-node-1ia0a$ kubectl get serviceaccount tiller -n kube-system
```

10. 验证 Tiller Pod 正在运行。

```
student@lfs458-node-1ia0a$ kubectl get pods -n kube-system
```

11. 验证 Helm 安装成功。

```
student@lfs458-node-1ia0a$ helm version
Client: v2.7.0(GitCommit:08c11f533)
Server: v2.7.0(GitCommit:08c11f533)
```

12. 确保两者都已升级到最新版本。

```
student@lfs458-node-1ia0a$ helm init --upgrade
```

Tiller（Helm 服务端组件）已升级到当前版本。

13. Chart 是部署应用程序的集合。在 https://github.com/kubernetes/charts/tree/master 中有由供应商提供的集合，你也可以自己制作。花点时间查看 Chart。搜索可用的稳定数据库。

| NAME | VERSION | DESCRIPTION |
| --- | --- | --- |
| stable/cockrodb | 2.0.3 | CockachDB 是一个可扩展、生存的数据库... |
| stable/bitnami | 3.3.0 | Bitnami 是一个标准的数据库... |
| stable/graphgraph | 0.2 | 开源可扩展图数据库 |
| stable/kubedb | 0.1 | 已弃用的 KubeDB 由 Apps - Making... |
| stable/mariadb | 5.2.3 | 快速、可靠且易用的... |

14. 我们将安装 mariadb。查看安装详情 https://github.com/kubernetes/charts/tree/master/stable/mariadb-custom-config - `--debug` 选项允许 Chart 使用本地。注意部署名称，它将是 illmanned-salamander。此外我们不会使用持久化存储，这通常需要我们创建一个可用的。

```
student@lfs458-node-0a$ helm install illmanned-salamander stable/mariadb \
  --set persistence.enabled=false
```

我们将使用上一个命令输出末尾的一些信息来部署另一个容器并访问数据库。首先获取 `illmannered-salamander` 的 root 密码。由于该输出缺少换行符，因此下一个提示符将出现在同一行。我们需要该密码来访问运行中的 MariaDB 数据库。

```
student@fs458-node-ia0a:$ kubectl get secret -n default \
illmannered-salamander-mariadb \
-o jsonpath="${data.mariadb.root-password}" \
| base64 --decode
```

```
IFBldzAQfx
```

我们现在安装另一个容器作为数据库的客户端。我们将使用 `apt-get` 安装客户端软件。

```
student@fs458-node-ia0a:$ kubectl run -i --tty ubuntu \
--image=ubuntu:16.04 --restart=Never bash -il
如果你没有看到命令提示符，请尝试按回车。
root@ubuntu:/~
root@ubuntu:~# apt-get install -y mariadb-client
<output_omitted>
```

使用客户端访问数据库。以下命令使用了我们在上一步中找到的服务器名称和 root 密码。你们的密码会不同。

```
root@ubuntu:~# mysql -h illmannered-salamander-mariadb -p
Enter password: IFBldzAQfx
Welcome to the MariaDB server. Commands end with; or g.
Your connection ID is 153
Server version: 10.1.28-MariaDB Source distribution
Copyright (c) 2000, 2017, Oracle, MariaDB Corporation Ab and others.
Type 'help' or '\h' for help. Type '\' to clear the current input statement.
MariaDB ([none])> SHOW DATABASES;
+--------------------------------------+
| Database             |
| information_schema  |
| my_database          |
| mysql                |
| performance_schema   |
| test                 |
+--------------------------------------+
5 rows in set (0.00 sec)
MariaDB ([none])> quit
MariaDB ([none])>
root@ubuntu:~# exit
```

18. 查看历史列表。使用 `-a` 选项将显示所有 Chart，包括已删除和失败的尝试。下面的输出显示当前的 Chart 以及之前之前删除的 hadoop Chart。

```
student@fs458-node-ia0a:$ history list -a
NAME REVISION UPDATED STATUS CHART NAMESPACE
good-little 1 Wed 08:23:14 2017 DELETED hadoop-1.0.1 default
illmannered-salamander 1 Thu 09:05:12 2017 DEPLOYED mariadb-Chart.
```

19. 删除该 Chart。列表中不应显示任何输出。

#### 15.1. 实验

```
student@lfs458-node-la0a:~$ helm delete illmannered-salamander
release "illmannered-salamander" deleted
```

20. 添加另一个仓库并查看 Charts

```
student@lfs458-node-la0a:~$ helm repo add common \
```



`http://storage.googleapis.com/kubernetes-charts`

`"common"` has been added to your repositories

```
student@lfs458-node-la0a:~$ helm repo list

NAME    URL

stable https://kubernetes-charts.storage.googleapis.com

local   http://127.0.0.1:8879/charts

common  http://storage.googleapis.com/kubernetes-charts
```

```
NAME                    VERSION     DESCRIPTION

stable/acs-engine-autoscaler  2.1.0       Scales worker nodes within...

stable/artifactory             6.2.0       Universal Repository Manag...

<output_omitted>
```

## 第 16 章 安全

### 16.1 实验

#### 练习 16.1：使用 TLS

##### 概述

我们学习了带有 TLS 连接访问集群的流程，然后是身份验证以及授权，最后准入控制插件在请求执行之前允许高级功能。使用 Initializers（初始化器）允许像 shell 脚本一样动态修改请求。由于安全性是一个重要且持续关注的问题，根据集群的需求，可能会使用多种配置。

每个向集群发送 API 请求的进程必须经过身份验证或被视为匿名用户。

##### 使用 TLS

虽然默认情况下用户可能有多个集群证书颁发机构 (CA)，但每个集群都使用自己的 CA，用于内部通信。CA 证书包分发到每个节点，并作为默认服务账户的 secret。`kubelet` 是一个本地代理，确保容器运行且状态健康。

1. 查看主节点和从节点上的 `kubelet`。`kube-apiserver` 也显示证书和授权等安全信息。由于 `kubelet` 是一个系统服务，我们将查看该输出。

```
student@tls468-node-la0:~$ systemctl status kubelet.service

kubelet.service - The Kubernetes Node Agent

Loaded: loaded (/lib/systemd/system/kubelet.service; enabled; vendor preset: en

Drop-In: /etc/systemd/system/kubelet.service.d/10-kubeadm.conf
```

2. 如果我们查看状态输出并跟踪 cgroup 信息（这是一行提取配置设置的长行），我们就能找到配置文件的位置。

```
CGroup: /system.slice/kubelet.service

19523 /usr/bin/kubelet --config=/var/lib/kubelet/config.yaml
```

查看 `/var/lib/kubelet/config.yaml` 文件中的设置。在其他信息中，我们可以看到 `/etc/kubernetes/pki/` 目录用于 `kube-apiserver`。在输出的末尾，它还设置了查找其他 pod 的目录。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

其他代理使用 `kube-apiserver`。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

输出的末尾还设置了查找其他 pod 的目录。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

`kube-apiserver` 设置。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

`kube-apiserver` 设置。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

`kube-apiserver` 设置。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

`kube-apiserver` 设置。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

`kube-apiserver` 设置。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

`kube-apiserver` 设置。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

`kube-apiserver` 设置。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

`kube-apiserver` 设置。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

`kube-apiserver` 设置。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

`kube-apiserver` 设置。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

`kube-apiserver` 设置。

```
student@fs88-node-10a$: sudo vi /var/lib/kubelet/config.yaml

address: 0.0.0

apiVersion: kubelet.config.k8s.io/vbeta1

authentication:

  anonymous:

    enabled: false

webhook:

  cacheTTL: 2m

  enabled: true

x509:

  client-auth:/etc/kubernetes/pki/ca.crt
```

#### 练习 16.2：身份验证与授权

Kubernetes 集群有类型的用户服务账户和普通用户，但假设普通用户是由外部服务管理的。没有对象来表示这些普通用户，它们可以通过 API 调用添加，而服务账户也可以被添加。

我们将使用 RBAC 为新的承包商在命名空间内配置操作，该人员 Developer Dan 将参与一个新项目。

1. 创建两个命名空间，一个用于生产环境（`production`），另一个用于开发环境（`development`）。

```bash
student@fs458-node-ia0a~$ kubectl create ns development

namespace "development" created

student@fs458-node-ia0a~$ kubectl create ns production

namespace "production" created
```

2. 查看集群上下文。`context` 允许你方便地配置 `kubectl` 命令所使用的集群、命名空间和用户。

```bash
student@fs458-node-ia0a~$ kubectl config get-contexts

CURRENT NAME CLUSTER AUTHINFO

kubernetes@kubernetes kubernetes-admin
```

3. 创建一个新用户 `DevDan` 并分配密码 `lfs458`。

```bash
student@fs458-node-ia0a~$ sudo useradd -s /bin/bash DevDan

student@fs458-node-ia0a~$ sudo password DevDan

Enter new UNIX password: lfs458

Retype new UNIX password: lfs458

password updated successfully
```

4. 为 `DevDan` 生成私钥然后生成证书签名请求 (CSR)。

```bash
student@fs458-node-ia0a~$ openssl req -out DevDan.key \

Generating RSA key, 2048 bits modulus

****

****

e is 65537 (0x10001)
```

```bash
student@fs458-node-ia0a~$ openssl req -key DevDan.key \

-out DevDan.csr -subj "CN=DevDan/O=development"
```

5. 使用新创建的请求通过 `x509` 协议生成自签名证书。使用 Kubernetes 集群的 CA 密钥并设置 1 年有效期。你需要访问输入文件。

```bash
student@fs458-node-ia0a~$ openssl x509 -req -key DevDan.key \

-CA /etc/kubernetes/pki/ca.crt \

-CAkey /etc/kubernetes/pki/ca.key \

-CAcreateserial \

-days 365

Signature ok

subject=CN=DevDan/O=development

Getting CA Private Key
```

6. 更新访问配置以引用新的密钥和证书。通常情况下我们需要为非 root 用户创建一个安全家目录。

```bash
student@fs458-node-ia0a~$ kubectl config set-credentials DevDan \

--client-certificate=/home/student/DevDan.crt \

--client-key=/home/student/DevDan.key

User "DevDan" set.
```

### 16.2 实验

7. 查看你的凭据文件的更新。使用 `diff` 与我们之前创建的副本进行比较。

```bash
student@e1fs458-node-1a0a:~$ diff cluster-api-config .kube/config

9a10,14

  namespace: development

  user: DevDan

  name: DevDan-context

  context:

    cluster: kubernetes

15a21,25

  name: DevDan

  user:

    az-user-certificate: /home/student/DevDan.crt

    client-key: /home/student/DevDan.key
```

8. 我们现在要创建这个，我们需要之前步骤中设置的集群名称、命名空间和用户的 CN。

```bash
student@e1fs458-node-1a0a:~$ kubectl config set-context DevDan-context \

  --cluster=kubernetes \

  --namespace=development \

  --user=DevDan

Context "DevDan-context" created.
```



9. 尝试查看 `DevDan-context` 内部的 Pods。注意你会得到一个错误。

```bash
student@e1fs458-node-1a0a:~$ kubectl --context=DevDan-context get pods
Error from server (Forbidden) is forbidden: user "DevDan"
cannot list pods in the namespace "development"
```

10. 验证上下文已正确设置。

| CURRENT | NAME | CLUSTER | AUTHINFO | NAMESPACE |
|------|---|---|---|---|
| DevDan-context | kubernetes | DevDan | | development |
| * | | admin-admin | | |

11. 再次检查集群访问配置的更改。

```bash
student@e1fs458-node-1a0a:~$ diff cluster-api-config .kube/config
9a10,14
  namespace: development
  user: DevDan
  name: DevDan-context
  context:
    cluster: kubernetes
15a21,25
  name: DevDan
  user:
    <output_omitted>
```

12. 我们现在将创建一个 YAML 文件，为特定的命名空间和角色建立 RBAC 规则。

```bash
student@lfs458-node-1a0a:~$ vim role-dev.yaml
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  namespace: developer
  name: developer
rules:
  - apiGroups: ["","extensions", "apps" ]
    resources: ["deployments", "replicasets", "pods" ]
    verbs: ["list", "get", "watch", "create", "update", "patch", "delete"]
  # 你可以使用 ["*"] 表示所有动词
```

13. 创建对象。检查空格，如果遇到拼写错误将会产生错误。

```bash
student@lfs458-node-1a0a~$ kubectl create -f role-dev.yaml
role.rbac.authorization.k8s.io/created
```

14. 现在创建一个 RoleBinding，将你创建的角色与用户关联。创建该文件。

```bash
student@lfs458-node-1a0a~$ vim rolebind.yaml
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: developer-rolebinding
  namespace: development
subjects:
  - kind: User
    name: DevDan
roleRef:
  kind: Role
  name: developer
  apiGroup: rbac.authorization.k8s.io
```

```bash
student@lfs458-node-1a0a~$ kubectl apply -f rolebind.yaml
rolebinding.rbac.authorization.k8s.io/developer-rolebinding created
```

15. 测试该操作。这次应该可以运行。

```bash
student@lfs458-node-1a0a~$ kubectl --context=DevDan get pods
No resources.
```

16. 创建一个新的 pod，验证它，然后删除它。

```bash
student@fs458-node-ia0a~$ kubectl --context=DevDan run nginx --image=nginx
deployment.apps/nginx created
student@fs458-node-ia0a~$ kubectl --context=DevDan get pods
NAME    READY   STATUS    RESTARTS   AGE
nginx-7c8d  1/1   Running          0s
student@fs458-node-ia0a~$ kubectl --context=DevDan delete nginx
```

17. 现在为生产生产环境创建一个角色。现有的角色将具有查看权限，而不是创建权限。

```bash
student@fs458-node-ia0a~$ vim role-prod.yaml
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: dev-prod
  namespace: production
rules:
  - apiGroups: ["","extensions", "apps" ]
    resources: ["deployments", "replicasets", "pods" ]
    verbs: ["list", "get", "watch"]
```

18. 创建新对象。

```bash
student@fs458-node-ia0a~$ kubectl apply -f role-prod.yaml
role.rbac.authorization.k8s.io/dev-prod created
```

```bash
student@fs458-node-ia0a~$ kubectl apply -f rolebind.yaml
rolebinding.rbac.authorization.k8s.io/production-rolebinding created
```

19. 为生产使用创建上下文。

```bash
student@fs458-node-ia0a~$ kubectl config set-context ProdDan-context \
  --cluster=kubernetes \
  --namespace=production \
  --user=DevDan
Context "ProdDan-context" created.
```

20. 验证 DevDan 使用新上下文可以查看 pods。

```bash
student@fs458-node-ia0a~$ kubectl --context=ProdDan-context get pods
No resources found.
```

21. 尝试在生产环境中创建 pod。开发者应该被拒绝（Forbidden）。

```bash
student@fs458-node-ia0a~$ kubectl --context=ProdDan-context run nginx --image=nginx
Error from server (Forbidden): extensions is forbidden: user "DevDan"
create deployment extensions in the namespace "production"
```

22. 查看角色的详情。

```bash
student@fs458-node-1a0a~$ kubectl describe role dev-prod -n production
Name:
  dev-prod
Labels:
  <none>
Annotations:
  kubernetes.io/last-applied-configuration:
  {"apiVersion":"rbac.authorization.k8s.io/v1", "kind": "Role",
  "metadata": {"name": "dev-prod", "namespace": "production"},
  "rules":{
    "PolicyRule":
    "Resources": ["deployments", "replicasets", "pods"],
    "Non-Resource URLs": [],
    "Names": [],
    "Verbs": ["list", "get", "watch"]
  }]}
```

23. 在两种环境下尝试其他的子命令。它们应该与各自角色中列出的命令匹配。

### 练习 16.3：准入控制器 (Admission Controllers)

请求发送到 API 服务器之前的最后是准入控制插件。它们与功能交互，例如设置默认存储类、检查资源配额或安全设置。一个较新的特性（v1.7.x）是动态控制器，它允许在运行时摄取或配置新的控制器。

1. 查看当前的控制器设置。与早期版本的 Kubernetes 不同，控制器现在被编译到服务器中，我们不再通过控制器列表来使用，而是可以启用或禁用特定的插件。

```bash
student@lfs458-node-1oa0:$ sudo grep admission /etc/kubernetes/manifests/kube-apiserver.yaml
  --disable-admission-plugins=PersistentVolumeLabel
  --enable-admission-plugins=NodeRestriction
```
