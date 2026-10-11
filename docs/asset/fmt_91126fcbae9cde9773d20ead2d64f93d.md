
# This completes our travels

状态值在 `for` 列表中没有按照特定顺序排列。`for` 命令的输出被管道到 `sort` 命令，这更改了 `for` 输出的顺序。运行脚本确实显示输出在脚本内部已被正确排序。

## 实际示例

现在你已经了解了如何在 shell 脚本中使用不同的方法来创建循环，让我们来看一些如何使用它们的实际示例。循环是遍历系统数据的常用方法，无论是文件夹中的文件，还是文件中包含的数据。这里有几个演示如何使用简单循环处理数据的示例。

### 查找可执行文件

当你从命令行运行程序时，Linux 系统会搜索一系列文件夹来查找它。这些文件夹定义在 `PATH` 环境变量中。如果你想找出系统中有哪些可执行文件供使用，只需扫描 `PATH` 环境变量中的所有文件即可。手动完成这可能需要一些时间，但编写一个小脚本来完成它就轻而易得了。

第一步是创建一个 `for` 循环来遍历存储在 `PATH` 环境变量中的文件夹。当你这样做时，不要忘记设置 `IFS` 分隔符：

```bash

IFS=

for folder in $PATH

done

```

现在你已经在 `$folder` 变量中拥有了各个文件夹，你可以使用另一个 `for` 循环来遍历该特定文件夹内的所有文件：

```bash

for file in $folder/*

done

```

## 第二部分：Shell 脚本基础

最后一步是检查单独的文件是否设置了可执行权限，你可以使用 `if-then` 脚本功能来实现：

```bash

if [ -x $file ]

then

echo "$file"

fi

```

搞定！将所有内容结合起来，脚本如下：

```bash

$ cat test25

#!/bin/bash

# finding executable files

IFS=

for folder in $PATH

do

  echo "$folder:"

  for file in $folder/*

  do

    if [ -x $file ]

    then

      echo "$file"

    fi

  done

done

```

脚本的输出是：

```bash

$ ./test25

/bin:

/bin/bash

/bin/alias

/bin/awk

/bin/awk

/bin/bash

/bin/cat

/bin/cd

/bin/column

/bin/cp

/bin/diff

/bin/du

/bin/echo

/bin/env

/bin/false

/bin/fold

/bin/find

/bin/free

/bin/grep

/bin/hash

/bin/id

/bin/kill

/bin/less

/bin/ln

/bin/local

/bin/mail

/bin/mkdir

/bin/notify

/bin/mv

/bin/od

/bin/ps

/bin/path

/bin/python

/bin/python

/bin/read

/bin/ruby

/bin/rm

/bin/sed

/bin/sh

/bin/sort

/bin/su

/bin/sum

/bin/stat

/bin/tar

/bin/test

/bin/tty

/bin/tmp

/bin/uname

/bin/vi

/bin/wc

/bin/which

/bin/x

/bin/zip

/bin/bash

/bin/bash

/bin/alias

/bin/awk

/bin/awk

/bin/bash

/bin/cat

/bin/cd

/bin/column

/bin/cp

/bin/diff

/bin/du

/bin/echo

/bin/env

/bin/false

/bin/fold

/bin/find

/bin/free

/bin/grep

/bin/hash

/bin/id

/bin/kill

/bin/less

/bin/ln

/bin/local

/bin/mail

/bin/mkdir

/bin/notify

/bin/mv

/bin/od

/bin/ps

/bin/path

/bin/python

/bin/python

/bin/read

/bin/ruby

/bin/rm

/bin/sed

/bin/sh

/bin/sort

/bin/su

/bin/sum

/bin/stat

/bin/tar

/bin/test

/bin/tty

/bin/tmp

/bin/uname

/bin/vi

/bin/wc

/bin/which

/bin/x

/bin/zip

/bin/bash

/bin/bash

/bin/alias

/bin/awk

/bin/awk

/bin/bash

/bin/cat

/bin/cd

/bin/column

/bin/cp

/bin/diff

/bin/du

/bin/echo

/bin/env

/bin/false

/bin/fold

/bin/find

/bin/free

/bin/grep

/bin/hash

/bin/id

/bin/kill

/bin/less

/bin/ln

/bin/local

/bin/mail

/bin/mkdir

/bin/notify

/bin/mv

/bin/od

/bin/ps

/bin/path

/bin/python

/bin/python

/bin/read

/bin/ruby

/bin/rm

/bin/sed

/bin/sh

/bin/sort

/bin/su

/bin/sum

/bin/stat

/bin/tar

/bin/test

/bin/tty

/bin/tmp

/bin/uname

/bin/vi

/bin/wc

/bin/which

/bin/x

/bin/zip

```

`while` 的目标是让生活更简单。为了将数据喂给 `while`，你只需要在结尾使用重定向符号。如下所示：

```bash

$ cat test26

#!/bin/bash

# Creating user accounts

input=users.csv

while IFS=', ' read -r userid name

do

  echo "adding $name"

  useradd -c "$name" -m $userid

done < "$input"

```

`users.csv` 文件如下：

```text

rich,Richard Blum

christine,Christine Bresahan

barbara,Barbara Blum

tim,Timothy Bresahan

```

运行该问题，必须是 root 用户，因为 `useradd` 命令需要 root 权限：

```bash

# ./test26

adding Richard Blum

adding Christine Bresahan

adding Barbara Blum

adding Timothy Bresahan

```

然后通过快速查看 `/etc/passwd`，你可以看到创建的账户：

```bash

# tail /etc/passwd

rich:x:1001:0:Richard Blum:/home/rich:/bin/bash

cristine:x:1002:0:Christine Bresahan:/home/christine:/bin/bash

barbara:x:1003:0:Barbara Blum:/home/barbara:/bin/bash

tim:x:1004:0:Timothy Bresahan:/home/tim:/bin/bash
