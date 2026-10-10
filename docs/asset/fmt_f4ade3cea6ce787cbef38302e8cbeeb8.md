
Receiving objects: 100% (10060/10060), 852.58 Mib | 43.4 Mib/s, done.

Resolving deltas: 100% (6925/6925), done.

`vagrant@logger:-$ cd HELK/docker/`

`vagrant@logger:/HELK/docker ls`

```
helk-base helk-logstash
为了简洁起见省略...
k-kibana-notebook-analysis-alert-basic.yml helk_setup_firewall.sh
helk-kibana-notebook-analysis-basic.yml helk_update.sh
helk-ksql
```

对于云端实验室，IP 将自动设置。对于基于主机的实验室，请务必先检查 `eth1` 的 IP，记录下来，并在脚本要求 IP 时使用它：

```bash
vagrant@logger:~/HELK/docker ifconfig eth1

eth1: flags=4163<UP, BROADCAST, RUNNING,MULTICAST> mtu 1500

inet 192.168.38.105 netmask 255.255.255.0 broadcast 192.168.38.255
```

### 现在，安装 HELK：

```bash
vagrant@logger:~/HELK/docker sudo ./helk_install.sh
```

1. KAFKA + KSQL + ELK + NGINX + ELASTALERT
2. KAFKA + KSQL + ELK + NGINX + SPARK + JUPITER
3. KAFKA + KSQL + ELK + NGINX + SPARK + JUPITER
4. KAFKA + KSQL + ELK + NGINX + SPARK + JUPITER + ELASTALERT

如果你遵循了之前的云端说明，请如所示选择选项 2。稍后，你可以尝试其他选项；它们很棒，但本章不需要。

输入构建选择 [ 1 - 4]: 2
[HELK-INSTALLATION-INFO] 设置 HELK IP。默认值为你的当前 IP：
192.168.38.105
[HELK-INSTALLATION-INFO] HELK IP 已设置为 192.168.38.105
[HELK-INSTALLATION-INFO] 请确保创建一个自定义 Kibana 密码并将其存储以备后用。
[HELK-INSTALLATION-INFO] 设置 HELK Kibana 密码: hunting
[HELK-INSTALLATION-INFO] 验证 HELK UI: hunting
[HELK-INSTALLATION-INFO] 正在通过脚本安装 docker...
[HELK-INSTALLATION-INFO] 正在评估 Docker 是否运行...
[HELK-INSTALLATION-INFO] Docker 正在运行...为了简洁起见省略。
************************************************
[HELK-INSTALLATION-INFO] HELK 安装成功
[HELK-INSTALLATION-INFO] 使用以下设置与 HELK 交互

HELK KIBANA URL: http://192.168.38.105
HELK KIBANA USER: helk
HELK KIBANA PASSWORD: hunting
HELK ZOEEPER: 192.168.38.105:2181
HELK KQL SERVER: 192.168.38.105:8080

你可以运行以下命令停止所有 HELK 容器：`docker-compose -f helk-kibana-analysis-alert.yml stop`

现在启动浏览器并使用之前的代码中的 IP（如果是本地构建的）或云地址访问 HELK (Kibana)。由于我们使用的是基于主机的实验室，我们将使用 IP 192.168.38.105。

## 实验 8-5: 安装 Winlogbeat

为了将日志获取 Logstash 并最终显示在如图所示的 Kibana 面板中，你需要安装 beats（即 filebeat、packetbeat、winlogbeat 等）。出于由于我们对 Windows 日志感兴趣，因此我们将使用 winlogbeat。使用 Guacamole 终端（http://192.168.38.105:8080，基于主机实验室）或 RDP（云端实验室）连接到你的服务器，然后从 https://www.elastic.co/downloads/beats 下载并安装 winlogbeat。

将 `winlogbeat.zip` 解压到 `C:\Program Files\` 并解压后的文件夹重命名为 `C:\Program Files\winlogbeat`。

然后，从该服务器打开以下文件并覆盖 `C:\Program Files\winlogbeat` 文件夹中的默认 `winlogbeat.yml` 文件：https://raw.githubusercontent.com/GrayHatHacking/master/ch08/winlogbeat.yml

接下来，使用管理员权限从 PowerShell 安装并启动服务：

```powershell
PS C:\Windows\System32> cd C:\Program Files\Winlogbeat

PS C:\Program Files\Winlogbeat> powershell.exe -ExecutionPolicy Restricted -File .\install-service-winlogbeat.ps1

Start-Service winlogbeat
```

现在，检查 Services 面板确保服务正在运行，如所示。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_308_0.png)

回到 Kibana 面板，如果你点击左侧的 Discover 图标（第二个图标），你应该能看到来自 winlogbeat 的新数据，如所示。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_309_0.png)

## 实验 8-6: Kibana 基础

Kibana 使用索引模式（Index patterns）访问 Elasticsearch 内部的数据。它指定了数据的分组（用于搜索）以及字段如何定义（通过属性）。我们将演示如何创建索引模式以及如何使用 Kibana 查询。

### 索引模式

在 Elasticsearch 中创建自己的索引模式通常很有用。首先点击左上角的 Kibana Logo 进入首页。然后向下滚动并选择 Index Patterns：

![](img/0add480ffb73b6bc89b65d99f7d6b37a_310_0.png)

接下来，选择右侧的 Create Index Pattern 按钮：

![](img/0add480ffb73b6bc89b65d99f7d6b37a_310_1.png)

然后，通过过滤可用日志源完成第 1/2 步。在我们的示例中，我们将创建一个所有以 "log" 开头的日志的主索引。在 index pattern 字段中输入 `log*` 然后点击 Next Step：

### 创建索引模式

Kibana 使用模式从 Elasticsearch 获取数据以用于可视化等功能。

#### 第 1/2 步：定义索引模式

| 索引模式 |
| :--- |
| logs* |

你可以在索引模式中使用 `*` 作为通配符。你不能使用空格或字符 ( /, ?, :, < )。

- 成功！你的索引模式匹配了 10 个索引。

```
logs-endpoint-winevent-additional-2021.05.30
```

接下来，完成第 2/2 步，指定对哪个字段进行时间范围过滤。选择 `@timestamp` 以保持简单。选择 Advanced Options（高级选项）下拉菜单并命名你的新索引。在这种情况下，我们将其命名 logs Gray Hat。然后点击 Index Pattern。

#### 第 2/2 步：配置设置

你已经定义 `*` 为你的索引模式。现在你可以在创建之前指定一些设置。

| 时间字段名称： |
| :--- |
| @timestamp |

Time Filter（时间过滤器）将使用此字段根据时间过滤你的数据。你不需要时间字段，但你将无法通过时间范围缩小数据范围。

- 隐藏高级选项

自定义索引模式

```
logs* Gray Hat
```

Kibana 会为每个索引模式生成一个唯一标识符。如果你不想使用这个唯一 ID，可以输入自定义的 ID。
