
### 手动更改将会丢失

此标头的存在意味着在运行`printtool`时，系统中并不存在`printcap`。

![](img/0a4925a63d7144788f84b23689a2d0da_430_0.png)

#### 第 3 部分：`##PRINTTOOL3##` 本地 POSTSCRIPT 600x600 letter

```
lp:
  :sd=/var/spool/lpd/lp:
  :mx#0:
  :sh:
  :lp=/dev/lp1:
  :if=/var/spool/lpd/lp/filter:
```

#### `##PRINTTOOL3##` 远程

```
lp0:
  :sd=/var/spool/lpd/lp0:
  :mx#0:
  :sh:
  :rm=wren:
  :rp=lj:
```

#### `##PRINTTOOL3##` SMB

```
lp1:
  :sd=/var/spool/lpd/lp1:
  :mx#0:
  :sh:
  :af=/var/spool/lpd/lp1/acct:
  :lp=/dev/null:
  :if=/usr/lib/rhs/rhs-printfilters//smbprint:
```

第一个打印机（名为`lp1`）是直接连接到并行端口上的。大多数配置参数都可以轻松追溯到`Print-Tool`配置窗口中的字段。这些参数是：

-   `sd`：定义打印池目录（spool directory）的路径。
-   `mx`：定义打印文件可接受的最大字节数。将其设置为`0`表示对打印作业的大小没有限制。
-   `sh`：指定是否打印页头或横幅页。这是“抑制页头（suppress headers）”布尔值。默认情况下，它是`false`，意味着不抑制页头。换句话说，默认打印页头。然而，`PrintTool`将该布尔值设置为`true`。（只需指定一个布尔值即可将其设置为`true`）。这意味着在打印作业之间不打印页头和横幅页。此设置适用于小型服务器，但如果你有多个用户，或希望为每个打印作业打印一个标识性横幅页，则可能需要注释掉此布尔值。
-   `lp`：定义打印机的设备名称。对于本地打印机，这是打印机连接的端口。
-   `if`：定义此打印机的输入过滤器。

该文件中的第二个打印机（`lp0`）是远程打印机。连接到打印机的远程机器由`rm`参数定义，该机器上的远程打印机名称由`rp`参数定义。在示例中，远程主机是`wren`，远程打印机名称是`lj`。该打印机的大部分实际配置都在远程系统上完成。尽管这是一个远程打印机，但它有一个本地打印池目录。文件被写入本地打印池目录，并在那里排队交付到远程系统。

第三个打印机称为`lp1`，是远程 SMB 打印机。这是最独特的定义。`lp1`自然地处理本地打印机和远程`lpd`打印机。远程 SMB 打印机需要更多的努力。这类打印机的实际工作由`smbprint`程序处理，它通过`if`参数作为打印机的输入过滤器被调用（`smbprint`将在本章稍后详细介绍）。由`lp`参数定义的设备名称是`/dev/null`。在这种情况下，你并不希望输入过滤器的任何输出发送到本地打印机，因此它被发送到空设备（bit-bucket）。实际输出由`smbprint`直接送到远程服务器。`af`参数定义了一个写入计数信息的文件。

从零开始编写`printcap`是很困难的。要创建`printcap`条目，请选择一个与你的 Linux 系统兼容的打印机，并使用`printcap`配置工具。如果需要进行任何更改，可以使用`printcap`手册帮助你读取和更新`printcap`。一旦配置完成并在本地运行，就可以与其他人共享了。

### 使用 `lpd` 共享打印机

线路打印守护进程（`lpd`）为本地和远程用户提供打印服务。这是一项基本服务，在系统启动时从启动脚本启动。在 Red Hat 和 Caldera 系统上，`lpd`由`/etc/rc.d/init.d/lpd`脚本启动，该脚本通常包含在启动过程中。如果它没有包含在服务器的启动中，你可以使用`linuxconfig`或`tksys`添加该脚本。

