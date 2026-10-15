
理想情况下，你应该从控制台执行 `shell` 脚本。或者勇敢地从远程机器或 `XWindow` 终端会话执行该 `shell` 脚本。不仅网络流量被阻塞，`X Windows` 使用的本地环回接口的访问也会被阻塞，直到该接口被显式重新启用。这是一个不必要且被用作服务器利用机制的典型软件示例。

作为一个管理地理距离数百英里的 Linux 计算机的人，我只能从远程位置激活防火墙脚本。在某些，建议做两件事：第一，在防火墙脚本的第一次或几次执行时，将默认策略更改为 `ACCEPT`。这样做是为了调试脚本本身的语法，而不是因为它在语法上是正确的，完成后将其改回 `DROP`。

第二，对于从远程位置处理脚本同样重要的是，创建一个 `cron` 任务在在不久的某个点停止防火墙。这样做可以有效地允许你启用防火墙并进行一些测试，同时也允许在你因错误缺失的规则而把自己锁在计算机之外时，重新进入计算机。例如，在调试防火墙时，我会创建一个 `cron` 条目在 10 分钟后禁用防火墙。

## 移除任何预存规则

在定义一组过滤规则时，首要工作是从它们的链中移除任何现有的规则。否则，你定义的新规则将会被添加到现有规则的末尾。数据包在到达你正在定义的链点之前，可能很容易匹配到预存规则。

这种移除操作被称为“冲空”`flushing`。对于 `iptables`，以下命令可以一次性冲空所有链中的规则：

```bash
# 从所有链中移除任何现有规则
$IPT --flush
```

然后可以使用 `-t <table>` 选项冲空特定的表：

```bash
$IPT -t nat --flush
$IPT -t mangle --flush
```

对于 `nftables`，需要指定表名，这样做将冲空该表内所有链的规则：

```bash
nft flush table <tablename>
```

如果你正在使用社区标准的命名规范，你将有一个 `filter` 过滤表和一个可能存在的 `nat` 网络转换表，可以使用以下命令进行冲空：

```bash
nft flush table filter
nft flush table nat
```

其他用户定义的表需要根据你特定的防火墙实现按需冲空。对于 `nftables`，可以使用此循环来冲空所有表中的链：

```bash
for i in $(NFT list tables | awk '{print $2}')
do
  echo "Flushing ${i}"
  $NFT flush table ${i}
done
```

更好的方法不仅删除规则，还删除链和表本身。这通过对 `nftables` 脚本进行两个嵌套循环来实现：

```bash
for i in $(NFT list tables | awk '{print $2}')
do
  echo "Flushing ${i}"
  $NFT flush table ${i}
  for j in $(NFT list table ${i} | grep chain | awk '{print $2}')
  do
    echo "...Deleting chain ${j} from table ${i}"
    $NFT delete chain ${i} ${j}
  done
  echo "Deleting ${i}"
  $NFT delete table ${i}
done
```

冲空链不会影响当前生效的默认策略状态。

## 第 104 页 第 5 章 构建和安装独立防火墙

对于 `iptables` 来说，下一步是删除任何用户定义的链。可以使用以下命令删除它们：

```bash
$IPT -X
$IPT -t nat -X
$IPT -t mangle -X
```

对于 `nftables`，所有表和链都是用户定义的，因此相同的语法并不真正适用。无论哪种情况，冲空链都不会影响生效的默认策略状态。到此时，你有了一个基础脚本，它定义了一些变量并清空了表和链如果已定义的话。

## 重置默认策略并停止防火墙

到为止，防火墙已经设置了一些默认值，无论 `Netfilter` 防火墙的状态如何都可以。在将默认策略设置为 `DROP` 之前，我会先将默认策略重置为 `ACCEPT`。这对于停止防火墙很有用，你很快就会这样做。这些行设置了默认策略：

