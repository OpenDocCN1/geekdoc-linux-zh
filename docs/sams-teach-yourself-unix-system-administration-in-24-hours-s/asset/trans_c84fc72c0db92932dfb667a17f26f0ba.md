
![](img/5ced0c78d748bd190e9027e5549a3622_77_0.png)

> Unix 老手们经常把反引号称为 backticks，因此一位老练的 Unix 管理员在此可能会说“把 dee-ew e 放在 backticks 里”。

以下是变化情况。首先，让我们将目录名加载到新变量中：

```
bigdirs="du -s /home/* | sort -rn | cut -f2- | head -5"
```

然后我们需要更改 for 循环以反映这一变化，这很简单：

```
for dirname in $bigdirs ; do
```

请注意，我还把 do 行上移以缩短脚本。回想一下，分号表示 shell 脚本中命令的结束，因此我们可以毫不犹豫地把下一行也上移。

3. 现在不要忘记在列出每个目录的大文件之前先输出大目录列表。总的来说，我们的脚本现在如下所示：

```
echo "Disk Hogs Report for System `hostname`"
bigdirs="du -s /home/* | sort -rn | cut -f2- | head -5"
echo "The Five biggest home directories are:"
echo $bigdirs
for dirname in $bigdirs ; do
  echo ""
  echo Big directory: $dirname
  echo Four largest files in that directory are:
  find $dirname -type f -printf "%k %p\n" | sort -rn | head -4
done
exit 0
```

这已经相当接近最终产品了，如其输出所示：

系统 staging.intuitive.com 的磁盘占用报告
五个最大的主目录是：
/home/staging  /home/chatter  /home/cbo  /home/sherlockworld  /home/launchline

大目录：/home/staging
该目录中最大的四个文件是：
423  /home/staging/waldorf/big/DSCF0165.jpg
410  /home/staging/waldorf/big/DSCF0176.jpg
402  /home/staging/waldorf/big/DSCF0166.jpg
395  /home/staging/waldorf/big/DSCF0161.jpg

大目录：/home/chatter
该目录中最大的四个文件是：

```
1076 /home/chatter/comics/lynx
388 /home/chatter/logs/access_log
90 /home/chatter/logs/error_log
64 /home/chatter/responding.cgi
```

大目录：/home/cbo
该目录中最大的四个文件是：
568 /home/cbo/financing.pdf
464 /home/cbo/investors/CBO-plan.pdf
179 /home/cbo/Archive/cbofinancial-modified-files/CBO Website.zip
77 /home/cbo/Archive/cbofinancial-modified-files/CBO Financial Incorporated .doc

大目录：/home/sherlockworld
该目录中最大的四个文件是：
565 /home/sherlockworld/originals-from gutenberg.txt
56 /home/sherlockworld/speckled-band.html
56 /home/sherlockworld/copper-beeches.html
54 /home/sherlockworld/boscombe-valley.html

大目录：/home/launchline
该目录中最大的四个文件是：
151 /home/launchline/logs/access_log
71 /home/launchline/x/submit.cgi
71 /home/launchline/x/admin/managesubs.cgi
64 /home/launchline/x/status.cgi

这是一个脚本，你可以很容易地在凌晨通过 cron 中的一行命令运行（我们将在第 15 小时“在未来运行作业”中详细探讨），或者你甚至可以把它放在你的 .profile 中，以便每次登录时自动运行。

4. 最后一点细微差别：要将输出通过电子邮件发送给你，只需追加以下内容：
| mail -s 'Disk Hogs Report' your-mailaddr
如果你像我一样将此脚本命名为 diskhogs.sh，你可以用以下命令将输出通过电子邮件发送给你（作为 root）：
sh diskhogs.sh | mail -s 'Disk Hogs Report' root
试试看，然后检查 root 的邮箱，看看报告是否已送达。

5. 对于使用 Solaris、Darwin 或其他 Unix 的用户，nifty 的 -printf 选项可能在你的 find 版本中不可用。因此，更通用的脚本版本会更复杂，因为我们不仅需要规避 -printf 的缺失，还需要解决 Darwin 上大多数目录名中包含嵌入空格的挑战。为此，我们使用 sed 和 awk 将所有空格更改为双下划线，然后在将参数传递给 find 命令时再改回来：

