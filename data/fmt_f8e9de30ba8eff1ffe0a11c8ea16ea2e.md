
# 运行 MRTG

运行 `MRTG` 有两种方式：手动或作为 `Cron` 任务。第一种方式适用于测试和调试目的。第二种方式是运行 `MRTG` 的首选方式。最好以拥有 `Apache` 进程的用户身份运行 `MRTG` `Cron` 任务。以下命令将揭示该用户：

```bash
$ ps aux | grep -i apache
```

第一次运行时，你会看到许多错误和警告消息，这是因为所有输出和数据文件都缺失，`MRTG` 不得不创建它们。如果一切正常，你的下一个任务将是设置 `MRTG` 作为 `Cron` 任务运行。

在 `Debian 7` 系统上，`MRTG` 可执行文件需要以 `root` 身份运行，因为当环境变量 `LANG` 设置为 `UTF-8` 时，`MRTG` 很可能无法正常工作：

```bash
#### env LANG=C mrtg ../mrtg.cfg
```

![](img/c7d3278283754436651c50a2e9c72912_31_2.png)

## 11 配置 Cron

为 `www-data` 用户设置 `Cron` 需要以 `root` 身份运行以下命令：

```bash
#### crontab -u www-data -e
```

`Cron` 是一个可靠的服务，因此一旦你看到 `MRTG` 作为 `Cron` 任务运行正常，你就不必担心其他问题了。`MRTG` 在你运行 `cfgmaker` 工具时定义的目录中生成其 `HTML` 和图像文件。

![](img/c7d3278283754436651c50a2e9c72912_31_3.png)

## 12 仔细查看配置文件

对于所用设备而言，感兴趣的 `Cisco` `SNMP` `OID`（对象标识符）是 `1.3.6.1.2.1.2.2.10.10.10.14`，它返回 `ADSL` 连接的传入流量。

#### 提示

##### 如果可能，请使用内部接口

每个 `ADSL` 路由器都有两个 `IP` 地址：一个用于内部网络，一个用于外部。当可能时，使用内部网络的 `IP` 来查询你的设备，因为它更安全且速度更快。

##### 不要关闭路由器

如果网络设备被关闭或不可达，`MRTG` 将使用上一个值，直到它能获取新值，因此你会在输出中看到直线。

##### 安全

观察 `MRTG` 的输出可以告诉你关于你网络的许多事情，所以将其养成习惯来观察。在周末看到过多流量或有奇怪的峰值是一个安全警告，需要进一步调查。

##### 日志文件包含数据

`MRTG` 将其 `SNMP` 数据存放的文件命名为 `.log` 扩展名。例如，对于 `cwilf` 设备，日志文件名为 `cwilf.log`。

##### 测试最大速度

测试 `ADSL` 路由器的最大速度被认为是一种良好的实践，方法是下载一个大文件并观察 `MRTG` 的输出。

![](img/c7d3278283754436651c50a2e9c72912_31_0.png)

# 使用 MRTG 监控 Cisco 路由器

开始使用 `MRTG` 及其工具来监控流量负载和 `1.3.6.1.2.1.2.2.1.16.14`，该值返回 `ADSL` 连接的出站流量。

在下一步中，您将学习如何自行查找这些值。

为了让 `mrtg` 跟踪这两个值，您可能需要手动修改 `MRTG` 配置文件中的 `Target[]` 行。

**图 01** 中展示了支持仅一台名为 `c0wi`、`IP` 为 `2.86.19.123` 的 `Cisco` 路由器的最终 `mrtg.cfg` 文件版本。

![](img/c7d3278283754436651c50a2e9c72912_32_0.png)

## 13 Cisco SNMP 对象标识符

