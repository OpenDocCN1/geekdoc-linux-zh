
第一个是简单的条件判断；如果条件（`test -x $file`）为真，则执行后面的语句，即将 `$perm+execute` 赋值给变量 `perm`。如果条件不为真，shell 会跳到下一条指令继续执行。

第二个稍微复杂一些，但仍然容易理解：如果 `test -O $file` 为真，则执行第二行。否则，`else` 语句会使第四行（即“不属于 `$LOGNAME` 所有”）得到执行。

最后，第三个示例（`elif`）是以下嵌套结构的简写形式：

```sh
if test -d $file ; then
    echo "$file is a directory"
else
    if test -f $file ; then
        echo "$file is a file"
    else
        echo "$file doesn't exist"
    fi
fi
```

`elif` 的好处在于，它有助于避免复杂语句中过深的嵌套。可以想象，如果我们的脚本里有四五个 `else-if` 条件判断，最后十几行都是 `fi-fi-fi-fi`，看起来会很奇怪，而且可能让人困惑。

- **4.** 当然，处理一系列 `elif` 语句的一种方法是把这一系列语句转换成一个 `case` 语句，从而能以更优雅的方式针对多个不同的值进行测试。这在某些情况下有效，但在其他情况下则不然。

实际上，如果每个条件都针对不同的测试选项，那么它就行不通；但在许多情况下，当你针对多个可能值测试同一个变量或值时，`case` 语句是理想的选择。

下面是一个相当长且更复杂的 shell 脚本，用于演示 `case` 语句和条件语句的用法。请注意缩进如何帮助理清控制流：

```sh
#!/bin/sh

# DOCRON - simple script to run the daily, weekly and monthly
#          system cron jobs on a system where it's likely that
#          it'll be shut down at the usual time of day when
#          this would occur        For Mac OS X Unix only.
#
# By Dave Taylor <taylor@intuitive.com>
# Note: most of this is copied from /etc/crontab

SHELL=/bin/sh
PATH=/bin:/sbin:/usr/bin:/usr/sbin
HOME=/var/log

if [ "$#" -ne 1 ] ; then
  echo "Usage: `basename $0` [daily|weekly|monthly]"
  exit 0
fi

if [ "`id -u`" -ne 0 ] ; then
  echo "Please enter your 'sudo' password for authorization"
  sudo $0 $1
  if [ $? -ne 0 ] ; then
    echo "(didn't run `basename $0` because sudo auth failed)"
  fi
  exit 0
fi

case $1 in
  daily )
    sh /etc/daily  2>&1 | tee /var/log/daily.out | \
      mail -s "`hostname` daily output" root
    ;;
  weekly )
    sh /etc/weekly  2>&1 | tee /var/log/weekly.out | \
      mail -s "`hostname` weekly output" root
    ;;
  monthly )
    sh /etc/monthly 2>&1 | tee /var/log/monthly.out | \
      mail -s "`hostname` monthly output" root
    ;;
  * ) echo "Usage: `basename $0` [daily|weekly|monthly]"
esac

exit 0
```

这是一个较长的 shell 脚本，但如果分段来看，它并不比前面的示例更复杂。特别要注意的是，`case` 语句的结构是

```
case $1 in
  daily ) statements
  ;;
  weekly ) statements
  ;;
  monthly ) statements
  ;;
  * ) statements
esac
```

这或多或少等同于

```
if [ $1 = daily ] ; then
  statements
elif [ $1 = weekly ] ; then
  statements
elif [ $1 = monthly ] ; then
  statements
else
  statements
fi
```

唯一的区别是 `case` 语句的子句可以进行通配符模式匹配，因此，如果要使用 `if` 语句编写匹配 `dail*` 的条件测试会很难，但在 `case` 语句中却很轻松：`dail* )`

实际上，你经常会看到复杂的正则表达式作为 `case` 语句的一部分，而且允许同时使用单字符和较长标志的一组选项也很常见，可能如下所示：

```
-a | --append ) statements
```

还要注意，在 `case` 语句中，每个块都以非常重要的双分号（`;;`）结束，否则脚本会继续执行与下一个条件关联的语句。当然，在最后一个 `case` 中，没有“下一个”条件，因此可以省略。

### 5. shell 脚本中的其他循环机制是 `for`、`while` 和 `until` 循环。

我们已经见过很多 `for` 循环的实际示例，但它在脚本编写中确实是个得力助手，所以我们再看一看。

下面的简单脚本使用一个简单的 `for` 结构，在 `$PATH` 中的所有目录里搜索给定的文件名。这里有一个巧妙的小技巧：`IFS` 变量是 shell 的输入字段分隔符，通过将其改为冒号，我们就能非常轻松地将 `$PATH` 分割成其组成部分的目录。这还能巧妙地让我们匹配名称中包含空格的目录，而不会出现任何问题：

```sh
$ cat search.sh
#!/bin/sh

# search - look for the specified file name in the PATH directories
IFS=:
for directory in $PATH
do
    if [ -e $directory/$1 ] ; then
        echo Found $1 in directory $directory
    fi
done
exit 0
```

运行后，输出非常简洁：

```
$ search xterm
Found xterm in directory /usr/X11R6/bin
$ search vi
Found vi in directory /bin
$ search search
Found search in directory /home/taylor/bin
$ search not-found
$
```

如果有一个错误条件会很有用，这样在失败时就不会什么都不返回（正如你在前面代码片段的最后一个示例中看到的），而是会显示“未找到”。这个任务将在本课（相当长！）后面的练习中再次出现。关于 `for` 循环的一个有趣技巧是，如果你不指定 `in` 子句，它会自动遍历起始参数，如下所示：

```sh
$ cat args
#!/bin/sh

# args - step through starting args
for arg
do
    echo got argument $arg
done
$ args this is a test
got argument this
got argument is
got argument a
got argument test
$
```

![](img/5ced0c78d748bd190e9027e5549a3622_448_0.png)

> 这个 `for` 循环技巧可以在更复杂的 shell 脚本中简化对起始参数的解析，不过如果你想要多个启动选项，使用 `getopts` 是更明智的方式。详情请参阅 `man 1 getopts`。

### 6. 其余的循环结构在根本上是一样的，唯一区别在于它们测试的条件最终会变为假还是真。

考虑这个示例：

```sh
$ cat args2
#!/bin/sh

# args2 - step through starting args, stop at '--' if seen
```
