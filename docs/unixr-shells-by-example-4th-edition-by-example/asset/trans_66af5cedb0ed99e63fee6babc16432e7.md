

## 示例 8-4

```
（The Script）
#!/bin/sh
# Program opts4
# Using getopts - Fourth try
while getopts xyz: arguments 2>/dev/null
do
    case $arguments in
        x) echo "you entered -x as an option.";;
        y) echo "you entered -y as an option.";;
        z) echo "you entered -z as an option.";;
           echo "\$OPTARG is \$OPTARG,";;
        \?) echo "Usage: opts4 [-xy] [-z argument]"
            exit 1;;
    esac
done
echo "The initial value of \$OPTIND is 1.
The final value of \$OPTIND is \$OPTIND.
Since this reflects the number of the next command-line argument,
the number of arguments passed was `expr \$OPTIND - 1`."
```

```
（The Command Line）
$ opts4 -xyz foo
you entered -x as an option.
you entered -y as an option.
you entered -z as an option.
\$OPTARG is foo.
The initial value of OPTIND is 1.
The final value of OPTIND is 3.
Since this reflects the number of the next command-line argument, the number of arguments passed was 2.

$ opts4 -x -y -z boo
you entered -x as an option.
you entered -y as an option.
you entered -z as an option.
\$OPTARG is boo.
The initial value of OPTIND is 1.
The final value of OPTIND is 5.
Since this reflects the number of the next command-line argument, the number of arguments passed was 4.

$ opts4 -d
Usage: opts4 [-xy] [-z argument]
```

## 解释

- 1. while 命令测试 getopts 的退出状态。如果 getopts 能成功处理一个参数，则返回 0 退出状态，while 循环体将被进入。附加在 z 选项后的冒号告诉 getopts 必须在 -z 选项后跟一个参数。如果选项需要参数，则该参数会存储在 getopts 内建变量 OPTARG 中。
- 2. 如果 x 作为选项给出，则它会被存储在变量 arguments 中。
- 3. 如果 z 作为选项并带参数给出，则参数会被存储在内建变量 OPTARG 中。
- 4. 如果输入了无效选项，则问号会被存储在变量 arguments 中，并显示错误信息。
- 5. 特殊的 getopts 变量 OPTIND 保存下一个要处理的选项的编号。其值始终比实际命令行参数的数量多一。

### 8.9.2 eval 命令和解析命令行

eval 命令会评估命令行，执行所有 shell 替换，然后执行命令行。本质上，它会将命令行解析两次。当正常的命令行解析不足时，就会使用它。

## 示例 8.63

```
1 $ set a b c d
2 $ echo The last argument is \$#
   The last argument is $4
3 $ echo The last argument is $4
   The last argument is d
4 $ eval echo The last argument is \$#
   The last argument is d
5 $ set -x
$ echo The last argument is \$#
+ eval echo the last argument is $4
+ echo the last argument is d
   The last argument is d
```

## 解释

- 1. 设置了四个位置参数。
- 2. 期望的结果是打印最后一个位置参数的值。\$ 会打印字面量的美元符号。$# 会求值为 4，即位置参数的数量。shell 在求值 $4 之后，不会再次解析该行以获取 $4 的值。
- 3. 打印的是 $4 而不是最后一个参数。
- 4. 在 shell 执行变量替换后，eval 命令会执行变量替换然后执行 echo 命令。
- 5. 打开回显以观察解析的顺序。

## 示例 8.66

```
(From SVR4 Shutdown Program)
1 eval `/usr/bin/id | /usr/bin/sed 's/[^a-z0-9=].*/'"
2 if [ "$uid"-0 -ne 0 ]
3 then
    echo $0: Only root can run $0
    exit 2
fi
```

## 解释

1 这是一个棘手的问题。id 程序的输出被发送到 sed 以提取字符串中 uid 部分。id 的输出为
uid=9496(e11e) gid=40 groups=40
uid=0(root) gid=1(daemon)

sed 正则表达式的含义为：查找任何不是字母、数字或等号的字符并删除该字符及之后的所有字符。其结果是将从第一个左括号到行尾的所有内容替换为空。剩下的就是 uid=9496 或 uid=0。

在 eval 评估命令行后，它会执行 resulting 命令：
uid=9496
或
uid=0

例如，如果用户的 ID 为 root，则执行的命令将为 uid=0。这会在 shell 中创建一个名为 uid 的局部变量并将其赋值为 0。

2 使用命令修饰符测试 uid 变量的值是否为 0。

3 如果 uid 不是 0，则 echo 命令会显示脚本名称 ($0) 和消息。

### 8.10 Shell 调用选项

当使用 sh 命令启动 shell 时，它可以接受选项来修改其行为。参见表 8.7。

## 表 8.7 Shell 调用选项

| Option | Meaning |
|---|---|
| -i | Shell is in the interactive mode. QUIT and INTERRUPT are ignored. |
| -s | Commands are read from standard input and output is sent to standard error. |
| -c string | Commands are read from string. |

