
```
NAME        TYPE       CLUSTER-IP   PORT(S)      AGE
wordpress   NodePort   10.96.x.x    80:31367/TCP   5m
```

现在你可以通过浏览器访问 `http://<IP>:31360`。但是，我们需要让它通过域名工作。为此，我们需要添加一个 Ingress。

### 设置 MetalLB

创建一个 `metallb.yaml` 的文件并添加以下内容：

```yaml
apiVersion: metallb.io/vbeta1
kind: IPAddressPool
metadata:
  name: pool
  namespace: metallb-system
spec:
  addresses:
    - 192.168.122.133/32
---
apiVersion: metallb.io/vbeta1
kind: L2Advertisement
metadata:
  name: pool
  namespace: metallb-system
spec:
  addressPools:
    - pool
```

我们需要将配置应用到我们的集群。使用 `kubectl apply` 应用配置。现在，我们需要为该服务添加 Ingress：

```bash
root@8smaster~/deploy# kubectl annotate service traefik metallb.universe.io/address-pool=pool
service/traefik annotated
root@8smaster~/deploy# kubectl get svc
NAME      TYPE          CLUSTER-IP     EXTERNAL-IP     PORT(S)         AGE
traefik   LoadBalancer   10.105.142.83  192.168.122.133  80:31360,443:32717 2d
```

现在 IP 已经设置为 traefik。如果你打开浏览器并访问该 IP，你将看到预期的 404 页面。我们需要这样做：

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.class: traefik
  name: wordpress
spec:
  rules:
    - host: "wordpress.home.lan"
      http:
        paths:
          - backend:
            service:
              name: wordpress
              port:
                number: 80
          path: /
          pathType: Prefix
```

然后，我们还需要告诉我们的电脑去哪里寻找 WordPress。在你有一个安装了 DNS 服务器的地方，你可以设置 DNS 记录，或者你可以打开 `/etc/hosts` 并添加以下内容：

```
192.168.122.133 wordpress.home.lan
```

你需要更新该 IP 以匹配我们在 metallb 配置中使用的相同 IP。现在打开浏览器，访问 `wordpress.home.lan` 并安装 WordPress。

### 使用 Grafana 监控 Kubernetes 集群

让我们创建另一个 Ingress。创建一个名为 `grafan-ingress.yaml` 的新文件并添加以下内容：

```yaml
- name: grafana
  spec:
    rules:
    - host: "grafana.home.lan"
      http:
        paths:
        - backend:
          service:
            name: monitoring-grafana
            port:
              number: 80
          path: /
          pathType: Prefix
```

然后，更新你的 DNS 服务器或本地 host 文件，将其指向集群的正确 IP 地址：

```
192.168.122.133 grafana.home.lan
```

现在你就可以通过 `grafana.home.lan` 访问 Grafana 了。

现在你可以添加越来越多的服务并对其进行设置，让它们拥有自己的 Ingress。

在集群设置期间，我们添加了指标和日志，通过 Grafana，你现在可以查看数据了。登录你的 Grafana，我们可以为你添加数据源。我们在监控章节中已经过这一操作。

要查找源的 URL，请使用以下命令：

```bash
kubectl get svc
```

| NAME | TYPE | CLUSTER-IP | PORTS | AGE |
| :--- | :--- | :--- | :--- | :--- |
| `monitoring-kube-prometheus-prometheus` | ClusterIP | 10.111.200.8 | 9090/TCP, 8080/TCP | 2d14h |

### Kubernetes Secrets

连接到 Prometheus 时，使用 URL `http://monitoring-kube-prometheus-prometheus:9090`。

Kubernetes 将密码存储在称为 secrets 的对象中。secrets 并没有加密，而是经过 base64 编码的。要获取 secret，我们需要编辑该 secret 并将其从 base64 解码。这是一个良好的实践。

首先，使用 `edit` 打开 secret，例如：

```bash
kubectl edit secret monitoring-grafana
```

```yaml
apiVersion: v1
data:
  admin-password: cHJvS1vcGVyY==
  admin-user: YWRtaW4=
kind: Secret
metadata:
  annotations:
    helm.sh/release-name: monitoring
    helm.sh/release-namespace: default
  creationTimestamp: "2023-11-07T17:28:14Z"
  labels:
    kubernetes.io/instance: monitoring
    kubernetes.io/managed-by: Helm
    kubernetes.io/name: grafana
    kubernetes.io/version: "10.5"
    helm.sh/chart: grafana-6.6.0
name: monitoring-grafana
namespace: default
resourceVersion: 13911
type: Secret
```

让我们复制 base64 字符串并解码：

```bash
root@k8s:~/deploy# echo cHJvS1vcGVyY== | base64 -d
```

Grafana 中 admin 用户的密码是 `prom-operator`。

### 需要记住的 kubectl 命令

在操作 Kubernetes 集群时，有几个命令是特别实用的。还有更多，但这些适用于我们现在设置的 Kubernetes 集群，并提供一些关于查找和排除 Kubernetes 问题的知识。

#### Pods

Pods 运行在不同的命名空间中。运行以下命令查找并定位集群中的 Pod。如果我们想更深入地查看某个 Pod，可以使用 `get pods` 来查找：

```bash
kubectl get pods -A
kubectl get ns
kubectl get pods -n
```

然后我们可以通过运行以下命令并按如下方式添加 pod 名称来从这些 Pods 获取更多信息：

```bash
kubectl describe pod NAME_FROM_CLUSTER
kubectl logs -f NAME_FROM_CLUSTER
kubectl edit pod NAME_FROM_CLUSTER
```
