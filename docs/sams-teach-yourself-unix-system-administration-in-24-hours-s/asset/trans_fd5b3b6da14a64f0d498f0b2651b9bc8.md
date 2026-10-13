
这看起来并不那么严重；它只是说我们需要添加至少一个用户配额。这是通过 edquota 完成的，首先，让我们为用户 taylor 设置一个配额。

```
# edquota -u taylor
```

如果你立即收到“没有带配额的磁盘系统”的错误信息，最好的办法是仔细检查你是否已适当修改了 /etc/fstab，然后重新启动。一旦一切就绪，系统会弹出 vi 编辑器，其中包含以下信息：

```
Disk quotas for user taylor (uid 500):
Filesystem   blocks   soft   hard   inodes   soft   hard
/dev/hdb      1578     0      0      2        0      0
```

你可以看到该用户没有磁盘配额，尽管他使用了 1578 个磁盘块的空间并消耗了两个索引节点。你也可以看到，你可以按磁盘块（每个 1K）或按用户可以创建的索引节点数（本质上是文件数）来指定配额。通常，你会同时指定两者。

![](img/5ced0c78d748bd190e9027e5549a3622_251_0.png)

> 可用的配额有两种类型。超出软限制的用户在操作过程中会由文件系统生成警告，但他们仍可以继续工作。然而，硬限制通常会立刻阻止他们，拒绝任何写入磁盘的尝试。务必将软限制设置得明显低于硬限制，以避免用户感到沮丧。

![](img/5ced0c78d748bd190e9027e5549a3622_251_1.png)

用户 taylor 并不是太占用磁盘，所以我们将通过编辑所示的值为他设置相对宽松的磁盘配额：

```
Disk quotas for user taylor (uid 500):
Filesystem   blocks   soft   hard   inodes   soft   hard
/dev/hdb      1578     7500   9000   2        3000   4000
```

退出编辑器后，配额值将被保存。

如果你想将一个用户的配额限制复制到另一个用户，可以为 edquota 命令指定 -p prototype-user 标志。例如，要将 taylor 的配额复制给用户 sangeeth，就使用 edquota -p taylor sangeeth。当然，你也可以用一个简单的 shell 脚本来自动化整个过程。

5. 再一步：我们需要使用 quotaon 启用配额系统。对于此操作，我更喜欢使用 -a、-g、-u 和 -v，分别表示打开所有配额、详细输出、检查组配额和用户配额。要一次性完成，我们只需输入：

```
# quotaon -aguv
/dev/hdb [/disk2]: user quotas turned on
```

## 5. 现在当用户 taylor 输入 quota 时，他会看到

```
% quota
Disk quotas for user taylor (uid 500):
Filesystem blocks quota limit grace files quota limit grace
/dev/hdb 1578 7500 9000 2 3000 4000
```

在已启用配额的系统上，通常建议将 quota 命令添加到用户的 .login 或 .bash_profile 文件中。

## 6. 从管理角度来看，你可以使用 repquota 生成一份美观的输出报告：

```
# repquota -a
*** Report for user quotas on device /dev/hdb
Block grace time: 7days; Inode grace time: 7days
Block limits File limits
User used soft hard grace used soft hard grace
root ... 66 0 0 5 0 0
taylor .. 1578 7500 9000 2 3000 4000
```

## 7. 我们尚未涉及的唯一问题是如何在启动时自动打开配额，这样你就不用每次重启系统时都记得运行 quotaon 了。

我们稍微超前了一点（启动过程中读取的文件序列将在接下来的几个小时讲解），但简而言之，如果其中尚未包含启用配额的代码，你需要将以下行追加到你的 /etc/rc.local 文件中：

```
echo "Checking quotas. This may take a moment or two..."
/sbin/quotacheck -aguv

if [ $? -eq 0 ] ; then
 echo "Turning on disk quotas."
 /sbin/quotaon -aguv
else
 echo "*** Did not turn on disk quotas due to quotacheck errors."
fi
```

这会检查配额文件的格式是否有效，然后，如果一切正常（返回码，经测试为 $? 等于零），则打开配额管理系统。否则，会输出错误信息。

