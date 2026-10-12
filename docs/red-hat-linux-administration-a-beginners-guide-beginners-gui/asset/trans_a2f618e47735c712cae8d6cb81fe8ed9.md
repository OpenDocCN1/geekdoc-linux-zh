
## 19.1 了解 lpd 基础知识

**lpd** 使用的模型实际上类似于电子邮件处理流程：守护进程静静地监听通过网络到来的打印请求。这意味着守护进程将来自其他主机的打印请求视为与来自该守护进程所在主机的请求完全相同，从而使配置文件的管理更加简单。

对于每个到达的打印作业，文件首先被放入暂存目录（spool directory）。通常，该目录是 `/var/spool/lpd/printername`，其中 *printername* 是作业将要发送的打印机名称。一旦暂存完成，**lpd** 便会将请求的打印作业独立地发送到打印机，而不依赖于发送方。这使得发送方可以恢复操作，而不必让用户盯着沙漏图标看。

以下是 **lpd** 将打印作业发送到打印机的步骤：

- 1. 在 `/etc/printcap` 中查找打印机配置信息。
- 2. 如果打印机要求作业通过打印过滤器，则将文件通过该过滤器发送。
- 3. 如果打印机物理上连接到服务器，则直接将经过过滤的打印请求发送到打印设备。
- 4. 如果打印机是远程的（通过网络访问），则联系相应的 **lpd** 服务器，并将经过过滤的作业发送到该服务器。

## 19.2 安装 LPRng

当你启动 **redhat-config-packages** 时，你会在列表底部找到一个标记为“Printing Support”的条目。点击右侧的“Details”将弹出一个对话框，列出你可以安装的与打印相关的软件包。此时，我们要关注的是 **LPRng** 系统和 **hpjs** 打印机驱动程序。底层安装的 RPM 包也分别名为 LPRng 和 **hpjs**。

下表总结了随 LPRng 系统安装的一些程序和配置文件，我们将在后续章节中详细讨论这些内容。

| 程序 | 用途 |
|---|---|
| `/usr/sbin/lpd` | 打印服务器守护进程 |
| `/usr/bin/lpr` | 用于提交打印作业 |
| `/usr/bin/lpq` | 检查打印队列的状态 |
| `/usr/bin/lprm` | 移除队列中的打印作业 |
| `/usr/sbin/lpc` | 控制打印服务器守护进程 |
| `/usr/bin/lpstat` | 显示打印机的状态 |
| `/etc/printcap` | 列出系统中的打印机 |
| `/etc/lpd.conf` | 包含客户端和服务器均使用的 LPRng 配置选项 |
| `/etc/lpd.perms` | 包含 `lpd` 服务器用于控制用户操作的权限信息 |
| `/usr/sbin/checkpc` | 检查打印系统的配置 |

### 启动时运行 LPRng

如果你使用图形界面工具 `redhat-config-services` 来更改 LPRng 的启动或停止运行级别，你需要查找的条目是 **lpd**。另一方面，如果你打算手动操作符号链接，你可能需要考虑使用 **S60lpd** 和 **K60lpd**，以保持与图形界面工具的同步。

```bash
[root@scribe rc3.d]# rm K60lpd
[root@scribe rc3.d]# ln -s ../init.d/lpd S60lpd
```

## 19.3 配置 /etc/printcap

`/etc/printcap` 文件告知 LPRng 服务器守护进程（**lpd**）所有打印机的名称和特性。每个打印机都有一个类似以下的条目：

```text
printername1|printername2|printername3:
    :command=value:
    :command:
    :command=value:
```

其中 *printername1* 是打印机的名称，而 *printername2* 和 *printername3* 是 *printername1* 的别名。每个 *command* 后面可能跟着一个值。

在我们看到最终的 **printcap** 文件是什么样子之前，请查看表 19-1，该表详细介绍了打印机配置中每个参数的含义。注意这是一个简化列表。你可以在 `/usr/share/doc/LPRng-3.8.9/LPRng-HOWTO.html` 处的 LPRng-HOWTO 指南中阅读完整的配置选项。

### 表 19-1 打印机配置参数

| 命令 | 用途/值 |
|---|---|
| sd | 暂存目录路径名。这是 `lpr` 服务器将正在发送到打印机的文件放置的位置。由于可能在打印另一个文件的同时收到新文件，因此 `lpr` 会将这些新文件暂存到这个指定目录中。通常，该目录是 `/var/spool/lpd/printname`，其中 `printname` 是打印机的名称（例如，`sd=/var/spool/lpd/plato`）。随着文件被打印，`lpr` 会自动删除它们。如果你预期某台打印机的印量很大，你需要确保该目录有足够的空间来容纳所有排队等待的文档。 |
| sh | 抑制标题页/横幅页。标题页显示谁打印了该文档以及文档的名称。这一功能背后的想法是让到达高印量打印机的作业能够由先到达打印机的人轻松分类。大多数站点认为标题页不值得浪费纸张，并倾向于关闭此功能。 |
| rm | 指定远程机器。由于 `lpr` 可以将打印作业重定向到其他打印服务器，因此必须能够指定远程打印服务器的名称。此命令允许你这样做。这通常与 `rp` 命令配合使用。 |
| rp | 指定远程打印队列。将打印作业重定向到远程打印服务器时，你还需要指定要提交作业的远程打印队列的名称。通常这是因为专用打印服务器控制多台打印机。此命令允许你指定打印队列的名称。（注意：如果你正在向支持网络的打印机（如带有 JetDirect 的 HP LaserJet）打印，则不需要指定远程打印队列。） |
| mx | 指定以 `K` 块为单位的最大作业大小。`0` 表示无大小限制。 |
| lp | 指定本地输出设备（例如，`/dev/lp0`）。如果你的打印机是本地连接的，你需要指定可以访问它的设备名称。大多数带有并口的打印机都可以通过 `/dev/lp0` 设备访问。你最好希望为此参数指定一个过滤器。 |
| filter | 指定在将数据发送到本地输出设备之前要通过的过滤器。你可以将过滤器视为 Windows 下打印机驱动程序的逻辑等价物。UNIX 系统（包括 Linux）有着直接处理 PostScript 的悠久历史，并且由于大多数原始排版系统都是由 UNIX 系统驱动的，PostScript 成为了事实上的标准。（开发 UNIX 的“官方”原因是贝尔实验室的专利部门想要制造一台排版机。更多细节，请参见 Peter H. Salus 著的 *A Quarter Century of UNIX* 一书的第 6 章 [Addison-Wesley, 1994]。）如果你的打印机已经能理解 PostScript，那么你大概可以保持此设置不变。另一方面，如果你的打印机不能理解 PostScript，你需要一个将 PostScript 转换为你的打印机格式的过滤器。 |

### /etc/printcap 文件示例

例如，在下面的 **/etc/printcap** 文件中，打印机的名称是 **plato**，其别名是 **lp**：

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

在这种情况下，有两台打印机：一台名为 **orwell**，另一台名为 **poe**。

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

- 一台名为 **huxley** 的 PostScript 打印机，连接到名为 **printserve** 的打印服务器：
    ```text
    huxley|ps|p:
        :sd=/var/spool/lpd/huxley:
        :mx#0:
    ```

