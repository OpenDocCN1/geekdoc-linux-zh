

## 创建定时事件

你可以使用 Timer 控件在定义的时间间隔内运行代码。Timer 控件在后台工作，在表单上按指定间隔触发事件。你可以使用 Timer 控件的事件以时间增量执行后台处理，而不会中断用户。

Interval 属性指定事件触发前的间隔时间。Interval 是一个整数，指定以毫秒为单位的时间。默认值是 100，这意味着 100/1000 秒，或每秒 10 次。例如，你可以将一秒指定为 1000，一分钟指定为 60000。小于 50 的间隔在大多数机器上不可靠，可能不规律触发。

Enabled 属性决定控件是否主动触发事件。默认值为 False。如果你希望控件在表单加载后立即根据 Interval 开始触发事件，可以在设计时将此属性设置为 True。

要在程序运行时启动控件，请使用 Start 方法。要停止计时器，请使用 Stop 方法。如果事件已经触发，它会运行直到完成，即使你执行了 Stop。

放置计时器代码的事件称为 Tick。你可以在这里放置需要在每次计时器计数时运行的任何代码。

如果你的代码在下一个时间间隔到来之前没有完成，另一个 Tick 事件将被加载，创建大量等待的事件堆栈，这在大多数情况下会导致不可取的结果，如果持续时间较长，可能导致程序崩溃或计算机内存耗尽。请确保你的 Interval 足够长，以允许事件内部的代码完成。

![](img/d6f772854306e15fb6df39b861a7b541_81_0.png)

- 1. 创建一个新的 Windows 应用程序项目或打开一个现有项目。
- 2. 在工具箱中，双击 Timer 控件将其添加到表单。
- 3. 添加其他控件以显示 Timer 的活动。
  示例向表单添加了一个 Label 控件。
- 4. 单击组件托盘中的 Timer 控件以编辑其属性。
- 5. 在属性窗口中，在 Interval 属性中输入表示你希望事件触发速度的值。
- 6. 双击 Enabled 属性将其切换为 True。
- 7. 双击组件托盘中的 Timer 控件。
你以毫秒为单位指定 Interval 属性。

## 额外

你必须仔细开发应用程序才能使 Timer 控件正常工作。Timer 控件不在单独的线程中运行，这意味着它只有在应用程序处于空闲状态时才能工作。如果你的应用程序正在运行计算或密集的操作循环，并且你希望 Timer 控件同时工作，你必须调用 Application 对象的 DoEvents 方法。此方法允许其他排队的事件和操作发生，例如 Timer 控件的 Tick 事件和 UI 重绘。请记住，当你调用 DoEvents 时，诸如鼠标点击之类的事件会被触发，因此你必须确保用户不会再次尝试启动已经在进行中的操作。

### 示例：

```
Do
' do lots of processing
' ...
' let the application do any necessary queued actions
Application.DoEvents()
Loop Until done
```

![](img/d6f772854306e15fb6df39b861a7b541_82_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_82_1.png)

代码编辑器加载了 Tick 事件。

8 在控件触发 Tick 事件时输入要运行的代码。

在示例中，代码递增表单上的标签。

9 按 F5 运行项目。

Timer 会按 Interval 属性中指定的方式触发事件。

## 额外

ShowToday 属性允许你启用或禁用日历底部显示今天日期的标签。ShowTodayCircle 启用或禁用今天日期的红色圆圈显示，既在底部也在日历中显示。

你可以通过将 Format 更改为 Time 来设置 DateTimePicker 控件以允许显示和输入时间。你必须将 ShowUpDown 属性设置为 True 才能将 DateTimePicker 控件用作时间编辑器。

三个属性允许你存储要在日历中以粗体显示的日期。BoldedDates 属性存储一个 DateTime 变量数组，在日历上显示时以粗体显示。通过调用 AddBoldedDate 方法并传递 DateTime 类来添加 BoldedDate。MonthlyBoldedDates 数组使用每个存储的 DateTime 中给出的日期，但在日历上每个月都显示。你可以使用 AddMonthlyBoldedDate 方法添加每月日期。AnnuallyBoldedDates 使用每个 DateTime 中指定的月份和日期，并在每年该天显示。你使用 AddAnnuallyBoldedDate 方法添加年度粗体日期。

> 示例：

```
Dim Birthday As DateTime = New DateTime(2001, 8, 23)
Dim Deadline As DateTime = New DateTime(2001, 10, 25)
MonthCalendar1.AddAnnuallyBoldedDate(Birthday)
MonthCalendar1.AddBoldedDate(Deadline)
```

![](img/d6f772854306e15fb6df39b861a7b541_84_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_84_1.png)

8 代码编辑器窗口出现。

8 要访问所选日期，请键入日期控件的名称后跟一个句点。

9 对于 DateTimePicker，键入 Value；对于 MonthCalendar，键入 SelectionStart 或 SelectionEnd。

在示例中，Button1_Click 事件显示一个包含所选日期范围的消息框。

10 按 F5 运行项目

日期控件与用户交互并返回适当的选定内容。

