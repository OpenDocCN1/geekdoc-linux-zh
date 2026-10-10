
## 代码清单 4.9
（续）

```pascal
Screen.Cursor := crHourglass;
try
  FCloneDS.SetRange([100], [199]);
  try
    FCloneDS.First;
    while not FCloneDS.EOF do begin
      FCloneDS.Edit;
      FCloneDS.FieldName('Salary').AsFloat := 50000.0;
      FCloneDS.Post;

      FCloneDS.Next;
    end;
  finally
    FCloneDS.CancelRange;
  end;
finally
  Screen.Cursor := crDefault;
end;
end.
```

图 4.7 展示了 Clone 应用程序在运行时的状态。

![](img/fe651f295b5f960d5463c4fb581d2281_203_0.png)

### 图 4.7
> *克隆的数据集对于插入和更新记录可能极其有用。*

查看这段代码，你可能会注意到几件事。其中之一是我在 FormCreate 方法中创建了克隆数据集，并在 FormDestroy 方法中销毁了它。我这样做是为了简化。在真实应用程序中，你通常会在需要它的方法中创建克隆，然后立即销毁它。在这个示例程序中，通过一次创建和销毁，我节省了几行代码。

“更新”按钮会遍历整个数据集，并给所有员工加薪 10%。请注意，即使代码没有调用 DisableControls（在本章开头附近有讨论），网格在遍历数据集时仍然不会滚动。这是因为网格连接到 ClientDataSet1，而更新是在克隆数据集上执行的。

“插入（第一部分）”和“插入（第二部分）”按钮在克隆上执行插入操作的两个部分。第一个按钮向数据集追加一个新记录并填入数据。第二个按钮将新记录提交到数据集，然后调用原始数据集上的 GoToCurrent 方法（将原始数据集与克隆同步）。GoToCurrent 使原始数据集跳转到克隆数据集的当前记录。

将插入操作分为两个按钮的原因是为了让你可以轻松看到插入过程中发生了什么。点击“插入（第一部分）”。现在向下滚动到网格底部。你不会看到网格中有一条对应员工 99999 的行——即新插入但尚未提交的记录。当你点击“插入（第二部分）”时，新记录会出现在网格中。相反，如果你将插入按钮事件处理程序中的代码改为使用 ClientDataSet1 而不是 FCloneDS，你会看到新记录在实际提交之前就会出现在网格中。

最后，“范围”按钮的工作方式与“更新”按钮非常相似：它对数据集应用一个范围，然后将该范围内所有员工的薪资设置为 50,000 美元。网格不会更新以反映该范围，因为该范围仅应用于克隆数据集，而不应用于 ClientDataSet1。

## 维护聚合

数据集中的记录通常不是彼此完全隔离的。很多时候，你希望获得整列或该列某一部分的总和或平均值。例如，你可能想要计算销售部门所有员工的平均薪资，或者你可能需要检索姓氏为 Jones 的员工数量。

如果你使用的是基于 SQL 的数据库，你可以发出 SQL 语句来计算这些值。例如，

```sql
SELECT AVG(SALARY) FROM EMPLOYEE WHERE DEPARTMENT = 'SALES';
SELECT COUNT(*) FROM EMPLOYEE WHERE LASTNAME = 'Jones';
```

然而，你不能直接对客户数据集执行 SQL 语句。

![](img/fe651f295b5f960d5463c4fb581d2281_204_0.png)

> 如果你通过数据库提供程序将客户数据集连接到 dBExpress 数据集，那么你可以向数据库后端发送 SQL 语句并在客户数据集中检索结果。这种技术在第 7 章中有讨论。

相反，客户数据集支持一种强大的功能，称为维护聚合。维护聚合会自动计算整个数据集（或一组记录）的总和、平均值、计数、最小值或最大值。

### 在设计时创建维护聚合

在设计时创建维护聚合类似于在设计时创建字段。与字段一样，维护聚合可以是持久性的或非持久性的。以下部分展示了如何创建每种类型。

#### 持久性聚合

你创建持久性聚合的方式与创建数据、计算或查找字段的方式非常相似。

- 1. 在窗体编辑器中右键点击客户数据集，并从弹出菜单中选择**字段编辑器**...
- 2. 按**Ins**键创建新字段。
- 3. 在**新字段**对话框中输入字段名和字段类型。对于维护聚合，字段类型应为*Aggregate*。
- 4. 在**字段类型**分组框中选择*Aggregate*单选按钮。
- 5. 点击**确定**以创建聚合。

