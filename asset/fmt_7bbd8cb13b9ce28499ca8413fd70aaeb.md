
**图 26.31** | 根据存储在 `session` 作用范围内的语言选择显示书籍推荐的 JSP 文件。（2 部分中的第 2 部分。）

### 从 SessionBean 属性创建书籍推荐的 Page Bean

图 26.32 展示了 `Recommendations.jsp` 的 page bean。再次，大部分内容与 cookie 示例中使用的 page bean 相似。我们只讨论新功能。

```java
// 图 26.32: Recommendations.java
// 根据 SessionBean 属性显示书籍推荐的 page bean。
package session;

import com.sun.rave.web.ui.appbase.AbstractPageBean;
import com.sun.rave.web.ui.component.Body;
import com.sun.rave.web.ui.component.Form;
import com.sun.rave.web.ui.component.Head;
import com.sun.rave.web.ui.component.Html;
import com.sun.rave.web.ui.component.Link;
import com.sun.rave.web.ui.component.Page;
import javax.faces.FacesException;
import com.sun.rave.web.ui.component.Listbox;
import com.sun.rave.web.ui.component.Label;
import com.sun.rave.web.ui.component.Hyperlink;
import com.sun.rave.web.ui.model.DefaultOptionsList;
import java.util.Enumeration;
import com.sun.rave.web.ui.model.Option;
import java.util.Properties;

public class Recommendations extends AbstractPageBean
{
    private int ___placeholder;
```

**图 26.32** | 根据 SessionBean 属性显示书籍推荐的 page bean。（3 部分中的第 1 部分。）

```java
private void _init() throws Exception
{
    // 空主体
    // 结束方法 _init
}
// 为了节省空间，我们省略了第 31-150 行的代码。完整的
// 源代码随本章示例一同提供。
public void Recommendations()
{
    // 空构造函数
    // 结束构造函数
}
protected RequestBean getRequestBean() {
    return (RequestBean) getBean("RequestBean");
    // 结束方法 getBean
}
protected ApplicationBean getApplicationBean() {
    return (ApplicationBean) getBean("ApplicationBean");
    // 结束方法 getBean
}
protected SessionBean getSessionBean() {
    return (SessionBean) getBean("SessionBean");
    // 结束方法 getBean
}
public void init() {
    super.init();
    try {
        _init();
    } // 结束 try
    catch (Exception e) {
        log("Recommendations", e);
        throw new FacesException(e);
    } // 结束 catch
} // 结束方法 init
public void preprocess() {
    // 空主体
    // 结束方法 preprocess
}
public void prerender() {
    // 从 SessionBean 获取选择
    Properties languages = getSessionBean();
    Enumeration selectionsEnum = languages.name();
    int numSelected = getSessionBean().getNumSelections();

    // 如果至少有一个选择
    if (numSelected > 0) {
        Option recommendations = new Option[numSelected];
        for (int i = 0; i < numSelected; i++) {
            String language = (String) selectionsEnum.nextElement();
            recommendations[i] = new Option(
                language));
        } // 结束 for
    } // 结束 if
    else {
        Option recommendations = new Option[1];
        recommendations[0] = new Option(
            "Please select a language.");
    } // 结束 else

    booksListBox.items(recommendations);
} // 结束方法 prerender
```

**图 26.32** | 根据 SessionBean 属性显示书籍推荐的 page bean。（3 部分中的第 2 部分。）

## 总结

## 第 26.1 节 引言

- 基于 Web 的应用程序为浏览器客户端创建 Web 内容。
- AJAX 帮助基于 Web 的应用程序提供用户通常在桌面应用程序中期望的交互性和响应。

## 第 26.2 节 HTTP 事务

- 超文本传输协议（HTTP）规定了一系列方法和请求头，允许客户端和服务器以统一且可靠的方式进行交互和信息交换。
- 在最简单的形式下，网页无非是一个 XHTML 文档，其中包含描述 Web 浏览器如何显示和格式化文档信息的标记（markup）。
- XHTML 文档可以包含超文本（超链接），当用户点击链接时链接到不同的页面或同一页面的其他部分。
- HTTP 使用 URL（统一资源标识符）来标识互联网上的数据。
- 指定文档位置的 URI 称为 URL（统一资源定位符）。常见的 URL 指向文件或目录，并可以引用这些对象。
- URL 包含了引导浏览器访问用户想要访问的资源的信息。运行 Web 软件的计算机提供了此类资源。
- 当给定一个 URL 时，Web 浏览器会执行简单的 HTTP 事务来检索并显示该地址的网页。
- HTTP 方法指示客户端想要从服务器获取某个资源。
- HTTP 头部提供了有关发送到客户端的数据的信息，例如 MIME 类型。
- 多用途互联网邮件扩展（MIME）是一项互联网标准，规定了程序可以正确解释数据的数据格式。

## 第 26.3 节 多层应用程序架构

- 基于 Web 的应用程序是多层（或 n 层）应用程序，它们将功能划分为驻在不同计算机上的层级。
- 最底层（也称为数据层或信息层）维护应用程序的数据。该层通常将数据存储在关系型数据库管理系统（RDBMS）中。
- 中间层实现业务逻辑、控制器逻辑和表示逻辑，以控制应用程序客户端与数据之间的交互。中间层在信息层和应用程序客户端之间充当中间节点。
- 中间层控制器逻辑处理客户端请求并从数据库检索数据。
- 中间层表示逻辑处理来自信息层的数据并将内容呈现给客户端。
- Web 应用程序通常以 XHTML 文档的形式向客户端呈现数据。
- 中间的业务逻辑执行业务规则，并确保在服务器应用程序更新或将数据呈现给用户之前，数据是可靠的。
- 业务规则规定了客户端可以以及如何访问应用程序数据，以及应用程序如何处理数据。
- 顶层（或客户端层）是应用程序的用户界面，负责收集输入和显示输出。用户通过用户界面（通常是 Web 浏览器）与应用程序交互。

## 总结 1299

- 为了响应用户操作，客户端层与中间层交互以发出请求并从信息层检索数据。然后客户端层为用户显示检索到的数据。客户端层直接与信息层交互。

## 第 26.4 节 Java Web 技术

- Java Web 技术不断演进，为开发者提供更高层次的抽象和应用程序层级之间更好的分离。这种分离使得 Web 应用程序更具可维护性和扩展性。
