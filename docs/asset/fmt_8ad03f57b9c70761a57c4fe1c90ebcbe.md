
[yY][eE][sS]) RESPONSE=y ;;

[nN][oO]) RESPONSE=n ;;

esac

}

```

这里有两个问题。第一个是 `read` 命令

```
read RESPONSE
```

如果用户只是按 Enter 或 Return，则不会为 `$RESPONSE` 设置值。由于你无法更改 `read` 命令，你需要找到解决该问题的不同方法。

问题。基本上你有一个逻辑问题——`case` 语句需要验证用户输入，而它目前并未执行此操作。解决问题的简单方法是按如下方式更改 `YesNo`：

```
YesNo() {

  echo "$1 (y/n)? \c"

  read RESPONSE

  case "$RESPONSE" in

    [yY][Ee][Ss]) RESPONSE=y ;;

    *) RESPONSE=n ;;

  esac

}
```

现在你将除 "yes" 之外的所有响应都视为否定响应。这包括用户简单地输入 Enter 或 Return 时生成的空响应。

### 使用调试钩子

在之前的示例中，你能够使用 shell 追踪推断出 bug 的位置。为了为脚本的特定部分启用追踪，你必须编辑脚本并插入 `debug` 命令：

```
set -x
```

对于较大的脚本，更好的做法是嵌入调试钩子。调试钩子是能够在关键代码段中启用 shell 追踪的函数。调试钩子通常以两种方式之一激活：

- 使用命令行选项（通常为 `-d` 或 `-x`）运行脚本。
- 使用环境变量设置为 `true` 运行脚本（通常为 `DEBUG=true` 或 `TRACE=true`）。

以下函数允许你通过将 `DEBUG` 设置为 `true` 来激活和停用调试：

```
Debug() {

  if [ "$DEBUG" = "true" ] ; then

    if [ "$1" = "on" -o "$1" = "ON" ] ; then

      set -x

    else

      set +x

    fi

  fi

}
```

要激活调试，可以使用以下命令：

```
Debug on
```

要停用调试，可以使用以下任一命令：
`Debug`
`Debug off`

实际上，向此函数传递除 `on` 或 `ON` 之外的任何参数都会停用调试。

![](img/3def70414996f811615f713b2077a154_353_0.png)

> 关于调试的常规做法是仅在必要时激活它。默认情况下，调试应处于关闭状态。

为了演示此函数的使用，你可以修改脚本 `buggy3.sh` 中的函数，使其在变量 `DEBUG` 被设置时自动启用调试。`buggy3.sh` 的修改版本如下：

```
#!/bin/sh

Debug() {

  if [ "$DEBUG" = "true" ] ; then

    if [ "$1" = "on" -o "$1" = "ON" ] ; then

      set -x

    else

      set +x

    fi

  fi

}

Failed() {

  Debug on

  if [ "$1" -ne 0 ] ; then

    echo "Failed. Exiting." ; exit 1 ;

  fi

  echo "Done."

  Debug off

}

YesNo() {

  Debug on

  echo "$1 (y/n)? \c"

  read RESPONSE

  case "$RESPONSE" in

    [yY]|[yY][eE][sS]) RESPONSE=y ;;

    *) RESPONSE=n ;;

  esac

  Debug off

}

YesNo 'Make backup'

if [ "$RESPONSE" = "y" ] ; then
```

```
echo 'Deleting old backups, please wait... \c'

rm -r backup > /dev/null 2>&1

Failed $?

echo 'Making new backups, please wait... \c'

cp -r docs backup

Failed $?

fi
```

如果脚本以以下任一方式执行，输出不会发生变化：

```
$ /bin/sh ./buggy3.sh

$ ./buggy3.sh
```

如果以以下任一方式执行同一脚本，则输出包含 shell 追踪：

```
$ DEBUG=true /bin/sh ./buggy3.sh

