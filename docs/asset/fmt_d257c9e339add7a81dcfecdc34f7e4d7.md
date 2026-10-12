
Nagiosgraph 的文件名由主机名、服务描述和数据库名称共同组成，例如 `linux01_PING_ping`。`db-name` 处可以自由选择，但应包含 `rta` 这样的关键字。占位符值在映射文件中被单引号包围，以防与关键词冲突。测量值本身通过 Perl 确定，而占位符值通过乘以 `$1` 进行替换。`DERIVE` 类型被 Nagiosgraph 推荐用于计数，随着运行而增长。

性能数据。可以寻求帮助，例如通过 Nagiosgraph 论坛：http://sourceforge.net/forum/forum.php?forum_id=394748。

## nagiosgraph

主机 linux01 · 服务：fs_a 的性能数据

每日

![](img/8e1ca2e9d03c845e2cebae88c24b6c80_433_0.png)

每周

![](img/8e1ca2e9d03c845e2cebae88c24b6c80_433_1.png)

图 19-1. 主机 linux01 上文件系统 /net/linux01/a 的使用空间和限制值，如 Nagiosgraph 所示。

对映射的更改至关重要。建议您先复制文件并编辑代码，然后使用 `perl -c` 进行语法检查：

```
nagios@linux:libexec/nagios$ cp map map.new
nagios@linux:libexec/nagios$ vi map.new
nagios@linux:libexec/nagios$ perl -c map.new
nagios@linux:libexec/nagios$ mv map.new map
```

如果语法检查无误，您可以将新文件安装为 map。

[194] 关于此主题的更多信息可以访问 http://www.rrdtool.org/。

[195] 安装请参阅 19.4.1 安装。

[196] 关于 `serviceextinfo` 对象的更详细描述见 16.4.2 扩展服务信息，第 366 页。

[197] 一对方括号包含备选项。

[198] 这将千字节（KB）转换为字节（bytes）。

## 19.3 为 Perf2frrd 准备性能数据

另一个将 Nagios 性能数据传输到 RRD 数据库的工具是 Java 程序 Perf2frrd。这需要安装 运行时环境（1.4.2 插件测试，或者优选 1.5 配置 Web 界面）。由于虚拟机在强大的计算机上会产生明显的负载，并且需要大量的内存，Perf2frrd 对 Nagios 服务器的要求显著高于 Nagiosgraph。

另一方面，在生成 RRD 数据库方面，安装完成后无需额外工作，因为 Perf2frrd 使用了 Nagios 的模板机制（见 19.1 使用 Nagios 处理插件性能数据，第 404 页）。对于模板中的每个服务和变量，该工具使用以下名称创建单独的 RRD 数据库：

```
host+service_description_variable_name.rta (平均值)
```

为了评估 check_imp 文件名 `linux01+PING+.plrd` 和 `linux01+PING+rta.rrd`，以及 `p`（丢包率），

Perf2frrd 现在使用 RRD 数据库存储数据，且不提供图形化显示存储在存储处数据的工具。Perf2frrd 的作者 Marc Deitano 参考了 `draw` 工具（见 19.4 图形专家 draw，第 420 页）。使用该工具是有益的，因为一方面 `draw` 允许显示比 Nagiosgraph 更多的内容，另一方面您就不需要与 Perl 正则表达式作斗争。

### 19.3.1 安装

安装时，您应该从 http://perf2frrd.sf.net/ 获取 tar 格式的压缩包，并复制它，为 `/usr/local` 层级结构做好准备：

```
linux: # cd /usr/local
linux:/usr/local # tar xvf /path/to/perf2frrd-1.0.tar.gz
perf2frrd/run
```

插入的可执行程序是一个名为 `run` 的脚本，它反过来调用 Java 字节码解释器 `java`。此外，该目录包含 Java 类文件以及可能的重新编译共享库 `libr2frrd.so`。对于较新的发行版通常是不需要的。

为了让 `run` 能够找到 `java` 程序，它必须位于 `/usr/bin`。如果不是这种情况（例如您是从 http://www.sun.com/ 安装的 Java 包），则应该设置链接：

```
linux: # ln -s /usr/local/perf2frrd-1.0/bin/java /usr/bin/java
```

短期测试可以显示 Perf2rd 是否正确启动：

```
nagios@linux:local/perf2rd$ /run
perf2rd starting
Using Nagios Config: /etc/nagios.cfg
Using RRD Repository: /var/log/nagios/rrd
Unable to create RRD Repository
```

最后一行行的错误信息目前不是问题，因为我们将 RRD 数据库保存在不同的目录中（Perf2rd 在持续运行时）。

### 19.3.2 Nagios 配置

Perf2rd 在 Nagios 配置中搜索它所需的所有数据：Nagios 应该写入性能数据的文件、为此使用的写入模式以及模板的格式：

```
# /etc/nagios/nagios.cfg
process_perdata=/var/nagios/service-perdata.dat
service_perdata=$template$TIME$\tHOSTNAME$\t
SERVICESTATUS$\tEXECUTION$\tLATENCY$\t
TIMEOUT$\tSERVICEPERDATA
serviceperdata_file_mode=w
```

这里使用的命名管道（`serviceperdata_file_mode=w`）必须手动创建——Perf2rd 1.0 在普通文件接口（`serviceperdata_file_mode=w`）上存在问题：

```
linux: # mkdir /var/nagios/service-perdata.dat
linux: # ls -l /var/nagios/service-perdata.dat
-rw-r-- 1 nagios nagios May 1 10:49
```

模板生成的 `[SERVICEPERDATA]` 戳缺失，因为 Perf2rd 1.0 无法正确解析。Nagios 配置的更改需要执行：

```
linux: # /etc/init.d/nagios reload
```

最后，创建 RRD 数据库的目录：

```
linux: # mkdir /var/lib/rrd/perf2rd
linux: # chown nagios /var/lib/rrd/perf2rd
```

### 19.3.3 实践中的 Perf2rd

每次 Perf2rd 加载虚拟机都需要大量的资源。因此，您不应该按照 Nagios 的特定间隔启动 Perf2rd，也不应该使用 `-o` 的单次模式（该模式软件一次处理一个文件）。在理论上，这可以通过 cron 任务定期运行 Perf2rd。相反，我建议您保持程序持续运行。首次使用时，我建议切换到调试模式，这将显示任何发生的问题。`-d` 选项指定工具创建和更新 RRD 数据库的目录：

```
nagios@linux:local/perf2rd$ /run -d /var/lib/rrd/perf2rd
perf2rd starting
Using Nagios Config: /etc/nagios.cfg
Using RRD Repository: /var/lib/rrd/perf2rd
Debug Mode is:
Reading data from named pipe.
Perf Data File is:/var/nagios/service-perdata.dat
I believe we are using Nagios ver.
Nagios interval_length=60
called with ...
called with ...
```
