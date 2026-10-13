
## 列表 22.2 继续

```
23 # get all matches and format them
24
25 grep "$1" $MYADDRESSBOOK |
26 awk -F: '{
27 printf "%-10s %-10s %-10s %-10s %-10s", $1,$2,$3,$4,$5
28 "Name:"$1,"Email:"$2,"Address:"$3,
29 "Phone:"$4 ;
30 }
31 exit $?
```

脚本中有三个主要操作：

- 1. 验证参数数量。
- 2. 检查地址簿是否存在。
- 3. 查找所有匹配项并打印它们。

在第一部分（第 10–13 行），脚本检查是否至少给出一个参数。如果是，脚本继续；否则，它打印使用信息并退出。在第二部分，脚本检查地址簿是否存在。如果不存在，脚本打印错误信息然后退出；否则继续。在脚本的最后一部分，grep 获取匹配项列表，awk 对其进行格式化。为了确保输出的间距均匀，awk 命令对信息及其描述都使用了格式化。

例如，

```
$ ./showperson ranga
```

生成与以下类似的输出：

```
Name:    Sirranga Veeraraghavan
Email:   ranga@soda.berkeley.edu
Address: 1136 Wunderlich Dr. San Jose CA
Phone:   408-444-4444
```

注意第二列中的所有信息是如何正确对齐的。

你也可以使用 showperson 来查找特定字符串的匹配项。例如。

```
$ ./showperson va
```

生成两个匹配项：

Name:
Email: vathsa@oosland.us
Address:
Phone: 408-444-4444

## 添加人员

地址簿最重要的事情之一是能够轻松地向其中添加信息。如果需要手动编辑地址簿来添加信息，你很可能会犯错误，例如忘记添加冒号来分隔字段。通过使用脚本，可以避免此类错误。

在本节中，你将查看 addperson 脚本。它使你能够通过交互式提供信息或通过命令行选项在命令行上提供信息来向地址簿添加条目。当未给出选项时，脚本进入交互模式。在非交互模式下，它尝试从命令行选项获取必要的信息。

无论模式如何，脚本都会将用户提供的信息存储到以下变量中：

- NAME 存储用户提供的姓名。
- EMAIL 存储用户提供的电子邮件地址。
- ADDR 存储用户提供的邮寄地址。
- PHONE 存储用户提供的电话号码。

在交互模式下，你按如下方式提示每条记录中的信息：

```bash
printf "%-10s " "Name:" ; read NAME
printf "%-10s " "Email:" ; read EMAIL
printf "%-10s " "Address:" ; read ADDR
printf "%-10s " "Phone:" ; read PHONE
```

在每个提示之后，你读取并将用户的输入，包括空格和特殊字符，存储在相应的变量中。在非交互模式下，你使用 getopts 来扫描选项：

```bash
while getopts n:e:a:p: OPTION
do
    case $OPTION in
        n) NAME="$OPTARG" ;;
        e) EMAIL="$OPTARG" ;;
        a) ADDR="$OPTARG" ;;
        p) PHONE="$OPTARG" ;;
        ?) echo "USAGE: $USAGE" >&2 ; exit 1 ;;
    esac
done
```

如你所见，非交互模式下脚本理解的选项是

- -n 用于姓名（设置 NAME）
- -e 用于电子邮件地址（设置 EMAIL）
- -a 用于邮寄地址（设置 ADDR）
- -p 用于电话号码（设置 PHONE）

获取所需信息后，你可以通过将格式化的记录追加到地址簿文件的末尾来更新文件，如下所示：

```
echo "$NAME;$EMAIL;$ADDR;$PHONE" >> "$MYADDRESSBOOK"
```

这里假设变量 MYADDRESSBOOK 包含地址簿文件的路径名。

完整的 addperson 脚本在列表 22.3 中给出（行号供你参考）。

## 列表 22.3 addperson 脚本的完整列表

```
1 #!/bin/sh
2 # Name: addperson
3 # Desc: add a person addressbook
4 # Args: -n <name>
5 #      -e <email>
6 #      -a <postal address>
7 #      -p <phone number>
8 #
9 # initialize the variables
10 PATH=/bin:/usr/bin
11 MYADDRESSBOOK=$HOME/addressbook
12 NAME=""
13 EMAIL=""
14 ADDR=""
15 PHONE=""
16
17 # create a function to remove the : from user input
18
19 remove_colon() { echo "$1" | tr ':' ' ' ; }
20
21 if [ $# -lt 1 ] ; then
22
23     # this is interactive mode
24
25     # enable erasing input
26
27
28 stty erase "?"
```

## 列表 22.3 继续

![](img/3def70414996f811615f713b2077a154_394_0.png)

