
# Java Studio Creator 2 允许你在拖放设计工具中开发应用程序的 GUI，同时在独立的 Java 类中处理业务逻辑。

## 第 26.4.1 节 Servlets

Servlets 使用客户端与服务器之间的 HTTP 请求-响应模型进行通信。

Servlets 通过允许服务器生成动态内容来扩展服务器的功能。Servlet 容器执行并与 servlet 交互。

`java.servlet` 和 `javax.servlet.http` 包提供了 servlet 类和接口。

Servlet 容器接收来自客户端的请求，并将每个请求定向到相应的 servlet。servlet 处理请求并向客户端返回响应——通常以 XHTML 或 XML 文档的形式。

所有 servlet 都使用 `java.servlet` 包中的 `servlet` 接口，这确保了每个 servlet 都能在提供的框架中执行。

中间层控制器逻辑处理客户端请求并从数据库检索数据。

中间层表示逻辑处理来自信息层的数据并将内容呈现给客户端。

Web 应用程序通常以 XHTML 文档的形式向客户端呈现数据。

中间的业务逻辑执行业务规则，并确保在服务器应用程序更新或将数据呈现给用户之前，数据是可靠的。

业务规则规定了客户端可以以及如何访问应用程序数据，以及应用程序如何处理数据。

顶层（或客户端层）是应用程序的用户界面，负责收集输入和显示输出。用户通过用户界面（通常是 Web 浏览器）与应用程序交互。

## 第 26.4.2 节 JSP 服务页面

Server Pages（JSP） 是 servlet 的扩展。

与 servlet 不同，JSP 帮助你将表示与逻辑分离。

JSP 允许通过自定义标签创建动态内容。

JSP 容器将 JSP 转换为 servlet。

JSP 有四种关键组件：指令（Directives）、动作（Actions）、脚本元素（Scripting elements）和标签库（Tag libraries）。

指令（Directives）用于向 JSP 定义页面设置。

动作（Actions）在 JSP 的生命周期内执行一次。

## 1300 第26章 Web 应用程序：第一部分

动作（Actions）在 JSP 中封装了功能。

脚本元素（Scripting elements）允许在 JSP 中插入 Java 代码。

标签库（Tag libraries）为 JSP 开发者提供了常用功能。

Java 页面标签库（JSTL）提供了许多常见的 Web 任务。

## 第 26.4.3 节 JavaServer Faces

JavaServer Faces (`JSF`) 是一种 Web 应用程序框架，它简化了用户界面的设计，并进一步分离了应用程序的表示。

框架通过提供库帮助你组织和构建应用程序。

`JSF` 提供的自定义标签简化了用户界面设计。`JSF` 还包含了一套处理事件的 API。

## 第 26.4.4 节 Java Studio Creator 2 中的 Web 技术

Studio Creator 2 Web 应用程序由 JavaServer Faces 框架中的多个 JSP 组成。每个 JSP 都有 `.jsp` 后缀并包含网页元素。

Studio Creator 2 允许你通过拖放 JSP 组件到页面上设计页面；你也可以通过手动编辑 `.jsp` 文件来自定义网页。

在 Studio Creator 2 中创建的每个 JSP 都代表一个网页，并有一个对应的 JavaBean 类。

JavaBean 类必须有一个默认（无参）构造函数，并为所有属性提供 `get` 和 `set` 方法。

# 总结 1301

用于应用程序范围的数据存储或处理；无论打开了多少会话，应用程序仅存在一个实例。

## 第 26.5.1 节 检查 JSP 文件

Java Studio Creator 2 根据你与可视化编辑器的交互生成 JSP 文件。

所有 JSP 都有一个 `JSP:root` 元素，带有一个版本属性用于表示使用的 JSP 版本，以及一个或多个 `xmlns` 属性。每个 `xmlns` 属性指定标签库的前缀和 URL，允许页面使用该库中指定的标签。

