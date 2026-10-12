
下一个测试检查主机的 CPU 温度。对于传感器，这里使用了 `lm-sensors` 软件包，它访问现代主板上相应的芯片。由于 `lm-sensors` 处于激活状态，它允许 NET-SNMP 代理从部分树 `ucdavis.outExperimental.lmSensors` 中读取相应信息：

```bash
nagios@linux/local/libexec6 ./check_snmp -H localhost -C public -o
lmTempSensors.Value -w 25000-45000 -c 48000 -u 'degrees Celsius (* 1000)'
-1 Temp/CPU
Temp/CPU OK 41000 degrees Celsius (* 1000)
```

输出取决于芯片组，在这里你必须将查询值乘以因子 1000。因此，你别无根据你正在使用的主板调整警告和严重限制。在示例中，CPU 温度 41 摄氏度处于“绿灯状态”；如果它降至 25 度以下或高于 45 度，将导致警告；如果低于 20 度或高于 48 度，将是严重状态。

### 正则表达式与固定字符串比较

你可以通过以下方式检查文本是否出现在系统中：

```bash
nagios@linux/local/libexec6 ./check_snmp -H localhost -C public -o system.sysName.0 -r SNMP OK
```

使用 `-r` 作为正则表达式时，而不是定义要搜索的字符串，文本必须完全精确匹配，这可能非常棘手，因为 `snmpget` 在分隔符之后输出的所有内容……

## 监控网络接口

最后一个示例查询 Cisco 路由器的第一个网络接口是否运行：

```bash
nagios@linux:local/libexec$ ./check_snmp -H cis -C public \
-o ifOperStatus.1 -w 1 -u 'SNMP: Status for Port 1 is: SNMP: Status for Port 1 is: OK'
```

可以在 `ifOperStatus` 中找到该信息。虽然 `ifOperStatus` 提供运行状态，但 `ifAdmin` 揭示接口在管理上是开启还是关闭。在此处指定限制时，我们使用范围 `1:1`，这样如果接口被物理关闭，插件将发出警告，返回值为0。由于使用了 `-u` 选项，`check_snmp` 在确定的数值的输出中添加了描述。

尽管如此，插件并没有告诉全部真相：使用 `df` 测试显示的负载为 96%，这是由于该程序正确地向上取五入了实际的 95.8% 负载，而 SNMP 中的整数很少向上取五入，而是简单被截断。你只能接受这种微小的不精确，因为 MIB 不提供浮点小数。

如果你希望内容更详细，可以使用选项 `-1`：`-1 SNMP-DISK: /net/subspace/b ' causes...` 会导致其他自定义信息被添加到命令的输出结果中：

```bash
SNMP-DISK:/net/subspace/b WARNING *95* percent
```

上述查询可以通过如下命令对象进行通用运行：

```bash
define command{
	command_name check_snmp
	command_line $USER1$/check_snmp -H $HOSTADDRESS -C $USER3 -P 1 -o $ARG1\
-w $ARG2 -c $ARG3 -l $ARG4
}
```

此定义假设被查询的值是数值或布尔值（参见“监控网络接口”），否则在同时指定警告和严重值时，我们在宏 `$USER3$` 中存储此逗号，其后跟的是协议版本（`-P 1` 代表 SNMPv1）、OID、警告和严重限制，以及一个前缀。

在服务定义中对该命令的调用格式如下：

`check_snmp oid! warn! critical !prefix`

如果你想专门监控 `dswspace` 计算机上索引为 2 的文件系统的负载，则将使用以下定义：

```bash
define service{
  service_description SNMP-DISK-a
  host_name dswspace
  check_command check_snmpdTable.checkEntry dskPercent.2|0:90|10:95|DIS
K: /net/dswspace/a
}
```

尽管 `check_command` 行被折叠，但在实践中所有参数必须在单行内，并用感叹号 `!` 分隔（分隔符前后不要有空格）。

```
sed=0
```

在实际上，此插件也不会像此处可能暗示的那样，跨多行显示其输出内容。由于这些信息之所以能以相对清晰的形式显示在 Nagios Web 界面上，是因为其中插入了 HTML 格式元素 `<BR>`。这导致每个端口的输出都显示在单独的一行。性能数据开头的字符在 Web 界面中完全没有出现。

此类查询被实现如下所示的命令对象：

```
command{
  command_name check_ifstatus
  command_line $USER$/check_ifstatus -H $HOSTADDRESS$ -C $USER$ -xARG1$
}
```

在这里，`$USER$` 也被用于定义 `resource.cfg` 资源文件中的团体字符串（community string）。总共有 `$32$` 个宏可用，其中前两个通常包含路径细节，其余可以按你需要的任何方式使用。

如果你倾向于排除端口而不是接口类型，可以在定义中使用 `-u` 选项代替 `-x`。

如果 Nagios 要像上面所示监控 `cisco01`，并排除编号为 1 和 53 的两个接口类型，相应的服务定义如下起始：

```
service{
  service_description Interfaces
  host_name cisco01
  check_command check_ifstatus!1, 53
}
```

### 11.3.3 测试单个接口的运行状态

要测试单个接口，你可以使用通用插件 `check_snmp` 或 `check_ifoperstatus`，后者专门测试网卡的运行状态（`ifOperStatus`）。该通用插件的优势主要在于其使用的易用性；你不需要使用端口的索引，也可以在此处指定它的描述——例如，`eth0`。

`check_ifoperstatus` 具有以下选项：

- `-H address` / `--host=address`

  这是要查询的 SNMP 代理的主机名或 IP 地址。

- `-C password` / `--community=password`

  此参数提供读取权限的团体字符串。

- `-p port` / `--port=port`

  只要 SNMP 代理没有在 UDP 端口 161 上运行，可以使用此选项指定端口。

- `-k ifIndex` / `--key=ifIndex`

  `ifIndex` 是要查询的网络接口编号（例如计算机的网卡或交换机的端口）。

- `-d ifDesc` / `--desc=ifDesc`

  插件不再处理索引键，而是从 `ifDesc` 处理接口名称（见下文）。

- `-v version` / `--snmp_version=version`

  这指定了查询的 SNMP 版本（1、2 或 3）。

- `-w return_value` / `--warn=return_value`

  此选项用于在接口处于休眠状态时选择返回值。`return_value` 可以是 `i`（忽略休眠状态并返回 OK!）、`w`（WARNING）或 `e`（CRITICAL，默认值）。

- `-D return_value` / `--admin-down=return_value`

  如果接口已在管理上关闭，插件应该返回什么值（`i`、`w` 或 `e`）？默认值 `w` 会发出警告，`e` 返回 CRITICAL，`i` 则返回 OK。

- `-M bytes` / `--maxmsgsize=bytes`

  这是 SNMP 数据包的最大大小；默认值是 1472 字节。

在名为 `igate` 的系统中，`snmpwalk` 找到了以下接口 ...

```
interfaces.ifTable.entry.ifDesc.3 = ipsec0
interfaces.ifTable.entry.ifDesc.4 = ipsec1
interfaces.ifTable.entry.ifDesc.7 = eth0
interfaces.ifTable.entry.ifDesc.8 = eth1
interfaces.ifTable.entry.ifDesc.9 = eth2
interfaces.ifTable.entry.ifDesc.10 = ppp0
```