```
29
30 # prompt for the info
31
32 printf "%-10s " "Name: " ; read NAME
33 printf "%-10s " "Email: " ; read EMAIL
34 printf "%-10s " "Address: " ; read ADDR
35 printf "%-10s " "Phone: " ; read PHONE
36
37 else
38
39 # this is noninteractive mode
40
41 # initialize a variable for the usage statement
42
43 USAGE=`basename $0` " [-n name] [-e email] [-a address] [-p phone]"
44
45 # scan the arguments to get the info
46
47 while getopts n:e:a:p: OPTION
48 do
49 case $OPTION in
50 n) NAME="$OPTARG";;
51 e) EMAIL="$OPTARG";;
52 a) ADDR="$OPTARG";;
53 p) PHONE="$OPTARG";;
54 ?) echo "USAGE: $USAGE" >&2; exit 1 ;;
55 esac
56 done
57 fi
58 NAME=`remove_colon $NAME `
59 EMAIL=`remove_colon $EMAIL `
60 ADDR=`remove_colon $ADDR `
61 PHONE=`remove_colon $PHONE `
62
63 echo "$NAME:$EMAIL:$ADDR:$PHONE" >> "$MYADDRESSBOOK"
64
65 exit $?
```

该脚本首先初始化其变量（第 11–16 行）。然后你将存储用户信息的内部变量设置为 null，以避免与用户环境中导出的变量冲突。

下一步是创建以下函数（第 20 行）：

```
remove_colon() { echo "$1" | tr ':' ' ' ; }
```

你使用此函数确保用户输入中不包含任何冒号。

然后你检查是否给出任何参数（第 22 行）。如果没有给出参数，你进入交互模式（第 23–36 行）；否则，你进入非交互模式（第 38–56 行）。

在交互模式下，你提示每条信息并读取它。在产生第一个提示之前，你发出 stty 命令（第 28 行），以确保用户可以在输入过程中擦除任何错误。

在非交互模式下，你使用 getopts 获取命令行上提供的信息。在本节中，你还初始化包含此命令使用语句的变量 USAGE。

获取必要信息后，你对每个变量调用 remove_colon 函数（第 59–62 行）。由于用户可能指定包含冒号的信息，跳过此步骤可能会损坏地址簿并混淆 show-person 脚本。最后你更新地址簿并退出。

使用脚本在交互模式下的示例是

```
$ ./addperson
Name: James Kirk
Email: jim@enterprise.a.starfleet.mil
Address: 1781 Main Street James Town Iowa UFP
Phone:
```

这里你只提供了 Jim Kirk 的姓名、电子邮件地址和邮寄地址。因此当你在地址簿中查找 James Kirk 时，你会发现他的电话号码为空：

```
$ ./showperson
Name: James Kirk
Email: jim@enterprise.a.starfleet.mil
Address: 1781 Main Street James Town Iowa UFP
Phone:
```

你可以使用命令的非交互形式执行相同的操作，如下所示：

```
$ ./addperson -n 'James Kirk' -e jim@enterprise.a.starfleet.mil \
-a '1781 Main Street James Town Iowa UFP'
```

注意在命令行上，你需要引用包含空格的条目。

## 删除人员

偶尔，你需要从地址簿中删除某人。在本节中，你将查看一个名为 delperson 的脚本，它从地址簿中删除人员。

从地址簿中删除某人是一项更困难的任务，因为你必须确认每个选定删除的记录。你需要执行两个主要任务

- 1. 制作地址簿中与指定名称匹配的行列表。
- 2. 基于用户反馈，从地址簿中删除适当的条目。

由于删除操作可能会从地址簿中删除信息，因此你必须格外小心地备份并在原始地址簿的副本上工作，而不是在原始地址簿上工作。

为了简化提示和打印错误消息，此脚本使用在第 21 章中介绍的 shell 函数库 libDTYSP2.sh。

脚本的基本流程如下：

- 1. 复制地址簿并使用副本进行所有修改。
- 2. 从此副本获取所有匹配行列表并将它们存储在删除文件中。
- 3. 对删除文件中的每条记录，打印出该记录并询问用户是否应删除该行。
- 4. 如果用户希望删除该记录，则从地址簿副本中删除该记录。
- 5. 删除完成后，备份原始地址簿。
- 6. 使编辑后的副本成为地址簿。
- 7. 清理临时文件并退出。

对于这些步骤中的每一步，你都使用一个函数来确保执行的操作成功。

完整的 delperson 脚本在列表 22.4 中给出（行号供你参考）。

## 列表 22.4 delperson 脚本的完整列表

```
#!/bin/sh
# Name: delperson
# Desc: del a person addressbook
# Args: $1 -> name of person to delete

# get the helper functions

. $HOME/lib/sh/libDTYSP2.sh

PATH=/bin:/usr/bin
```
