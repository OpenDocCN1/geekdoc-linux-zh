
```
<?xml version="1.0" encoding="UTF-8"?>

<!-- 图 26.17 WebComponents.jsp -->

<!-- 示例如一个演示 JSF 组件的注册表单。 -->

<jsf:root version="1.2" xmlns:f="http://java.sun.com/jsf/core"

xmlns:h="http://java.sun.com/jsf/html" xmlns:ui="http://www.sun.com/web/ui">

<jsp:directive page contentType="text/html" charset="UTF-8"

encoding="UTF-8">

<f:view>

 <ui:page page="#{WebComponents.page}" id="page">

 <ui:html html="#{WebComponents.html}" id="html">

  <ui:head header="#{WebComponents.header}" id="head">

   <ui:link binding="#{WebComponents.link}" id="link"

   url="/resources/stylesheet.css"/>

  </ui:head>

  <ui:body body="#{WebComponents.body}" id="body"

   style="-layout: grid">

   <ui:form binding="#{WebComponents.form}" id="form">

    <ui:staticText binding="#{WebComponents.header}"

    id="header" style="font-size:18px; top:24px; position:absolute; left:24px" text="这是一个注册表单。"/>

    <ui:staticText binding="#{WebComponents.instructions}"

    id="instructions" style="font-style: italic; left:24px; top:72px; position: absolute" text="请填写所有字段并点击 Register。"/>

   </ui:form>

  </ui:body>

 </ui:page>

</f:view>

```
**图. 26.17** | 演示 JSF 组件的注册表单。（3部分中的1部分）

## 26.6 JSF 组件

在讨论此 JSP 文件中使用的 JSF 组件之前，我们先解释创建图 26.17 布局的 XHTML。如之前讨论过的，Java Studio Creator 使用绝对定位，因此组件会在它们在可视化编辑器中被放置的位置进行渲染。在本例中，除了绝对定位外，我们还使用了调色板布局组件中的网格面板（Grid Panel）组件（31–52）。`h:` 前缀表示可以在 JSF HTML 标签库找到找到。该组件是 `javas.content.html` 包中 `HtmlGrid` 类的对象，控制其包含的组件的位置。网格面板组件允许设计人员指定网格应包含的列数。然后可以将组件拖放到面板内的任何位置，它们将按照拖放的顺序自动重新排列为间距均匀的列。当组件数量超过列数时，面板会将额外的组件移动到新的一行。通过这种方式，网格面板的行为类似于 XHTML 表格，并且实际上由浏览器渲染为 XHTML 表格。在本例中，我们使用网格面板来控制页面用户信息部分中图像和文本字段组件的位置。

## 在网页上添加表单组件

要创建图 26.17 表单用户信息部分的布局，将网格面板组件拖到页面上。在属性窗口中，将组件的 `columns` 属性设置为 4。该组件还具有单元格填充、间距及其外观其他元素的属性。在这种情况下，接受这些属性的默认值。现在你可以将用户信息的图像和文本字段拖入网格面板中。网格面板将管理它们的间距并按行和列进行组织。

## 检查示例注册表上的 Web 组件

图 26.17 的第 28–31 行定义了一个图像（Image）组件，它是 `Image` 类的对象，用于向网页插入图像。本示例中使用的图像位于本章的示例中。显示在网页上的图像必须放置在项目的资源文件夹中。要向项目添加图像，将图像组件拖到页面，并点击属性窗口中 `url` 属性旁边的省略号按钮。这将打开一个对话框，你可以在其中选择要显示的图像。由于尚未向资源文件夹添加任何图像，请点击 `Add File` 按钮，在计算机的文件系统中找到该图像并点击 `Add File`。你选择的文件将出现在资源目录的文件列表中。现在点击 OK 将图像插入到项目中。

第 31–52 行包含网格面板组件。在该元素内部有八个图像和文本字段组件。文本字段（Text Fields）允许你获取用户的输入内容。例如，第 37–38 行定义了一个文本字段控件来收集用户的名字。第 49–51 行定义了一个文本字段，其 `label` 属性设置为“Be in the form (555) 555–5555”。设置文本字段的 `label` 属性会将文本直接放在文本字段上方。或者，你也可以通过将标签（Label）组件拖放到面板上来为文本字段设置标签，这允许你自定义标签的位置和样式。

将文本字段拖到页面上的顺序很重要，因为 JSP 标签是按该顺序添加到 JSP 文件中的。当用户按下 Tab 键时，这些字段将按照 JSP 标签在 JSP 文件中出现的顺序进行导航。要指定导航顺序，你可以按照该顺序将组件拖到页面上。或者，你可以在属性中设置每个字段的 `Tab Index` 属性，以控制用户在字段之间切换的顺序。索引为 1 的组件将是制表序列中的第一个。

第 62–65 行定义了一个下拉列表（Drop Down List）。当用户点击下拉列表时，它会展开并显示列表，用户从中可以选择一个组件。该组件是 `DropDownList` 类，并绑定到控制选项的 `books` 对象。可以通过在设计模式下右键点击下拉列表并选择 `Configure Default Options` 配置默认选项）来自动配置此组件，这将打开 `Options` 对话框向列表添加选项。每个选项都包含一个在浏览器中代表该选项的显示字符串（String）和一个在程序化从下拉列表检索用户选择时返回的数值字符串（String）。Java Studio Creator 2 在 Custom 对话框中构造 `SingleSelectOptionsList`，它在页面文件中显示值。要查看该对象，点击 OK 关闭对话框，打开页面文件，并编辑页面顶部附近的 Created-Managed Component Definition 创建托管组件定义）。对象在 `_init` 方法中构造，该方法在页面首次加载时被调用。

超链接（Hyperlink）组件的 `url` 属性指定了用户点击超链接时请求的资源（在本中 http://www.deitel.com）。将 `target` 属性设置为 `_blank` 表示请求的网页应在新的浏览器窗口中打开。默认，超链接组件使用 `page` 在同一个浏览器窗口中打开。

第 78–82 行定义了一个 `radioButton` 类的单选组（Radio Button Group），它提供了一系列按钮，用户从中选择一个。与下拉列表类似，单选组绑定到 `SingleSelect` 对象。可以通过点击组件并设置 `Configure Default Options` 来编辑选项。同样通过下拉列表，IDE 会自动生成 `SingleSelectOptionsList` 并将其放置在页面文件的 `_init` 方法中。

26.17 中的最后一个 Web 控件是按钮（Button）（第 83–85 行），这是一个 JSF 组件。

## 26.2 使用组件和自定义验证器

确保用户在必填输入中进行了选择或输入了文本是一种基础类型的验证。这是通过勾选元素属性窗口中的 `required` 框来实现的。如果你向输入字段添加验证器或自定义验证器，该字段的 `required` 属性必须设置为 true。

## 在 Web 中验证数据

确保用户在必填输入中进行了选择或输入了文本是一种基础类型的验证。这是通过勾选元素属性窗口中的 `required` 框来实现的。如果你向输入字段添加验证器或自定义验证器，该字段的 `required` 属性必须设置为 true。

发生。请注意，此示例中的三个输入 `ui:textField`（图 26.18，第 30–44 行）的 `required` 属性均已设置为 `true`。同时请注意在可视化编辑器（Visual Editor）中，必填字段的标签会自动用红色星号标记。如果用户提交带有空字段的表单，必填字段的默认错误消息将显示空字段关联的 `ui:message` 内容。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- Fig.26.18: Validation.jsp -->
```
