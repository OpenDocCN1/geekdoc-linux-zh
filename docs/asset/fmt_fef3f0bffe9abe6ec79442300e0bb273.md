
如果你之后想切换到 Evolution 或 Contact，你可以随时像后文“将邮件导入 Evolution”和“将邮件导入 Contact”章节中描述的那样，将你的 Thunderbird 邮件导入到这些应用程序中。

![](img/e3248f698da647444405a34229bd9df5_498_0.png)

## 将邮件导入 Thunderbird：现有用户

如果你一直在 Ubuntu 上使用 Thunderbird，并且正在从 Windows 系统小小部分迁移邮件，那么目录 `~/mozilla-thunderbird` 已经存在于你的 Ubuntu 系统家目录中了。该目录已经包含一个名为类似 `xxxxx` 的默认配置目录，以及你的配置初始化文件 `.ini`。

如果你想使用 Thunderbird 的导入功能将 Windows 系统的邮件导入到现有的 Thunderbird 邮件中，你将访问 Thunderbird 存储拷贝版本邮件的目录。这应该位于你备份了 `C:\Documents and Settings\Username\Thunderbird Profiles` 目录的 CD、DVD、外部驱动器或网络位置上。

你的邮件已经存储在该目录的一个子目录中，名称类似于 `xxxxx.default/Mail/Local Folders`，其中 `xxxxx` 是你第一次启动 Thunderbird 时生成的随机字符串。该目录下的文件包含你的邮件以及用于存储 Thunderbird 配置信息的辅助文件。要确定你需要导入哪些文件到 Thunderbird，请使用 Ubuntu 系统或控制台窗口，切换到 `xxxxx.default/Mail/Local Folders` 目录，并执行如下命令：

```bash
$ find -not -empty | grep -v '\.msf\.sbd|dat$'
~/Personal/Folders/Inbox
~/Personal/Folders/Personal
~/Personal/Folders/Writing
```

在这种情况下，`Inbox`、`Personal` 和 `Writing` 均为非零（即非空），并且包含你想要导入的邮件。命令的输出部分过滤掉了 Thunderbird 邮件摘要文件 (MSF)、邮件子目录 (SBD) 以及 Thunderbird 存储注册表和版本数据的 DAT 文件。

一旦你确定了包含要导入到现有 Thunderbird 邮件中的文件，你需要将这些文件拷贝到你现有的 Thunderbird 配置目录中，以便你能够从 Thunderbird 中访问它们。你可以通过两种方式之一来实现：

- 如果你的 Ubuntu 系统上没有重同名的 Thunderbird 邮件文件夹，你可以直接按其现有名称进行拷贝。

- 如果你的 Ubuntu 系统上已经有了同名的 Thunderbird 邮件文件夹，你必须拷贝 Windows 邮件文件夹并给它们赋予新名称，以防覆盖现有的同名 Thunderbird 邮件文件夹。

## 第二部分 Ubuntu 和 Kubuntu 桌面用户

为了安全起见，我总是使用第二种方法，因为很容易覆盖像 `Inbox` 这样具有重要名称的文件。在切换到 Windows 备份的 `xxxxx.default/Mail/Local` 目录后，执行如下命令会将之前识别的邮件文件夹拷贝到你的 Ubuntu 安装中，并为拷贝的文件夹添加 `-imported` 后缀：

```bash
cp ~/Personal/Folders.sbd/Inbox* \
~/mozilla-thunderbird/hf8dwpmj.default/Mail/Local\ Folders/Inbox-imported
~/Personal/Folders.sbd/Personal \
~/mozilla-thunderbird/hf8dwpmj.default/Mail/Local\ Folders/Personal-imported
~/Personal/Folders.sbd/Writing* \
~/mozilla-thunderbird/hf8dwpmj.default/Mail/Local/Writing-imported
```

对于多个邮箱来说，手动输入这些内容极其繁琐，因此以下是一个脚本，它需要 `-t` 参数来指定你正在迁移 Thunderbird 邮件，将你的配置目录名称作为参数，并为你完成操作：

```bash
#!/bin/bash

function usage {
    echo "Usage: import_thunderbird_mail.sh [-e] [-t profile-dir]"
    echo " -e : import Thunderbird mail into Evolution"
    echo " -t : import Thunderbird mail into Thunderbird"
    exit 1
}

if [ $# == 0 ]; then
    usage
    exit
fi

while getopts "t:e" opt
do
    case $opt in
        e)
            TARGETDIR=~/.evolution/mail/local
            ;;
        t)
            if [ $# -ne 1 ]; then
                echo "No Thunderbird profile directory specified."
                exit 1
            fi
            TARGETDIR=~/mozilla-thunderbird/$1/Mail/Local\
            ;;
        *)
            usage
            exit 1
            ;;
    esac
done
shift $((OPTIND - 1))

# 迁移逻辑
find . -not -empty | egrep -v '.msf|.sbd|.dat$|^.$' | \
while read mbox; do
    newmbox=$(echo "$mbox" | sed -e 's:.*::' -e 's/;$/imported')
    echo "Copying mbox to $newmbox"
    cp "$mbox" "$TARGETDIR/\$newmbox"
done
```

**注意**：你可以从我的网站 `vonhagen.org/scripts` 下载此脚本并从书中导入它。该脚本的名为 `import_thunderbird_mail.sh`。

要运行此脚本并将 Thunderbird/Outlook 创建的邮件导入到 Windows 系统，请先切换到备份了 `C:\Users\username\AppData\Local\Thunderbird\Profiles` 目录的 CD、DVD 或位置。你的邮件通常存储在该目录的一个子目录中，名称类似于 `xxxxx.default/Mail/Local Folders`，其中 `xxxxx` 是你第一次启动 Thunderbird 时生成的随机字符串。该目录包含了你用于存储 Thunderbird 配置的所有邮件邮件辅助文件。切换到 `xxxxx.default/Mail/Local Folders` 目录，并带有 `-e` 参数运行 `import_thunderbird_mail.sh` 脚本，表示你正在将邮件迁移到 Evolution。

下次启动 Evolution 时，你将看到新导入的文件，如图 12-4 所示。

## 图 12-4

Evolution 中现有和已导入的邮箱

![](img/e3248f698da647444405a34229bd9df5_502_0.png)

## 图 12-5

在 Evolution 导入向导中识别导入类型

![](img/e3248f698da647444405a34229bd9df5_502_1.png)

选择“导入单个文件”并点击“下一步”继续。将显示图 12-6 所示的对话框。

## 第二部分 Ubuntu 及桌面版 Ubuntu 用户

## 图 12-6

在 Evolution 导入向导中定位要导入的文件

![](img/e3248f698da647444405a34229bd9df5_503_0.png)

点击“文件”按钮将显示一个对话框，允许你浏览并选择想要导入的文件。你使用 Thunderbird 转换的文件应该位于 CD、DVD、外部驱动器或网络位置上，这些地方是你备份 `C:\Users\Username\AppData\Thunderbird\Profiles` 目录的地方。它们将位于该目录下名为 `xxxxx.default/Mail/Local Folders` 的子文件夹中，其中 `xxxxx` 是在你第一次启动 Thunderbird 时生成的随机字符串。
