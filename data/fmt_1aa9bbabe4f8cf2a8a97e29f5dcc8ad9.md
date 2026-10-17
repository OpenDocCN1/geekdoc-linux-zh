
- 保存脚本，退出编辑器，然后使脚本具有执行权限。
- 执行脚本，并在提示输入 `Status` 时输入 `H` 和 `2`。参见图 6-10。会出现一条显示你没有获得奖金的消息。

## 第 6 章 决策结构

6. 再次执行脚本，在提示 `Status`（状态）时输入 `H`，在提示 `Shift`（班次）时输入 `3`。参见图 6-10。屏幕会出现一条表示你已获得奖金的消息。

7. 第三次执行脚本，在提示 `Status` 时输入 `S`（代表 `Salaried` 薪制），在提示 `Shift` 时输入 `3`。参见图 6-10。屏幕会出现一条表示你未获得奖金的消息。

8. 不要注销。

![](img/cad5396e3e49a03edb322ef333cfad40_551_0.png)

图 6-9 `ShiftBonus` 脚本的内容

![](img/cad5396e3e49a03edb322ef333cfad40_551_1.png)

第 5 步：出现符合的消息
第 6 步：出现奖金消息
第 7 步：出现不符合的消息

图 6-10 `ShiftBonus` 脚本的输出

### 使用逻辑运算符 221

如果你在 `ShiftBonus` 脚本中使用 `||` 运算符代替 `&&`，那么只要 `Status` 等于 `"H"` 或 `Shift` 等于 `3`，逻辑上就会奖发奖金。只需满足其中一个条件为真，真条件语句就会执行。使用正确的逻辑运算符至关重要。否则，可能会遇到逻辑问题。即使脚本在语法上是正确的，你用于设置脚本的逻辑也可能是错误的。

在接下来的示例中，Have Fun 酒店和度假软件公司的管理层决定根据席位人员接听电话的数量和处理完成电话的数量来奖励技术支持人员。`Calls Handled`（处理通话数）是一个人接听的电话。`Calls Closed`（关闭通话数）是客户满意的电话数量。以下是部分逻辑：

如果 `Calls Handled` > 150 或 `Calls Closed` > 50

```
Then

    Display "You are entitled to a bonus"

Else

    Display "You are only entitled to a bonus if the calls handled exceeds 150 or calls closed exceeds 50"

End-if
```

接下来，你将使用逻辑 OR 运算符为 Have Fun 酒店和度假软件公司创建脚本。

#### 要创建一个使用 `||` 运算符的脚本：

- 1. 在 `$HOME/bin` 目录下创建一个名为 `Calls` 的脚本。
- 2. 插入以下代码以从键盘读取数据，并插入一个使用 `||` 运算符的语句：

```
read -p "Enter the calls handled: " CallsHandled

read -p "Enter the calls closed: " CallsClosed

if [[ $CallsHandled -gt 150 || $CallsClosed -gt 50 ]]

then

    echo "You are entitled to a bonus"

    echo "You are only entitled to a bonus if the calls handled exceeds 150 or calls closed exceeds 50."

fi
```
- 3. 保存脚本，退出编辑器，然后使脚本具有可执行权限。
- 4. 执行脚本，在提示 `calls handled` 时输入 `159`，在提示 `calls closed` 时输入 `40`。参见图 6-11，出现一条表示你有获得奖金的消息。

## 第 6 章 决策结构

- 5. 再次执行脚本，在提示 `calls handled` 时输入 `120`，在提示 `calls closed` 时输入 `76`。参见图 6-11。出现一条表示你有获得奖金的消息。
- 6. 第三次运行脚本，在提示 `calls handled` 时输入 `76`，在提示 `calls closed` 时输入 `44`。参见图 6-11。出现一条表示你只有在处理通话超过 150 且关闭通话超过 50 的情况下才能获得奖金的消息。
- 7. 不要注销。

