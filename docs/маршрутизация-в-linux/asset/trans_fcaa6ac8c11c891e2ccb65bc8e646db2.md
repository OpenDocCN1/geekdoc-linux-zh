

另一个难以界定的语句是 traceoptions。造成这种别扭的原因之一是存在两组可用的值：一组适用于整个 gated（见表 5.11），另一组仅适用于 RIP 流量（见表 5.12）。还有全局跟踪选项可用，但在 rip 等特定协议语句中没有意义。

## 表 5.11 gated 中适用于所有协议的跟踪选项——尽管其中一些对特定协议毫无意义

| Option | Purpose |
|---|---|
| all | 要为此协议语句启用本表中每个选项。如果某个选项对协议毫无意义，则会被忽略。 |
| general | 要启用 normal 和 route 选项。 |
| normal | 记录常规协议活动以及异常情况。 |
| policy | 记录导入和导出路由的策略信息。 |
| route | 记录路由表更改。 |
| state | 对于使用各种路由器状态的协议（RIP 不是其中之一），记录这些状态更改的信息。 |
| task | 记录此协议对接口使用和处理器使用的信息。 |
| timer | 记录此协议的计时器使用情况。 |

## 表 5.12 gated 特有的 RIP 跟踪选项

| Option | Purpose |
|---|---|
| other | 记录未被其他选项指定的数据包。 |
| packets | 记录所有 RIP 数据包。 |
| request | 记录 RIP 信息请求数据包。 |
| response | 记录包含 RIP 信息的数据包。 |

## 开放最短路径优先（OSPF）配置

最受欢迎的内部单播路由协议之一是 OSPF。正如你在第 1 章中可能记得的那样，该协议包含指定路由器和路由区域等功能。由于这种复杂程度，OSPF 涉及更长的配置代码集。所以让我们开始吧。

你以以下内容开始 OSPF 配置语句：

```
ospf status
```

ospf 的 status 条目具有与 rip 语句相同的选项：

+   - no; 不处理 OSPF 流量。
+   - off; 不处理 OSPF 流量。
+   - on { 处理 OSPF 流量。
+   - yes { 处理 OSPF 流量。

通常，ospf 中的第一个子语句是 defaults，因此语句的开头通常如下所示：

```
ospf on {
    defaults {
```

defaults 语句中可用的项目列在表 5.13 中。

## 表 5.13 gated ospf 语句的 defaults 部分中可用的选项

| Option | Purpose | Format | Value(s) |
|---|---|---|---|
| cost | 设置从 gated 路由表获取的、未通过 OSPF 学习到的路由的成本值。 | cost value; | 一个整数，指定要添加到路由成本中的值。默认值为 1。 |
| ospfarea | 告诉 gated 所有接口都在同一个 OSPF 区域内。 | ospfarea location; | location 值可以是 backbone 或你分配给此特定区域的 ID。OSPF 规定区域 ID 为 0 为骨干网，其他区域 ID 必须为 32 位数字。可以利用格式为 xxx.xxx.xxx.xxx 的 IP 地址或网络号作为区域 ID。 |
| preference | 设置 gated 对从 OSPF 学习到的路由相对于其他协议的偏好程度。 | preference value; | 值是 0 到 255 之间的数字，值越低偏好越高。OSPF 路由的默认偏好为 10。 |
| router-prio | 允许此路由器参与 OSPF 指定路由器选举。 | router-prio; | N/A |
| tag | 允许你为此路由器通过 OSPF 源发的数据分配标签。 | tag valueL; or tag as valueS; | 这里的两个值是长值（valueL）和短值（valueS）。长值可以为 32 位，而短值必须仅为 12 位，因为你的 AS 号也包含在内。 |
| type | 允许你指定你的 AS 是类型 1 还是 2，如第 1 章 OSPF  coverage 中“工作原理”部分所述。 | type num; | 1 或 2。 |

## 表 5.13 继续

| Option | Purpose | Format | Value(s) |
|---|---|---|---|
| tag | 允许你为此路由器通过 OSPF 源发的数据分配标签。 | tag valueL; or tag as valueS; | 这里的两个值是长值（valueL）和短值（valueS）。长值可以为 32 位，而短值必须仅为 12 位，因为你的 AS 号也包含在内。 |
| type | 允许你指定你的 AS 是类型 1 还是 2，如第 1 章 OSPF  coverage 中“工作原理”部分所述。 | type num; | 1 或 2。 |

设置 defaults 后，你可以关闭 defaults 语句，然后继续进行 ospf 语句的主要部分，如下所示：

```
ospf on {
    defaults {
        option1;
        ...
        optionN;
    };
}
```

ospf 的主要选项列在表 5.14 中。

## 表 5.14 gated 的 ospf 语句中可用的选项

| Option | Purpose | Format | Value(s) |
|---|---|---|---|
| backbone area | 设置 OSPF 骨干网而不是特定区域。 | backbone area value { option1; ... optionN; }; | value 是分配给骨干区域的编号。有关此复杂语句的进一步解释，请参阅章节正文。其选项在表 5.15 中定义。 |

