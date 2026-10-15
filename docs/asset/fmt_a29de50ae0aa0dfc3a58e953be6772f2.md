
> Note: New releases of some flavors of UNIX are using the Posix shell for cron. The Korn shell is compliant with Posix, so your crontab scripts must be either Korn shell or Posix shell. The man pages for cron will tell you which shell is used.

然而，你不想在真正、非常想删除文件时，自己却没有办法运行真正的 `rm` 命令。所以再使用另一个别名，这次是 `rm!`，以保持我们一直使用的惯例。

```
alias rm!=''/bin/rm''
```

这使用了 `rm` 命令的绝对路径，可以绕过任何可能存在的外部脚本，直接访问源文件。

```sh
# A script to purge files that have been copied to the $HOME/tmp
# directory using the aliased rm command. Checks for files
# not changed in the last week and removes them. This is the
# bang version. Also included in our crontab file to run once
# a week. Thus, all files in $HOME/tmp are absolutely removed
# after 14 days.
cd $HOME/tmp
find . -ctime +7 -exec rm -f {} \;
```

**Figure 12-4** When you run a script from your **crontab**, you have to use the Bourne shell

## What’s the very best way to protect crucial files against accidental erasure?

保护文件免于意外删除，甚至更糟的蓄意破坏的一个重要方法是使用 UNIX 内置的保护机制。

第一步是使真正重要的文件变为只读。这很容易做到，并且可以为你节省大量麻烦。如果你有不需要更改但需要定期访问的文件，请更改其权限，使任何人——甚至你自己——都无法写入。

```
chmod a-w filename
```

现在，该文件在不采取额外步骤的情况下无法被更改，即使是由你所有者也是如此。当然，你可以通过在更改文件前先更改权限来绕过这一点。但你已经使这个过程变得足够繁琐，以至于不太可能意外执行。

> **Warning:** The superuser can delete your file no matter what you do. This is one of those sad but true facts. No matter how much protection you put on a file, the superuser can blithely delete the file or change it, with barely a moment’s thought. Yet another reason to stay on friendly terms with this person.

目录——除非有人知道你的密码。

另一个保持密码安全的好理由。

> Warning: Don't forget to change your `$HOME` directory as well. It's easy enough to protect your own directories, but also easy to forget to change the home directory itself.

```
chmod 700 $HOME
```

将只更改你的主目录，使任何人都无法随意窥探。

## BACKUP, BACKUP, BACKUP!

## UNIX and Backups

所有这些防止意外删除文件或在不打算更改时更改文件的技巧都很棒，我们强烈建议你使用其中的一些组合。但当灾难发生时，没有什么能比得上经过验证的备份。系统管理员对备份负有主要责任，但每个使用计算机的人都需要对自己关键文件的备份负责。这并不难，也不必繁重，而且可能成为救命稻草。

UNIX 的美妙之处在于，你通常不必担心备份程序或庞大的数据文件，因为这些通常是系统管理员的职责范围。但你确实需要考虑自己的本地数据文件。你使用的方法将取决于系统的功能、可用硬盘空间的大小，以及系统上对个人用户可用的程序和媒体。但大多数系统都有足够的硬盘空间供你至少在硬盘上维护一份最新工作的副本，如果你有访问权限和权限，复制这些文件到软盘上也相当容易。使其无痛的关键是只备份你需要的内容，然后经常进行备份。个人而言，我们更喜欢大约每天两次备份当前工作文件，但你需要决定什么适合你。许多用户喜欢将其作为注销例程的一部分进行自动化，而 C shell 甚至为此目的有一个特殊文件——`.logout`。但如果你使用 Korn shell，你将需要创建自己的等效文件。在我们深入了解如何自动化备份的具体细节之前，让我们先看看你可以，也应该做的备份类型。

### 为什么我会考虑制作硬盘备份？

