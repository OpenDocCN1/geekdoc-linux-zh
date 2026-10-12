
```bash
echo "You may retire!"

else

echo "In order to retire, you must be at least age 60 with 10 Years of Service or have 25 years of service."

fi

fi

else

echo "Your age is less than your Years of Service! This is invalid!"

fi
```

读取数据。年龄必须大于工年数量。如果员工至少 60 岁且在机构工作至少 10 年，该员工即可退休。如果员工未满 60 岁且有 10 年经验，为了检查员工是否在机构工作了至少 25 年，在所有条件都不满足时执行此 `else`；此 `fi` 结束 25 年工龄测试。此 `fi` 结束年龄和年份的测试。此 `fi` 结束年龄大于年份的测试。图 6-16 Lucy’s Books and Tapes, Inc. 退休要求脚本

数据完整性将在第 9 章中详细讨论。

接下来你将创建图 6-16 所示的脚本。

要创建一个使用嵌套 `if` 语句的脚本：

- 以用户身份登录 Linux 系统，然后打开终端仿真窗口。
- 在 `$HOME/bin` 目录下创建一个名为 `RetirementStatus` 的脚本。
- 插入图 6-16 所示的代码行以创建一个使用嵌套 `if` 语句的脚本。
- 保存脚本，然后退出编辑器。
- 使脚本具有可执行权限，执行脚本，并在提示 `Age` 时输入 50，在提示 `Years of Service` 时输入 10。参见图 6-17。显示了一条你未满足要求的消息。
- 再次执行脚本。这次在提示 `Age` 时输入 62，在提示 `Years of Service` 时输入 26。参见图 6-17。显示了一条你已满足要求的消息。
- 最后执行一次脚本。在提示 `Age` 时输入 15，在提示 `Years of Service` 时输入 20。参见图 6-17。显示了一条你的输入无效的消息。
- 关闭窗口，然后注销。

图 6-17 执行 `RetirementStatus` 脚本

让我们看看另一个嵌套 `if` 语句的更复杂的示例。在这个例子中，Hugh Nguyen 总是需要一个脚本来帮助乘客订票系统。该脚本将作为公司主订票系统的原型

## 嵌套 if 语句 231

将用另一种编程语言编写。公司需要一个确定预订票的程序。图 6-18 显示了脚本满足乘客预订系统需求需要遵循的逻辑。

![](img/cad5396e3e49a03edb322ef333cfad40_562_0.png)

图 6-18 计算机票价格的逻辑流程图

图 6-19 显示了应用图 6-18 中逻辑的实际脚本。注意图 6-19 显示的 `AirFare` 脚本接受三个变量——`DestCity`、`Class` 和 `WeekDay`，并根据这些输入确定价格。图 6-18 中确立的逻辑规定：如果乘客前往洛杉矶（城市代码为 `LAX`）且乘坐经济舱（`Class` 为 `C`），则在周六旅行的机票价为 50 美元，其他任何日期的价格为 75 美元。如果乘客乘坐其他舱前往洛杉矶，机票价为 80 美元。前往任何其他城市的机票价为 100 美元。

## 第6 章 决策结构

```bash
[~dodd]$ cat AirFare

read -p "Enter Destination City" DestCity

read -p "Enter Class" Class

read -p "Day of week" WeekDay

if [[ $DestCity -eq "LAX" ]];

# Class is Coach

if [[ $Class = "C" ]]

then

    if [[ $WeekDay = "Sat" ]]

then

        ((AirFare = 50))

else

        ((AirFare = 75))

fi

else

    ((AirFare=0))

fi

else

    ((AirFare = 100))

echo "Air Fare: $AirFare"
```

**图 6-19** Hugh Nguyen 航空的机票计算脚本

## 理解 case 语句

`case` 语句是决策结构的另一种实现方式。当你需要根据多个输入进行决策时（例如根据几个菜单选项收到的用户反馈），就应该使用 `case` 语句。

> 虽然没有固定的规则，但当你有三个或更多决策时，应该考虑使用 `case` 语句。同样，由程序员决定使用哪种方法。

通常，当有多个输入时，相比 `if` 语句，`case` 语句更容易读。从逻辑上讲，`case` 语句的功能类似于一个大的语句。

## case 语句的伪逻辑

让我们先看看 `case` 语句的通用逻辑：

- 变量名
- Case1: 如果 Case1 的内容与变量名的内容相等，则执行活动
- Case2: 如果 Case2 的内容与变量名的内容相等，则执行活动
- Case3: 如果 Case3 的内容与变量名的内容相等，则执行活动

## 理解 case 语句

Case Else: 如果之前的所有 Case 都不等于变量名的内容，则执行活动

结束 case (End-Case)

这就是 `case` 语句的工作原理：测试变量名，检查其内容是否与指定的 Case（如 Case1、Case2 或 Case3）匹配，然后执行匹配右侧的活动。匹配发生后，将不再测试其他 case。处理继续到 case 语句之后的语句。在没有匹配项的情况下，可以使用 case else 子句。如果用户没有从给定的选项列表中输入值，该子句非常有用。

## case 语句的语法

让我们看看 shell 对 `case` 语句的实现：

```
case word in
  pattern1) statements
    statements
    ;
  pattern2) statements
    statements
    ;
  patternN) statements
    statements
    ;
esac
```

`case` 语句以及 `in` 和 `esac` 子句是必须的。"What is the case in" 这个短语是必须的。这个代码短语类似于口语“要匹配的模式是什么？”。`word` 是一个匹配某个模式的变量。对于模式，你可以使用字符和数字。你还可以使用模式匹配符号：`*` 用于匹配所有字符；`?` 用于匹配单个字符；或者 `[ ... ]` 用于匹配字符范围。

> 大多数脚本使用 `*` 作为 case else 伪代码的一种形式。它匹配任何内容，并且通常放在 case 语句的末尾，用于捕捉不匹配任何之前模式的情况。

每个 `patternN` 都都需要右括号符号 `)`，它将单个 case 与在该 case 匹配时要执行的语句隔离开。`;;` 符号是必须的，用于终止每个 case。`esac` 用于终止整个 case 语句。与 `if` 和 `fi` 类似，`esac` 是 "case" 的倒写。

## 第6 章 决策结构

接下来，你将使用 `case` 语句创建一个简单的 shell 脚本。
要创建一个使用 `case` 语句的简单脚本：

- 1. 以用户身份登录 Linux 系统，然后打开终端仿真窗口。
- 2. 将早些练习中使用的名为 `$HOME/bin/ColorRed` 的脚本复制到名为 `$HOME/bin/ColorRed1` 的新脚本。
- 3. 修改脚本使其包含以下代码行：
```
read -p "Enter color: " Color

case $Color in

red) echo "The color is red"

*) echo "The color is not red"

esac
```
- 4. 保存脚本，然后退出。

## 模式匹配与 case 语句

假设你想编写一个询问“是或否”问题的脚本。为了实现这一点，你需要将答案转换为大写。

- 1. 以用户身份登录 Linux 系统，然后打开终端仿真窗口。
- 2. 在 `$HOME/bin` 目录下创建一个名为 `YesCase` 的脚本。
- 3. 插入以下代码行以接收用户输入、将输入转换为大写并创建 `case` 语句：
```
read -p "Do you want to see all files? (Y or N)"

YN=$(echo $YesNo | tr [:lower:] [:upper:]])

case $YN in

  Y|YES)

    echo "Displaying all files..."

    ls -a

  N|NO)

    echo "Displaying all files except hidden..."

    ls

  *) echo "Invalid response!"

esac
```
