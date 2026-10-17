
时钟滴答的准确性也不会比此高。`sort`然后将两个相关的字段作为列进行数值排序。

## 使用 Proc::ProcessTable 模块

`use Proc::ProcessTable;`

## 创建一个临时对象并保存它生成的进程表

`my $table = Proc::ProcessTable->new->table;`

第一个数字列列出了时钟滴答数，第二列列出了用户 ID。

该解决方案非常接近我们的目标，但无法显示进程的用户名。此外，某些确定在系统启动后很久才启动的进程（例如 Tor 浏览器）意外地显示为在系统启动后零秒启动的。另一方面，`init`进程直到启动后 468 个时钟滴答或 4.68 秒才启动。在测试用例中，可能是因为必须先输入硬盘加密密码。从代码中移除 `awk`并指定匹配字段 22 和 21 可以可视化进程。

## 表的 Schwartz 变换

```perl
my @result = 
## 对列表排序，先按启动时间，再按 PID
sort { ($a->[0] <=> $b->[0]) or ($a->[1] <=> $b->[1]) }
## 仅使用进程的启动时间、PID 和 UID
map { [ $_->start, $_->pid, $_->uid ] } # 紧跟引用标量后的数组是数据源
@table;

## 通过经典迭代输出结果
foreach $p (@result[0..$max-1]) {
    say sprintf('PID: %6i | Start: %s | UID: %s', $p->[1], ''.localtime($p->[0], $p->[2]));
}
```

## 深度解析

## 查找进程

### 列表 11：紧凑 Perl 变体

每个列表项包含四个数据字段：PID、程序或调用名称、创建时间和用户名。

第二个函数 `calculateTimestamp()` 计算时间，该时间将作为限制过滤器，用于后续过滤掉无关的进程。

主程序首先调用 `getListOfOfProcesses()` 函数，然后根据创建时间和 PID 对进程列表进行排序。这产生了列表 07 所示的输出，其中包含了所有标识进程及其所有者、PID、程序名和创建时间。

```perl
#!/usr/bin/perl
use Proc::ProcessTable;

sub getListOfOfProcesses {
    my @processes;
    my $table = Proc::ProcessTable->new->table;
    foreach my $row (@$table) {
        push @processes, $row;
    }
    return @processes;
}

sub calculateTimestamp {
    my ($sec, $min, $hour) = @_;
    return localtime($sec, $min, $hour);
}

### ... (其余的 Perl 逻辑)
```

### 列表 12：导入所需的模块

```go
package main

import (
    "bufio"
    "fmt"
    "io/ioutil"
    "log"
    "os"
    "strconv"
    "strings"
    "time"

    "github.com/mitchellh/go-ps"
    "github.com/tkla/go-sysconf"
)
```

### 列表 14：时间范围

```go
// 计算时间范围
// 当前时间 - 天数 * 24h * 60min * 60s
timeBoundary := time.Now().Unix() - timeLimit64*24*60*60

// 从 /proc/stat 获取启动时间（自 11970 年起的秒数）
// 可在 /proc/stat 中以 btime 开头的行
fileHandle, err := os.Open("/proc/stat")
if err != nil {
    log.Fatalf("Error calling os.Open(): %v\n", err)
}
defer fileHandle.Close()

scanner := bufio.NewScanner(fileHandle)
for scanner.Scan() {
    currentLine := scanner.Text()
    if strings.HasPrefix(currentLine, "btime") {
        dataFields := strings.Fields(currentLine)
        bootTime = dataFields[1]
        break
    }
}
```

### 列表 13：变量

```go
var bootTime string
var userID string

// 将字符串转换为数值
bootTime64, err := strconv.ParseInt(bootTime, 10, 64)
if err != nil {
    log.Fatalf("Error: %v\n", err)
}
// 抑制日期和时间输出
log.SetFlags(0)
```

### 列表 15：CLK_TCK

```go
// 存储的 CLK_TCK 参考值：每秒数值
timeLimit64 := int64(10)
clkTck, err := sysconf.Sysconf(sysconf.SC_CLK_TCK)
if err != nil {
    log.Fatalf("Error calling Sysconf")
}
```

### 列表 16：进程列表

```go
// 获取进程列表
processList, err := ps.Processes()
if err != nil {
    log.Fatalf("Error in call to ps.Processes()")
}
timeLimit64 = timeArg
log.Printf("Set time limit to %d days\n", timeLimit64)
```

04 // 提取 PID 和执行程序

35 dataFields := strings.Fields(string(dataBytes)) 05 pid := process.Pid()

36

06 exec := process.Executable()

37 // 计算进程启动时间

38 // 读取自系统启动以来的时钟周期数 08 // 从 /proc/<pid>/status 读取用户 ID