Java Studio Creator 2 生成的所有 JSP 均包含 JSF 核心组件库、JSP HTML 组件库、JSP 标准组件库和 JSP 用户界面库的标签库。

`j:directive.page` 元素的 `contentType` 属性指定了页面使用的 MIME 类型和字符集。`pageEncoding` 属性指定了页面源使用的字符编码。这些属性帮助客户端确定如何渲染内容。

所有包含 JSP 组件的页面都在组件树中表示，根 JSP 元素为 `f:view`（类型为 `uiView`）。所有的 JSP 组件元素都放置在此树中。

许多 UI 元素都有一个 `binding` 属性，将其值绑定到 Web JavaBeans 的属性上。使用 Web 表达式语言执行这些绑定。

`ui:head` 元素有一个 `title` 属性，指定页面标题。

`ui:link` 元素用于指定页面使用的 CSS 样式表。

`ui:body` 元素定义页面的主体。

`ui:static` 组件显示不改变的文本。

JSP 元素映射到 XHTML 元素以便在浏览器中渲染。同一个 JSP 元素根据客户端浏览器和组件的属性设置映射到不同的 XHTML 元素。

`ui:static` 组件通常映射到一个 XHTML `span` 元素。`span` 元素的文本显示在页面上并用于控制文本格式。当浏览器渲染页面时，`ui:static` 元素的 `style` 属性将作为相应 `span` 元素 `style` 属性的一部分。

## 第 26.5.2 节 检查 Page Bean 文件

Page bean 继承自 `AbstractPageBean`（包 `com.sun.rave.ui.appbean`），该类提供了页面生命周期方法。

包 `com.sun.rave.ui.component` 包含基本 JSP 组件的类。

`ui:static` 组件是一个 `StaticText` 对象（包 `com.sun.rave.ui.component`）。

## 第 26.5.3 节 事件处理生命周期

Java Studio Creator 2 的应用程序模型将多个方法（`init`、`preprocess`、`prerender` 和 `destroy`）放在页面 bean 中，进入 JSP 处理生命周期。这些方法代表了四个主要阶段：初始化、预处理、预渲染和销毁。

`init` 方法由 JSP 容器在第一次请求页面和回传（post-backs）时调用。当提交表单数据并将页面及其内容发送到服务器时就会发生回传。

`init` 方法调用其父类，然后尝试调用 `_init` 方法，该方法处理组件初始化任务。

`preprocess` 方法在 `init` 之后调用，但仅当页面正在渲染回传时调用。`prerender` 方法在浏览器渲染页面之前调用。该方法应用于设置组件属性；较早设置的属性（例如在 `init` 方法中设置）可能会在浏览器实际渲染页面之前被覆盖。

`destroy` 方法在页面渲染后调用，但仅当 `init` 方法被调用过时。该方法处理如释放渲染页面资源等任务。

## 第 26.5.4 节 JSP 与 Page Bean 文件之间的关系

Page bean 为 JSP 文件中的每个元素都拥有一个属性。

## 第 26.5.5 节 检查 Java Web 应用程序生成的 XHTML

要创建一个新的 Web 应用程序，选择 `File > New Project...` 显示“新项目”对话框。在对话框中，在 Categories（类别）中选择 `Web`，在 Projects（项目）中选择 `JSP Web Application` 并点击 `Next`（下一步）。指定项目名称和位置。点击 `Finish`（完成）创建 Web 应用。

当你创建一个新项目时，Java Studio Creator 会创建一个单个网页 `Page1`。当项目首次加载时，该页面在可视化编辑器的 Design（设计）模式下默认打开。当你将新组件拖放到页面上时，设计 模式允许你看到页面在浏览器中的渲染情况。此页面的 JSP 文件 `Page1.jsp` 可以通过点击可视化编辑器顶部的 JSP 按钮或点击可视化编辑器的任意位置并选择 `Edit Source`（编辑源代码）来查看。
