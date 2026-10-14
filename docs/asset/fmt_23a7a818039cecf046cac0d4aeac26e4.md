
![](img/494a93e1dbdce90cc5cca36f1589d45f_330_0.png)

# 302 第三部分 + 系统管理

*pjl* *pjl*  
*printer job language* pjl  
*text* pcl

我将 `default_language` 设置为 `test`。如果 `ifhp` 无法确定文件类型，它会假设它是文本，并遵循为文本定义的规则。`forceconversion` 行指示了你希望是要使用 `ifhp` 文件类型检测程序还是 Linux `file` 工具。如果 `forceconversion` 以 `@` 字符开头，则使用 `ifhp` 程序。如果你选择使用 Linux `file` 工具，则必须定义 `file_util_path`。此行描述了该命令的用法。`-` 参数将 `STDIN` 传递给 `file` 工具。

`file_output_match` 块指示了对你预期看到的每个文件要执行哪些转换。块中的每行都标识一个文件类型的处理程序。每行有三个由空格分隔的条目。第一个条目是文件的正则表达式匹配。第二个条目标识转换类型。如果设置为 `unknown`，则文件不被打印。最后一列指示了调用哪个程序/脚本将文件转换为可打印格式。该程序/脚本必须是 postscript 条目，这是最有趣的。因为你必须能够从 `STDIN` 获取输入并能够输出到 `STDOUT`。我们使用 Ghostscript 将 postscript 文件转换为打印机设备 `cdj550`。你必须选择与你的打印机匹配的设备。`-sOutputFile` 参数表示输出被发送到 `STDOUT`。最后一个 `-` 表示输入从 `STDIN` 获取。

切换目录到 `/usr/share/ghostscript/5.50`。该目录下存在许多 postscript 文件。例如，查看 `lines.ps`。

```
> cd /usr/share/ghostscript/5.50

> ghostview lines.ps
```

`ghostview` 工具在你的屏幕上渲染 `lines.ps` postscript 文件。你应该看到类似于图 16-3 的内容。

Ghostscript 工具在你的电脑屏幕上显示的 postscript 输出与其在打印机上显示的几乎完全一样（不完全是）。当然，你的电脑屏幕和打印机之间存在差异——分辨率、宽高比等。然而，你应该能得到一个非常接近的近似。现在，让我们看看使用上述的 postscript 到打印机设备转换将其打印到打印机时会得到什么。

```
lpr-PHP2000C lines.ps
```

你应该看到与在 `ghostview` 中相同的行和方框。如果你看到带有 `%` 字符且看起来像编程语言的文本，你看到的是 postscript 文件的原始输出。你的输入文件没有将 postscript 文件识别为 postscript，因此将其作为文本文件传递。如果你使用的是 TurboLinux 自带的默认输入过滤器，这种情况不应该发生。

| File | State | Page | Portrait | 1.000 | Letter | lines | Fri Dec 17 02:46:28 |
|---|---|---|---|---|---|---|---|
| Variable | | | | | | | | | |
| Size | | | | | | | | | |
| Open | | | | | | | | | |
| Print All | | | | | | | | | |
| Print Marked | | | | | | | | | |
| Save All Marked | | | | | | | | | |
| << >> | | | | | | | | | |
| Redisplay | | | | | | | | | |

图 16-3：Ghostscript 在你的电脑屏幕上显示 postscript 输出。

## IFHP 和其他复杂输入过滤器的替代方案

`ifhp` 的一种替代方案涵盖了大多数打印情况，即简单地创建一个笨的输入过滤器来为你转换 postscript。由于大多数应用程序都以 postscript 格式打印，你可以创建一个简单的输入过滤器，接收 postscript 并将其转换为你的打印机可以打印的格式。

1. 切换目录到 `/usr/lib/filters`
2. 创建名为 `ps_input_filter.sh` 的脚本

```
#!/bin/sh

/usr/bin/gs -DEVICE=cdj550 -sAPERSIZE=letter -sOutputFile-- -q
```

此输入过滤器从标准输入 `-` 获取输入，并将其写入标准输出 `-sOutputFile--`。当你完成与你的打印机匹配的 Ghostscript 设备驱动 `cdj550` 后。创建脚本后，务必更改执行权限以便所有人都可以执行。

3. 将 `/etc/printcap` 中的 `ifhp` 输入过滤器条目替换为 `ps_input_filter.sh`
4. 尝试打印下面的 postscript 文件：

```
lpr -PHP2000C /usr/share/ghostscript/5.50/lines.ps
```

## 网络打印机配置

打印到位于网络上的打印机非常简单。你可以轻松打印到 UNIX 和 Windows 打印机。同样，你可以让你的打印机接受来自远程 Unix 和 Windows 计算机的打印请求。

## 到其他 UNIX/Linux 打印机

由于 LPRng 兼容 UNIX 打印系统，向 UNIX 网络上的打印机打印只需要指定远程主机和打印机的 printcap 条目。`rm` 选项和 `rp` printcap 选项分别定义了这些设置。下面的列表说明了一个 printcap 条目，它打印到连接到主机 `lemur.home.now` 的打印机，打印机名称/队列为 `1p`。

```
:sd=/var/spool/lpd/lp

:mx#0

:sh

:rm=lemur.home.now

:rp=lp

:if=/usr/lib/filters/ifhp
```

重启 LPD 并尝试使用之前示例中使用的相同 `lpr` 命令打印到远程打印机。

## 为其他 Unix Linux 机器提供打印服务

要告诉 LPD 你希望接受打印请求，请如文所示向 printcap 条目中添加 `server` 选项。

```
-- 打印服务器 printcap 条目

lp:server

:sd=/var/spool/lpd/lp

:mx#0

:sh

:lp=/dev/lp0

:ifhp-model=hpdj160c.status@

:ofhp-model=hpdj160c.status@

:if=/usr/lib/filters/ifhp

:of=/usr/lib/filters/ofhp
```

## 到 Windows 打印机

可以将打印作业发送到连接到 Windows 计算机的打印机。你可以使用 TurboPrintCfg 为你创建 printcap 和缓存目录。

# 第 16 章 + 打印机配置 305

从主菜单添加。从添加屏幕选择 SMB/LAN Manager Printer。输入你使用的打印队列名称。进入 SMB 设置。你必须指定 Netbios 主机名。这是计算机的 Windows 名称。你还必须确保打印机在 Windows 计算机上共享。指定打印机的共享名称。最后，如果 Windows 计算机需要，指定访问打印机的密码——否则将使用应用程序的用户名。以下是生成的 printcap 条目：

```
winlp

:sd=/var/spool/lpd/winlp

:mx#0

:sh

:if=/usr/bin/smbprint

:af=/var/spool/lpd/winlp/acct

:lp=/dev/null
```