现代硬盘非常安全稳定，几乎从不崩溃。今天购买的硬盘平均“平均无故障时间”（MTBF）为 100,000 到 300,000 甚至 500,000 小时的连续服务，具体取决于品牌和型号。这相当于 11-56 年才发生一次故障，这显然比你需要担心的要长得多，因为今天购买的电脑在 11 年——更不用说 56 年——后就不会再使用了。它们在那之前就会因技术过时而被淘汰。当然，仍然有可能买到次品，这就是为什么系统管理员忠实地进行备份的原因。因此，将备份到你的硬盘上对于你的文件来说可能已经足够了。这可以保护你免受意外删除的影响，以及由你无法控制的情况引起的关键文件偶发损坏。

### 制作硬盘备份最简单的方法是什么？

将工作文件副本保存在备份目录中。这可能是处理备份任务最简单的方法，并且对大多数用户来说已经足够。我们称之为 `.backup` 并将权限设置为 700（即所有者拥有完全权限，但其他任何人都没有任何权限）。这足以保护你免受随意（甚至不那么随意）的恶作剧，因为除了超级用户之外，没有其他人可以进入此目录。然后我们将工作文件的当前版本保存在该目录中。对于不需要或不想要保留文件不同版本之类的简单任务，我们有一个简单的别名，在每次注销时调用。它会将今天更改过的文件复制到 `.backup` 目录。

```
alias savwrk='find $HOME/* -mtime -1 -exec cp {} $HOME/.backup \;'
```

这个别名工作得相当好，但并不完美。例如，它不会复制以点开头的文件或目录。替代方案是添加你想要确保被复制的任何特殊目录或文件。或者编写一个构建更智能目录树的脚本。

### 在什么情况下我应该考虑制作磁带或软盘备份？

硬盘备份很好，并且对于许多目的来说提供了足够的保护，尤其是考虑到你的系统管理员无疑会定期进行完整的磁带备份。但在某些情况下，硬盘备份并不合适。如果你从事极其敏感的工作，无法在硬盘上留下你所做的副本，例如，你就需要不在场时将工作从硬盘上取走。而且，如果你丢失某些文件会完全毁灭，你可能希望在系统管理员所做的备份之外自行备份，尤其是如果你所在的系统环境中系统范围的备份每周才进行一次，例如。

### 制作磁带或软盘备份最简单的方法是什么？

将文件备份到磁带或软盘等外部存储介质最常见的机制是 UNIX `tar`（磁带归档和恢复）命令。此命令在几乎所有 UNIX 系统上都可用，也可用于 DOS 等其他系统，是处理大多数用户备份任务的一种简单且相当高效的方法。系统管理员可能拥有更强大的工具，可以轻松跨网络的多个机器和文件系统，但幸运的是你不太可能需要这些。

`tar` 命令的语法是

```
tar key files
```

其中 `key` 是以下基本操作之一：

- `-c` 创建新的归档
- `-r` 追加到现有归档
- `-t` 列出归档的内容
- `-u` 更新归档，添加不存在或更新的文件
- `-x` 从归档中提取文件

以及以下一个或多个修饰符：

- `-A` 抑制绝对文件名
- `-l` 如果链接无法解析则给出错误消息
- `-L` 跟随符号链接以及硬链接
- `-m` 不恢复修改时间（所有内容都获得当前日期/时间）
- `-p` 使用原始权限提取
- `-v` 详细-`tar` 默认是安静的
- `-w` 每次操作前等待确认
- `-f` 下一个参数是要使用的设备名称

这些是 `tar` 选项中最重要的部分，并且在各种平台上行为基本一致。可能还有适用于你特定情况或 `tar` 实现的特定选项，如果有疑问，请咨询你的系统管理员。

`tar` 的最后一个参数是要归档的文件。这可以是特定的文件或目录，或者 `tar` 可以作为管道命令行的部分，如果设备为 `"-"` 表示标准输入或输出。

## 我可以使用 tar 将文件复制到不同的机器或文件系统吗？
