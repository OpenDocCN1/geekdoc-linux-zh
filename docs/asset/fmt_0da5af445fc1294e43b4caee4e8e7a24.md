
# Spark 和 Jupyter

有几个原因说明了我们需要 Spark 和 Jupyter 来推进我们的学习。尽管 Elasticsearch 很好用，但它并不是关系型数据库，因此连接（joins）的计算开销非常大。12, 13 连接是 SQL 中一种常用的函数，允许我们在查询过程中组合数据，以便我们的调查更具针对性。例如，如果我们有两个数据源，其中一个包含 `static_ip` 和 `user_name`，另一个包含 `static_ip` 和 `host_name`，我们可以通过以下方式对它们进行连接。

左连接（left join）返回来自左源的记录，并带有来自右源的匹配项：

| 数据源 1 | | 数据源 2 | | 结果 | |
|---|---|---|---|---|---|
| static_ip | user_name | static_ip | user_name | static_ip | host_name |
| 192.168.1.25 | peebly | 192.168.1 | 01 | 192.168.1.25 | peebly |
| 192.168.2.23 | bsimpson | Left Join | 192.168.1 | 04 | 192.168.2.23 | | |
| 192.168.1.2 | ckent | | 192.168.1 | philly01 | 192.168.1.2 | ckent | 192.168.1.2 | 01 |

内连接（inner join）仅返回左右两个源中均具有匹配值的记录：

全外连接（full outer join）在来自任一源存在匹配项时返回记录：

| 数据源 1 | | 数据源 2 | | 结果 | | | | |
|---|---|---|---|---|---|---|---|
| static_ip | user_name | static_ip | host_name | static_ip | user_name | static_ip | user_name |
| 192.168.1.25 | peebly | Full Outer Join | 192.168.1 | 01 | 192.168.1.25 | peebly | 192.168.1 | 04 |
| 192.168.2.23 | bsimpson | | 192.168.1 | 04 | 192.168.2.23 | bsimpson | 192.168.1 | 01 |
| 192.168.1.2 | ckent | | 192.168.1 | philly01 | 192.168.1.2 | ckent | 192.168.1.2 | philly01 |
| | | | | 192.168.1.5 | | 192.168.1.5 | philly01 | |

这些连接可以使用 Apache Spark 结合 Elasticsearch 中的数据来完成，这在威胁狩猎（threat hunting）时特别有用，允许我们通过结合多个数据源来增强或丰富我们的数据。14 我们将在将在下一个实验中看到演示。

# 实验 9-5：自动化剧本与分析共享

![](img/0add480ffb73b6bc89b65d99f7d6b37a_349_0.png)

注意：在开始此实验之前，请理解我们将切换学习环境以提升我们的知识和能力。在将来，你可能会切换回内置剧本，但正如之前解释的那样，你需要更多的系统资源。

为了共享分析并提供更稳健的训练环境，Rodriguez 兄弟开发了一系列存储在 Binderhub 平台上的 Jupyter notebooks。15, 16

首先，访问 https://threathunterplaybook.com/introduction.html。

在屏幕左侧，点击 Free Telemetry Notebook 链接。这将加载 Jupyter notebook 页面，包含 Mordor 数据集以及所有准备好供学习的分析。

# 遥测检测类别

- ATT&CK 评估
- APT 29
- Free Telemetry Report
- Free Telemetry Notebook

BokehJS 2.2.2 已成功加载。
遥测检测类别（平均覆盖率: 82%）

然后，点击屏幕顶部的火箭图标并启动 Binder 链接。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_350_0.png)

# Free Telemetry Notebook

APT29 组

Jupyter notebook 可能需要几分钟才能启动，请耐心等待。加载后，点击顶部的 Run 按钮或按 SH-ENTER 运行该代码块并加载所需的库。请记住，此库中的某些步骤将需要一段时间。在代码块左侧，进行中的符号显示为 [*]，完成后会显示数字。务必在继续之前让这些代码块运行完成。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_350_1.png)

```python

In [1]: Importing Libraries

from bokeh.io import output

from bokeh.plotting import figure

from bokeh.models import ColumnDataSource, HoverTool

from bokeh.transform import dodge

import pandas as pd

# 你需要在开头显示此代码以便在 Jupyter 中显示可视化

apt29=pd.read_json('https://raw.githubusercontent.com/ThreatHunter-Playbook/master/docs/apt29_results.json')

```

务必阅读每个代码块上文本；然后点击 Run 或按 SHIFT-ENTER 执行后续代码直到到达解压块。如果在拉取 Mordor 数据时出现错误，请在运行此块之前更改命令：

```bash

wget https://github.com/OTR/Security-Datasets/raw/master/apt29_manual.zip

```

继续执行代码直到：

| 攻击者 - 检测步骤 | |
|---|---|
| 1.A 用户执行 |
| 过程: 用户执行了 rcs.doc |
| 标准: rcs.doc 从 explorer.exe 生成 |

下一个代码块执行的是 Spark SQL，它从 `apt29Host` 的 Sysmon/Operational 中选择记录，其中 `EventID` = 1，`ParentImage` 包含 "%explorer.exe"，`Image` 包含 "%apt29"。这些信息来自我们之前的狩猎，发现了一个屏幕保护程序。让我们看看这有多深。

```python

In [11]: df = spark.sql("""

SELECT Message

FROM apt29Host

WHERE Channel = "Windows-Sysmon/Operational"

AND EventID = 1

AND LOWER(ParentImage) LIKE "%explorer.exe%"

AND LOWER(Image) LIKE "%apt29%"

""")

df.show(100,truncate=False, vertical=True)

```

```text

Message: Process Create:

RuleName: -

Utc: 2020-05-02 02:55:56.157

ProcessGuid: (47ab858c-e13c-3bae-f331-3700000000)

ProcessId: 8524

Image: C:\ProgramData\victim\u0063.jaka.scr

FileVersion:

Description:

Product:

Company:

OriginalFileName: C:\ProgramData\victim\u0063.jaka.scr

CommandLine: C:\ProgramData\victim

ParentDirectory: C:\ProgramData\victim

User: DMWPE3

LogonId: (47ab858c-e13c-3bae-f331-3700000000)

Length: 13197

TerminalSessionId: 2

IntegrityLevel: Medium

Hashes: MD5=E6A5E67A55A5A6E5F8B890D11689A5E2,SHA1=9D50C17E3867336174460D33A716AE,SHA256=0DF38A55D94F948B9487EB0603C94BD04B2102B55A6F,IMHASH=F000447512345E5930D201AEA8417

ParentProcessId: (47ab858c-dac-3bae-e202-0000000000)
```
