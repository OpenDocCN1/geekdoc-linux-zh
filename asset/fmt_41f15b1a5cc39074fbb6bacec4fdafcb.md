
其中 `printername1` 是打印机的名称，而 `printername2` 和 `printername3` 是 `printername1` 的别名。每个 `command` 后面可能跟着一个值。

在我们看到最终的 `printcap` 文件是什么样子之前，请查看表 19-1，该表详细介绍了打印机配置中每个参数的含义。注意这是一个简化列表。你可以在 `/usr/share/doc/LPRng-3.8.9/LPRng-HOWTO.html` 处的 LPRng-HOWTO 指南中阅读完整的配置选项。

### 表 19-1 打印机配置参数

| 命令 | 用途/值 |
|---|---|

| `sd` | 暂存目录路径名。这是 `lpr` 服务器将正在发送到打印机的文件放置的位置。由于可能在打印另一个文件的同时收到新文件，因此 `lpr` 会将这些新文件暂存到这个指定目录中。通常，该目录是 `/var/spool/lpd/printname`，其中 `printname` 是打印机的名称（例如，`sd=/var/spool/lpd/plato`）。随着文件被打印，`lpr` 会自动删除它们。如果你预期某台打印机的印量很大，你需要确保该目录有足够的空间来容纳所有排队等待的文档。 |
| `sh` | 抑制标题页/横幅页。标题页显示谁打印了该文档以及文档的名称。这一功能背后的想法是让到达高印量打印机的作业能够由先到达打印机的人轻松分类。大多数站点认为标题页不值得浪费纸张，并倾向于关闭此功能。 |
| `rm` | 指定远程机器。由于 `lpr` 可以将打印作业重定向到其他打印服务器，因此必须能够指定远程打印服务器的名称。此命令允许你这样做。这通常与 `rp` 命令配合使用。 |
| `rp` | 指定远程打印队列。将打印作业重定向到远程打印服务器时，你还需要指定要提交作业的远程打印队列的名称。通常这是因为专用打印服务器控制多台打印机。此命令允许你指定打印队列的名称。（注意：如果你正在向支持网络的打印机（如带有 JetDirect 的 HP LaserJet）打印，则不需要指定远程打印队列。） |
| `mx` | 指定以 `K` 块为单位的最大作业大小。`0` 表示无大小限制。 |
| `lp` | 指定本地输出设备（例如，`/dev/lp0`）。如果你的打印机是本地连接的，你需要指定可以访问它的设备名称。大多数带有并口的打印机都可以通过 `/dev/lp0` 设备访问。你最好希望为此参数指定一个过滤器。 |
| `filter` | 指定在将数据发送到本地输出设备之前要通过的过滤器。你可以将过滤器视为 Windows 下打印机驱动程序的逻辑等价物。UNIX 系统（包括 Linux）有着直接处理 PostScript 的悠久历史，并且由于大多数原始排版系统都是由 UNIX 系统驱动的，PostScript 成为了事实上的标准。（开发 UNIX 的“官方”原因是贝尔实验室的专利部门想要制造一台排版机。更多细节，请参见 Peter H. Salus 著的 *A Quarter Century of UNIX* 一书的第 6 章 [Addison-Wesley, 1994]。）如果你的打印机已经能理解 PostScript，那么你大概可以保持此设置不变。另一方面，如果你的打印机不能理解 PostScript，你需要一个将 PostScript 转换为你的打印机格式的过滤器。 |

### /etc/printcap 文件示例

例如，在下面的 `/etc/printcap` 文件中，打印机的名称是 `plato`，其别名是 `lp`：

```text
plato|lp:
    :sd=/var/spool/lpd/plato:
    :sh:
    :rm=bookworm:
    :rp=plato:
```

你可以在该文件中列出多台打印机，如下所示：

```text
orwell|lp:
    :sd=/var/spool/lpd/orwell:
    :sh:
    :rm=bookworm:
    :rp=laserprint:
poe|lp2:
    :sd=/var/spool/lpd/poe:
    :sh:
    :rm=bookworm:
    :rp=colorprint:
```

