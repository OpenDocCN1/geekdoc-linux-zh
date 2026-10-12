

您可以在 www.linuxprinting.org 找到一个支持 Linux 的打印机出色列表。我强烈建议您在购买与 Linux 配合使用的打印机之前访问该网站。除了显示受支持的打印机外，该网站还有一个页面介绍如何为 Linux 选择打印机（www.linuxprinting.org/suggested.html）。

## 在 Red Hat Linux 中管理文档打印

在 Red Hat Linux 中，大多数打印都可以通过 `lpr` 命令完成。诸如 StarOffice 和 AbiWord 等文字处理应用程序已设置使用此功能进行打印。

使用 Red Hat 的 `printconf-gui` 命令，您可以为每台打印机定义所需的过滤器，以便正确格式化文本。`lpr` 命令的选项可以添加过滤器以正确处理文本。用于管理打印文档的其他命令包括 `lpq`（用于查看打印队列内容）、`lprm`（用于从队列中移除打印任务）和 `lpc`（用于控制打印机）。

也有命令可将打印任务定向到远程打印机（例如 NetWare 或 SMB 打印服务器上的打印机）。正如前文所述，使用 `smbclient` 命令打印到远程 SMB 打印机。同样，对于 NetWare 打印，可以使用 `nprint` 命令。`lpr` 命令分别依赖这些命令打印到 SMB 和 NetWare。但是，如果您希望选择不同的打印选项，可以直接使用 `smbclient` 或 `nprint`。

> **交叉引用：** 第 6 章包含如何以多种不同格式（包括 `troff` 和 `TeX`）格式化和打印文档的示例。

## 使用 lpr 进行打印

使用 `lpr` 命令，您可以将文档打印到本地和远程打印机。文档文件可以添加到 `lpr` 命令行的末尾，或者使用管道（`|`）定向到 `lpr` 命令。以下是一个简单的 `lpr` 命令示例：

```
$ lpr doc1.ps
```

仅使用 `lpr` 指定文档文件时，输出将定向到默认打印机。作为个人用户，您可以通过设置 `PRINTER` 变量的值来更改默认打印机。通常，您将 `PRINTER` 变量添加到其中一个启动文件中，例如 `$HOME/.bashrc`。以下是您可以添加到 `.bashrc` 文件中的行，用于将默认打印机设置为 `lp3`：

```
export PRINTER=lp3
```

要覆盖默认打印机，请在 `lpr` 命令行中指定特定打印机。以下示例使用 `-P` 选项选择其他打印机：

```
$ lpr -P canyons doc1.ps
```

`lpr` 命令具有多种选项，使 `lpr` 能够解释和格式化几种不同类型的文档。以下是您可以用于命令行以及这些选项可处理的文本类型：

- **`-c`** — 处理 ciplot 数据。
- **`-d`** 处理 DVI 格式的 TeX 数据。
- **`-f`** — 将每行的第一个字符解释为标准 FORTRAN 回车控制字符。
- **`-g`** — 处理绘图数据。
- **`-l`** — 处理内容以便控制字符可以打印并且抑制分页。
- **`-n`** — 处理 ditroff（设备无关 troff）格式的数据。
- **`-t`** — 处理由 troff 命令产生的数据。
- **`-v`** — 处理针对 Benson Varian 等设备的栅格图像。

以下 `lpr` 选项可用于处理打印任务本身：

- **`-m`** — 作业打印完成后发送邮件。
- **`-r`** — 文件暂存后删除该文件。
- **`-s`** — 使用符号链接获取要打印的文件，而不是将文件复制到暂存目录。这防止非常大的打印任务占用打印队列中的空间。但是，如果您这样做，必须确保在打印完成后不要删除原始文件。
- **`-#n`** — 将 `n` 替换为代表要打印副本数的数字。

可以为每个文档打印一张突发页（burst page），以识别其内容和所有者。以下是您可以使用的一些与突发页相关的选项：

- **`-h`** — 抑制突发页的输出。
- **`-C class`** — 标识要在突发页上使用的作业分类。将 `class` 替换为显示在该页面上的单词或短语。此值替代通常在此处打印的主机名。
- **`-J job`** — 标识要显示在突发页上的作业名称。`job` 的值替代突发页上第一个打印文件的名称。
- **`-P printer`** — 标识打印任务将发送到的打印机。如果没有 `-P` 选项，则使用默认打印机。
- **`-U user`** — 标识要显示在突发页上的用户名。

