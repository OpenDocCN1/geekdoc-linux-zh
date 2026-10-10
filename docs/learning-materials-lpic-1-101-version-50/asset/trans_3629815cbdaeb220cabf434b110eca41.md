

# 引导练习答案

-   1. 保存由自动化脚本执行的操作的日期很方便。命令 `date +%Y-%m-%d` 以年-月-日格式显示当前日期。如何使用命令替换将该命令的输出存储到一个名为 `TODAY` 的 shell 变量中？

    ```bash
    $ TODAY=`date +%Y-%m-%d`
    ```
    
    或者
    
    ```bash
    $ TODAY=$(date +%Y-%m-%d)
    ```

-   2. 使用命令 `echo`，如何将变量 `TODAY` 的内容发送到命令 `sed s/-/.g` 的标准输入？

    ```bash
    $ echo $TODAY | sed s/-/.g
    ```

-   3. 如何将命令 `date +%Y-%m-%d` 的输出用作命令 `sed s/-/.g` 的 Here 字符串？

    ```bash
    $ sed s/-/.g <<< `date +%Y-%m-%d`
    ```
    
    或者
    
    ```bash
    $ sed s/-/.g <<< $(date +%Y-%m-%d)
    ```

-   4. 命令 `convert image.jpeg -resize 25% small/image.jpeg` 创建 `image.jpeg` 的缩小版本，并将生成的图像放置在子目录 `small` 中同名文件中。使用 `xargs`，如何对文件 `filelist.txt` 中列出的每个图像执行相同的命令？

    ```bash
    $ xargs -I IMG convert IMG -resize 25% small/IMG < filelist.txt
    ```
    
    或者
    
    ```bash
    $ cat filelist.txt | xargs -I IMG convert IMG -resize 25% small/IMG
    ```

## 探索性练习答案

1.  一个简单的备份例程定期使用 `dd < /dev/sda1 > sda1.img` 创建分区 `/dev/sda1` 的映像。为了进行未来的数据完整性检查，该例程还使用 `sha1sum < sda1.img > sda1.sha1` 生成该文件的 SHA1 哈希值。通过添加管道和命令 `tee`，如何将这两个命令合并为一个？

    ```bash
    $ dd < /dev/sda1 | tee sda1.img | sha1sum > sda1.sha1
    ```

2.  命令 `tar` 用于将多个文件归档到单个文件中，并保留目录结构。选项 `-T` 允许指定包含要归档的路径的文件。例如，`find /etc -type f | tar -cJ -f /srv/backup/etc.tar.xz -T -` 根据命令 `find` 提供的列表（选项 `-T -` 指示标准输入作为路径列表）创建压缩 tar 文件 `etc.tar.xz`。为了避免由于路径中包含空格而可能导致的解析错误，`find` 和 `tar` 应该使用哪些命令选项？

    选项 `-print0` 和 `--null`：

    ```bash
    $ find /etc -type f -print0 | tar -cJ -f /srv/backup/etc.tar.xz --null -T -
    ```

3.  除了打开一个新的远程 shell 会话外，命令 `ssh` 还可以直接执行作为其参数指定的命令：`ssh user@storage "remote command"`。鉴于 `ssh` 也允许将本地程序的标准输出重定向到远程程序的标准输入，`cat` 如何通过 `ssh` 将名为 `etc.tar.gz` 的本地文件管道传输到 `user@storage` 的 `/srv/backup/etc.tar.gz`？

    ```bash
    $ cat etc.tar.gz | ssh user@storage "cat > /srv/backup/etc.tar.gz"
    ```
    
    或者
    
    ```bash
    $ ssh user@storage "cat > /srv/backup/etc.tar.gz" < etc.tar.gz
    ```

![image](img/824749d5fc1d265354d0e66a01af9ced_297_0.png)

## 103.5 创建、监控和终止进程

**LPI 目标参考**

| 类别 | 详情 |
| :--- | :--- |
| 考试 | LPIC-1 v5, 考试 101 |
| 目标 | 103.5 |
| 权重 | 4 |

**关键知识领域**

-   在前台和后台运行作业。
-   向程序发送信号以在注销后继续运行。
-   监控活动进程。
-   选择和排序进程以供显示。
-   向进程发送信号。

**所用文件、术语和实用工具的部分列表**

-   `&`
-   `bg`
-   `fg`
-   `jobs`
-   `kill`
-   `nohup`
-   `ps`
-   `top`
-   `free`
-   `uptime`
-   `pgrep`
-   `pkill`
-   `killall`
-   `watch`
-   `screen`
-   `tmux`

![image](img/824749d5fc1d265354d0e66a01af9ced_299_0.png)

# 103.5 第 1 课