在这种情况下，有两台打印机：一台名为 `orwell`，另一台名为 `poe`。

以下是一些经过测试并证明可用的示例配置文件。你会发现，基于每台打印机的配置文件实际上非常简单明了。

- 一台直接连接到你的网络且支持 PostScript 的 HP LaserJet：

```text
orwell|lp:
    :sd=/var/spool/lpd/orwell:
    :mx#0:
    :rm=hplj:
```

- 一台直接连接到并行端口的 HP DeskJet 550C：

```text
carroll|lp:
    :sd=/var/spool/lpd/carroll:
    :mx#0:
    :lp=/dev/lp0:
    :ifhp:model=ghostscript,gx_device=cdj550:
    :filter=/usr/libexec/filters/ifhp:
```

- 一台名为 `huxley` 的 PostScript 打印机，连接到名为 `printserve` 的打印服务器：

```text
huxley|ps|p:
    :sd=/var/spool/lpd/huxley:
    :mx#0:
```

::rm=printserve:  

::rp=pslp:

## 实施您的更改

在您跑去修改 `/etc/printcap` 之前，还有一点需要注意。与许多版本的 UNIX 不同，Red Hat 上的 `/etc/printcap` 文件实际上是许多来源的综合体。某些事件，例如使用下一节中描述的 GUI 工具，会导致 `/etc/printcap` 文件被重新生成；您手动进行的更改有丢失的风险。如果您想安全地进行更改，需要实际将它们放入 `/etc/printcap.local` 中。当后者重新生成时，此文件将原样合并到 `/etc/printcap` 中。一旦您更新了 `/etc/printcap.local` 文件，您需要重启 `lpd` 才能使更改生效。

```
[root@scribe /root]# /etc/init.d/lpd restart
```

## 项目 19-1 图形化打印机配置

如果您不想尝试手动设置所有内容，还有一个图形化工具可以帮助您完成所有设置。在 GUI 工具中设置打印机既会创建队列并修改 `/etc/printcap`，还会在完成后提供重启 `lpd` 并向打印机发送测试页的选项。

您已在 `/etc/printcap.local` 中设置好的打印机不会显示在图形化工具中，但可以与您在此处配置的打印机一起工作。然而，系统不会尝试将您通过图形界面配置的打印机与您手动设置的打印机进行协调，因此您的图形配置很容易覆盖手动编辑的更改。出于这个原因，强烈建议您使用手动配置或图形化设置之一，但不要同时使用两者。在有多位管理员的环境中尤其如此。

## 分步操作

- 1. 您可以通过从系统设置菜单中选择 Printing，或在命令行中输入 `redhat-config-printer` 来调出打印机 GUI 工具。

![](img/ec2066d370d3af1a767664d36aa7ddfe_550_0.png)

- 2. 在按钮栏上选择 New 以创建新的打印队列。
- 3. 点击 Forward 继续到队列类型选择对话框。
- 4. 为您的打印队列输入名称。
- 5. 根据打印机是本地连接还是被发送到远程打印服务器来选择队列类型。如果被发送到远程打印服务器，请选择远程机器运行的打印服务器类型。
- 6. 如果这是本地打印机，请选择本地打印机使用的设备。对于并行打印机，这通常是 `/dev/lpd`。或者，如果此队列指向远程服务器，您将在此时输入服务器信息。
- 7. 如果您的打印机不直接支持 PostScript，请在 Driver 页面上选择适合您特定硬件的相应过滤器，然后点击 Forward 按钮。
- 8. 检查生成的设置，如果看起来正确，请点击 Apply。
- 9. 如果需要更改现有队列的值，请选择该队列并点击 Edit 以更改现有打印队列的属性。除了您输入的值外，还有一个 Driver Options 标签页，您可以在其中对您的设置进行一些微调：

![](img/ec2066d370d3af1a767664d36aa7ddfe_551_0.png)

- 10. 选择您希望作为默认的打印队列，然后点击工具栏上的 Default 按钮。打印机列表的第一列将显示默认打印机旁边的绿色对勾，该打印机是未通过名称指定打印队列的命令的默认设置。

## 项目总结
