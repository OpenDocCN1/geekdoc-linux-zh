

# 13.10.9 子字符串变量展开

模式匹配参数用于从字符串的前端或后端剥离某些部分。 这些操作符最常见的用途是从路径的头部或尾部剥离路径名元素。 请参阅表 13.19。

## 表 13.19 变量展开子字符串ᵃ

| 表达式 | 功能 |
|---|---|
| ${variable%pattern} | 匹配变量值的最小尾部部分与 pattern，并将其移除。 |
| ${variable%%pattern} | 匹配变量值的最大尾部部分与 pattern，并将其移除。 |
| ${variable#pattern} | 匹配变量值的最小头部部分与 pattern，并将其移除。 |
| ${variable##pattern} | 匹配变量值的最大头部部分与 pattern，并将其移除。 |
| ${#variable} | 替换为变量中的字符数。 如果为 * 或 @，长度为位置参数的数量。 |

a 在 bash 2.x 之前的版本中不可用。

## 示例 13.65

```
1 $ pathnames="/usr/bin/local/bin"
2 $ echo ${pathnames%/*bin}
/usr/bin/local
```

## 解释

- 1 本地变量 pathname 被赋值为 /usr/bin/local/bin。
- 2 % 移除 pathname 中包含模式 /bin 后跟零个或多个字符的最小尾部部分；也就是说，它剥离了 /bin。

## 示例 13.66

```
1 $ pathnames="usr/bin/local/bin"
2 $ echo ${pathname%%/*bin}
/usr
```

## 解释

## 示例 13.67

```
1  $ pathname=/home/1111input/jake/.bashrc
2  $ echo ${pathname#/home}
   /1111input/jake/.bashrc
```

## 解释

- 1  本地变量 pathname 被赋值为 /home/1111input/jake/.bashrc。
- 2  # 移除 pathname 中包含模式 /home 的最小头部部分；也就是说，/home 从路径变量的开头被剥离。

## 示例 13.68

```
1  $ pathname=/home/1111input/jake/.bashrc
2  $ echo ${pathname##/}
   .bashrc
```

## 解释

- 1  本地变量 pathname 被赋值为 /home/1111input/jake/.bashrc。
- 2  ## 移除 pathname 中包含零个或多个字符直到且包括最后一个斜杠的最大头部部分；也就是说，它从路径变量中剥离 /home/1111input/jake。

## 示例 13.69

```
1  $ name="Ebenezer Scrooge"
2  $ echo ${#name}
   16
```

## 解释

- 1  变量 name 被赋值为字符串 Ebenezer Scrooge。
- 2  ${#variable} 语法显示分配给变量 name 的字符串中的字符数。 Ebenezer Scrooge 中有 16 个字符。

# 13.10.10 位置参数

通常，特殊内置变量，通常称为位置参数，在 shell 脚本中用于从命令行传递参数时使用，或在函数中用于保存传递给函数参数的值。 这些变量称为位置参数，因为它们按数字 1、2、3 等引用，表示它们在参数列表中的各自位置。 请参阅表 13.20。

shell 脚本的名称存储在 $0 变量中。 位置参数可以用 set 命令设置、重置和取消设置。

## 表 13.20 位置参数

| 表达式 | 功能 |
|---|---|
| $0 | 引用当前 shell 脚本的名称 |
| $1-$9 | 位置参数 1-9 |
| ${10} | 位置参数 10 |
| $# | 计算为位置参数的数量 |
| $@ | 计算为所有位置参数 |
| $* | 与 $@ 相同，除了在双引号中时 |
| "$*" | 计算为 "$1 $2 $3"，等等 |
| "$@" | 计算为 "$1" "$2" "$3"，等等 |

## 示例 13.70

```
1  $ set punky tommy bert jody
     $ echo $@        # Prints all the positional parameters
     punky tommy bert jody
2  $ echo $1          # Prints the first position
     punky
3  $ echo $2 $3       # Prints the second and third position
     tommy bert
4  $ echo $#          # Prints the total number of positional parameters
     4
5  $ set a b c d e f g h i j k l m
     $ print $10       # Prints the first positional parameter followed by a 0
     a0
     $ echo ${10} ${11}  # Prints the 10th and 11th positions
     j k
6  $ echo $*
     13
7  $ echo $*
     a b c d e f g h i j k l m
8  $ set file1 file2 file3
     $ echo \$$#
     $3
9  $ eval echo \$$#
     file3
10 $ set --           # Unsets all positional parameters
```

