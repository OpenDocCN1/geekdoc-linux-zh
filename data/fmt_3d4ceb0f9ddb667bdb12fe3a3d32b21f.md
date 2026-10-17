
```
# reject ainsley
# lpadmin -p ainsley -M -f bank
# lpadmin -p ainsley -f financial
# accept ainsley
```

打印过滤器扩展了 UNIX 器的概念，因为打印请求的输出通过过滤器管道产生原始文本的修改版本。通常在输入和输出之间会发生某种转置或解释。常用的过滤器包括将 diff、dmd、plot 和 tek 过滤器转换为 PostScript 的过滤器。可以使用 `lpfilter` 命令向系统添加新过滤器。例如，如果你开发了一个准备“fract”格式文档的新图像处理系统，可以使用以下命令安装一个新的将这些文件转换为 PostScript 的过滤器：

```
# lpfilter -f fract -P /etc/lp/fd/fract.fd
```

当不再需要该过滤器时，可以使用命令删除它：

```
# lpfilter -f fract -x
```

### 命令参考

以下命令可用于 Solaris 打印。

# Solaris 打印管理器

Solaris 打印管理器通过显示本地系统已知的所有打印机列表及其，提供了更复杂的当前打印设置视图。

## 第 18 章：打印机管理 385

配置设置。（有一个等效的 GNOME 打印管理器。）你可以为打印机管理器选择显示选项，以便根据本地站点偏好自定义视图。例如，图 18-1 显示了拥有三台可用打印机的网络默认视图：yasimov、наryov 和 prova。每个打印机图标旁边都会出现 [Empty]（空）项，因为目前没有任何打印机正在处理作业。点击相应图标旁边的减号 (-) 符号，可以缩小每台打印机的打印作业详情。

你可以打开系统上定义的每台打印机的“属性”窗口。对于打印机 yasimov，当前属性如图 18-2 所示。在“属性”窗口中列出了几个关键特征：

- *图标标签，通常是打印机的名称 (yasimov)*
- 打印机设置的要使用的图标集
- 打印机描述
- 打印队列名称
- 打印队列状态
- 打印机设备名称
- 打印机设备状态

![](img/11bcccd1804574cca0c3018732958dd5_414_0.png)

图 18-1 查看已配置的打印机

图 18-2

查看打印机 yasimov 的属性

![](img/11bcccd1804574cca0c3018732958dd5_415_0.png)

可以通过选择“查看 | 设置选项”（View | Set Options）进一步修改打印管理器中打印机集的显示，如图 18-3 所示。

- 使用大图标还是小图标表示打印机，以及仅显示每台打印机的名称还是显示完整详情
- 是否显示打印机上的所有作业，或仅显示当前用户的作业
- 遇到错误时是否显示各种标记
- 如何更新系统上打印机的显示

## `lp`

`lp`（行打印机）命令是 `admintool` 和 Solaris Print Manager 接口的基础，Solaris 管理员可能会遇到它们。它们通常用于添加和删除远程打印机项，并执行许多其他管理任务。

配置打印机后，提交作业非常简单，如下例所示。要向本地服务器上的打印机 hpi 提交 Postscript 文件，请使用命令

```
$ lp -d hpi file.ps
```

作业进入池化后，打印机将正确解释文件中嵌入的 Postscript 命令。如果你的打印机不支持 Postscript，你将打印出嵌入的 Postscript 代码而非渲染后的文档。`-d` 标志用于指定打印机名称 (hp1)。如果没有指定打印机，作业将发送到默认打印机。

图 18-3

设置打印管理器选项

![](img/11bcccd1804574cca0c3018732958dd5_416_0.png)

可以使用类似的命令将文本文件暂存（spool）到同一台打印机：

```
$ lp file.txt
```

可以向 `lp` 传递大量选项以实现各种目的。例如，与其执行 50 次 `lp` 命令来打印 50 份报告，你可以使用以下命令：

```
$ lp -n 50 report.txt
```

