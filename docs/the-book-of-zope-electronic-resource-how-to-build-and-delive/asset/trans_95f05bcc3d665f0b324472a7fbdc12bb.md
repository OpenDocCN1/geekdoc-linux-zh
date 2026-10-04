

```
<dtml-call "propertiesheets.Book_description.manage_editProperties(REQUEST)">
```

此行代码调用了我们 Book_Description 属性表上的内置方法 `manage_editProperties`，并传递了包含表单中输入的所有值的 `REQUEST` 对象。该方法将新 Book 实例的属性值设置为输入表单（BookClass_addForm）中指定的值。

## 3. 插入行

```
<dtml-if NoRedir>
<dtml-else>
```

在以下行之间：

```
<dtml-with>
```

和

```
<dtml-if DestinationURL>
```

最后几行代码，即：

```
<dtml-if DestinationURL>
<dtml-call>
"RESPONSE.redirect(DestinationURL+'//manage_workspace')"
<dtml-else>
<dtml-call "RESPONSE.redirect(URL2+'//manage_workspace')")
</dtml-if>
```

当你使用文件夹的添加菜单创建书籍时，这些代码将将你带到正确的管理界面。从那里，你将被重定向到你创建书籍的文件夹的内容视图。然而，如果你想使用 DTML 代码创建书籍实例，则不需要执行此重定向——因为你将使用你自己的 DTML 方法，而不是内置的 Zope 管理界面。在修改后的构造方法中，你将指定创建书籍后要显示哪个界面。

## 4. 关闭步骤 3 中的 <dtml-else> 标签

```
</dtml-if>
```

并在其之后插入以下几行：

```
<dtml-if>
</dtml-with>
```

5. 点击“保存更改”。DTML 方法 `BookClass_add` 现在看起来应该如列表 10-3 所示。

## 列表 10-3：修改后的 BookClass_add

```
<HTML>
<HEAD><TITLE>BookClass</TITLE></HEAD>
<BODY COLOR="#FFFFFF" VLINK="#555555">
<html-with "BookClass.createObject(REQUEST['id'], REQUEST)">
<html-call "propyertysheets.Book_description.manage_editProperties(REQUEST)">
<html-if NoRedir>
<html-return name="this">
<html-else>
<html-if DestinationURL>
<html-call>
<RESPONSE.redirect(DestinationURL+'//manage_workspace')
<html-else>
<html-call "RESPONSE.redirect(URL2+'/manage_workspace')"
</html-if>
</html-if>
</html-with>
<body>
</html>
```

列表 10-3 的最后几行重定向到文件夹 `manage_workspace`，一旦你创建了对象，就会出现在那里。例如，如果你在文件夹中创建一个 id 为 `B0193` 的书籍，完成后你会发现回到该文件夹。如果你尝试在产品内部查看此方法，将得到 Zope 错误。要对其进行测试，你必须从添加表单（BookClass_addForm）调用它。

### 10.1.2 使用 ZClasses 创建对象

在我们测试 ZClass 之前，需要先创建一个文件夹来容纳我们的 Book 实例。方法如下：

- 1. 打开根文件夹，通过从添加菜单选择 Folder（文件夹）来创建一个文件夹。
- 2. 在 Id 字段中输入 Books，取消勾选两个复选框，并点击 Add。
- 3. 打开你的新文件夹，从添加菜单选择 Book（或第 9.3 节指定的 ZClass 元类型）。
- 4. 来自 DTML 方法 `BookClass_add` 的输入表单。输入书籍数据并点击 Create，如图 10-3 所示。

## 创建书籍

| 字段 | 值 |
|---|---|
| 书籍 ID | B09362 |
| 标题 | The Sickness unto Death |
| 作者 | Soren Kieregaard |
| 出版社 | Penguin USA |
| 出版日期 | 1989 |
| 体裁 | 哲学 |
| 价格 | 13.95 |
| 交货时间 | 3 天 |

图 10-3：创建对象

你现在应该在 Books 文件夹中看到对象 `B09362`，如图 10-4 所示。

![](img/43a28cce5475b2f487bf45536567fb6_202_0.png)

图 10-4：创建对象 B09362 后的管理界面

- 5. 使用以下详情创建另一个书籍：

| 字段 | 值 |
|---|---|
| 书籍 ID | B19381 |
| 标题 | Dead Zone |
| 作者 | Stephen King |
| 出版社 | Viking |
| 出版年份 | 1987 |
| 体裁 | 惊悚 |
| 价格 | 35.00 |
| 交货时间 | 2 天 |

你现在已经通过在 Books 文件夹的添加菜单中选择 Book 创建了两个对象。

### 10.1.3 类工厂

如果你好奇为什么当你从可用对象（Available Objects）菜单中选择 Book 时，Zope 知道使用 ZClass，请查看对象 `BookClass_factory`（如图 10-5 所示），它是当你创建 ZClass 时由 Zope 自动创建的。

如图 10-5 所示，在工厂中，当选择 Book 时将调用 DTML 方法 `BookClass_addform`。

![](img/43a28cce5475b2f487bf45536567fb6_203_0.png)

图 10-5：BookClass_factory

为了让你的 ZClass 正常工作，请确保工厂中的名称与文件夹中的元类型一致。

## 10.2 运行

在这个示例应用程序中，我们的目标是：

- 使用管理界面管理书籍。
- 为游客提供书籍。
- 为了做到这一点，我们需要：
    - `adminhtml` 页面。
    - `indexhtml` 页面（见 10.3 节）。

这两种方法 `adminhtml` 和 `indexhtml` 非常相似，区别在于 `indexhtml` 允许看到书籍。

## 10.3 如何编辑你的书籍

当你创建书籍时，可以进入文件夹管理界面（如图 10-4 所示），遵循以下步骤：

- 1. **添加**：通过菜单选择书籍。点击 Add 会调用 `BookClass_add`。
- 2. **删除**：勾选书籍旁边的复选框并点击 Delete。
- 3. **编辑**：点击书籍旁边的属性。

你可以通过在 Books 文件夹的添加菜单中选择 Book 创建对象。

### 10.3.1 在文件夹中进行界面

10-4 显示了用于管理书籍的界面，你可以通过它进行添加、编辑或删除操作。

