

## 示例 14.2

```
(The Script)
#!/bin/bash
# Program: opts1
# Using getopts -- First try --

1  while getopts xy options
   do
2      case $options in
3      x) echo "you entered -x as an option";;
       y) echo "you entered -y as an option";;
       esac
   done

(The Command Line)
4  $ opts1 -x
   you entered -x as an option
5  $ opts1 -xy
   you entered -x as an option
   you entered -y as an option
6  $ opts1 -y
   you entered -y as an option
7  opts1: illegal option -- b
8  $ opts1 b
```

## 解释

- 1. getopts 命令被用作 while 命令的条件。此程序的有效选项列在 getopts 命令之后；它们是 x 和 y。每个选项都在循环体中依次进行测试。每个选项将被分配给变量 options，且不带前导的连字符。当没有更多参数需要处理时，getopts 将以非零状态退出，导致 while 循环终止。
- 2. case 命令用于测试 options 变量中发现的每个可能选项，即 x 或 y。
- 3. 如果 x 是选项，则显示字符串 you entered -x as an option。
- 4. 在命令行中，opts1 脚本被赋予 x 选项，这是 getopts 处理的合法选项。
- 5. 在命令行中，opts1 脚本被赋予 xy 选项；x 和 y 都是 getopts 处理的合法选项。
- 6. 在命令行中，opts1 脚本被赋予 y 选项，这是 getopts 处理的合法选项。

### 解释（续）

- 7. opts1 脚本被赋予一个错误选项，即非法选项。Getopts 将错误消息发送到 stderr。
- 8. 没有连字符前缀的选项不是选项，会导致 getopts 停止处理参数。

## 示例 14.7

```
(The Script)
#!/bin/bash
# Program: opts2
# Using getopts -- Second

1  while getopts xy options ?
   do
2      case $options in
          x) echo "you entered -x as an option";;
          y) echo "you entered -y as an option";;
3         ?) echo "Only -x and -y are valid options" 1>&2;;
         esac
   done

(The Command Line)
   $ opts2 -x
   you entered -x as an option
   $ opts2 -y
   you entered -y as an option
   $ opts2 xy
   $ opts2 -xy
   you entered -x as an option
   you entered -y as an option
4  $ opts2 -q
   Only -x and -y are valid options
5  $ opts2 -d
   Only -x and -y are valid options
```

## 解释

- 1. 如果 getopts 有错误消息，它将被重定向到 /dev/null。
- 2. 如果选项是错误选项，则问号将被分配给 options 变量。可以使用 case 命令测试问号，从而允许你将自己的错误消息打印到标准错误。

### 解释（续）

3 如果 options 变量被分配问号，则执行 case 语句。问号用反斜杠保护，以防止 shell 将其视为通配符并尝试执行文件名替换。

4 q 不是合法选项。问号被分配给变量 options 并显示错误消息。

5 c 不是合法选项。问号被分配给变量 options 并显示错误消息。

特殊 getopts 变量。getopts 函数提供两个变量来帮助跟踪参数：OPTIND 和 OPTARG。OPTIND 是一个特殊变量，初始化为一，并在 getopts 完成处理命令行参数的每次处理时递增，为 getopts 将处理的下一个参数编号。OPTARG 变量包含合法参数的值。参见示例 14.74 和 14.75。

## 示例 14.74

```
(The Script)
#!/bin/bash
# Program: opts3
# Using getopts -- Third try --

1 while getopts dq: options
do
  case $options in
 2 d) echo "-d is a valid switch" ;;
 3 q) echo "The argument for -q is $OPTARG";;
 \?) echo "Usage:opts3 -dq filename ..." 1>&2;;
esac
done

(The Command Line)
4 $ opts3 -d
 -d is a valid switch
5 $ opts3 -q foo
 The argument for -q is foo
6 $ opts3 -q
Usage:opts3 -dq filename ...
7 $ opts3 -e
Usage:opts3 -dq filename ...
8 $ opts3 e
```

