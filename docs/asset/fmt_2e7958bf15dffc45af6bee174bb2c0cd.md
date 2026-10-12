
### 工作原理

在本配方中，我们考虑了通过命令行使用 `rsync`。当然，这只是许多可用方法之一，但通过使用这种方法，我们能够探索这一非常有用的工具提供的若干功能。

那么，我们从这次经历中学习了什么呢？

`rsync` 并不复杂。它是一个快速高效的同步工具，通过让你拥有命令行上一系列功能的完全访问权限来实现多功能性。它可以用于在同一台机器或完全不同的系统上维护源目录的精确副本（或镜像），其原理是先复制所有文件，然后在下次运行时仅更新已更改的文件。使用 `--delete` 选项在通过网络复制数据时将是你的主要工具。使用 `rsync` 可以删除目标上在源中不存在的文件，而选定的标志意味着 `rsync` 应使用 `-a` 归档模式递归复制文件和目录，同时保留所有权限和时间信息；`-v` 详细模式可以让你看到正在发生什么；以及 `-z` 在文件传输期间压缩数据，以节省带宽并缩短完成整个过程所需的时间。

![](img/a6dbf7df749be83c0faae2334e970c0b_513_0.png)

# 监控服务器基础设施

在本配方中，我们将使用一个小型脚本，通过 `cron` 定期监控可用文件系统的磁盘空间，如果超过了特定的百分比阈值，脚本将发送一封带有警告消息的邮件。

```bash
if [ $usep -ge $THRESHOLD ]; then
  (echo "Subject: Alert: Free space low on \$hostname -s", $usep % used on \$partition"; echo)
  sendmail -t $EMAIL
fi
```

现在，保存文件并赋予可执行权限：

```bash
chmod +x /etc/cron.daily/monitor_disk_space.sh
```

### 工作原理

我们赋予了该脚本可执行权限，并将其放入 `/etc/cron.daily` 目录下，这样我们就可以通过 `cron` 服务每天自动运行它。

这个简单的脚本展示了监控脚本是多么容易，这可以作为安装和配置如 `Nagios` 等监控套件的真实替代方案。你可以将此脚本作为起点进行扩展，添加其他需要监控的重要资源，例如 `CPU` 负载、内存等。

我们使用了一个执行 Linux 命令 `df` 的脚本，该命令是一个用于报告文件系统磁盘使用情况的工具。从该命令的输出中，我们使用 `awk` 和 `cut` 工具打印出 `USE%` 列，从而得到总磁盘使用百分比。这个数字将与用户通过编辑脚本并更改环境变量 `THRESHOLD` 设置的阈值进行比较。如果提取的百分比高于我们的阈值，`EMAIL` 将发送到由环境变量定义的地址（如有需要请进行相应更改）。

# 使用 GIT 和 Subversion 进行控制

修订控制系统（或有时称为版本控制系统）用于管理文档的更改。随着现代工作将全球各地的人连接起来共同协作处理各种文档（例如源代码），这些系统变得越来越重要，因此通过修订来管理不同人员产生的文件更改变得至关重要。在本食谱中，我们将向你展示如何使用 `GIT` 和 `Subversion` 等现代版本控制系统来管理配置文件的版本控制。

### 准备工作

完成此食谱，你需要一个具有 root 权限的 `CentOS 7` 操作系统的可运行安装，并且连接到互联网以便下载额外的软件包。

## 管理系统

### 如何操作

在本食谱中，我们将整个主 Linux 配置目录 `/etc/` 置于 `Git` 仓库的修订控制之下，以跟踪我们对配置文件的所有更改：

1. 首先，以 root 身份登录，安装 `Git`，并通过提供电子邮件地址和用户名进行配置（请将 `your_username` 和 `your_email_address` 替换为真实名称）：

```bash
yum install git
git config --global user.email "your_email_address"
git config --global user.name "your_username"
```

2. 现在，在 `/etc/` 目录下创建一个新仓库：

```bash
cd /etc/
git init
```

3. 现在，在我们拥有新仓库后，将 `/etc/` 目录下的所有文件添加到修订控制中：

```bash
git add *
```

4. 将文件提交到仓库并创建第一个修订，输入以下内容：

```bash
git commit -a -m "inital commit of the full /etc/ directory"
```

5. 现在，让我们修改一个文件：

```bash
echo "FILE HAS CHANGED" >> yum.conf
```

6. 接下来，显示仓库的更改：

```bash
git status
```

7. 接下来，我们将提交这些更改并创建一个新修订：

```bash
git commit -a -m "changing yum.conf files"
```

8. 接下来，显示目前为止所有的提交：

```bash
git log --pretty=oneline --abbrev-commit
```

9. 这将在我的系统中输出以下提交（哈希值在你的系统中会不同）：
   `8069c4a` changing yum.conf
   `5f0d50a` initial commit of the full /etc directory

10. 根据上一步的输出，我们现在将显示两个修订版本之间的所有差异（根据上一步的输出更改你系统上的哈希值）：

```bash
git diff 8069c4a 5f0d50a
```

11. 为了完成此食谱，我们将更改还原到原始文件修订版本（初始提交）：

```bash
git checkout 5f0d50a
```