![](img/cad5396e3e49a03edb322ef333cfad40_553_0.png)

图 6-11 通话及相应输出

在类脚本中，考虑如果漏掉一个条件或使用 `||` 运算符，结果会如何。脚本在语法上是正确的，但在逻辑上是错误的，因为它不符合管理层的意愿。在第 4 到第 6 步的输入情况下，只有一名员工符合奖金条件，而不是两个。

在 Have Fun 酒店和度假软件公司的最后一个示例中，管理层创建了一个脚本，用于指示工龄 25 年的人员是否可以退休。以下是使用 NOT 逻辑运算符的部分逻辑。

### 使用逻辑运算符

如果 `Years of Service` NOT 小于 25

Then
Display "You can retire now.",

Else
Display "You will need 25 years to retire.",

End-if
接下来你将使用逻辑 NOT 运算符创建脚本。

#### 要创建一个使用 `!` 运算符的脚本：

1. 在 `$HOME/bin` 目录下创建一个名为 `Retire` 的脚本。
2. 插入以下代码以从键盘读取数据，并创建一个使用 `!` 运算符的 `if` 语句：

```
read -p "Years of Service: " Years

if [[ ! $Years -lt 25 ]]

then

echo "You can retire now."

else

echo "You will need 25 years to retire."

fi
```
- 3. 保存脚本，退出编辑器，然后使脚本具有可执行权限。
- 4. 执行脚本，在提示 `calls handled` 时输入 `32`，在提示 `calls closed` 时输入 `40`。参见图 6-11，出现一条表示你有获得奖金的消息。
- 5. 再次执行脚本，在提示 `calls handled` 时输入 `120`，在提示 `calls closed` 时输入 `76`。参见图 6-11。出现一条表示你有获得奖金的消息。
- 6. 第三次运行脚本，在提示 `calls handled` 时输入 `76`，在提示 `calls closed` 时输入 `44`。参见图 6-11。出现一条表示你只有在处理通话超过 150 且关闭通话超过 50 的情况下才能获得奖金的消息。
- 7. 不要注销。

## 第 6 章 决策结构

![](img/cad5396e3e49a03edb322ef333cfad40_555_0.png)

图 6-12 `Retire` 脚本及输出

### 使用逻辑运算符

如果你在 `ShiftBonus` 脚本中使用 `||` 运算符代替 `&&`，只要 `Status` 等于 `"H"` 或 `Shift` 等于 `3`，逻辑上就会奖发奖金。只需满足其中一个条件为真，真条件语句就会执行。使用正确的逻辑运算符至关重要。否则，可能会遇到逻辑问题。即使脚本在语法上是正确的，你用于设置脚本的逻辑也可能是错误的。

在接下来的示例中，Have Fun 酒店和度假软件公司的管理层决定根据席位人员接听电话的数量和处理完成电话的数量来奖励技术支持人员。`Calls Handled` 是一个人接听的电话。`Calls Closed` 是客户满意的电话数量。以下是部分逻辑：

如果 `Calls Handled` > 150 或 `Calls Closed` > 50

```
Then

    Display "You are entitled to a bonus"

Else

    Display "You are only entitled to a bonus if the calls handled exceeds 150 or calls closed exceeds 50"

End-if
```

接下来你将使用 OR 运算符为 Have Fun 酒店和度假软件公司创建脚本。

#### 要创建一个使用 `||` 运算符的脚本：

- 1. 在 `$HOME/bin` 目录下创建一个名为 `Calls` 的脚本。
- 2. 插入以下代码从键盘读取数据，并插入一个使用 `||` 运算符的语句：

```
read -p "Enter the calls handled: " CallsHandled

read -p "Enter the calls closed: " CallsClosed

if [[ $CallsHandled -gt 150 || $CallsClosed -gt 50 ]]

then

    echo "You are entitled to a bonus"

    echo "You are only entitled to a bonus if the calls handled exceeds 150 or calls closed exceeds 50."

fi
```
