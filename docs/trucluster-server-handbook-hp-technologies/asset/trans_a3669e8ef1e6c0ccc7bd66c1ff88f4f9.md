

- REQUIRED_RESOURCES
  将资源放置在拥有所需资源且运行资源数量最少的成员上。如果没有任何成员拥有可用的所需资源，则不启动。

- PLACEMENT 为 "favored"
  - No Dependencies
    将资源放置在在线资源数量最少的优选成员上。如果没有可用的优选成员，则将资源放置在在线资源数量最少的非优选成员上。
  - OPTIONAL_RESOURCES
    将资源放置在拥有所需资源且运行资源数量最少的优选成员上。
    如果没有可用的优选成员，但存在拥有所需资源的非优选成员，则在非优选成员上启动该资源。
    如果没有任何成员拥有可用的所需资源，则仍在优选成员上启动该资源。
    如果没有可用的优选成员且没有任何拥有所需资源的非优选成员可用，则仍在非优选成员上启动该资源。
  - REQUIRED_RESOURCES
    将资源放置在拥有所需资源且运行资源数量最少的优选成员上。如果没有拥有所需资源的优选成员，但存在拥有所需资源的非优选成员，则在非优选成员上启动该资源。如果没有任何成员拥有可用的所需资源，则不启动。

- PLACEMENT 为 "restricted"
  - No Dependencies
    将资源放置在在线资源数量最少的受限成员上。如果没有可用的受限成员，则不启动。
  - OPTIONAL_RESOURCES
    将资源放置在拥有所需资源且运行资源数量最少的受限成员上。如果没有任何受限成员拥有可用的所需资源，则仍在受限成员上启动。
  - REQUIRED_RESOURCES
    将资源放置在拥有所需资源且运行资源数量最少的受限成员上。如果没有任何受限成员拥有可用的所需资源，则不启动。

1. 将 REBALANCE 属性设置为每周一、周三和周五午夜及中午重新评估。

```
# caa_profile -update memberUP -o bt="t:1,3,5:00,12:00"
```

2. 更新注册。

```
# caa_register -u memberUP
REBALANCE entries will be added to clustercron
```

3. 验证更改是否已生效。

```
# caa_stat -p memberUP | grep REBALANCE
REBALANCE=t:1,3,5:00,12:00
```

# NOTE:

应用程序资源负载均衡是通过集群范围的 cron(8) 应用程序资源 clustercron 实现的，该资源在 V5.1B 中引入。

类似的解决方案记录在 2001 年 9 月的《在 TruCluster Server 集群中使用 cron》最佳实践中。然而，我们在此讨论的 clustercron 应用程序资源实现严格用于 CAA 使用，不应作为通用集群范围的 cron 使用。

本质上，clustercron 被实现为单实例、高可用性应用程序。其任务是确保某些集群相关任务由 cron 运行。clustercron 运行在哪台成员上，该成员的 root crontab 文件就会被修改以运行这些集群相关任务。

例如，当我们更新 memberUP 的注册时，显示了以下消息：

```
REBALANCE entries will be added to clustercron
```

在 clustercron 运行的成员的 crontab 中放置了一个条目，该条目指示 cron 在每周一、周三和周五午夜及中午执行 "caa_balance memberUP" 命令。

让我们来证明一下。首先，查看 clustercron 运行的位置。

```
# caa_stat -t clustercron
Name        Type        Target    State     Host
-----------------------------------------------
clustercron application  ONLINE    ONLINE    moleri
```

由于 clustercron 运行在节点 molari 上，我们将在其 crontab 文件中搜索 memberUP 应用程序资源。