许多 Unix 系统管理员回避磁盘配额，更喜欢忽略这个问题或假设用户会妥善管理自己的磁盘空间。这在某些环境中可能是正确的，但一次性设置较大的磁盘配额然后不再理会，可能是更优雅的解决方案。如果没有人成为磁盘占用大户，你甚至会忘记配额的存在。但如果有人开始扩大文件系统使用量，系统会自动标记它并帮助避免更大的问题。

## 其他 Unix 系统上的配额细微差别

尽管在几乎所有现代 Unix 操作系统中启用磁盘配额的基本方法相同，但 Solaris 8 存在一些值得简要探讨的细微差别。

> 从 Mac OS X 的 Unix 级别设置磁盘配额相当棘手——棘手到本书无法深入探讨。基本挑战在于除根盘之外的磁盘都是由 autodiskmounter 挂载的，因此启用配额非常困难。完成之后，标准配额命令可用，正如 man -k 所证实的那样。希望随着 OS X 的成熟，启用配额也会变得更容易。如果你真的想深入研究，请从阅读 quotaon 手册页开始。

## 任务 12.2：其他系统上的配额

了解在特定版本的 Unix 上实现配额的细微差别的最佳方式，当然是阅读配额命令的手册页。

- 1. 让我们从那里开始，在 Solaris 系统上：

```
# man -k quota
edquota      edquota (1m)      - edit user quotas for ufs file system
quota        quota (1m)        - display a user's ufs file system disk quota
quotacheck   quotacheck (1m)   - ufs file system quota consistency checker
quotactl     quotactl (7i)     - manipulate disk quotas
quotaoff     quotaon (1m)      - turn ufs file system quotas on and off
quotaon      quotaon (1m)      - turn ufs file system quotas on and off
repquota     repquota (1m)     - summarize quotas for a ufs file system
rqquotad     rqquotad (1m)     - remote quota server
```

这些命令看起来肯定很熟悉，对吧？

> 实际上，这里列出并值得了解的一个命令是 rqquotad，它使你能够在共享的 NFS（网络文件系统）磁盘上使用配额。

Solaris 版本的 quota 仅报告用户超出软限制的磁盘，因此他们最好养成使用 -v 标志的习惯，该标志会报告所有启用配额的磁盘上的状态，无论是否超限。或者，你也可以将其设为系统范围的 shell 别名。

- 2. 我们需要做的第一个更改是编辑 /etc/vfstab（注意不是 fstab，而是 vfstab），在挂载时选项列表中添加 rq。然后，不是创建 quota.user 和 quota.group，而是简单地创建一个名为 quotas 的单个文件：

```
# cd /export/home
# touch quotas ; chmod 600 quotas
```

现在，卸载磁盘并重新挂载它；然后使用 edquota 为用户设置配额。edquota 命令本质上是相同的，尽管编辑器中显示的信息实际布局略有不同。

- 3. 接下来，使用 quotacheck 确保一切设置正确。Solaris 版本的 quotacheck 在理解的标志上有所不同。要获得与 Linux 中 -aguv 相同的效果，使用 -pva，它还有额外好处，即可以并行检查配额，这可能会快得多！

```
# quotacheck -pva
*** Checking quotas for /dev/rdsk/c0d0s7 (/export/home)
#
```

repquota 报告启用配额的设备上用户的情况：

```
# repquota -a
/dev/dsk/c0d0s7 (/export/home):

               Block limits          File limits
User   used  soft   hard  timeleft   used  soft  hard  timeleft
taylor  0   5000   7500            0     0     0
```

- 4. 用户 taylor 在 Solaris 机器上使用 quota 会看到以下内容：

```
$ /usr/sbin/quota
$
```

记住，没有 -v 标志时它只报告用户超额的系统。再试一次：

```
$ /usr/sbin/quota -v
Disk quotas for taylor (uid 100):
Filesystem  usage  quota  limit  timeleft  files  quota  limit  timeleft
/export/home  0   5000   7500          0     0     0
```

许多系统管理书籍建议你不要费心使用磁盘配额，因为它们已过时或没人真正使用。我不同意。如果你的系统是多用户系统，为确保资源公平共享，设置高但有意义的磁盘配额符合每个人的利益。如果你先于分配账户设置好这一点，以后就不用再与不满的用户争吵了！
