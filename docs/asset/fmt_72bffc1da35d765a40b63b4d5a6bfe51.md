
管理员可用于提高 Linux 系统安全性的最基本工具之一是 `sudo` 命令。该命令允许你授予用户特定权限，而无需给予他们完全的 root 访问权限。例如，如果你想允许用户在本地工作站上挂载 CD-ROM，你可以配置 `sudo` 允许他们此权限。`sudo` 命令通过查阅配置文件工作，该文件指定用户被允许运行的系统和命令。如果用户输入的命令不是他被授予访问权限的命令，则会向系统管理员发送警告消息，指出用户尝试的命令。如果用户有权运行指定命令，他会被提示输入自己的密码，输入后命令将以 root 权限执行。你会认为如此有用的命令会包含在 Red Hat Linux 发行版中；然而，它没有。它可从 Red Hat FTP 服务器和镜像的贡献软件目录中获得，名为 `sudo-x.x.x-x.i386.rpm`，其中 `x.x.x-x` 是版本号，目前为 `1.6.1-1`。你也可以从 `sudo` 主页 at `http://www.courtesan.com/sudo/` 获取 `sudo` 的最新版本。

该软件包不仅包括 `sudo` 命令，还包括一个初始 `sudoers` 文件和 `visudo`，用于编辑 `sudoers` 文件的实用程序。`sudoers` 文件是授予用户权限的机制，应仅使用 `visudo` 命令进行编辑。本章后面将讨论此文件的语法。为了更好地了解 `sudo` 能为你做什么，让我们先看看表 27.1 中的一些命令行选项。

## 表 27.1 `sudo` 命令行选项

| 选项 | 描述 |
|---|---|
| `-V` | 打印 `sudo` 版本并退出。 |
| `-l` | 列出用户被允许运行的命令以及明确禁止的命令。 |
| `-h` | 打印使用消息并退出。 |
| `-v` | 更新用户的 `timestamp` 文件。`timestamp` 文件提供一种机制，以便一旦你通过身份验证，就有一个超时期限，在此期间你无需重新验证。 |
| `-k` | 删除用户的 `timestamp` 文件。这是在用户 `.logout` 文件中使用的一个好选项。 |
| `-b` | 在后台运行指定的命令。由于 shell 作业控制无法用于此操作，因此需要此选项。 |
| `-p prompt` | 用 `prompt` 指定的密码提示覆盖默认密码提示。 |
| `-u username/#uid` | 以 `username` 或数字 `uid` 指定的用户身份运行指定的命令。 |
| `-s` | 如果设置了，则运行 `SHELL` 环境变量指定的 shell，否则运行 `/etc/passwd` 文件中指定的 shell。 |
| `-H` | 将 `HOME` 环境变量设置为 `/etc/passwd` 中指定的目标用户的主目录。 |
| `--` | 强制 `sudo` 停止处理命令行参数。 |

正如你可能从选项列表中推断的那样，`sudo` 命令有许多应用场景。立即想到的一个用途是创建操作员菜单脚本。示例操作员菜单脚本显示在列表 27.1 中。此菜单向用户提供运行备份软件、添加新用户、禁用用户账户、重启打印机、重启所有打印机以及退出菜单的选项。它相对粗糙，但经过一点工作后，可用于允许新手操作员执行这些任务，而无需给予他们 root 账户访问权限。通过创建你希望操作员能够运行的命令菜单，并在 `sudoers` 文件中授予操作员对这些命令的访问权限，你可以让一个非特权账户运行特定的一组特权命令。

## 列表 27.1 示例操作员菜单脚本 `opermenu.sh`

```bash
#!/bin/bash

trap "" 1 2 3 15

function new_user {
  # Prompt for the desired username
  printf "\nEnter the desired username: "
  read username

  EXISTS=`grep "^$username:" /etc/passwd`
  if [ "$EXISTS" != "" ]; then
    printf "\nUsername requested already exists...exiting.\n"
    sleep 1
    return
  fi

  printf "\n"

  # Prompt for primary group
  printf "\nEnter the primary group for this user (default $username): "
  read group

  if [ "$group" == "" ]; then
    group=`echo $username`
    creategroup=1
  else
    GEXISTS=`grep "^$group:" /etc/group`
    if [ "$GEXISTS" == "" ]; then
      printf "\nGroup $group does not exist...create it (y/n): "
      read yesno

      if [ "$yesno" != "y" ]; then
        printf "\nFATAL USER CREATION ERROR...aborting.\n"
        sleep 1
        return
      else
        creategroup=1
      fi
    fi
  fi
```

## 列表 27.1 继续

```bash
printf "\n"

# Prompt for the users real name
printf "\nEnter the users real name: "
read realname

printf "\n"

# Prompt for the users home directory
printf "\nEnter the users home directory (default /home/$username): "
read homedir

if [ "$homedir" = "" ]; then
    if [ -d /home/$username ]; then
        printf "\nDirectory /home/$username exists...use anyway (y/n): "
        read yesno

        if [ "$yesno" != "y" ]; then
            printf "\nFATAL USER CREATION ERROR...aborting.\n"
            sleep 1
            return 1
        fi
    fi
    homedir=`echo /home/$username`
fi

printf "\n"

# Prompt for the users shell
printf "\nEnter the users shell (default /bin/bash): "
read shell

if [ "$shell" = "" ]; then
    shell="/bin/bash"
else
    if [ -x $shell ]; then
        VALIDSHELL=`grep $shell /etc/shells`
        if [ "$VALIDSHELL" = "" ]; then
            printf "\nInvalid shell for user...aborting.\n"
            return 1
        fi
```