```bash
# 重置默认策略
$IPT --policy INPUT ACCEPT
$IPT --policy OUTPUT ACCEPT
$IPT --policy FORWARD ACCEPT
$IPT -t nat --policy PRERUTING ACCEPT
$IPT -t nat --policy OUTPUT ACCEPT
$IPT -t nat --policy POSTROUTING ACCEPT
$IPT -t mangle --policy PRERUTING ACCEPT
$IPT -t mangle --policy OUTPUT ACCEPT
```

对于 `nftables`，链没有像 `iptables` 那种意义上的默认策略，且链和表已经被删除。其效果是将策略设置为 `ACCEPT`，因为此时没有防火墙在运行。因此，`nftables` 在这里不需要做任何操作。

这里是我认为的防火墙脚本开头的最后添加部分，命名为：允许防火墙易于停止的代码。将此代码放置在之前的代码下方后，当你带参数 `"stop"` 调用脚本时，该脚本将冲空、清空并重置默认策略，防火墙将实际有效停止：

```bash
if [ "$1" = "stop" ]
then
    echo "Firewall completely stopped! WARNING: THIS HOST HAS NO FIREWALL RUNNING."
    exit 0
fi
```

在对 `nftables` 进行进一步配置之前，需要重新创建基础表。这可以使用 `nftables` 规则文件来实现，我将其命名为 `setup-tables`。`setup-tables` 规则的 own如下：

```nftables
table filter {
    chain input {
        type filter hook input priority 0;
    }
    chain output {
      type filter hook output priority 0;
    }
}
```

然后使用以下命令加载该文件。此命令应在停止防火墙的条件判断之后添加到防火墙脚本中：

```bash
NFT -f setup-tables
```

## 环回接口

你需要启用无限制的环回流量。这允许你运行你选择的任何本地网络服务——或系统所依赖的服务——而无需担心要指定所有的防火墙规则。

本地服务运行在环回网络接口上。系统启动后，系统的默认策略接受所有数据包。预存的连接没有影响。然而，如果防火墙重新初始化并且之前使用了“默认拒绝”策略，那么 `drop` 策略将仍然生效。在没有任何接受防火墙规则的情况下，环回接口将无法无法的。

由于环回接口是本地内部接口，防火墙可以立即允许回环流量。以下是 `iptables` 脚本的命令：

```bash
# 环回接口上的无限流量
$IPT -A INPUT -i lo -j ACCEPT
$IPT -A OUTPUT -o lo -j ACCEPT
```

对于 `nftables`，通过向 `setup-tables` 文件添加以下内容可以启用环回接口：

```nftables
table filter {
    chain input {
        type filter hook input priority 0;
        add rule input lo accept
    }
    chain output {
        type filter hook output priority 0;
        add rule output lo accept
    }
}
```

## 第 128 页 第 5 章 构建和安装独立防火墙

## 定义默认策略

默认，你希望防火墙丢弃一切。`iptables` 的可用选项是 `ACCEPT` 和 `DROP`。`REJECT` 不是 `iptables` 中的合法策略，但可以用于拒绝传出数据包并返回 `ICMP` 消息。终端用户的区别在于，例如，如果远程站点尝试连接你的 `Web` 服务器，浏览器会挂起，没有指示你的站点或 `Web` 服务器是否存在。另一方面，如果你尝试连接到远程服务器，你的浏览器会立即收到操作不允许的提示：

```bash
# 将默认策略设置为 drop
$IPT --policy INPUT DROP
$IPT --policy OUTPUT DROP
$IPT --policy FORWARD DROP
```

## 默认策略规则与第一个匹配规则优先

在 `iptables` 中，默认策略允许作为第一个匹配规则优先场景的例外。默认策略命令本身不是依赖性的。它们不是严格意义上的规则。链的默认策略是在数据包与链中的每个规则比较后未匹配时应用的。这与 `nftables` 有显著不同，`nftables` 是第一个匹配优先，且没有默认策略。