![](img/0a4925a63d7144788f84b23689a2d0da_432_0.png)

你可以使用`lpd`脚本停止、启动或重新加载线路打印守护进程。由于`printcap`文件仅在`lpd`启动时读取，`reload`选项有助于在不重启守护进程的情况下应用更改。

```bash
/etc/rc.d/init.d/lpd reload
```

### 线路打印守护进程安全

线路打印守护进程使用基于主机的安全机制。为了控制哪些用户可以访问哪些打印机，你需要编辑`printcap`文件。参数指定了是否打印页头或横幅页。这是“抑制页头（suppress headers）”布尔值。默认情况下，它是`false`，意味着不抑制页头。换句话说，默认打印页头。然而，`PrintTool`将该布尔值设置为`true`。（只需指定一个布尔值即可将其设置为`true`）。这意味着在打印作业之间不打印页头和横幅页。此设置适用于小型服务器，但如果你有多个用户，或希望为每个打印作业打印一个标识性横幅页，则可能需要注释掉此布尔值。

### 使用 `lpr`

使用线路打印远程（`lpr`）程序将打印作业发送到打印进程。`lpr`有多个命令行参数，但命令通常标识打印机和文件，如示例所示：

```bash
lpr -Plj sample.txt
```

此命令将名为`sample.txt`的文件发送到`lp0`的打印机。打印机可以是本地的或远程的；只要该打印机在`printcap`文件中有定义并被`lpd`识别即可。

### 管理 `lpd`

线路打印控制（`lpc`）程序是用于控制打印机和管理`lpd`打印队列的工具。表 12.1 列出了`lpc`命令、语法及其含义。

#### 表 12.1 `lpc` 命令

| 命令 | 用法 |
| :--- | :--- |
| `abort printer` | 杀死打印守护进程。 |
| `clean printer` | 清除打印队列中的所有文件。 |
| `disable printer` | 关闭对打印队列的操作。 |
| `down printer message` | 停止池和打印，并输出消息。 |
| `enable printer` | 启用对打印队列的操作。 |
| `exit` | 退出`lpc`。 |
| `help command` | 显示每个命令的描述。 |
| `restart printer` | 启动一个新的打印守护进程。 |
| `start printer` | 启用打印和池。 |
| `status printer` | 显示打印机和队列的状态。 |
| `stop printer` | 当前作业结束后停止打印机。 |
| `topq printer job# user` | 将打印作业移动到队列顶部。 |
| `up printer` | 启用池和打印。 |

对于所有命令，打印机名称都是可选的。如果没有指定，将使用默认打印机。`topq`命令还可以接收作业号或用户名来标识要移动到队列顶部的打印作业。

“队列中的顶部”意味着它将是下一个打印的任务。其他常用命令选项包括可以添加到`down`命令中的消息，以及可以添加到`help`命令中的命令。`message`是发出的通知用户打印机正在停机的文本消息。`command`是你想要帮助信息的`lpc`命令的名称。

```
% lpc
lpc> status all
lp:
    queuing is enabled
    printing is enabled
    2 entries in spool area
    no daemon present

lw:
    queuing is enabled
    printing is enabled
    no entries
    no daemon present

dj:
    queuing is enabled
    printing is enabled
    no entries
    no daemon present
lpc> restart lp
lp:
    no daemon to abort
lp:
    daemon started
lpc> exit
```

#### 与 Samba 共享打印机

注意，在示例`status`命令中，使用了`all`关键字代替了打印机名称，`all`可用于引用接受打印机名称作为可选参数的`lpc`命令中的所有打印机。

示例中使用的`status`和`restart`命令可以由任何用户使用。大多数`lpc`命令只能由`root`用户使用。例如，以下命令将属于用户`tyler`的打印作业移动到打印机`lp`队列的顶部：

```bash
# lpc topq lp tyler

lp:
moved cfa405owl
```