## 使用 lprm 移除打印任务

用户可以使用 `lprm` 命令从队列中移除自己的打印任务。在命令行中单独使用 `lprm` 时，它将从默认打印机中移除该用户的所有打印任务。要从特定打印机中移除任务，请使用 `-P` 选项，如下所示：

```
$ lprm -P lp0
```

要移除当前用户的所有打印任务，请输入以下内容：

```
$ lprm -
```

root 用户可以通过在 `lprm` 命令行中指定该用户来移除特定用户的所有打印任务。例如，要移除名为 mike 的用户的所有打印任务，root 用户将输入以下内容：

```
$ lprm mike
```

要从队列中移除单个打印任务，请在 `lprm` 命令行中指定该打印任务的作业编号。要首先了解作业编号，请输入 `lpc` 命令。该命令的输出可能如下所示：

```
$ lpc

Printer: lp@localhost
Queue: 2 printable jobs
Server: pid 4134 active
Unspooler: pid 4135 active
Status: waiting for subprocess to exit at 18:54:05.230

Rank  Owner/ID       Class Job Files            Size Time
active root@localhost+133  A    133 /home/jake/pr1   467 18:53:49
2     root@localhost+197  A    197 /home/jake/mydoc 23948 18:54:05
```

输出显示队列中有两个可打印任务等待中。（在这种情况下，由于打印机关闭，它们没有打印。）在 Job 列下，您可以看到与每个文档关联的作业编号。要移除第一个打印任务，请输入以下内容：

```
# lprm 133
```

## 使用 lpc 控制打印机

`lpc` 命令使您可以检查打印机状态、启用和禁用打印机，以及更改队列中任务的排列。您对 `lpc` 命令执行的任何操作都可以针对单个打印机（通过指定打印机名称）或所有打印机（通过使用单词 *all*）执行。要禁用特定打印机（例如名为 canyonps 的打印机），请使用 `disable` 选项并输入以下内容：

```
$ lpc disable canyonps
Printer: canyonps@localhost
kill server PID 4134 with User defined signal 1
canyonps@localhost.localdomain: disabled
```

要启用已禁用的打印机（如前面的例子中的打印机），请使用 **enable** 选项并输入以下内容：

```
$ lpc enable canyonpsps
Printer: canyonpsps@localhost
canyonpsps@localhost.localdomain: enabled
```

当打印机被禁用时，它仍然可以接收打印任务并将其保留在队列中，直到打印机再次启用。如果您希望完全防止任务暂存，请使用 **stop** 选项，如下所示：

```
$ lpc stop canyonpsps
Printer: canyonpsps@localhost
canyonpsps@localhost.localdomain: stopped
```

要再次启动打印守护程序并恢复打印，请使用 **start** 选项，如下所示：

```
$ lpc start canyonpsps
Printer: canyonpsps@localhost
canyonpsps@localhost.localdomain: started
```

要禁用打印机并终止 lpd 守护程序（以便无法再打印任何任务），请使用 **abort** 选项，如下所示：

```
$ lpc abort canyonpsps
Printer: canyonpsps@localhost
kill server PID 4239 with Interrupt
canyonpsps@localhost.localdomain: aborted_job
```

## 配置打印服务器

连接到您的 Red Hat Linux 系统的打印机可以以不同方式与网络上的其他计算机共享。您的计算机不仅可以作为 Linux 打印服务器，还可以向其他客户端计算机表现为 NetWare 或 SMB 打印服务器。在本地打印机连接到您的 Red Hat Linux 系统并且您的计算机连接到本地网络后，您可以使用本节中的步骤通过 Linux (UNIX)、NetWare 或 SMB 接口将其共享给客户端计算机。

### 在 lpd.perms 中配置共享 Linux 打印机

将本地打印机添加到您的 Red Hat Linux 计算机后，使其可供网络上的其他计算机使用相当简单。如果在共享打印机的计算机之间存在 TCP/IP 网络连接，那么您只需授予来自远程主机的个别主机或用户访问您计算机打印服务的权限。本地打印机的设置过程在本章前面已讨论过。

来自其他计算机的用户对您 Red Hat Linux 打印机的权限是根据您 `/etc/lpd.perms` 文件中的值确定的。默认情况下，您应该

