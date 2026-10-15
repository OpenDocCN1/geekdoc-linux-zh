
### 18. 如果输入文件描述允许名字为15个字符，而第一条记录存储的名字为 `"John"`，那么通常

- a. 第一条记录的实际字段将缩短为四个字符
- b. 后所有记录的名字字段将缩短为四个字符
- c. 第一条记录的名字字段末尾会有四个零
- d. 第一条记录的名字字段末尾会有空格

### 19. 在大多数系统中，包含小数点的数字是存储的；其位置假设

- a. 小数点不存储
- b. 小数点占用一个字节
- c. 小数点占用两个字节
- d. 大多数系统无法存储

### 20. 存储学生姓名的字段存储在每个记录的 10 到 29 字节。因此，当你设计包含每个学生姓名的打印表时，

- a. 姓名必须打印在打印表的第 10 到 29 位
- b. 姓名必须占据打印表的 20 个位置
- c. 两者都正确
- d. 两者都不正确

## 练习题

1. 重绘以下流程图，使决策和补偿计算位于模块中![](img/cad5396e49a03edb22ef33cf4011_0.png)

2. 重写以下伪代码，使折扣和计算位于模块中。

```
start
    read customerRecord
    if quantityOrdered > 100 then
        discount = .20
    else
        if quantityOrdered > 12 then
            discount = .10
        endif
    endif
    total = priceEach * quantityOrdered
    total = total - discount
```

3. 执行以下程序后 `a`、`b` 和 `c` 的最终值是多少？

```
start

    a = 2

    b = 4

    c = 10

    while c > 6

        changeB()

    endif

    if a = 2 then

        perform changeA()

    endif

    if c = 10 then

        perform changeA()

    else

        perform changeC()

    endif

    print a,b,c
```

```
changeB()

    b = b + 1

    c = c - 1
```

```
changeA()

    a + 1
```

4. 执行以下程序后 `d`、`e` 和 `f` 的最终值是多少？

```
start

  d = 1

  e = 3

  f = 100

  while e > d

    perform module1()

  endif

  if f > 0 then

    perform module2()

  else

    d = d + 5

endif

print d, e
```

```
module1()

    f = f - 50

    e = e + 1

    d = 3
```

```
module2()

    f = f + 13

    d = d * 10
```

5. 为工资单程序绘制一个层次图。尝试考虑至少10个独立模块。例如，一个模块可以计算牙科保险。

6. 设计一个工资表打印表，列出员工的：名、姓和工资。

7. 设计一个工资表打印表，列出以下内容：工作小时、每小时费率、总工资、联邦预扣税、州预扣税、净工资。

8. 给以下输入描述，确定是否有足够的信息生成每个所需的报告：

保险列表
文件名：`INSPREM`

| 字段描述 | 位置 | 数据类型 | 小数位 |
|---|---|---|---|
| 被保险人姓名 | 1-40 | 字符 | |
| 出生日期 | 41-46 | 数字 | 0 |
| 性别 | 47 | 字符 | |
| 汽车品牌 | 48-57 | 字符 | |
| 车型 | 58-61 | 数字 | 0 |
| 年里程 | 62-67 | 数字 | 0 |
| 交通违单数 | 68-69 | 数字 | 0 |
| 欠款 | 70-75 | 数字 | 2 |

- a. 所有被保险人的姓名列表
- b. 极风险被保险人列表，定义为男性、25岁以下且有两张以上单的人
- c. 低风险被保险人列表，定义为过去三年无违单且超过30岁的人
- d. 联系被保险人的列表，针对每年行驶里程低于10,000英里的乘用车主提供特殊保费优惠
- e. 欠款超过`$99.99`的女性驾驶员姓名列表

9. 根据练习题8中的 `INSPREM` 文件描述，设计一个打印表以满足以下请求：

- a. 每个驾驶人的姓名和汽车品牌列表
- b. 所有每年行驶超过20,000英里的被保险人姓名列表
- c. 所有有两张以上违单的驾驶人的姓名、性别、汽车品牌和车型列表
- d. 一份总结出生于1940年或以前、1941–1960年、1961–1980年以及1981年以后驾驶员违单数量的报告
- e. 一份按d部分列出的四个出生日期分类、按性别总结驾驶员违单数量的报告

## 第3章 • 模块、层次结构图、文档

### 10. 一个程序计算学生参加毕业典礼所需的学位袍尺寸。该程序接受学生的身高（英尺和英寸）和体重（磅）作为输入。它将学生的身高转换为厘米，将体重转换为克。然后，它通过将体重（克）的一半加上身高（厘米）来计算出所需的毕业学位袍尺寸。最后，程序打印结果。1英寸等于 2.54 厘米，1磅等于 453.59 克。编写与以下流程图匹配的伪代码。

![](img/cad5396e3e49a03edb322ef333cfad40_117_0.png)

### 11. 一个程序计算客户因开具空票应支付的服务费。该程序接受客户姓名、支票开具日期（月、日、年）、当前日期（月、日、年）以及支票金额（美元和分）。服务费为 20.00 美加上支票金额的 2%，以及自支票开具以来每过去一个月加收 5 美元。绘制与该伪代码匹配的流程图。

（此伪代码假设输入的所有支票已开具——即日期在今天日期之前。此外，一旦新月份开始，支票就逾期一个月——因此，9 月 30 日开具的空票在 10 月 1 日就满一个月。）

```
declare variables      getDates()

    print "Enter the date of the check"

    char custName       input checkMonth

    num checkMonth      input checkDay

    num checkDay        input checkYear

    num checkYear       print "Enter today's date"

    num today           input todayMonth

    num todayDay        input todayDay

    num todayYear       input todayYear

    num checkAmount    return

    num serviceCharge calculateService()

    num baseCharge      baseCharge = .20.00

    num extraCharge     extraCharge = .02 * checkAmount

    num yearsLate       serviceCharge = baseCharge + extraCharge + monthsLate * 5

    num checkField

perform getInput()          printResults()

    perform calculateServiceCharge()

    print custName, serviceCharge

    perform printResults()  return

stop

getInput()

    print "Enter customer name"

    input custName

    perform getDates()

    print "Enter check amount"

    input checkAmount

return
```
