

![](img/0c1fc10350aa06ca92e7921c96c628ec_218_0.png)

## Figure 12-2 A safe way to purge unneeded files in your tmp directory

确认每一项删除操作。如果想要更强制的版本，可以尝试 Figure 12-3 中所示的 purge!.ksh。

当然，你可能也想为它设置别名。所以我们有这个别名：

```
alias purge!=`$HOME/bin/purge!.ksh`
```

现在，每当我们想清理目录中较旧的文件，并且确定其中没有任何我们真正关心的文件时，我们只需使用 purge! 来删除 tmp 目录中至少七天旧的所有文件。

## Can I add purge! to my crontab?

我们通常并不赞成自动进行这种绝对清理，但如果你是懒散的类型，或者绝对确定 tmp 目录中的文件可以被删除，你可以考虑在有权限使用 cron 进程的情况下将其添加到你的 crontab 中。一种做法是只在每周星期日晚上运行。这样，你就知道目录中没有文件超过两周旧，但上周的文件尚未被删除。对应的 crontab 条目为

```
0 1 * * 0 $HOME/bin/purge!.sh
```

![](img/0c1fc10350aa06ca92e7921c96c628ec_219_0.png)

Figure 12-3 The purge-bang script is for when you are really sure

嗯，也许你注意到了一个变化？名称已从 purge!.ksh 变为 purge!.sh。这当然是有意为之。当 cron 运行你的 crontab 文件时，它只使用基本的 Bourne shell 来执行。因此，我们相应地修改了脚本，如 Figure 12-4 所示。

> Note: New releases of some flavors of UNIX are using the Posix shell for cron. The Korn shell is compliant with Posix, so your crontab scripts must be either Korn shell or Posix shell. The man pages for cron will tell you which shell is used.

然而，你不想在真正、非常想删除文件时，自己却没有办法运行真正的 rm 命令。所以再使用另一个别名，这次是 rm!，以保持我们一直使用的惯例。

```
alias rm!=''/bin/rm''
```

这使用了 rm 命令的绝对路径，可以绕过任何可能存在的外部脚本，直接访问源文件。

```
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
```

**Figure 12-4** When you run a script from your **crontab**, you have to use the Bourne shell

## What’s the very best way to protect crucial files against accidental erasure?

保护文件免于意外删除，甚至更糟的蓄意破坏的一个重要方法是使用 UNIX 内置的保护机制。

第一步是使真正重要的文件变为只读。这很容易做到，并且可以为你节省大量麻烦。如果你有不需要更改但需要定期访问的文件，请更改其权限，使任何人——甚至你自己——都无法写入。

```
`chmod a-w filename`
```

现在，该文件在不采取额外步骤的情况下无法被更改，即使是由你所有者也是如此。当然，你可以通过在更改文件前先更改权限来绕过这一点。但你已经使这个过程变得足够繁琐，以至于不太可能意外执行。

> **Warning:** The superuser can delete your file no matter what you do. This is one of those sad but true facts. No matter how much protection you put on a file, the superuser can blithely delete the file or change it, with barely a moment’s thought. Yet another reason to stay on friendly terms with this person.

目录——除非有人知道你的密码。
另一个保持密码安全的好理由。

> Warning: Don't forget to change your $HOME directory as well. It's easy enough to protect your own directories, but also easy to forget to change the home directory itself.

```
chmod 700 $HOME
```

将只更改你的主目录，使任何人都无法随意窥探。

## BACKUP, BACKUP, BACKUP!

## UNIX and Backups

所有这些防止意外删除文件或在不打算更改时更改文件的技巧都很棒，我们强烈建议你使用其中的一些组合。但当灾难发生时，没有什么能比得上经过验证的备份。系统管理员对备份负有主要责任，但每个使用计算机的人都需要对自己关键文件的备份负责。这并不难，也不必繁重，而且可能成为救命稻草。

UNIX 的美妙之处在于，你通常不必担心备份程序或庞大的数据文件，因为这些通常是系统管理员的职责范围。但你确实需要考虑自己的本地数据文件。你使用的方法将取决于系统的功能、可用硬盘空间的大小，以及系统上对个人用户可用的程序和媒体。但大多数系统都有足够的硬盘空间供你至少在硬盘上维护一份最新工作的副本，如果你有访问权限和权限，复制这些文件到软盘上也相当容易。使其无痛的关键是只备份你需要的内容，然后经常进行备份。个人而言，我们更喜欢大约每天两次备份当前工作文件，但你需要决定什么适合你。许多用户喜欢将其作为注销例程的一部分进行自动化，而 C shell 甚至为此目的有一个特殊文件——.logout。但如果你使用 Korn shell，你将需要创建自己的等效文件。在我们深入了解如何自动化备份的具体细节之前，让我们先看看你可以，也应该做的备份类型。