```sh
#!/bin/sh
echo "Disk Hogs Report for System `hostname`"

bigdir2=`du -s /Library/* | sed 's!/ /g' | sort -rn | cut -f2- | head -5`

echo "The Five biggest library directories are:"
echo $bigdir2

for dirname in $bigdir2 ; do
  echo ""
  echo Big directory: $dirname
  echo Four largest files in that directory are:
  find "$dirname" | sed 's!/ /g' -type f -ls | \
  awk '{ print $7, $11 }' | sort -rn | head -4
done

exit 0
```

好消息是输出最终几乎完全相同，如果你有 OS X 或其他 BSD 系统可用，可以验证这一点。

当然，用更复杂的 GNU 版本替换 find 的原生版本是明智的，但更改关键系统工具是大多数 Unix 用户不愿做的！

> 如果你想探索升级 Darwin 中的一些 Unix 工具以利用复杂的 GNU 增强功能，那么最好先查看 http://www.osxgnu.org/ 上的移植代码。该网站还包含下载说明。
> 如果你使用的是 Solaris 或其他不是 Mac OS X 的 Unix 变种，请查看工具升级的 GNU 主站点 http://www.gnu.org/。

这个 shell 脚本的演变方式在 Unix 工具中相当常见——它最初作为一个简单的命令行出现；然后随着工具的复杂性增加，命令序列的复杂性也增加到直接输入过于繁琐的地步，因此被放入 shell 脚本中。Shell 变量随后提供了保存中间输出、微调演示等功能，因此我们通过构建更强大的工具来利用它。最后，通过将其添加到 root cron 作业中，该工具本身被添加为系统中的自动化监控任务。

## 摘要

本小时不仅向你展示了用于分析磁盘使用和利用率的两个基本 Unix 命令，还演示了有用的管理 shell 脚本 diskhogs 的演变和发展。

这种从命令到多阶段命令再到 shell 脚本的序列将在你学习如何成为强大的系统管理员的过程中一再重复。

## 问答

Q 为什么有些 Unix 系统基于 512 字节块构建，而另一些则基于 1024 字节块构建？

A 这完全是因为 Unix 系统的历史和演变。当 Unix 最初部署时，磁盘很小，重要的是尽可能从磁盘中挤出尽可能多的字节。因此，文件系统是用 512 字节的基本块大小开发的（即为文件分配的空间始终以 512 字节块为单位）。随着磁盘变大，数百万个 512 字节块的管理开始证明比允许更有效地利用磁盘的好处更困难。因此，块大小加倍到 1KB 并一直保持至今。一些 Unix 系统仍保留 512 字节的历史块大小，而另一些则使用更现代的 1KB 块大小。

Q 所有设备名称都有意义吗？

A 尽可能地，是的。有时你无法避免出现 /dev/fd13x4s3，但即使如此，其命名约定背后可能也有合乎逻辑的解释。

Q 如果 du 有一个标志可以使其在默认使用 512 字节块的系统上以 1KB 块报告结果，为什么 1KB 系统上没有标志可以以 512 字节块报告？

A 啊，你期望一切都有意义？也许你最终在错误的领域了....

## 工作坊

### 测验

- 1. 为什么大多数 Unix 安装要将磁盘组织成大量分区，而不是少量巨大的物理设备？
- 2. 当你把大型硬盘上所有分区的大小加起来时，总会有一些缺失的空间。为什么？
- 3. 如果你看到设备 /dev/sdb3、/dev/sdb4 和 /dev/sdc1，关于引用的物理硬盘数量，你可能会怎样猜测？
- 4. Solaris 和 Darwin 都提供了非常有用的 df 命令的 -k 标志。它做什么，为什么会很有用？
- 5. 使用 ls 的 -s 标志、sort 的 -rn 标志和 head 的 -5 标志，构造一个命令行，显示你主目录中最大的五个文件。
- 6. 你认为如果一个非常大的文件意外地在 /home 目录中过夜，我们的脚本会发生什么？

### 答案

- 1. 通过将磁盘分成多个分区，你创建了一个更健壮的系统，因为一个分区填满不会影响其他分区。
- 2. 缺失的空间通常分配用于低级磁盘格式信息。在典型的 10GB 磁盘上，格式化后可能多达两到四个百分比的磁盘空间将不可用。
- 3. 这可能代表两个驱动器：/dev/sdb 和 /dev/sdc。
- 4. -k 标志使默认使用 512 字节块的系统以 1KB 块大小报告文件大小。
- 5. `ls -s $HOME | sort -rn | head -5`
- 6. 按编写的脚本会将非常大的文件标记为最大的主目录之一，然后在尝试分析其中的文件时失败。这是一个很好的例子，说明编程时需要大量错误条件代码和一些创造性思考。

下一小时将继续构建系统管理员知识的基础，即经常令人困惑的文件所有权模型。这将包括深入研究 passwd 和 groups 文件，并学习如何安全地更改它们以创建各种不同的权限场景。

![](img/5ced0c78d748bd190e9027e5549a3622_81_0.png)
