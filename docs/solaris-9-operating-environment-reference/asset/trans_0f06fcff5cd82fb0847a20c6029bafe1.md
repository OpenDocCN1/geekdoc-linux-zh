

# prof

## 1123

由于在共享对象中花费的时间无法被统计，因此在使用 `prof` 对程序进行性能分析时，请尽可能减少共享对象的使用。你可以将程序链接到经过分析的库版本（如果没有分析版本，则链接到标准归档），而不是共享对象，以获取库函数的性能分析信息。系统在 `/usr/lib/libprof` 目录下提供了经过分析的库版本。请参阅编译器驱动程序中关于性能分析的文档。

考虑一个示例。一个动态链接到标准 C 库的分析程序在某些例程（例如 `malloc()`）中花费了100个单位的时间。假设 `malloc()` 仅从例程 B 调用，且 B 消耗了1个单位的时间。进一步假设例程 A 消耗了100个单位的时间，超过主程序中的任何其他例程。在这种情况下，`prof` 的结论是大部分时间花在 A 中，而不是 B 中。实际上，通过查看例程 B 而不是 A，无法判断最大的改进在哪里。在这种情况下，性能分析器的价值严重降低；解决方案是尽可能使用归文件进行性能分析。

## 选项

互斥选项 `-a`、`-c`、`-n` 和 `-t` 决定输出行的排序类型。

- `-a` 按符号递增排序。
- `-c` 按调用次数递减排序。
- `-n` 按符号字母顺序排序。
- `-t` 按时间百分比递减排序（默认）。

互斥选项 `-o` 和 `-x` 指定每个监控符号地址的打印格式。

- `-o` 以八进制打印符号地址及符号名。
- `-x` 以十六进制打印符号地址及符号名。

互斥选项 `-g` 和 `-l` 控制报告中符号的类型。使用 `-l` 选项时要小心；它将静态函数花费的时间应用到前面的（全局）函数而不是静态函数本身。如果所有静态函数都被正确定位，此功能将非常有用。如果没有，生成的报告可能具有误导性。

假设 A 和 B 是只调用静态 S 的局部函数。如果 S 紧跟在 A 之后（即如果 S 被正确定位），那么使用 `-l` 选项可以很容易确定在 A 中花费的时间，包括在 S 中花费的时间。然而，如果 A 和 B 都调用 S，那么使用 `-l` 选项的报告是误导性的；B 调用 S 的时间被归于 A，使得似乎时间是花在 A 中的。在这种情况下，S 无法被正确定位。

- `-g` 分别列出静态（全局）函数花费的时间。`-g` 选项是 `-l` 函数的反。
- `-l` 将执行静态函数的时间分配给静态函数之前的全局函数。这是默认选项。它是 `-g` 函数的反，应谨慎使用。

## 1124 prof

以下选项可以任意组合使用。

```
-C 在打印前对符号名进行去混合。
-h 抑制报告中通常打印的标题。如果需要进一步处理报告，此选项很有用。
-m 使用 `mdata` 文件代替 `mon.out` 作为输入文件。
-s 在标准错误输出上打印监控参数和统计信息的摘要。
-V 在标准错误输出上打印 prof 版本信息。
-z 包含性能范围内的所有符号，即使其调用次数和时间为 0。
```

如果程序使用 `-p` 选项进行编译，则会创建一个性能文件。该选项安排在执行开始和结束时监控调用。在执行结束时监控调用写入性能文件。如果使用 `-p` 选项，会统计函数的调用次数。单个函数可以通过 `MARK` 宏拆分为子函数进行分析。参见 `prof(5)`。

## 环境变量

```
PROFDIR 指定由分析程序创建的文件目录。如果未设置 PROFDIR，则在当前目录产生 `mon.out`。如果设置 PROFDIR=string，则产生 string/progname.pid，其中 progname 包含去除了任何前缀的 argv[0]，pid 是程序的进程 ID。如果 PROFDIR 设置为 null，则不产生性能输出。
```

## 文件

```
mon.out 默认性能文件。
a.out 默认列表文件。
```

## 属性

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 | SUNwb |

## 相关

```
gprof(1), cc(1), exit(2), profil(2), psample(2), malloc(3), MALLOC(3M), monitor(3C), attributes(5), prof(5)
```

## 1125 profiles — 打印用户的执行性能

## 概要

```
/bin/profiles [-l] [user...]
```

## 描述

使用 `profiles` 命令（于 Solaris 8 中引入）在标准输出上打印指定用户或角色执行特定功能所需的命令和权限。权限是基于角色的访问控制 (RBAC) 封装机制，列出每个可执行文件的属性，以及有效用户和组 ID。性能 shell 是 `pfsh`、`pfksh` 和 `pfexec`。

你可以组合多个 profiles 来构建相应的访问控制。当分配 profiles 时，权限会被添加到现有集合中。如果同一命令在多个 profiles 中出现，则根据 profiles 的顺序使用第一个出现项。为了方便起见，你可以指定通配符来匹配所有命令。

从 Solaris 9 发布开始，如果在 `/etc/security/policy.conf`（参见 `policy.conf(4)`）中定义了任何默认策略，则默认策略将被添加到从 `user_attr(4)` 加载的列表中。`prof_attr(4)` 中的匹配项提供了命令列表。

## 选项

- -1 列出每个 profile 中的命令，随后是用户和组 ID 等特殊进程属性。

## 示例

以下示例显示了 `profiles` 命令的输出。在没有选项的情况下，`profiles` 显示当前用户的性能。

```
profiles
Primary Administrator
Basic Solaris User
All
```

以下示例显示了三个用户的 `profiles` 命令输出。winsor 拥有 Primary Administrator 权限，ray 拥有 System Administrator 权限，des 拥有默认的 Basic Solaris User 和 All 权限。确定一组权限是否停止另一组的方法是使用 All 权限，它始终是列表中的最后一个。

```
profiles winsor ray des
Primary Administrator
Basic Solaris User
```

## 1126 profiles

- All
System Administrator
Audit Review
Printer Management
Cron Management
Device Management
File System Management
Mail Management
Maintenance and Repair
Media Backup
Media Restore
Name Service Management
Network Management
Object Access Management
Process Management
Software Installation
User Management
All
Basic Solaris User
Basic Solaris User
All
m%

以下示例使用列表选项显示具有 Primary Administrator 权限的用户的命令和属性。

```
profiles -1 winsor
```

```
Primary Administrator:
* uid=0, gid=0
All:
*
```

```
%
```

以下示例使用列表选项显示具有 System Administrator 权限的用户的命令和属性。

```
profiles -1 ray
```

```
Audit Review:
/usr/sbin/praudit euid=0
/usr/sbin/auditreduce euid=0
/usr/sbin/auditstat euid=0
Printer Management:
/usr/sbin/accept euid=1lp
/usr/ucb/lpq euid=0
/etc/init.d/lp euid=0
/usr/bin/lpstat euid=0
/usr/lib/lp/lpsched uid=0
/usr/sbin/lpfilter euid=1lp
/usr/bin/lpset egid=14
/usr/sbin/lpadmin egid=14
/usr/sbin/lpsystem uid=0
/usr/sbin/lpmove euid=1lp
*
```

