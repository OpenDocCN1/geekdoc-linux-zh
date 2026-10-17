
此示例中的 `quotacheck` 命令会查看挂载在 `/home` 上的文件系统分区并构建磁盘使用表。`-v` 选项产生命令的详细输出，`-u` 选项导致检查用户配额，`-g` 选项导致检查组配额。这两个文件的权限被设置为只有 root 用户可以访问（`chmod 600 aquota.*`）。

## 创建包启动脚本

如果该包不包含启动脚本（在当前的 Fedora 或 RHEL 发行版中并不包含），你可以创建自己的。你希望此脚本检查配额（使用 `quotacheck` 命令）、启动配额服务并关闭配额服务。创建一个名为 `/etc/init.d/quota` 的新文件，其内容如下：

```bash
#!/bin/bash

# init file for quota
# description: Checks disk usage
# name: quota
# config: 0

case $1 in
  start)
    echo "Checking quotas: "
    quotacheck -vug /home
    aquota -a)
    echo "Starting quotas: "
    aquota -a
    ;;
  stop)
    echo "Shutting down quotas: "
    quotaoff -a
    ;;
  *)
    echo "Usage: $0 {start|stop|restart}"
    exit 1
    ;;
esac
```

此脚本会查看挂载在 `/home` 上的文件系统分区并构建磁盘使用表。`-v` 选项产生命令的详细输出，`-u` 选项导致检查用户配额，`-g` 选项导致检查组配额。这两个文件的权限被设置为只有 root 用户可以访问（`chmod 600 aquota.*`）。

## 第 11 章：设置与支持用户

每个目录中的文件。添加 `-h` 可以数字形式显示使用的磁盘空间，单位为千字节（k）、兆字节（M）或千字节（G）。`-c` 选项会在末尾添加所有请求目录的总和。以下命令检查了几个主目录的磁盘占用情况：

```
# du -hcs /home/tom /home/bill /home/tina /home/sally
```

这应该列出所有用户主目录的列表，每个目录前面都有该目录结构占用的千字节（K）、兆字节（M）或千字节（G）。它看起来如下：

```
1G
339M /home/tom
81M /home/bill
31M /home/tina
44K /home/sally
1.45G total
```

# 自动删除临时文件

某些潜在的磁盘消耗问题被设置为自动处理。例如，应用程序存储临时文件的目录（如 `/tmp` `/var/tmp`）会随着时间的推移消耗大量磁盘空间。为了解决这个问题，Fedora 和 RHEL 包含了 `tmpwatch` 功能。`tmpwatch` 命令从 `/etc/cron.daily/tmpwatch` cron 文件运行，删除未使用的临时文件。该文件内容如下：

```
/usr/sbin/tmpwatch 240 /tmp
/usr/sbin/tmpwatch 720 /var/tmp
for d in /var/(cache/man,catman){cat?,X11R6/cat?,local/cat?}; do
  if [ -d "$d" ]; then
    /usr/sbin/tmpwatch -f 720 $d
  fi
done
```

`tmpwatch` 脚本每天运行，删除一段时间未使用的临时文件。来自 `/tmp` 和 `/var/tmp` 目录的文件在未被访问 240 小和 720 小时后会被删除。存储在 `/var/cache` 子目录中的临时 man 页在闲 720 小时后也会被检查并删除。

# 向所有用户发送邮件

偶尔，你需要向系统上的所有用户发送消息。硬件升级的计划停机警告就是一个很好的例子。逐一向每个用户单独发送电子邮件非常耗时且浪费；这正是电子邮件别名和邮件列表发明的任务类型。然而，为系统上的所有用户维护邮件列表可能会出现问题。如果你不勤于更新邮件列表，随着你添加和删除用户，该列表会变得越来越不准确。此外，如果你的系统有许多用户，仅仅别名列表的大小就可能变得难以管理。

以下名为 `mailfile` 的脚本提供了一种解决这些问题的简单方法。它从 `/etc/passwd` 文件中获取登录名并向所有用户发送电子邮件。

