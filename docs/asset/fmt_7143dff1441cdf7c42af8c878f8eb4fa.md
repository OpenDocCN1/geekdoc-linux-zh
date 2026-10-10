
```bash
echo "Profits and Costs are equal - breakeven"
elif [[ $Net -gt "0" ]]
then
  echo "Profit of " $Net"
elif [[ $Net -lt "0" ]]
then
  echo "Loss of " $Net"
fi
}
BELP $Sales $Costs # 调用 BELP (收支亏损利润)
```
- 4. 保存脚本，关闭编辑器，然后使脚本具有可执行性。
- 5. 执行脚本，在提示时输入 1000 作为销售额，2000 作为成本，然后返回输出。
- 6. 运行脚本，在提示时输入 80000 作为销售额，27000 作为成本，然后返回输出。
- 7. 运行脚本，在提示时输入 50000 作为销售额，50000 作为成本，然后返回输出。
- 8. 关闭窗口，然后注销。

## 项目 8-3

在本项目中，如果输入数组的值为空，你将显示一条消息。将调用两个函数，一个用于读取数据，另一个用于检查数据。该项目的目标是帮助你实现函数和数组，并测试数据元素的长度。

- 1. 以用户身份登录 Linux 系统，然后打开一个终端仿真窗口。
- 2. 在 `$HOME/bin` 目录下创建一个名为 `Project 8-3` 的 shell 脚本。
- 3. 插入以下行代码：

```bash
ReadEntries ()
{
    read -p "Enter total number of entries " tot # 读取总值。
    for ((n=0; n < $tot; n++)) # 循环并读取值。
    do
        read -p "Enter value " entries[$n]
    done
}
CheckForBlanks()
{
    for ((n=0; n < $tot; n++))
    do
        if [[ ${#entries[n]} eq 0 ]] # 如果元素长度为 0，假设为空。
        then
            echo "Value" $n "is blank"
        else
            echo "Value" $n "is" ${entries[n]}
        fi
    done
}
ReadEntries
CheckForBlanks
```
- 4. 保存文件，关闭编辑器，然后使脚本具有可执行性。
- 5. 运行脚本并输入 4 作为输入数量，然后在提示时插入以下值：frog、dog、第三个值按回车键、以及 400。
- 6. 记录输出。
- 7. 使用不同的值重新运行，并记录你的发现。
- 8. 关闭窗口，然后注销。

## 项目 8-4

在本项目中，你将使用数组存储目录名称。你将测试每个目录是否存在，如果存在，则显示目录的树状列表。此项目强化了对数组的使用。

- 1. 以用户身份登录 Linux 系统，然后打开一个终端仿真窗口。
- 2. 在 `$HOME/bin` 目录下创建一个名为 `Project8-4` 的 shell 脚本。
- 3. 插入以下行代码：

```bash
declare -a dir
```
```bash
dir=( cats dogs birds snakes cats/large cats/small )
# 目录
max=${#dir[@]}
for (( num=0; num < $max; num++ ))
do
  if [[ ! -d ${dir[num]} ]]; # 如果目录不存在，则创建并执行任务。
  then
      echo "Creating directory ${dir[num]}"
      mkdir ${dir[num]}
  fi
done
```
- 4. 保存脚本，关闭编辑器，并使脚本具有可执行性。
- 5. 执行脚本，并记录输出。
- 6. 关闭窗口，然后注销。

![](img/72e8a95d2755ff262251b6d92baa27_355_0)

在本项目中你将处理变量的作用域。你将创建一个带有局部定义数组的函数和一个全局数组。你将尝试在内部和外部访问它们。

- 1. 以用户身份登录 Linux 系统，然后打开一个终端仿真窗口。
- 2. 在 `$HOME/bin` 目录下创建一个名为 `Project8-5` 的 shell 脚本。
- 3. 插入以下行代码：

```bash
function Arrays {
  local -a LocalArray # 局部定义数组。
  LocalArray[0]=1 # 设置局部值。
  LocalArray[1]=2
  LocalArray[2]=3
  echo "Local inside: ${LocalArray[@]}"
}
GlobalArray[0]=100 # 设置全局值。
GlobalArray[1]=101
GlobalArray[2]=102
echo "Global outside: ${GlobalArray[@]}"
Arrays
echo "Local outside: ${LocalArray[@]}"
```
- 4. 保存脚本，关闭编辑器，并使脚本具有可执行性。
- 5. 执行脚本，并记录输出。
- 6. 关闭窗口，然后注销。

## 项目 8-6

在本项目中，你将使用数组存储用户输入的多个值。

- 1. 以用户身份登录 Linux 系统，然后打开一个终端仿真窗口。
- 2. 在 `$HOME/bin` 目录下创建一个名为 `Project8-6` 的 shell 脚本。
- 3. 插入以下行代码：

```bash
PopulateArray() {
  max=$# # 参数总数。
  for ((i=0; i<max; i++))
  do
    values[$i]=$1 # 设置值。
    shift # 移位参数。
  done
}
ListArray() {
  echo ${values[@]} # 显示数组内容。
}
PopulateArray $@ # 传递所有参数。
ListArray # 调用函数。
```
- 4. 保存脚本。
- 5. 使脚本具有可执行性。
- 6. 执行脚本，在提示时输入以下值：4、50、110、200。
- 7. 记录输出。
- 8. 再次运行并使用不同的值，记录你的发现。
- 9. 尝试不传递参数运行脚本。观察会发生什么什么？
- 10. 关闭窗口，然后注销。

## 项目 8-7

在本项目中，你将创建一个函数，使用 `date` 命令显示儒历格式、MM/DD/YYYY 格式或 H:M:S（小时:分钟:秒）格式。通过参数将 J、T 或 M 传递给该函数。

- 1. 以用户身份登录 Linux 系统，然后打开一个终端仿真窗口。
- 2. 在 `$HOME/bin` 目录下创建一个名为 `Project8-7` 的 shell 脚本。
- 3. 插入以下行代码：

```bash
function DateFun()
  if [[ $# -eq 1 ]]
  then
    case "$1" in
      J|j) echo "The Julian date including the year is:" `date +%Y%j`
      T|t) echo "The time is:" `date +%X`
      M|m) echo "The date in MM/DD/YYYY format is:" `date +%x`
      *) echo "Invalid format. Use J, T or M"
    esac
  else
    echo "Invalid number of parameters. Use J, T or M"
  fi
end
DateFun $1
```
- 4. 保存脚本，然后关闭编辑器。
- 5. 使脚本具有可执行性。
- 6. 执行脚本，在提示时输入 t 作为参数，然后记录输出。
- 7. 执行脚本，在提示时输入 J 作为参数，然后记录输出。
- 8. 执行脚本，在提示时输入 m 作为参数，然后记录输出。
- 9. 执行脚本，在提示时输入 a 作为参数，然后记录输出。
- 10. 关闭窗口，然后注销。

## 项目 8-8

在本项目中，你将创建一个菜单，可以在其中输入成绩以计算平均值。成绩将存放在数组中。

- 1. 以用户身份登录 Linux 系统，然后打开一个终端仿真窗口。
- 2. 在 `$HOME/bin` 目录下创建一个名为 `Project8-8` 的 shell 脚本。
- 3. 插入以下行代码：

```bash
declare -a grade
Ans="Y"
while [[ $Ans == "Y" ]]
do
  read -p "Enter grade: " g
  grade+=($g)
```
