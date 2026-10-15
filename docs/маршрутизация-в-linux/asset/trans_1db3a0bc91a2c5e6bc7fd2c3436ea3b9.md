

在指定了此规则适用的网络、主机等之后，你可以添加 `restrict` 关键字以阻止导入这些特定路由，或添加 preference 值——其中默认的 preference 仍为 150。最终格式看起来类似如下：

```
import proto ospfase
    options {
        192.168.15.* preference 200;
    };
```

现在我们继续介绍如何告诉 gated 处理通过 EGP 和 BGP 广告的路由。如往常一样，有多种方法可以实现此目的。你从现在已熟悉的以下语句开始：

```
import proto
```

如果你要配置 EGP 路由导入，则继续写为：

```
import proto egp autonomoussystem
```

接下来添加要此规则适用的自治系统的 AS 号码。之后，如果你不想将通过 EGP 从该 AS 学习到的路由保存到路由表中，则将短语补全如下：

```
import proto egp autonomoussystem value restrict;
```

如果你想允许与此规则匹配的项目进行路由，则你有选择。你可以在 autonomoussystem value 条目之后添加 preference value 短语，或保留 EGP 默认的 200 preference。然后，将语句扩展为熟悉的格式：

```
import proto egp autonomoussystem value
preference value {
```

此语句以通常的方式结束。在大括号内，你定义要规则适用的网络、主机等，然后以以下其中之一结束语句：`restrict` 关键字、`preference value` 短语，或两者都不写。最终，你会得到类似如下的内容：

```
import proto egp autonomoussystem value
preference value {
    all;
};
```

你可以使用与 EGP 完全相同的格式用于 BGP；你只需将 egp 替换为 bgp 即可。然而，BGP 包含一些额外功能。另一种 BGP 配置语句类型允许你告诉 gated 如何处理将更广泛的路由协议数据导入其路由表。此语句类型以以下内容开始：

```
import proto bgp aspah value
origin type
```

value 变量包含一个正则表达式，其中包含此规则适用的自治系统列表。在这种情况下，我们并不是在寻找数据直接来自哪个 AS——尽管此信息也可以包含在这里。相反，value 包含数据可能经过的 AS 号码。

选择要放在 type 变量位置的内容则相对简单。

以下设置可用：

- blank. 你可以在此处完全不填写任何内容。
- any. 设置此规则适用于无论来自哪个协议组的路由。
- egp. 此规则指的是外部网关协议，或 EGP。
- igp. 此规则指的是内部网关协议，或 IGP。
- incomplete. 此规则指的是给定数据不完整的路由。

你实际上可以根据需要同时使用一个或多个 egp、igp 和 incomplete。

在下一行，如果你想阻止导入定义的路由，则需要以下内容来完成规则：

```
restrict;
```

还有此语句的另一种格式，允许你不仅设置协议类型，还设置规则应适用的路由数据。它以我们刚刚介绍的内容开始：

```
import proto bgp aspah value
origin type
```

现在决定你是想使用 BGP 默认的 170 preference，还是从下一行开始写：

```
preference value {
```

即使你不设置 preference，也需要大括号。继续到下一行并使用通常的格式设置要导入的路由列表。对于这些路由中的每一个，从定义要规则适用的地址的 data 开始该行，因此你可能会从下一行开始写：

```
host 192.168.15.5
```

然后，通过以下其中之一结束该行来设置是否要将此路由保存到路由表中：

```
host 192.168.15.5;
host 192.168.15.5 preference value;
```

或者，使用以下内容告诉 gated 此项目指向不应保存到路由表的数据：

```
host 192.168.15.5 restrict;
```

在为此规则输入所有地址行后，使用以下内容关闭它：

```
};
```

## 配置路由导出

如果互联网上的其他部分要知道如何到达你，gated 或其他边界路由器必须导出信息以进入他人的路由表。这并不意味着你必须让所有人知道你每台机器的详细信息。至少，外界必须知道如何到达你的网络网关。就像 import 语句一样，export 语句允许对每个路由协议应用特定规则。

