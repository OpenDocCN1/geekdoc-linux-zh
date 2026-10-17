
## 6.2 创建一个程序，绘制 10 个具有随机颜色、位置和大小的填充圆（图 6.19）

`paintComponent` 方法应该包含一个迭代 10 次的循环。在每次迭代中，循环应该决定是绘制填充矩形还是椭圆，创建一个随机颜色和

随机选择坐标和维度。坐标应根据面板的宽度和高度选择。边的长度应限制为窗口宽度或高度的一半。

![](img/1df0d1e8ac6007b95647eb8ea38390af_315_0.png)

**图 6.18** 具有交替随机颜色的靶心。

![](img/1df0d1e8ac6007b95647eb8ea38390af_315_1.png)

**图 6.19** 随机生成的形状。

## 6.14 (可选) 软件工程案例：识别类操作

在第 3 至第 5 章末尾的软件工程案例章节中，我们执行了 ATM 系统对象设计的前几个步骤。在第 3 章中，我们识别了需要实现的类，并创建了我们的第一个类图。

### 6.14 识别类操作

在第 4 章中，我们描述了类的一些属性。在第 5 章中，我们检查了对象的状态，并对对象的状态转换和活动进行了建模。在本节中，我们确定了实现 ATM 系统所需的类操作（或行为）。

#### 识别操作

操作是类对象提供给该类客户端（用户）的服务。收音机的操作包括其调台和音量调节（通常由人员调整收音机控制装置调用）。汽车的操作包括加速（由驾驶员按下加速踏板调用）、减速（由驾驶员按下刹板调用）、转弯和换挡。软件对象也可以提供操作——例如，软件图形对象可以提供画圆、画线、画正方形和画线的操作。电子表格对象可能提供打印电子表格、计算行或列的总和以及将电子表格中的信息制成饼图等操作。

我们可以通过检查需求文档中的关键词和动词短语，推导出每个类的许多操作。我们将其中每一个操作与系统中的特定类相关联（图 6.20）。图 6.20 中的动词短语帮助我们确定每个类的操作。

#### 建模操作

为了识别操作，我们检查了图 6.20 中列出的每个类的动词短语。与 `ATM` 类关联的“执行金融交易”短语意味着 `ATM` 类构建了要执行的交易。因此，`BalanceInquiry`、`Withdrawal` 等类：

| ATM | 执行金融交易 |
| :--- | :--- |
| BalanceInquiry | [需求文档中无] |
| Withdrawal | [需求文档中无] |
| Deposit | [需求文档中无] |
| BankDatabase | 验证账户余额、检索账户余额、向账户存入存款金额、从账户扣除取款金额 |
| Account | 检索账户余额、向账户存入存款金额、从账户扣除取款金额 |
| Screen | 向用户显示消息 |
| Keypad | 接收用户的数字输入 |
| CashDispenser | 吐钞，指示其是否包含足够的现金以满足取款请求 |
| DepositSlot | 接收存款封 |

**图 6.20** ATM 系统中每个类的动词和动词短语。

为每个类添加所需的操作，以向 ATM 提供此服务。我们将此操作（我们命名为 `execute`）放在图 6.21 更新后的类图中三个事务类的第三个隔间中。在 ATM 会话期间，`ATM` 对象将根据需要调用这些操作。

UML 通过列出操作（在 Java 中实现为方法）来表示操作，后面跟一个括号内的逗号分隔的参数列表、冒号和返回类型：

```
operationName( parameter1, parameter2, ..., parameterN ) : return type
```

逗号分隔的参数列表中的每个参数都由参数名称、随后的冒号和参数类型组成：

```
parameterName : parameterType
```

目前，我们还没有列出操作的参数——稍后我们将识别并建模某些操作的参数。对于某些操作

![](img/1df0d1e8ac6007b95647eb8ea38390af_317_0.png)

| ATM | Account |
| :--- | :--- |
| userAuthenticated : Boolean = false | accountNumber : Integer |
|  | pin : Integer |
|  | availableBalance : Double |
| **BalanceInquiry** | totalBalance : Double validate() : Boolean |
| accountNumber : Integer | getAvailableBalance() : Double |
| execute() | getTotalBalance() : Double |
|  | credit() |
|  | debit() |
| **Withdrawal** | **Screen** |
| accountNumber : Integer | displayMessage() |
| amount : Double |  |
| execute() | **Keypad** |
| **Deposit** | getInput() : Integer |
| accountNumber : Integer |  |
| amount : Double |  |
| execute() |  |
| **BankDatabase** | **CashDispenser** |
| authenticateUser() : Boolean | count : Integer = 500 |
| getAvailableBalance() : Double | dispenseCash() |
| getTotalBalance() : Double | isSufficientCashAvailable() : Boolean |
| credit() | **DepositSlot** |
| debit() | isEnvelopeReceived() : Boolean |

**图 6.21** 具有属性和操作的 ATM 系统类。

## 第 6 章 方法：深入观察

我们不知道返回类型，因此也从图中删除了它们。这是封装和信息隐藏的良好示例。

# 274 第 6 章 方法：深入观察

如果这是一个真实的 ATM 系统，`BankDatabase` 类和 `Account` 类还应该提供一组操作，允许另一个银行系统在确认或拒绝全部或部分存款后，更新用户的账户余额。例如，`confirmDeposit` 操作将把金额添加到 `available` 属性中，使存入的资金可供取款。`rejectDeposit` 操作将从 `totalBalance` 中减去某个金额，以表示最近通过 ATM 存入并添加到 `totalBalance` 的指定金额在存款封中未找到。银行在确定用户是未包含正确金额的现金，还是由于任何支票未能兑现（即“支票退回”）后，将将调用此操作。虽然添加这些操作会使我们的系统更完整，但我们没有在类图或实现中包含它们，因为它们超出了本案例研究的范围。

`Screen` 类在 ATM 会话中向用户显示消息。视觉输出通过 ATM 屏幕实现。需求文档描述了屏幕显示给用户的多种类型的消息（例如：欢迎消息、错误消息、信息）。需求文档还指示了描述用户应该输入内容的消息，而菜单本质上是一种由一系列连续显示的消息（即菜单选项）组成的提示类型。因此，我们没有为 `Screen` 类分配一个单独的操作来通过参数显示每种消息、提示和任何消息，而是简单地在类图（图 6.21）中 `Screen` 类的第三隔间中创建了一个操作（`displayMessage`）。然后，我们现在暂不担心该操作的参数——我们将在本节的稍后部分对参数进行建模。

从“来自用户的数字输入”这一短语来看，`Keypad` 类应该执行 `getInput` 操作。在图 6.20 中，我们指示 `keypad` 类使用计算机键盘，仅包含数字 0-9，我们指定此操作返回一个整数值。回想需求，不同的用户可能被要求输入不同类型的数字（例如：账号、PIN 或菜单选项、以分数为单位的存款金额）。`Keypad` 类仅为该类的客户端获取一个数值——这意味着该操作必须验证用户在特定情况下是否输入了正确的数字，然后做出相应响应（即：通过 `Screen` 类显示错误消息）。[注：当我们实现系统时，我们用键盘模拟 ATM 的键盘，为了简单起见，我们假设用户不会使用 ATM 键盘上显示的按键输入非数字内容。]
