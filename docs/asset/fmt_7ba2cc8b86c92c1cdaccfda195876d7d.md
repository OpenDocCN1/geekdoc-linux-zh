
| Mode | LastWrite | Length |
|---|---|---|
| audit | 9/27/2022 11:00 PM | 12680 `audit_2022092723019_BloodHound.zip` |
| audit | 9/27/2022 11:00 PM | 9734 `MTk2MnZkkkJjty2Y00MWZLtYSzTM2E1ZDCwYThkMzLR.bin` |

# OffSec

## SharpHound 生成的文件
我们将在下一节中使用此文件，并使用 `BloodHound` 分析数据。这对于我们的分析不是必须的，我们可以安全地删除它。需要注意的是，`SharpHound` 还支持循环，这意味着收集器可以在一段时间内循环运行。虽然收集方法创建了域的快照，但在循环中运行可能会随着环境的变化收集到额外数据。缓存文件可以加快过程。例如，如果某个用户在我们收集快照后登录，我们将在分析中就会漏掉该信息。我们不会使用循环功能，但建议大家尝试一下。

## 使用 BloodHound 分析数据
在本节中，我们将使用 `Kali Linux` 分析域，但需要注意的是，我们也可以在 Windows 系统上安装该应用程序和所需的依赖项。为了使用 `BloodHound`，我们需要启动 `Neo4j`。

`Neo4j` 实际上是一个图数据库，它创建节点、边和属性而不是简单的行和列。为了方便关系查询，我们将使用 `Neo4j` 建立关系。

在这种情况下，`SharpHound` 实际上是从 `stephanie` 用户处获取了域的快照，我们应该能够分析该用户账户可以访问的所有内容。收集的数据存储在我们桌面的 zip 文件中：

```
PS C:\Tools> ls C:\Users\stephanie\Desktop\
```