图 4.8 展示了在添加了一个名为*AvgSalary*的聚合字段后的字段编辑器。

![](img/fe651f295b5f960d5463c4fb581d2281_205_0.png)

聚合创建完成后，你需要设置一些额外的属性（例如聚合表达式，以及聚合是否处于活动状态）。

- 1. 在字段编辑器中点击聚合字段。
- 2. 在**对象检查器**中，在*Expression*属性中输入聚合表达式。聚合表达式将在标题为“聚合表达式”的部分中讨论。暂时，你可以使用*Avg(Salary)*。
- 3. 将**Active**属性设置为**True**。默认情况下，聚合不处于活动状态，这意味着你无法访问它们。将**AggregatesActive**设置为**True**以激活聚合字段。

创建持久性聚合会自动创建一个类型为**TAggregateField**的组件，你可以用它来引用聚合值。然而，与大多数字段不同，你不使用**AsFloat**属性来获取聚合的值。相反，你使用**Value**属性，如下所示：

```pascal
ShowMessage('The average salary is ' + ClientDataSet1AvgSalary.Value);
```

因为**Value**是一个变体，你可以像它是字符串或浮点数一样引用它。因此，以下代码也是正确的：

```pascal
var
  AvgRaisedSalary: Double;
begin
  AvgRaisedSalary := ClientDataSet1AvgSalary.Value * 1.05;
end;
```

#### 非持久性聚合

要在设计时创建非持久性聚合，请点击窗体编辑器中的客户数据集，然后双击对象检查器中的**Aggregates**属性以显示聚合编辑器。

聚合编辑器看起来和运作起来很像字段编辑器。点击工具栏上的**添加新**按钮（或按**Ins**键）以创建新聚合。

同样，你需要设置一些额外的属性（例如聚合表达式，以及聚合是否处于活动状态）。

- 1. 在聚合编辑器中点击聚合。
- 2. 在**对象检查器**中，为聚合适中一个名称，例如**AvgSalary**。
- 3. 在**Expression**属性中输入一个聚合表达式，例如**Avg(Salary)**。
- 4. 将**Active**属性设置为**True**。
- 5. 将**AggregatesActive**设置为**True**。

与上一节不同，Delphi 不会为以这种方式使用创建的聚合创建组件。相反，你通过数据集的**Aggregates**属性访问聚合，如下所示：

```pascal
ShowMessage('The average salary is ' +
  ClientDataSet1.Aggregates.Find('AvgSalary').Value);
```

或者，如果你知道聚合的索引，你可以直接访问它：

```pascal
ShowMessage('The average salary is ' + ClientDataSet1.Aggregates[0].Value);
```

### 在运行时创建维护聚合

在运行时创建维护聚合类似于创建非持久性聚合，因为你利用了`Aggregates`属性。以下代码片段展示了如何在运行时创建聚合：

```pascal
var
  Aggregate: TAggregate;
begin
  Aggregate := ClientDataSet1.Aggregates.Add;
  Aggregate.AggregateName := 'AvgSalary';
  Aggregate.Expression := 'Avg(Salary)';
  Aggregate.Active := True;
end;
```

### 聚合表达式

在前面的代码片段中，我使用了表达式`Avg(Salary)`。正如你可能猜测的，该表达式计算`Salary`字段的平均值。

Delphi 支持表 4.6 中列出的聚合类型。

| 表 4.6 聚合类型 |
| :------------------------- | :------------------------------------------------------- |
| **聚合类型** | **描述** |
| Sum | 计算字段的总和。 |
| Avg | 计算字段的平均值。 |
| Count | 计算字段中非空白值的数量。 |
| Min | 计算字段的最小值。 |
| Max | 计算字段的最大值。 |

`Sum`和`Avg`只能用于数字字段类型；但`Count`、`Min`和`Max`可以用于数字、字符串或日期值。

聚合表达式不必是简单的表达式，如`Avg(Salary)`。它们可以包含多个函数，如`Sum(SalesPrice) - Sum(NetCost)`。然而，你不能嵌套函数。`Avg(Sum(SalesPrice))`不是一个有效的聚合表达式。

Delphi 帮助主题“指定聚合”提供了有效和无效聚合表达式的更多示例。

