
## 列表 6.1 一个将用户添加到系统的简单脚本

```bash
#!/bin/bash
# dlu - a simple script for adding users.
#print out the info for the user editing the account
if [ -z "$1" ]; then
      echo "usage: dlu <username>"
      echo
      exit
fi
# Check to see if the account exists
# If so, print out the name and user id
grep "$1:" /etc/passwd
if [ "$?" = "0" ]; then
      echo "Invalid username: user $1 already exists."
      echo
      exit
fi
# Check for a valid user name
if [ "$2" = "" ]; then
      echo
      echo "The user name field cannot be empty."
      echo
      exit
fi
# Check to see if the user name is valid
# Valid usernames are alphanumeric plus dash, underscore, and period
# Also, the first character must be a letter
echo -n "Please enter the user's full name: "
read FULLNAME
# Prompt for the group
if [ "$3" = "" ]; then
      echo -n "Please enter type of account (e,p,b,v,i,f,d): "
      read ATYPE
else
      ATYPE="$3"
fi
QNAME=""
GRP=0
if [ "$ATYPE" = "p" ]; then       QNAME=personal;       GRP=2000; fi
if [ "$ATYPE" = "b" ]; then       QNAME=business;       GRP=3000; fi
if [ "$ATYPE" = "e" ]; then       QNAME=e-mail;         GRP=500;  fi
if [ "$ATYPE" = "v" ]; then       QNAME=virtual;         GRP=4000; fi
if [ "$ATYPE" = "i" ]; then       QNAME=isdn;           GRP=1000; fi
if [ "$ATYPE" = "f" ]; then       QNAME=free;           GRP=5000; fi
if [ "$ATYPE" = "d" ]; then       QNAME=dsl;            GRP=6000; fi
if [ "$GRP" = "0" ]; then
      echo "Invalid account type: $ATYPE"
      echo
      exit
fi
# Use the useradd command and set quotas
echo ".. useradd -d \`/home/$FL/$1" -s /bin/bash -c "$FULLNAME" -m "$1"\nuseradd -d "/export/home/$FL/$1" -s /bin/bash -c "$FULLNAME" -m "$1"
echo ".. passwd \`$1/"
passwd "$1"
if [ "$ATYPE" = "b" ]; then     mail $1 < /usr/sbin/guide_dial-up.txtxt
fi
echo
echo "Setup complete."
echo

# End of file
```

你将从前面的章节中认出许多 `useradd` 选项。此脚本为用户创建一个账户。它会提示管理员输入信息，例如用户名，然后将其与 `/etc/passwd` 文件进行检查，以查看是否已有其他用户占用了该名称。如果用户名可用，脚本会提示输入用户的全名，最后提示输入该用户应分配的组。在收集到必要信息后，脚本将使用 `useradd` 命令并输入所有收集到的信息。最后，脚本将为用户账户分配配额，并发送一封文本电子邮件解释一些基本功能。

像这样的脚本处理了一些通常你需要手动处理的功能。它还展示了 Linux 中的其他独特创新，例如根据用户请求的账户类型将其分配到特定组，并向他们发送带有相应说明的电子邮件。

列表 6.2 中的脚本有助于手动删除任何流氓账户。它短得多，因为正如你在使用 Linux 时会发现的，删除文件比创建文件容易得多。与列表 6.1 中的脚本一样，此脚本也有一个简短的名称，简要描述了其功能。然而，名称并不是脚本最重要的方面。你可以将名称更改为最能描述其内容或适合其目的的名称。

## 列表 6.2 一个从系统中移除用户的简单脚本

```bash
#!/bin/bash
# dlu - a simple script for deleting users.
#print out the info for the user editing the account
if [ -z "$1" ]; then
echo "usage: dlu <username>"
echo
exit
fi
# Check to see if the account exists
# If so, remove the directories
grep "$1:" /etc/passwd
if [ "$?" = "0" ]; then
echo
	echo "Deleting user $1 ... "
	FL=`echo "$1" | cut -c1`
	userdel "$1"
	echo
	echo "Removing directory /home/$FL/$1"
	rm -r /home/$FL/$1
	echo
	echo "Removing /var/spool/mail/$1"
	rm /var/spool/mail/$1
	echo
	echo "User $1 deleted."
	echo
	exit
else
	echo "Sorry, user $1 does not exist"
	echo
	exit
fi
```

请记住，`/usr/sbin/usermod` 命令允许 root 用户修改现有账户。正确使用该命令相关的标志将能够更改用户的 shell、目录和识别名称。但是，如前所述，你也可以手动编辑 `/etc/passwd` 文件，除非你认为有必要，否则通常不建议这样做。