> **注意：** 下面的脚本跳过了你 `/etc/password` 文件中的前 17 个账户（以排除管理员账户接收邮件）。请检查你的 `/etc/password` 文件并修改脚本以包含准确的管理员账户数量（取决于你安装了哪些包，可能在 50 个左右）。然后，确保该文件中所有用户账户都列在你的管理员账户之后。

```
#!/bin/bash
#
# mailfile: 此脚本将指定的文件发送给系统所有
# 的用户。它跳过了前 17 个账户，以便
# 我们不会向如 'root' 等系统账户发送邮件。
#
# 用法: mailfile "这里是邮件主题" filename.txt
#
# 检查主题是否存在
#
if [ "$(echo $1 | awk '{ print $1}')" == "" ]; then
    echo 你没有为消息提供主题。
    echo 请确保将其包含在引号中。
    exit 1
else
    # 获取消息的主题
    set subject=$1
fi
#
# 检查文件名是否存在
#
if [ "$2" == "" ]; then
    echo 你没有提供文件名。
    exit 2
else
    # 获取要发送的文件名
    set filename=$2
fi
#
# 检查文件是否存在
#
if [ -f $filename ]; then
    echo 正在发送文件 $filename
else
    echo 文件不存在。
    exit 3
fi

# 循环遍历每一个登录名，但跳过前 17 个账户
foreach user in $( awk '{ print $1 }' /etc/passwd | tail +17 ); do
  # 发送邮件
  echo 正在向 $user 发送邮件
  mail -s "$subject" $user < $filename
done

# 睡眠几秒钟以免让邮件发送程序过载
# 在快速系统或账户较少的系统上，你
# 可能可以去掉这个延迟。
sleep 2
```

该脚本接受两个参数。第一个是邮件消息的主题，包含在引号中。第二个是包含要发送文本的文件名。因此，为了向所有用户发送警告有关即将到来的服务器硬件升级的邮件，我可能会执行类似以下的操作：

`mailfile` "系统将于下午 5:00 升级" `upgrade.txt`

文件 `upgrade.txt` 包含了要发送的消息正文。这种方法真正实用的地方在于，我可以保存此文本文件，并在下次升级系统时方便地修改和重新发送。

> 提示：如果你的用户使用文本登录而不是图形界面登录你的系统，你可以向 `/etc/motd` 文件中添加消息，以便触达给你的用户。

### 总结

并不常见一个 Linux 系统被用作没有实际用户的服务器。它静静地运行在房间中，提供网页或处理邮件服务，很少崩溃或需要注意。这并不总是如此。你可能需要在你的 Linux 系统上支持许多用户，这可能是系统管理中最具挑战性的部分。

Fedora 和 RHEL 提供了各种工具帮助你处理用户行政工作。`useradd`, `usermod` 和 `userdel` 命令可以对用户账户数据进行简单的别名操作。此外，为系统所有用户维护邮件列表并自动化任务减轻了你的负担。Fedora 和 RHEL 在 Unix 的丰富历史之上构建，为支持多样化需求提供了理想平台。

## 第 12 章：任务任务

## 本章内容

- 理解脚本

- 系统设置

- 任务调度

并不常见一个 Linux 系统被用作没有实际用户的服务器。它静静地运行在房间中，提供网页或处理邮件服务，很少崩溃或需要注意。这并不总是如此。你可能需要在你的 Linux 系统上支持许多用户，这可能是系统管理中最具挑战性的部分。

Fedora 和 RHEL 提供了各种工具帮助你处理用户行政工作。`useradd`, `usermod` 和 `userdel` 命令可以对用户账户数据进行简单的别名操作。此外，为系统所有用户维护邮件列表并自动化任务减轻了你的负担。Fedora 和 RHEL 在 Unix 的丰富历史之上构建，为支持多样化需求提供了理想平台。

# 理解脚本

你是否遇到过需要重复执行的任务？也许脚本就是你所寻找的。脚本是批处理文件的等物。

# 执行和调试脚本

脚本的一个主要优势是可以用任何文本编辑器打开查看其内容。一个很大的缺点是脚本的执行速度通常比编译程序慢。执行脚本有两种基本方法：

- 将文件名作为 shell 的参数（如 `bash myscript`）。在这种方法中，文件不需要具有执行权限；它只包含 shell 命令。命令行指定的 shell 将用于解释脚本中的命令。