或者，如果你正在打印一个大型作业，可以使用 `-m` 选项指定在作业打印完成后通过电子邮件通知你：

```
$ lp -m bigjob.ps
```

作为 `lp` 的替代方案，你可以使用 POSIX 风格打印来提交作业。这涉及同时指定打印服务器和打印机名称，而不仅仅是打印机。这确保了连接到不同主机的同名打印机之间不存在冲突。例如，服务器管理员可能有一台名为 hp1 的打印机，你也可以在命令行上通过 `lp` 传递 `-d hp1`，但此时哪台打印机会被选中用于你的作业？为了确保使用正确的打印机，你需要在命令行上同时指定服务器和打印机。

对于主机管理员，这里再次给出 PostScript 示例，这次使用符合 POSIX 标准的格式：

```
$ lp -P admin:hp1 file.ps
```

如果你想打印到连接在服务器 finance 上的 hp1 服务器上，你可以改用以下命令：

```
$ lpr -P finance:hpl file.ps
```

## `cancel`

可以使用 `cancel` 命令并将作业 ID 传递给命令来轻松取消打印作业。例如，要取消作业 hp1-212，你需要使用以下命令：

```
# cancel hp1-212
```

## `lpadmin`

`lpadmin` 是一种打印管理实用，用于添加和配置打印机。添加打印机或修改其特征通常通过多个 `lpadmin` 命令完成。

要设置打印机名称和端口，使用以下命令：

```
# lpadmin -p hp2 -v /dev/null
```

此命令将打印机 `hp2` 的端口设置为 `/dev/null`。

要指定要使用的打印机软件，使用以下命令：

```
# lpadmin -p hp2 -v /dev/null
```

# 392 第四部分：设备管理

此示例通过普通的进程列表显示了用户 `pwaters` 当前运行的 Korn shell (`ksh`)：

```
# ps -eaf | grep pwaters
pwaters 3190 291 0 Mar 20 ? 0:04 /usr/open/bin/Xsun
pwaters 11959 11934 0 09:21:42 pts/1 0:00 grep pwaters
pwaters 11934 11932 1 09:20:50 pts/1 0:00 ksh
```

现在你已经获取了目标 PID (`11934`)，你可以切换到 `/proc/11934` 目录并查看该进程的映像文件：

```
# cd /proc/11934
# ls -1
total 3497
--rw- 1 pwaters other 1769472 Mar 30 09:20 as
-r-- 1 pwaters other 152 Mar 30 09:20 auxv
-r-- 1 pwaters other 32 Mar 30 09:20 cred
-w-- 1 pwaters other 0 Mar 30 09:20 ctl ->
lr-x- 1 pwaters other 0 Mar 30 09:20 cwd ->
d-xr- 2 pwaters other 1184 Mar 30 09:20 fd
-r--r- 1 pwaters other 120 Mar 30 09:20 lpsinfo
-r-- 1 pwaters other 912 Mar 30 09:20 lusage
-r--r- 1 pwaters other 536 Mar 30 09:20 status
d-xr-Xr-X 3 pwaters other 48 Mar 30 09:20 lwp
-r-- 1 pwaters other 2016 Mar 30 09:20 map
d-x- 2 pwaters other 544 Mar 30 09:20 object
-r-- 1 pwaters other 2552 Mar 30 09:20 pagedata
-r--r- 1 pwaters other 336 Mar 30 09:20 psinfo
-r-- 1 pwaters other 2016 Mar 30 09:20 rmap
lr-x- 1 pwaters other 0 Mar 30 09:20 root ->
-r-- 1 pwaters other 1440 Mar 30 09:20 sigact
-r-- 1 pwaters other 1232 Mar 30 09:20 status
-r--r- 1 pwaters other 256 Mar 30 09:20 usage
-r-- 1 pwaters other 0 Mar 30 09:20 watch
-r-- 1 pwaters other 3192 Mar 30 09:20 xmap
```

每个以 PID 命名的目录都包含额外的子目录，这些子目录包含了状态信息和相关控制。例如，包括：

- 进程标志 (Process flags)
