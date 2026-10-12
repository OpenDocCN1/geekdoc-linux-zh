
#### 注意

将打印任务从打印队列发送到打印机的过程通常被称为**打印**。

图 11-1 展示了一个名为 `printer1` 的打印机的这一过程示例。

![](img/09bf13b782f71165e17bb3839040c96a_428_1.png)

### 图 11-1 打印过程

要查看系统中所有打印机及其状态的列表，可以使用 `lpstat` 命令的 `-t` (total) 选项，如下所示输出：

```bash
[root@server1 root]# lpstat -t
scheduler is running
system default destination: printer1
device for p1: parallel:/dev/lp0
p1 accepting requests since Jan 01 00:00
printer p1 is idle. enabled since Jan 01 00:00
[root@server1 root]# 
```

上述输出表明，系统中只有一个名为 `printer1` 的打印机，它向连接在计算机第一个并口（`//dev/lp0`）上的打印机进行打印，并且其打印队列中没有打印任务。此外，`cups` 守护程序（`scheduler`）正在运行，并正在接受传入此打印机打印队列的任务。另外，由于打印机已启用，`cups` 守护程序会将打印任务从打印队列发送到打印机。

# 第 11 章 常见管理任务

您可以使用 `accept`、`reject`、`enable` 或 `disable` 命令后跟打印机名称来操作打印机的状态。因此，要为打印机 `printer1` 启用假脱机并禁用打印，可以使用以下命令：

```bash
[root@server1 root]# accept printer1
[root@server1 root]# disable printer1
[root@server1 root]# lpstat -t
scheduler is running
system default destination: printer1
device for printer1: parallel:/dev/lp0
printer1 accepting requests since Jan 01 00:00
printer printer1 disabled since Jan 01 00:00 - Paused
[root@server1 root]# 
```

现在发送到打印机 `printer1` 的任何打印任务都会被发送到打印队列，但会保留在打印队列中，直到打印机再次启动。

> **注意**
>
> 如果您想启用打印机，必须指定 `enable` 命令的完整路径（`/usr/bin/enable`），因为还有一个名为 `enable` 的 `BASH` shell 函数。

您还可以使用 `disable` 和 `reject` 命令的 `-r` 选项来指定操作的原因，如下所示输出：

```bash
[root@server1 root]# disable -r "Changing toner cartridge" printer1
[root@server1 root]# lpstat -t
scheduler is running
system default destination: printer1
device for printer1: parallel:/dev/lp0
printer1 accepting requests since Jan 01 00:00
printer printer1 disabled since Jan 01 00:00 - Changing toner cartridge
[root@server1 root]# 
```

### 管理打印任务

回顾一下，您使用 `lp` 命令创建打印任务。要将 `/etc/inittab` 文件打印到前面示例中显示的打印机 `printer1` 的一份副本，可以使用以下命令，该命令将返回一个打印任务 ID，您可以稍后使用它来操作该打印任务：

```bash
[root@server1 root]# lp -d printer1 /etc/inittab
request id is printer1-1 (1 file(s))
[root@server1 root]# 
```

### 打印机管理

`lp` 命令使用 `-d` 选项来指定目标打印机名称。如果省略此选项，`lp` 命令将假设使用系统上的默认打印机。由于 `printer1` 是系统中唯一的打印机，因此也是默认打印机，所以命令 `lp /etc/inittab` 等价于前面输出中使用的命令。

![](img/09bf13b782f71165e17bb3839040c96a_430_0.png)

### 注意

> 您可以使用 `lpoptions -d printername` 命令来设置系统中所有用户的默认打印机，其中 `printername` 是默认打印机的名称。此信息存储在 `/etc/cups/lpoptions` 文件中。

> Linux 系统中的每个用户都可以通过在其主目录中的 `.lpoptions` 文件中添加行 `default printername` 来指定自己的默认打印机，其中 `printername` 是默认打印机的名称。或者，您可以使用 `PRINTER` 或 `LPDEST` 变量来设置默认打印机。例如，要将 `printer2` 指定为默认打印机，您可以将行 `export PRINTER=printer2` 或行 `export LPDEST=printer2` 添加到主目录中的环境文件（如 `.bash_profile`）中。

表 11-1 列出了 `lp` 命令的一些常用选项。

**表 11-1 lp 命令的常用选项**

| 选项 | 描述 |
|---|---|
| `-d` `printername` | 指定接收打印任务的打印机名称。 |
| `-i` `print job ID` | 指定要修改的某个打印任务 ID。 |
| `-n` `number` | 打印 `number` 份副本。 |
| `-m` | 通过电子邮件发送打印任务完成的确认信息。 |
| `-o` `option` | 指定某些打印选项。常见的打印选项包括以下项：<br>`cpi = number`—将每英寸字符数设置为 `number`<br>`landscape`—以横向方向打印<br>`number-up = number`—在单页上打印 `number` 页，其中 `number` 为 1、2 或 4<br>`sides = string`—设置双面打印，其中 `string` 为 ‘two-sided-short-edge’ 或 ‘two-sided-long-edge’ |
| `-q` `priority` | 指定打印任务优先级，从 1（低优先级）到 100（高优先级）。默认情况下，所有打印任务的优先级为 50。 |

您可以通过将文件作为参数来指定多个要打印的文件，使用单个 `lp` 命令。在这种情况下，只为所有文件创建一个打印任务。要将文件 `/etc/hosts` 和 `/etc/issue` 打印到打印机 `printer1`，可以执行以下命令：

```bash
[root@server1 root]# lp -d printer1 /etc/hosts /etc/issue
request id is printer1-2 (2 file(s))
[root@server1 root]# 
```

`lp` 命令接受来自标准输入的信息；因此，您可以将 `lp` 命令放在管道末尾以打印信息。要打印已登录用户的列表，可以使用以下管道：

```bash
[root@server1 root]# who | lp -d printer1
request id is printer1-3 (1 file(s))
[root@server1 root]# 
```

要查看 `printer1` 队列中打印任务的列表，可以使用 `lpstat` 命令。在没有参数的情况下，此命令显示您在打印队列中已打印的所有任务：

```bash
[root@server1 root]# lpstat
printer1-1        root            2048  Fri 29 Jul 2005 06:18:22 PM EDT
printer1-2        root            3072  Fri 29 Jul 2005 07:05:49 PM EDT
printer1-3        root            1024  Fri 29 Jul 2005 07:06:50 PM EDT
[root@server1 root]# 
```

表 11-2 列出了您可以与 `lpstat` 命令一起使用的其他选项。

**表 11-2 lpstat 命令的常用选项**

| 选项 | 描述 |
| :--- | :--- |
| `-a` | 显示正在接受打印任务的打印机列表 |
| `-d` | 显示默认目标打印机 |
