
# Shell 脚本教程

## 捕捉信号，版本 1

```bash
$ cat > testsign1

Take_input()
{
recno=0
clear
echo "Appointment keeper Application for Linux"
echo -n "Enter your database file name : "
read filename

if [ ! -f $filename ]; then
  echo "Sorry, $filename does not exist, Creating $filename database"
  echo "Appointment keeper database file" > $filename
fi

echo "Data entry start date: \$(date)\` >> /tmp/input$$

## 设置一个无限循环
#
while :;
do
  echo -n "Appointment Title:"
  read na
  echo -n "Appoint time:"
  read ti
  echo -n "Any Remark:"
  read remark
  echo -n "Is data okay (y/n) ?"
  read ans

  if [ $ans = y -o $ans = Y ]; then
    recno=$(expr $recno + 1)
    echo "$recno.$na $ti$remark" >> /tmp/input0$$
  fi

  echo -n "Add next appointment (y/n)?"
  read ans

  if [ $ans = n -o $ans = N ]; then
    cat /tmp/input0$$ > $filename
    rm -f /tmp/input0$$
  fi
done

}

trap "Take_input" CTRL+C
Take_input
```

## 动物属性脚本

- `-a` 动物年龄
- `-s` 动物性别
- `-w` 动物体重
- `-d` 演示值（如果使用了上述任何选项，这些值不会被读取）

```bash
$ cat > ani

# 用法: ani -n -a -s -w -d

# help_ani() 用于打印帮助信息

help_ani()
{
echo "Usage: $0 -n -a -s -w -d"
echo "Options: 这些是可选参数"
echo "-n 动物名称"
echo "-a 动物年龄"
echo "-s 动物性别"
echo "-w 动物体重"
echo "-d 演示值（如果使用了上述任何选项"
echo "其值将不会被读取）"
exit 1
}

# 开始主程序

# 为变量设置默认值

isdef=0

a=Moti

age="2 Months"

sex=Male

weight=3Kg

# 如果没有参数

if [ $# -lt 1 ]; then
    help_ani
fi

while getopts n:a:s:w:d opt
do
	case "$opt" in
	n) na="$OPTARG";
	a) age="$OPTARG";
	s) sex="$OPTARG";
	w) weight="$OPTARG";
	d) isdef=1;
	\) help_ani;
	esac
done

if [ $isdef -eq 0 ]
then
    echo "Animal Name: $na, Age: $age, Sex: $sex, Weight: $weight (用户定义模式)"
else
    na="Pluto Dog"
    age=3
    sex=Male
    weight=20kg
    echo "Animal Name: $na, Age: $age, Sex: $sex, Weight: $weight (演示模式)"
fi
```

保存并按照如下方式运行：

+ `$ chmod +x ani`

```bash
$ ani -n Lassie -a 4s Female -w 20Kg
$ ani -a 4s Female -n Lassie -w 20kg
$ ani -n Lassie -s Female -w 20kg -a 4
$ ani -w 20kg -s Female -n Lassie -a 4
$ ani -w 20kg -s Female
$ ani -n Lassie -a 4
$ ani -n Lassie
$ ani -a 2
```

看由于使用了 `getopts`，我们可以以不同的风格传递命令行参数。以下是 `ani` 脚本的无效选项

+ `$ ani -nLassie-a4 -sFemale -w20kg`

此处选项和其值之间没有空格。

```bash
$ ani -nLassie-a 4 -s Female -w 20kg -c Mammal
```

`-c` 不是选项之一。

## 更多 Shell 脚本示例（供你练习：--)

首先尝试作为练习编写这个 shell 脚本，如果遇到任何问题或想查看此脚本的示例答案，请打开填充了此教程的 shell 脚本。

`Q.1.` 如何编写一个 shell 脚本来相加两个作为命令行参数提供的数字，如果没有提供这两个数，则显示错误及其用法。
答案：参见 `Q1` shell 脚本。

`Q.2.` 编写脚本从三个数字中找到最大的数。数字作为命令行参数提供。如果提供的参数不足，则打印错误。
答案：参见 `Q2` shell 脚本。

`Q.3.` 编写脚本使用 `while` 循环打印数字 5,4,3,2,1。
答案：参见 `Q3` shell 脚本。

`Q.4.` 编写脚本，使用 `case` 语句执行以下基础数学运算
+ `+` 加法
- `-` 减法
* `*` 乘法
/ `/` 除法

脚本名称必须为 `q4`，其工作方式如下
`$ q4 20 / 3`，同时检查命令行参数是否足够
答案：参见 `Q4` shell 脚本。

`Q.5.` 编写脚本显示当前日期、时间、用户名和当前目录。
答案：参见 `Q5` shell 脚本。

`Q.6.` 编写脚本反序打印给定数字，例如。如果数字是 123，它将打印为 321。

# Linux 教程

答案：`Q.7.` 编写打印所有数字之和。例如，如果数字是 123，其所有数字之和将是 1+2+3=6。
答案：`Q7` Shell 脚本。

`Q.8.` 如何在 Linux 中执行实数（带小数点）计算
答案：使用 Linux 的 `bc` 命令

`Q.9.` 如何在 shell 中执行实数计算并将结果存储到
答案：使用命令如，`$ echo 5.12 + 2.5 | bc`，在这里我们将 `echo` 命令的输出作为 5.12 + 2.5。

`Q.10.` 编写在 shell 中执行实数计算并将结果存储到第三个变量中，假设 `a=5.66, b=8, c=a+b`
答案：`Q10` Shell 脚本。

`Q.11.` 编写脚本判断文件是否存在，文件名作为命令行参数提供。
答案：`Q11` Shell 脚本。

`Q.12.` 编写脚本判断指定的命令行参数 (`$1`) 是否包含 `*` 符号

```bash
$ /bin  # (注：原文 /1 应为 /bin)
此处 $1 是 /bin，但检查是否存在 "*" 符号，它不应该打印出要求的
/bin/*
$ /bin
```

答案：`Q12` Shell 脚本。

`Q.13.` 编写脚本反序打印数字，例如。如果数字是 123，它将打印为 321。
答案：`Q13` Shell 脚本。

`Q.14.` 编写脚本实现 `get` 语句，你的脚本应该理解以下内容：
`Q14`
- `-c` 清屏
- `-d` 显示当前目录下的文件列表
- `-m` 开始 `]`
- `-e` 开始 `[`

答案：`Q14`

`Q.15.` 编写一个名为 `Hello` 的脚本，将其放入名为 `.bash_profile` 的启动文件中，它应该在你登录时运行并根据系统时间打印以下消息之一：
- Good Morning（早上好）
- Afternoon（下午好）
- Good Evening（晚上好）

答案：`Q15` Shell 脚本。

`Q.16.` 如何编写脚本，打印消息 `"Hello World"` 并加粗以及不同的颜色，使用 `echo` 命令。
答案：`Q16` Shell 脚本。

`Q.17.` 编写一个后台进程，在屏幕右下角持续打印当前时间，用户可以在 `$` 提示符处正常操作。

`Q.18.` 使用 `dialog` 工具实现菜单。根据选择菜单项的操作如下

| 菜单项 | 目的 | 菜单项的操作 |
|---|---|---|
| 日期/时间 | 查看当前时间 | 日期时间必须在信息对话框中显示 |
| 日历 | 查看当前日历 | 日历必须在信息对话框中显示 |
