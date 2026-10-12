
# 配置部分包含以下参数：

## interface

此定义了与 Nagios 的连接类型。可能的连接类型包括管道（`pipe`）、网络（`network`）和文件（`file`）。对于管道类型，Nagios 和 `collect2.pl` 守护进程通过命名管道（`pipe` 类型参数定义）进行通信；对于网络类型，Nagios 通过网络套接字通过 UDP 传输协议发送性能数据（见参数 `port`）。

与所述的接口类型不同，文件类型（从 1.7 版本开始可用）利用了模板机制208，这意味着 Nagios 将性能数据写入文件，由 `collect2.pl` 守护进程定期对该文件进行性能数据处理，从而节省资源。1.6 版本及之前的默认接口类型是 `pipe`，从 1.7 版本起为 `file`。

## perfffile_path

此定义了 Nagios 通过模板机制写入所有性能数据的文件所在目录。

## pipe

此定义了一个命名管道，Nagios 通过程序 `fifo_write` 向其写入数据，并由收集脚本 `collect2.pl` 从中再次读取。该命名管道从 1.6.1 版本开始通过 `make install` 自动创建。

## port

此指定了网络通信类型使用的 UDP 端口。默认值为 5667。

## buffer

此决定了通过 UDP 字节发送性能数据的缓冲区大小。默认值为 1024 字节。

## pidfile

此定义了 NagiosGrapher 在启动时写入其进程 ID 的文件。

## user, group

这些定义了运行 `collect2.pl` 守护进程时所属的用户和组。在这里，指定 Nagios 工作时所属权限的用户和组是有意义的。

## step

此定义了 RRD 数据库的秒为单位的步长。在此期间记录的所有值都由 RRDTools 汇总为一个单一值。因此，`step` 也描述了 RRD 数据库中数据的最小时间分辨率。该值对新创建的 RRD 数据库有效，后续修改对现有数据库没有影响。

## heartbeat

心跳定义了一个以秒为单位的周期，在此期间 RRD 数据库始终期望接收数据。如果在此期间没有任何测量值到达，NagiosGrapher 将生成一个无效记录（nan，不是数字）。

为了在上述示例中出现有效记录，每 60 秒必须至少到达一个测量值。由于分辨率为 60 秒，数据库在“心跳”期间内包含十个条目。如果缺少其中一个值，NagiosGrapher 将简单地用上上一个有效值替换它。如果十分钟内只到达一个测量值，它将在数据库中被记录十次。

## rrdpath

此指定了 RRD 数据库的目录。该目录必须对 `nagios` 用户可写，并且（与数据库文件一起）对 Web 服务器用户可读。该目录在安装 NagiosGrapher 时自动创建。

## tmppath

此定义了 NagiosGrapher 临时保存内部 XML 文件的位置。

## fontfile

此指定了 RRDTools 用于图表标记的字体文件。

## serviceext_type

此描述了 `serviceinfo` 对象是如何创建的。使用 `SINGLE` 类型，NagiosGrapher 将所有内容写入 `serviceextinfo` 指定的文件。

Nagios 2.0 还可以递归读取目录，在这种情况下，使用 `MULTIPLE` 类型更好。此时 NagiosGrapher 会为每个主机创建一个带有相应 `serviceextinfo` 对象的独立文件。目录由 `serviceext_path` 参数指定。这必须通过 `cfg_dir` 指令让 Nagios 知晓。

```cfg
url
```

这包含了从 Web 服务器视角看 CGI 脚本 `graphs.cgi` 的路径（从服务器根目录开始的路径）或浏览器视角（即完整的 URL）。

```cfg
notes_url
```

NagiosGrapher 会自动生成 `serviceextinfo` 对象；同样能够设置 `notes_url` 参数（16.4.2，第 366 页扩展服务信息）也是很有用的，例如生成指向 Wiki 条目的服务相关链接。

```cfg
nagios_config
```

此向 NagiosGrapher 示了 Nagios 标准配置文件的位置。

```cfg
cgi_config
```

此指定了 Nagios CGI 配置文件。NagiosGrapher 使用此来查找除了联系组外，还有谁有权查询所有主机的信息。

```cfg
icon_image_tag
```
