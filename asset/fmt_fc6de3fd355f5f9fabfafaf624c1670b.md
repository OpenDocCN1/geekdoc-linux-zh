
![](img/0add480ffb73b6bc89b65d99f7d6b37a_333_0.png)

注意：如果你没有看到 `c:\Tools` 文件夹，那么可能在安装期间出现了问题；在这种情况下，请回到主机系统，并在管理员 PowerShell 窗口中运行 `vagrant provision win10`。对于 DC 和 WEF 服务器也是如此。此外，如果本章中的某个实验卡住，你可能需要通过 `vagrant halt <系统名称>` 重启然后再运行 `vagrant up <系统名称>`。如果这种情况频繁发生，请考虑增加内存或在云端（带有更多内存）运行。实验在 Windows 10 主机上如演示所示运行正常，但在其他操作系统上的实际情况可能会有所不同。

此外，从 Web浏览器打开以下 URL：

https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/T1003.002/T1003.002.md

向下滚动查看 AtomicRedTeam 将如何模拟攻击，或者你也可以手动输入这些命令。它们看起来眼熟吗？应该是的，因为这些我们在 MITRE ATT&CK 框架页面上看到的相同命令。

或者，可以使用 `Reg` 从注册表中提取 SAM：

现在，在你的管理员命令行提示符（在 Windows 10 主机上）中，输入上图所示的命令来手动模拟攻击者。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_334_0.png)

现在，打开你的 Kibana 仪表板（上一章）。接下来，通过在左侧面板搜索框中找到 `#event_id` 并点击 Add（添加）按钮，为你的 Kibana 结果列表添加一列。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_334_1.png)

从现在起，`event_id` 将作为搜索结果列表顶部的表头。刷新页面查看效果。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_335_0.png)

接下来，搜索命令 `"reg save HKLM\sam"`。注意，你必须使用引号来转义斜杠。确保你点击日历并选择 Today（今天）：

你应该能看到以下搜索结果：

![](img/0add480ffb73b6bc89b65d99f7d6b37a_336_0.png)

接下来，搜索命令 `"reg save HKLM\sam"`。注意你必须使用引号来转义斜杠。确保你点击日历并选择 Today：

你应该看到以下搜索结果：

![](img/0add480ffb73b6bc89b65d99f7d6b37a_336_0.png)

接下来，搜索命令 `"reg save HKLM\sam"`。注意你必须使用引号来转义斜杠。确保你点击日历并选择 Today：

你应该看到以下搜索结果：

![](img/0add480ffb73b6bc89b65d99f7d6b37a_336_0.png)

接下来，搜索命令 `"reg save HKLM\sam"`。注意你必须使用引号来转义斜杠。确保你点击日历并选择 Today：

你应该看到以下搜索结果：

![](img/0add480ffb73b6bc89b65d99f7d6b37a_336.png)

### 基于假设的狩猎

由于我们已经知道 SAM 复制可以通过三种方式检测——命令、文件和注册表（见图表）——我们可以利用这些信息开始狩猎。我们记得事件 ID `4688` 和 `4103` 是命令执行的指标。打开你的 Kibana 控制台并搜索 `"HKLM\sam"` 和 `event_id:4103`，你应该能看到一些命中，如下：

![](img/0add480ffb73b6bc89b65d99f7d6b37a_339_0.png)

花点时间熟悉一下日志输出，特别是查看 `Payload` 字段。展开日志并滚动查看详情，如下：

```powershell
CommandInvocation(ForEach-Object): name="ForEach-Object"
ParameterBinding(ForEach-Object): name="Process"; value=$Regex.Matches($.)
CommandInvocation(Select-Object): name="Select-Object"
ParameterBinding(Select-Object): name="ExpandProperty"; value="Groups"
CommandInvocation(Where-Object): name="Where-Object"
ParameterBinding(Where-Object): name="FilterScript"; value="$.Name -eq 'ArgName a"
CommandInvocation(Select-Object): name="Select-Object"
ParameterBinding(Select-Object): name="ExpandProperty"; value="Value"
CommandInvocation(Sort-Object): name="Sort-Object"
ParameterBinding(Sort-Object): name="Unique"; value="True"
CommandInvocation(ForEach-Object): name="InputObject"; value="reg save HKL\system"
timestamp
reg save HKL\system %system
reg save HKL\security %security
ParameterBinding(ForEach-Object): name="InputObject"; value="del %timestamp %nul 2> nul
del %system 2> nul
del %security 2> nul
```

现在你知道 PowerShell 负载的格式是什么样的了。如果你在生产网络中尝试这样做，你将搜索相同的日志，但不需要限制日期条件。

# 爬、走、跑 (Crawl, Walk, Run)

到本章为止，你已经学习了“爬”（手动）和“走”（使用 AtomicRedTeam 自动化脚本）。你已经掌握了威胁狩猎的基础，但仅针对一个 MITRE ATT&CK 子技术。为了走得更快，你现在必须开始练习其他技术，通过逐一攻克 MITRE ATT&CK 框架，确保你拥有正确的数据源、模拟攻击，然后学习如何在日志中识别它。随着时间的推移，你将获得经验，最重要的是了解 Windows 日志的工作原理。6 为了获得额外加分，请研究实验 9-1 末尾显示的针对 T1003.002 的文件和注册表访问。

花点时间使用 AtomicRedTeam 脚本再运行几个例子。7 当你准备好开始“跑”时，请继续本章。

# 进入 Mordor (Enter Mordor)

在本节中，我们将使用上一节安装的 Mordor 数据集8，并以威胁狩猎者的身份开始“跑”。为了加快速度，我们将使用 Roberto Rodriguez 在 2020 年夏天捕的预录攻击者数据9，这些数据基于 MITRE Engenuity ATT&CK 评估报告的早期工作。10 我们将加载 Rodriguez 录制的 APT29 攻击数据，从数据的角度模拟我们网络中的 APT29 组。这是非常强大的，因为我们可以省去设置和执行所有这些命令的时间。要了解更多关于设置和实际攻击序列的信息，请参见本章末尾的“参考文献”部分。

# 实验 9-4：假设有管理员之外的人启动了 PowerShell

## 启动 PowerShell

在实验中，我们将试图证明一个假设：管理员之外的人启动了 PowerShell。注意，这可能是恶意的，也可能不是，但这是一个很好的起点。根据你的网络规模，你可能会有很多 PowerShell 被使用，但你应该能够隔离你的管理员用户，并检测其他运行 PowerShell 的人。顺便说，这是一个很好的第一步，但最终你也将监控并调查你所有的管理员活动。如果其中一个被攻破，攻击者将非常喜欢利用他们在网络中的权限。

为了了解 PowerShell 可能启动的所有方式，我们回到 OS 笔记本。如果它超时了，你可能需要重启。

检查 MITRE ATT&CK 框架，看到 `T1059` 是启动 PowerShell 的技术：

```
In []: payload_network(mapping['technique_id']='T1059')
```