## 使用 GUI 工具

Red Hat 预装的命令行工具足以满足大多数管理任务。然而，由于 Linux 是一个正在发展的操作系统，并且每个管理员都希望以自己的方式完成其任务，因此许多开发人员正在开发新的可点击界面，提供图形格式来完成与命令行工具相同的任务。快速浏览 Freshmeat ([http://www.freshmeat.net/](http://www.freshmeat.net/)) 或 Linuxberg ([http://www.linuxberg.com](http://www.linuxberg.com)) 的首页，这些网站托管了广泛的开发人员工具，可以迅速看出当前市场上程序的多样性。大多数程序可供下载。

幸运的是，Red Hat 在默认安装中提供了一个非常通用且强大的客户端。Linuxconf 现在被视为大多数配置任务的默认工具。大多数 Linux 发行版，包括 Red Hat，都提供较旧的工具来修改配置文件，但随着要求更用户友好界面的新 Linux 用户数量不断增加，这些 GUI 程序为那些仍在努力掌握 Linux 复杂性的用户带来了令人欣慰的缓解。

## 使用 Linuxconf 编辑账户

Linux 管理工具的最新进展之一是一个名为 Linuxconf 的工具。Linuxconf 首次随 Red Hat 5.1 一起提供，并已被证明是希望更好地调整和系统中工具和管理用户的福音。它不仅有助于配置 Linux 操作系统的几乎每个方面，而且易于使用，对刚开始学习 Linux 的初学者也很有帮助。用户账户管理只是 Linuxconf 能够操纵的所有功能的一个小方面。

如果你熟悉旧版本的 Red Hat，或者在旧版本的 Red Hat 发行版上积累了经验，你会认出 Linuxconf 中 Red Hat 控制面板的部分内容。虽然控制面板仍然可用于 Red Hat 和其他发行版，但其范围有限。它曾经是，现在仍然是一个出色的工具，用于设置打印机、启用调制解调器和拨号账户以及编辑网络配置，但在更改或修改用户账户方面有限。

Linuxconf 程序有多种版本。最常见的是基于 GNOME 的 Linuxconf，这也是本节将研究的版本。它正在迅速成为配置 Linux 系统大多数方面的标准。由于它处于持续和活跃的开发中，用户预计很快就能看到许多升级。本书中包含的屏幕截图基于最新的 Red Hat 版本。你可以期待每个新版本都会增加更多的选项和功能。

MANAGING USERS Chapter 6 191

## 理解 Linuxconf 版本

Linuxconf 不仅仅是一个编辑文件和用户变量的 GUI 工具。当然，它可以用于这些目的，但也可以用于控制系统各个方面。你还可以使用 Linuxconf 工具来配置守护进程和进程，如 Samba 和 sendmail。它是一个管理系统许多功能的高度通用工具。

你可以以四种不同的方式调用 Linuxconf 运行：

- **命令行。** 命令行模式允许你查看脚本，以便你可以正确编辑它们。如果你不喜欢 GUI 环境，这是首选模式。此外，熟悉脚本及其位置有助于你尝试远程更改设置或在没有 X Window 界面的情况下更改设置。命令行方法是访问远程系统并编辑设置的最快方式。你通常使用 xterm 窗口访问远程系统，而不是 X Window 环境或在系统控制台上。

- **字符单元。** 类似于旧版本的 Red Hat 安装程序，类似于 DOS 或 WordPerfect 5.1 环境，此模式允许你在不运行 X Window 的情况下访问设置，但仍提供编辑器的易用性和简洁性。这种使用 Linuxconf 的方法也是在控制台终端内或在 xterm 或相关终端窗口内解决的。

- **GNOME-Linuxconf。** 这也许是可识别性最强的界面，也是最容易使用的。你将在本节中更详细地检查此界面。该界面使用其中一个更好的窗口管理器 GNOME 的库。有关使用窗口管理器的更多信息，请参见第 12 章。

- **基于 Web 的。** 无论是 Netscape，它是一个图形 Web 浏览器，还是 Lynx，一个基于文本的浏览器，在编辑配置方面同样有效。

根据你的机器上 `$DISPLAY` 变量的设置，Linuxconf 通常以 GNOME-Linuxconf 或字符单元格式启动。更改此选项有助于确定你如何访问程序。基于 Web 的方法还将显示一个信息屏幕，向你展示访问程序的替代方法。仔细注意这些替代方法，因为此屏幕将只显示一次。
