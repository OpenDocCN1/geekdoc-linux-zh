

## Extra

尽管超链接为用户从项目中的页面移动到互联网上的任何位置提供了一种简单的方法，但您可以使用代码在用户不主动点击超链接的情况下重定向用户。当用户点击按钮并需要转到新页面时，您可能希望重定向用户。例如，用户填写个人信息的表单以登录网站。当用户按下提交时，您可以将信息添加到数据库并将用户定向到成员页面。要进行重定向，请调用 Response 对象的 Redirect 方法。在括号中放置要加载的 URL。您无需将 URL 设为 Web 表单或项目内部的东西。您可以使用任何对客户端可访问的 URL。

示例：

```
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click

    Response.Redirect("webform2.aspx")

End Sub
```

![](img/d6f772854306e15fb6df39b861a7b541_266_0.png)

VB .NET 将新的 Web 表单添加到项目中。

- 5 打开一个可供客户端浏览器访问的表单，该表单需要打开新页面。
- 6 添加一个超链接控件并将 NavigateUrl 属性设置为新表单的名称。
- 注意：要创建超链接，请参阅“添加超链接控件”部分。
- 7 按 F5 运行您的项目。

项目构建新页面并在项目中显示默认页面。

您可以通过单击主页面上的超链接来访问新的 Web 表单。

## BIND A FIELD TO A LIST CONTROL

您可以将数据库字段绑定到列表控件，以便用户通过 Web 表单显示动态数据库信息。Web 表单的数据绑定是只读的，这意味着控件可以加载信息但不会将更改保存到数据集中。

在 Web 表单中，您最常使用列表控件进行绑定。ListBox、DropDownList、CheckBoxList 和 RadioButtonList 控件都显式支持数据绑定。您可以使用列表控件显示从数据源读取的项目。控件中的每个项目对应于数据源中的一行。控件显示源中的一个字段，并且可以选择使用第二个字段作为项目值。您可以选择将项目值设置为数据库中的唯一键字段，以便轻松定位要处理的记录。

要设置列表控件，请指定 DataSource 属性以引用页面的数据源，例如 DataSet 或 DataView 组件。有关创建数据库连接的更多信息，请参阅第 9 章。

您使用 DataTextField 属性指定控件显示的数据源字段。使用 DataValueField 指定用作项目值的字段。如果数据源只有一个字段，则无需设置这些属性，控件会自动显示该单个字段。

要更新每个绑定的控件，您必须调用其 DataBind 方法。或者，您可以调用表单的 DataBind 方法，它会绑定表单上包含绑定的每个控件。您只应在页面加载时以及数据更改时调用此方法。为确保页面不会在每次加载时重新绑定数据源，请检查 IsPostBack 属性。如果该属性为 False，则页面是首次加载，您需要绑定控件。

## BIND A FIELD TO A LIST CONTROL

- 1 创建新的 Web 应用程序项目或打开现有项目。
- 2 向页面添加数据源。
- 3 在工具箱中单击 ListBox、DropDownList、CheckBoxList 或 RadioButtonList 控件并将其添加到表单中。
- 注意：要创建数据库连接，请参阅第 9 章。有关 CheckBoxList 和 RadioButtonList 控件的更多信息，请参阅“使用选项列表控件”部分。
- 4 在属性窗口中单击 DataSource 并选择 DataSet 或 DataView。如果 DataSet 包含多个表，请单击 DataMember 并选择适当的表。
- 5 单击 DataTextField 并选择要显示的字段。可选地，单击 DataValueField 并选择指定项目值的字段。
- 6 双击页面。

![](img/d6f772854306e15fb6df39b861a7b541_267_0.png)