$ DEBUG=true ./buggy3.sh
```

### 摘要

在开发或维护大型 shell 脚本的过程中，你需要查找并修复其中的错误。本章介绍了如何使用 shell 来促进此任务。涵盖的一些主题包括：

- 启用调试
- 使用 `sh -n` 和 `sh -nv` 进行语法检查
- 使用 shell 追踪查找语法和逻辑错误
- 在 shell 脚本中嵌入调试钩子

通过学习调试 shell 脚本所使用的技术，你可以修复自己的脚本并维护其他程序员编写的脚本。

### 问题

- 1. 在 shell 脚本中启用调试的三种主要形式是什么？
- 2. 增强本章给出的 `Debug()` 函数，以便在调试停用后程序员必须按 Enter 或 Return。

当你调试包含数十个函数的脚本时，此功能使你能够在执行下一个函数之前研究特定函数的调试输出。

### 术语

`调试钩子` 在关键代码段中启用 shell 追踪的函数。

`执行追踪` 参见 shell 追踪。

`调用激活` 在脚本被调用时生效的调试模式的启用方法。

`程序员激活` 仅当 shell 脚本程序员使用 `set` 命令时才激活的调试模式。

`Shell 追踪` 每个命令都以其执行的确切形式打印。

`语法检查` 在不执行脚本的情况下验证其语法的过程。

## 第 21 小时

![](img/3def70414996f811615f713b2077a154_356_0.png)

### 使用函数解决问题

在之前的章节中，你编写了执行特定任务的简短 shell 脚本。这些脚本中的许多执行了常见的操作，例如显示错误和警告消息以及提示用户输入。为了轻松重复这些任务，你为脚本创建了可重用的函数。

在本章中，你将此步骤更进一步，创建一个可在 shell 中 readily 重用的函数库。库是 shell 脚本可以访问的函数的存储库。你将检查的与库相关的具体主题是

- 库基础
- 创建库

### 库基础

在这本书的许多脚本中，你创建了显示错误消息并提示用户输入的实用函数。当两个脚本需要

使用相同的函数，你只是把函数从一个脚本复制到另一个脚本。这种方法在处理一两个脚本时效果很好，但在处理大量脚本时就会失效。假设你有一打脚本共享同一个函数，并且你在该函数中发现了一个错误。你可以想象修复所有这些脚本会有多困难。通用函数的存储库或库可以降低开发和维护这些 shell 脚本的复杂性。

### 什么是库？

创建函数库与创建 shell 脚本完全一样。脚本与库之间的唯一区别在于，库只包含函数定义，而脚本可以同时包含函数定义和可执行代码。脚本中的可执行代码由脚本中函数定义之外的所有命令组成。

在下面的 shell 脚本中，第 1、2 和 4 行是可执行代码：

```sh
1 #!/bin/sh
2 MSG="hello"
3 echo_error() { echo "ERROR:" $1 ; }
4 echo_error $MSG
```

第 3 行包含函数定义，不是可执行代码。

库不包含任何可执行代码；它只包含函数定义。例如，下面是一个库：

```sh
#!/bin/sh
echo_error() { echo "ERROR:" $1 ; }
echo_warning() { echo "WARNING:" $1 ; }
```

严格来说，没有什么能阻止库包含可执行代码；脚本与库之间的区别纯粹是概念上的。

### 使用库

你可以使用 `.` 命令在脚本中访问作为库定义的函数。其语法是

`. file`

这里，`file` 是库的路径名。当库通过 `.` 命令访问时，被称为 sourced 或 loaded。如果 `file` 不是有效的路径名或不是脚本，shell 将显示错误消息然后退出。因此，大多数脚本在执行任何命令之前都会先加载所有库。

例如，如果前一个示例中给出的函数存储在名为 `messages.sh` 的文件中，可以使用以下命令加载它们：

```sh
. messages.sh
```

你可以重写脚本

```sh
1 #!/bin/sh
2 MSG="hello"
3 echo_error () { echo "ERROR: $1" ; }
4 echo_error $MSG
```

以使用库 `messages.sh` 如下：

```sh
1 #!/bin/sh
2 . $HOME/lib/sh/messages.sh
3 MSG="hello"
```