找到正确的 `OID` 并不总是容易，有时您可能需要仔细查阅路由器的文档或联系制造商。`Wi-Fi` 连接由 `cfgmaker` 实用程序自动找到，但配置 `ADSL` 部分要复杂一些。要查找您自己的 `OID`，您需要访问 [https://www.oldview.com/mibs/O/IF-MIB.html](https://www.oldview.com/mibs/O/IF-MIB.html)（在 `Google` 上搜索“`IF MIB download`”）。接下来，您应该寻找 `In` 和 `Out Octets`。然后在每个序列的末尾添加所需的 `Cisco` 接口编号。可以通过执行以下 `IOS` 命令来查找 `Cisco` 设备可用的接口：

```
cisco87w# show snmp mib mib index
```

我们想要的接口名为 `Dialer1`，其索引号为 `14`，但您的可能会不同。

![](img/c7d3278283754436651c50a2e9c72912_32_1.png)

## 14 关于 Cacti

`MRTG` 的一种替代方案是 `Cacti`。`Cacti` 也是一个开源网络图形应用，支持插件并利用 `RRDtool`，后者是一个用于时间序列数据的数据记录和图形系统。`Cacti` 插件允许开发者在不处理 `Cacti` 源代码的情况下生成额外的 `Cacti` 功能。

```
EnableIPv6: no
WorkDir: /srv/www/mrtg/mrtg.tsoukalos.eu/public_html
Target[c0wi1]: 1.3.6.1.2.1.2.2.1.10:481  1.3.6.1.2.1.2.2.1.16.14:481 2.86.19.123:
SetEnv[c0wi1]: MRTG_INT_IP="192.168.2.1"  MRTG_INT_DESCR="ADSL"
MaxBytes[c0wi1]: 475000
Title[c0wi1]: Traffic Analysis for 14 — cisco87w.mtsouk.local
PageTop[c0wi1]: <h1>Traffic Analysis for 14 — cisco87w.mtsouk.local</h1>
<div id="sysdetails">
  <table>
    <tr>
      <td>System:</td><td>cisco87w.mtsouk.local in</td>
    </tr>
    <tr>
      <td>Maintainer:</td><td>Mihalis Tsoukalos</td>
    </tr>
    <tr>
      <td>Description:</td><td>ADSL connection</td>
    </tr>
    <tr>
      <td>iType:</td><td>ADSL model</td>
    </tr>
    <tr>
      <td>iName:</td><td>Dialer</td>
    </tr>
    <tr>
      <td>Max Speed:</td><td>475.0 KBytes/s</td>
    </tr>
    <tr>
      <td>Ip:</td><td>2.86.19.123 (No DNS name)</td>
    </tr>
  </table>
</div>
```

图 01

> 一旦您看到 `MRTG` 作为 `Cron` 任务运行正常，您将不会遇到其他问题。

![](img/c7d3278283754436651c50a2e9c72912_32_2.png)

## 15 最后的话

`MRTG` 配置简单，但不支持插件。另一方面，`Cacti` 是一个更强大、功能更丰富的工具，但为了充分发挥其潜力，您需要对其进行实验。`Cacti` 将是即将发布的一篇文章的主题，届时您可以将其与 `MRTG` 进行比较，并决定哪一个更适合您的需求。

我强烈建议学习 `Cacti` 和 `MRTG` 两者，以便能够根据工作任务选择合适的工具。

##### 教程

- `OrangeHRM` 的主要模块。点击其中任何一个将带您进入相应模块的着陆页
- 选择主要模块之一后，子模块会出现在这个橙色菜单栏中
- 按姓名、`ID` 或其他详细信息搜索员工。搜索非常灵活，允许即使字段已填充也能进行搜索

![](img/c7d3278283754436651c50a2e9c72912_33_0.png)

- 员工详情添加在此处。点击添加按钮会显示一个新表单，允许您输入新员工的详细信息
- 系统中已存在的员工列表。点击姓名将显示该员工的信息

# 使用 OrangeHRM 简化人力资源管理

员工是任何组织最重要的部分，管理工具对于维持效率至关重要。

# 顾问

`Nitish Tiwari` 职业是软件开发者，内心是开源爱好者。除了为一家领先的开源杂志撰稿外，他还帮助企业设置和使用开源软件来满足其业务需求。

![](img/c7d3278283754436651c50a2e9c72912_33_1.png)

#### 资源

- `OrangeHRM`: `www.orangehrm.com`
