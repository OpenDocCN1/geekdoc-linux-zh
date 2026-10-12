
```
   a. hi
   b. echo hi
   c. 语法错误信息
   d. 无
```

# 第7章 循环结构

## 项目 7-1

在这个项目中，你将创建一个包含目录列表的文件。你将使用 `for` 循环结构来控制过程。需要使用命令替换来读取目录列表文件的内容。需要为文件中的每一行创建一个目录。

1. 以用户身份登录 Linux 系统，然后打开终端仿真窗口。
2. 在 `$HOME/bin` 目录下创建一个名为 `inlist` 的文件。该文件将包含要创建的目录列表，每行一个。
3. 插入以下代码：

```
Dir1

Dir2

Dir2/Dir2a1

Dir2/Dir2a2

Dir2/Dir2a2/Dir2b1

Dir2/Dir2a2/Dir2b2
```

4. 在你的 `$HOME/bin` 目录下创建一个名为 `Project-1` 的 shell 脚本。
5. 插入以下代码：

```
for dirname in `inlist`
do
  mkdir $dirname
done
```

6. 保存脚本，然后退出编辑器。
7. 赋予脚本执行权限，然后执行该脚本。
8. 记录输出结果。
9. 关闭窗口，然后注销登录。

## 项目 7-2

在这个项目中，你将使用一种循环结构来判断主机计算机是否可用。你将使用 `ping` 命令来实现这一目标。如果主机可用，你将使用 `telnet` 连接到该主机。

1. 以用户身份登录 Linux 系统，并打开终端仿真窗口。
2. 在 `$HOME/bin` 目录下创建一个名为 `Project7-2` 的 shell 脚本。
3. 插入以下代码：

```
read -p "要 ping 的 IP 地址或主机名: " PingName

ping -c 2 $PingName

until [[ $? -eq 0 ]]

do

  sleep 2

  echo "主机不可用。正在重新 ping..."

  ping -c $PingName

done

echo "主机可用。"

echo "正在 telnet 到主机。"

telnet $PingName
```

4. 保存脚本，然后退出编辑器。
5. 赋予脚本执行权限，执行脚本，并输入一个已的主机地址。
6. 再次执行脚本。这次使用一个不存在的主机地址。
7. 关闭窗口，然后注销登录。

## 项目 7-3

在这个项目中，你将创建一个使用 shell 的 `$RANDOM` 变量来生成随机数的脚本。用户将被要求输入一个 1 到 10 之间的数字。循环将一直持续到用户猜中正确答案。`$RANDOM` 语句会生成一个 0 到 32,767 之间的随机数；因此，循环内的 `$RANDOM` 语句将确保系统生成一个 1 到 10（包含边界）之间的随机数。

1. 以用户身份登录 Linux 系统，然后打开终端仿真窗口。
2. 在 `$HOME/bin` 目录下创建一个名为 `Project7-3` 的脚本。
3. 插入以下代码：

```
read -p "猜一个 1 到 10 之间的数字: " guess

rand=$RANDOM

while

  if [[ $rand -ge 1 && $rand -le 10 ]]

  then

    if [[ $guess -eq $rand ]]

    then

        echo "正确"

        break

    else

        echo "再试一次"

        read -p "猜一个 1 到 10 之间的数字: " guess

        rand=$RANDOM

    fi

  else

    rand=$RANDOM

  fi

done
```

4. 保存脚本，然后退出编辑器。
5. 赋予脚本执行权限，执行脚本，然后不断输入相同的数字直到你猜中为止。
6. 记录你猜中数字所需的次数。
7. 关闭窗口，然后注销登录。

## 项目 7-4

在这个项目中，你将使用 `while` 和 `until` 语句以及嵌套循环。

1. 以用户身份登录 Linux 系统，然后打开终端仿真窗口。
2. 在 `$HOME/bin` 目录下创建一个名为 `Project7-4` 的 shell 脚本。
3. 插入以下代码：

```
let "x=1"                              # 等同于 ((x=1))

while [[ $x -le 5 ]]                   # 外层循环开始

    let "y=4"

    until [[ $y -le 1 ]]                # 内层循环开始

        let y--                             # 等同于 ((y--))

        echo $y

        let c++                             # 等同于 ((c++))

    done                                # 内层循环结束

    let x++                             # 等同于 ((x+))

done                                 # 外层循环结束

echo "循环次数为: " $c
```

4. 保存脚本，然后退出编辑器。
5. 赋予脚本执行权限，然后执行脚本。
6. 关闭窗口，然后注销登录。

## 项目 7-5

在这个项目中，你将创建一个脚本，如果当前月份和日期恰好匹配系统日期，则显示“生日快乐！”

1. 以用户身份登录 Linux 系统，然后打开终端仿真窗口。
2. 在 `$HOME/bin` 目录下创建一个名为 `Project7-5` 的 shell 脚本。
3. 插入以下代码：

```
read -p "输入你的三字母出生月份（例如 Feb）: " BirthMonth

read -p "输入你的两位出生日期（例如 07）: " BirthDay

month=$(date | cut +%b)

day=$(date | cut +%d)

if [ "$BirthMonth" == "$month" ] && [ "$BirthDay" == "$day" ]

then

    HappyBirthday="Y"

else

    HappyBirthday="N"

fi

while [[ $HappyBirthday == "Y" ]]

do

    echo "Happy Birthday!"

    sleep 1

done
```

4. 保存脚本，然后退出编辑器。