39 // 可用 /proc/<pid>/stat 的第 22 列 09 // 可用 Uid 开行的第 2 列

40 // Go 的计数从 0 开始；因此数据字段 21

10 // Go 的计数从 0 开始；因此数据字段 1

41 executionTime := dataFields[21]

11 statusPath := fmt.Sprintf("/proc/%d/status", pid) 42 executionTime64, err := strconv.ParseInt(executionTime, 10, 64)

12 fileHandle, err := os.Open(statusPath)

13 if err != nil {

14 log.Fatalf("Error: %v\n", err)

14 if err != nil {

15 log.Fatalf("Error calling os.Open(): %v\n", err)

15 }

16

16 defer fileHandle.Close()

17 // 将通过的时钟周期数除以存储的内核值

18 scanner = bufio.NewScanner(fileHandle)

18 // 提供自启动以来的秒

19 for scanner.Scan() {

19 // 并加上启动时间

20 currentTime := scanner.Text()

20 executionTime64 = (executionTime64 / clTck) + bootTime64

21 if strings.HasPrefix(currentLine, "Uid") {

22 uidFields := strings.Fields(currentLine)

22 // 检查时间范围

23 userId = uidFields[1]

23 if executionTime64 < timeBoundary {

24 break

24 // 将开始时间计算日期

25 startDate := time.Unix(executionTime64, 0)

27 // 输出进程信息

27 // 从 /proc/<pid>/stat 读取进程状态

28 fmt.Printf("User ID: %s, Process ID: %d, Program name: %%s, Started on %%s\n", userId, pid, exec, startDate) 29 procPath := fmt.Sprintf("/proc/%d/stat", pid) 30 dataBytes, err := iutil.ReadFile(procPath) own

31 if err != nil {

30)

## 深度解析

## 查找进程

在下一步中，用户扫描进程并创建一个列表（列表 18）。然后使用一个 `for` 循环遍历此列表，并根据用户和进程运行时间对每个进程进行分析。如果进程处于在一秒到最多一秒半之间的时间范围内，那么这对于日常使用是足够的。

我们要感谢 Tobias Klauser 提供的 `go-sysconf` 包以及对优化 Go 变体的支持。Python 脚本以及 Perl 和 Go 实现都使用了一个匹配的库，可以轻松访问进程信息。结果所示（列表 17）。输出显示了脚本是如何带有参数 1 被调用的，然后通过管道通过 `grep` 处理以找到进程列表中调用的所有 Bash 实例。

### 列表 18：Go 脚本输出

```
$ ./list-processes 1 | grep bash
```

用户 ID: 1000, Process ID: 604, Program name: bash, Started on 2020-04-14 11:31:51 +020 CEST

User ID: 1000, Process ID: 5318, Program name: bash, Started on 2020-04-16 16:15:21 +020 CEST

User ID: 1000, Process ID: 6984, Program name: bash, Started on 2020-04-16 19:04:52 +020 CEST

User ID: 1000, Process ID: 6998, Program name: bash, Started on 2020-04-16 19:08:57 +020 CEST

然而，Go 库仍然有扩展空间。已经集成在 Python 库中的函数在 Go 变体中必须手动构建。

如果你比较所有的解决方案，除了 Bash 变体 3 之外，所有变体都提供了有用的结果。在程序大小方面，Bash 变体 2 胜出；Go 变体最长，超过 140 行。Python 实现处于中低水平。

对于可理解性和可读性，意见分很大。特别是对于列表 11（紧凑的 Perl 变体），即使是熟练的 Perl 程序员也需要时间（以及我们使用的模块的文档）来理解它。Python 或 Go 的实现可能更长，但学者更容易理解。

## 作者

Frank Hofmann 大部分时间在路上工作，最好是在柏林、日内瓦和开普敦，担任开发者、培训师和作者。他目前是弗朗什-科特大学 Mesocentre de Calcul 科学计算集群的 Linux 系统管理员。

Axel Beckert 在苏黎世联邦理工学院中央 IT 服务担任 Linux 系统管理员和网络安全专家。他还是 Debian GNU/Linux 发行版、瑞士 Linux 用户组 (LUGs)、Hackfunk 广播节目和播客的志愿者。

## 结论

[1] 弗朗什-科特大学的 Mesocentre de Calcul：http://meso.univ-fcom.fr/

[2] MATLAB：https://www.mathworks.com/products/matlab.html

[3] Linux 进程执行时间：https://linux-process-time

[4] psutil：https://psutil.readthedocs.io/en/latest/

[5] MetaCPAN：https://metacpan.org

[6] Proc::ProcessTable：https://metacpan.org/pod/Proc::ProcessTable

[7] Schwartz 变换：https://en.wikipedia.org/wiki/Schwartzian_transform

[8] “2020 年值得学习的最佳编程语言”：https://hackr.io/blog/best-programming-languages-to-learn-2020-jobs-future

[9] go-ps：https://github.com/mitchellh/go-ps

[10] go-sysconf：https://github.com/tklauser/go-sysconf

[11] Debian 包管理：https://www.dpmb.org/index.html

# 多参数传感器

## 花园中的分布式天气监控

在花园中放置远程无线传感器，并通过仪表和时间图跟踪环境状况，并在需要更换电池时进行记录。

对于此类应用的传感器，最重要的要求是它能够无线传输数据，这显然意味着需要电池电源。我考虑了多种无线技术，包括 WiFi 和蓝牙，但由于功耗原因拒绝了这些技术。一个大 1000mAh 电池会有火柴盒大小。

## 仪器化花园

许多商业传感器 [2] 都能满足这些要求，使用此类设备构建传感器数组是完全可能的。然而，作为一名硬件工程师，我决定设计符合自己需求的传感器（图 1）。

有线传感器位于单一固定位置，仅测量当前温度，且离房子太近。为此，我选择了一个火柴盒大小的外壳。传感器位于室外，室内指示器用于

锂电池为多个地点的测量类型提供了足够的功率，其功耗低、测量范围有限，且传感器可运行数年，且不需要到处拉乱电线。我之前工作过一种方案，让单元每隔 10 分钟睡眠一次，以提供季节性数据以便更好地规划种植，并具有报警功能以警报霜冻和高温。理想情况下，数据将以如下形式可用。

LoRa [1] 是一种专为低数据速率、低功耗和远距离数据遥测设计的无线技术。此外，所需测量的传感器均以 I2C 设备的形式提供，使得所有设备可以通过总线汇合并连接到小型微控制器上。LoRaWAN 广域网协议与公共网关和公共“着陆点”组成的网络协同工作，以保护数据安全。传感器产生的功率通过一个 MOS-FET 开关 [3] 提供给设备，因此设备在测量之间可以关闭电源。

Andrew Malcolm (CEng, MIET) 致力于物联网（IoT）传感器工作。作为 Guru Systems (https://www.gurusystems.com/)（一家快速成长的物联网硬件和 SaaS 公司）的资深工程师，他正致力于低碳能源项目。在空余时间，他喜欢结合软件工程。凭借对可用开源工具的掌握，他从不设计项目。

你可以通过 andrewrussellmalcolm@gmail.com 联系 Andrew。

图 1：自定义传感器设置。

LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM | 第 239 期 | 2020年10月 | 57

![](img/4124af05f4c60b6759782ba44ba4bc7f_378_0.png)

![](img/4124af05f4c60b6759782ba44ba4bc7f_378_1.png)

MAKERSPACE 仪表花园

图 2：原理图 [6]。

通过测量，我确认了在投入设计自己的 PCB（图 3）之前，传感器的待机功耗（图 2）小于 50µA，这对于机械限制严格的设计特别有帮助。LoRa 无线调制解调器通过 SPI 总线连接到微处理器。电源由电池提供，无线天线采用螺旋设计以保持紧凑性。还可以将 STEP 文件 [7] 导出到其他 CAD/CAM 软件包，例如 FreeCAD（另一个免费开源软件包），因此 PCB 可以集成到更大的微控制器中 [4]。

PCB 设计包含一个锂电池支架、螺旋天线、编程连接器、螺丝孔，以及一个适配我所选外壳 Hammond 1551FGLGY [8] 的轮廓。选择微控制器是因为 I/O 引脚、低功耗和小型封装之间的良好平衡。外壳盖子带有法兰，允许通过螺丝、线或扎带将其固定在支撑结构上。紧邻传感器簇的小孔允许空气和光线进入外壳。必须确保外壳垂直安装以防止积水。

## 原理图与 PCB 设计

对于设计工作，我使用了 KiCad [5]，这是一个运行在 Linux 上的免费开源设计软件包，允许对布局进行 3D 可视化。

传感器的软件改编自 STMicroelectronics 提供的示例，因此大部分软件涉及整合 I2C 传感器的驱动程序并为无线收发器格式化数据，该收发器可以同时在多个通道上发送和接收。我选择了一个由 IMST [13] 生产的商用网关，它需要通过 SPI 总线与主机通信。

IMST 提供了一个优秀的教程 [14]，介绍如何使用树莓派构建完整的网关，这增强了本文关于构造、软件设置和网关配置的逐步说明，并包含一个用于转发上行和下行数据包的完整软件应用程序。
