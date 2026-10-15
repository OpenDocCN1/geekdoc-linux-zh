
```
$ sudo deleteuser snowy
Please change the password for account snowy to something new.
Changing password for user snowy.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
Account snowy has been suspended.
Files still left to remove (if any):
/var/log/dogbone.avi

Account snowy (uid 502) has been deleted, and their home directory (/home/snowy) has been removed.
```

Listing 5-20: 在用户 `snowy` 上测试 `deleteuser` 脚本

狡猾的 `snowy` 在 `/var/log` 中隐藏了一个 AVI 文件（`dogbone.avi`）。幸运的是我们注意到了这一点——谁知道那会是什么？

# Hacking the Script

此 `deleteuser` 脚本是有意不完整的。你应该决定采取哪些额外步骤——是否压缩并归档账户文件的最终副本，将其写入磁带，备份到云服务，刻录到 DVD-ROM，甚至直接邮寄给 FBI（希望我们只是开玩笑说最后一点）。此外，账户需要从 `/etc/group` 文件中删除。如果用户主目录之外存在零散文件，`find` 命令可以识别它们，但最终由系统管理员检查并酌情删除每个文件。

此脚本的另一个有用补充是 `dry-run` 模式，允许你在实际执行用户删除之前查看脚本将从系统中删除的内容。

## 验证用户环境

由于人们会将登录、配置文件和其他 shell 环境自定义设置从一个系统迁移到另一个系统，因此这些设置逐渐衰减的情况并不少见；最终，`PATH` 可能包含系统中不存在的目录，`PAGER` 可能指向不存在的二进制文件，更糟糕的是。

解决此问题的复杂方案是首先检查 `PATH` 以确保它仅包含系统上的有效目录，然后检查每个关键辅助应用程序设置，以确保它们要么指示一个存在完全限定文件，要么指定 `PATH` 中的二进制文件。这在 Listing 5-21 中有详细说明。

### The Code

```
#!/bin/bash
# validator--Ensures that the PATH contains only valid directories
# and then checks that all environment variables are valid.
# Looks at SHELL, HOME, PATH, EDITOR, MAIL, and PAGER.
errors=0

source library.sh # This contains Script #1, the in_path() function.

validate() {
  varname=$1
  varvalue=$2

  if [ ! -z $varvalue ] ; then
    if [ "$(varvalue%$(varvalue%?)/" )" != "/" ] ; then
      echo "*** $varname set to $varvalue, but I cannot find executable."
      errors=$(($errors + 1))
    fi
  else
    if in_path $varname $PATH ; then
      echo "*** $varname set to $varvalue, but I cannot find it in PATH."
      errors=$(($errors + 1))
    fi
  fi
}

# BEGIN MAIN SCRIPT
# ================

if [ ! -x $SHELL ] ; then
  echo "*** SHELL set to $SHELL, but I cannot find that executable."
  errors=$(($errors + 1))
fi
```

```
if [ ! -d ${HOME:?"You need to have your HOME set to your home directory"} ]
then
    echo "** HOME set to $HOME, but it's not a directory."
    errors=$(($errors + 1))
fi

# Our first interesting test: Are all the paths in PATH valid?

oldIFS=$IFS; IFS=":"   # IFS is the field separator. We'll change to ':'.

for directory in $PATH
do
    if [ ! -d $directory ] ; then
        echo "** PATH contains invalid directory $directory."
        errors=$(($errors + 1))
    fi
done

IFS=$oldIFS            # Restore value for rest of script.

# The following variables should each be a fully qualified path,
#   but they may be either undefined or a progname. Add additional
# # variables as necessary for your site and user community.

validate "EDITOR" $EDITOR
validate "MAILER" $MAILER
validate "PAGER" $PAGER

# And, finally, a different ending depending on whether errors > 0

if [ $errors -gt 0 ] ; then
    echo "Errors encountered. Please notify sysadmin for help."
else
    echo "Your environment checks out fine."
fi

exit 0
```

> 清单 5-21：验证器脚本

## 工作原理

此脚本执行的测试并不复杂。为了检查 `PATH` 中的所有目录是否有效，代码会逐一遍历每个目录，确保它存在 ⑥。请注意，在 ⑤ 处必须将内部字段分隔符（`IFS`）改为冒号，以便脚本能够正确遍历 `PATH` 中的所有目录。按照惯例，`PATH` 变量使用冒号来分隔其中的各个目录：

```
$ echo $PATH
/bin:/sbin:/usr/bin:/sw/bin:/usr/X11R6/bin:/usr/local/mybin
```

为了验证环境变量值是否有效，`validate()` 函数 ② 首先检查每个值是否以 `/` 开头。如果是，该函数将检查该变量是否为可执行文件。如果不是以 `/` 开头，脚本将调用 `in_path()` 函数——该函数是从我们在第 11 页脚本 #1 中开始使用的库中导入的 ①——以查看在当前 `PATH` 的某个目录中能否找到该程序。

此脚本最不寻常的地方在于它在某些条件语句中使用默认值，以及使用变量切片。它在条件语句中使用默认值的例子是 ③ 处的行。符号 `${varname:?'errorMessage'}` 可以理解为：“如果 `varname` 存在，则替换为其值；否则，以错误信息 `errorMessage` 失败退出。”

在 ③ 处使用的变量切片符号 `${varvalue%${varvalue%?}}` 是 POSIX 子字符串函数，它只产生变量 `varvalue` 的第一个字符。在此脚本中，它用于判断环境变量是否具有完整限定文件名（即以 `/` 开头并指定二进制文件路径的名称）。

如果你的 Unix/Linux 版本不支持这两种符号中的任何一种，可以直接替换它们。例如，可以用下面的代码来替代 `${SHELL:?'No Shell'}`：

```
if [ -z "$SHELL" ] ; then
echo "No Shell" >&2; exit 1
fi
```

而对于 `{varvalue%${varvalue%?}}`，你可以使用以下代码实现相同的结果：

```
$(echo $varvalue | cut -c1)
```

## 运行脚本

这是一段用户可以运行来检查自身环境的代码。如清单 5-22 所示，它没有任何启动参数。

## 结果