| | | |
| :--- | :--- | :--- |
| **证书：** | LPIC-1 |
| **版本：** | 5.0 |
| **主题：** | 103 GNU 和 Unix 命令 |
| **目标：** | 103.5 创建、监控和终止进程 |
| **课程：** | 1 / 2 |

## 简介

每次我们调用命令时，都会启动一个或多个进程。训练有素的系统管理员不仅需要具备创建进程的能力，还需要能够跟踪这些进程，并在必要时向它们发送不同类型的信号。在本课中，我们将查看作业控制以及如何监控进程。

## 作业控制

*作业*是通过终端交互式启动、发送到后台且尚未完成执行的进程。您可以通过运行 *jobs* 来了解您 Linux 系统中的活动作业（及其状态）：

```bash
$ jobs
```

上面的 *jobs* 命令没有产生任何输出，这意味着目前没有任何活动作业。让我们通过运行一个需要一些时间才能完成执行的命令（参数为 60 的 `sleep` 命令）来创建我们的第一个作业，并在运行过程中按 `Ctrl` + `Z`：

```bash
$ sleep 60
^Z
[1]+  Stopped                 sleep 60
```

命令的执行已被停止（或者——更确切地说——挂起），并且命令提示符再次可用。你可以第二次查找作业，现在会发现那个*挂起*的作业：

```bash
$ jobs
[1]+  Stopped                 sleep 60
```

让我们解释一下输出：

-   `[1]`
    此数字是作业 ID，可以配合百分号符号 (%) 一起使用，通过 `fg`、`bg` 和 `kill` 实用工具来更改作业状态（后文将向您展示）。
-   `+`
    加号指示当前默认作业（即最近被挂起或发送到后台的那个）。前一个作业用减号 (-) 标记。其他较早的作业没有标记。
-   `Stopped`
    作业状态的描述。
-   `sleep 60`
    命令或作业本身。

使用 `-l` 选项，jobs 将在状态右侧额外显示进程 ID (PID)：

```bash
$ jobs -l
[1]+  Stopped  1114 sleep 60
```

`jobs` 的其他可能选项包括：

-   `-n`
    仅列出自上次通知以来状态发生变化的进程。可能的状态包括：运行中 (Running)、已停止 (Stopped)、已终止 (Terminated) 或已完成 (Done)。
-   `-p`
    列出进程 ID。
-   `-r`
    仅列出正在运行的作业。
-   `-s`
    仅列出已停止（或挂起）的作业。

**注意** 请记住，作业既有一个*作业 ID*，也有一个*进程 ID* (PID)。

## 作业指定

`jobs` 命令以及其他实用工具如 `fg`、`bg` 和 `kill`（将在下一节中介绍）需要作业指定符（或 *jobspec*）来针对特定作业进行操作。正如我们刚刚看到的，这可以是（通常也是）以 % 开头的作业 ID。然而，也可以使用其他作业指定符。让我们来看看它们：

-   **%n**
    ID 为 n 的作业：

    ```bash
    $ jobs %1
    [1]+  Stopped              sleep 60
    ```

-   **%str**
    命令行以 *str* 开头的作业：

    ```bash
    $ jobs %sl
    [1]+  Stopped              sleep 60
    ```

-   **%?str**
    命令行包含 *str* 的作业：

    ```bash
    $ jobs %?le
    [1]+  Stopped              sleep 60
    ```

-   **%+ 或 %%**
    当前作业（最后一个在后台启动或从前台挂起的作业）：

    ```bash
    $ jobs %+
    [1]+  Stopped     sleep 60
    ```

-   **%-**
    前一个作业（在默认的当前作业之前是 %+ 的那个）：

    ```bash
    $ jobs %-
    [1]+  Stopped     sleep 60
    ```

在我们的情况下，由于只有一个作业，它既是当前的也是前一个。

## 作业状态：挂起、前台和后台

一旦作业在后台或已挂起，我们可以对其执行以下三种操作之一：

1.  使用 `fg` 将其带到前台：

    ```bash
    $ fg %1
    sleep 60
    ```

    `fg` 将指定的作业移至前台并使其成为当前作业。现在我们可以等待它完成，再次用 `Ctrl + Z` 停止它，或用 `Ctrl + C` 终止它。

2.  使用 `bg` 将其带到后台：

    ```bash
    $ bg %1
    [1]+ sleep 60 &
    ```

    一旦在后台，作业可以用 `fg` 带回前台或被终止（见下文）。注意，& 符号表示作业已发送到后台。事实上，您也可以使用 & 符号直接在后台启动进程：

    ```bash
    $ sleep 100 &
    [2] 970
    ```

    除了新作业的 ID ([2])，我们现在还得到了它的进程 ID (970)。现在两者

