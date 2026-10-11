
<html><html>

<title>SiteSelector</title>

<body>

  <applet name="SiteSelector.class" width="300" height="75">

    <param name="title0" value="Java Home Page">

    <param name="location0" value="http://www.sun.com/"/>

    <param name="title1" value="Deitel">

    <param name="location1" value="http://www.deitel.com/"/>

    <param name="title2" value="JGuru">

    <param name="location2" value="http://www.jGuru.com/"/>

    <param name="title3" value="Javaaworld">

    <param name="location3" value="http://www.javaworld.com/">

  </applet>

</body>

</html>
```

**Fig. 24.1** 用于加载 `SiteSelector` applet 的 HTML 文档。

```java
// Fig. 24.2: SiteSelector.java
// 此程序从 URL 加载文档。

import java.net.MalformedURLException;
import java.net.URL;
import java.util.HashMap;
import java.util.ArrayList;
import java.awt.GridLayout;
import java.applet.AppletContext;
import javax.swing.JApplet;
import javax.swing.JLabel;
import javax.swing.JList;
import javax.swing.JScrollPane;
import javax.swing.event.ListSelectionEvent;
import javax.swing.event.ListSelectionListener;

public class SiteSelector extends JApplet {
  private HashMap<Object, Object> sites; // 名称和 URL
  private ArrayList<String> siteNames;
  private JList siteChooser; // 可选站点列表

  // 读取 HTML 参数并设置 GUI
  public void init() {
    sites = new HashMap<Object, Object>(); // 创建 HashMap
    siteNames = new ArrayList<String>(); // 创建 ArrayList
```

**Fig. 24.2** 从 URL 字符串加载文档到浏览器。（3 部分中的 1 部分）

## 24.2 操作 URL

```java
// 从 HTML 文档中获取参数
getSitesFromHTMLParameters();
```

```java
// 创建 GUI 组件并布局界面
add(new JLabel("Choose a site to browse"), BorderLayout.NORTH);
```

```java
siteChooser = new JList(siteNames.toArray()); // 填充 JList
siteChooser.addSelectionListener( // 匿名内部类
new ListSelectionListener() {
```

```java
// 跳转到选定的站点
public void valueChanged(ListSelectionEvent event) {
  // 获取选定的站点名称
  Object object = siteChooser.getSelectedValue();
  // 使用名称定位对应的 URL
  URL newDocument = sites.get(object);
  // 获取 applet 容器
  AppletContext browser = getAppContext();
  // 通知 applet 切换页面
  browser.showDocument(newDocument);
} // 方法 value 结束
} // 匿名类结束
); // addSelectionListener 调用结束
```

```java
add(new JScrollPane(siteChooser), BorderLayout.CENTER);
} // 方法 init 结束
```

```java
title = getParameter("title" + counter); // 获取第一个站点标题
// 循环直到 HTML 文档中没有更多参数
while (title != null) {
  // 获取站点位置
  location = getParameter("location" + counter);
  try {
    // 将标题/URL 存入 HashMap 和 ArrayList
    URL url = new URL(location); // 将位置转换为 URL
    sites.put(title, url); // 将标题/URL 存入 HashMap
    siteNames.add(title); // 将标题存 ArrayList
  } // try 结束
  counter++;
}
```

**Fig. 24.2** 从 URL 加载文档到浏览器。（3 部分中的 2 部分）

```java
catch (MalformedURLException urlException) {
    urlException.printStackTrace();
} // catch 结束
counter++;
title = getParameter("title" + counter); // 获取下一个站点标题
} // while 结束
} // 方法 getSitesFromHTMLParameters 结束
} // 类 SiteSelector 结束
```

![](img/1df0d1e8ac6007b95647eb8ea38390af_1157_0.png)

**Fig. 24.2** 从 URL 加载文档到浏览器。（3 部分中的 3 部分）

该 applet 利用了调用它的 HTML 文档中指定的 applet 参数。在浏览万维网时，你经常会遇到属于公有领域的 applet——你可以在自己的网页上免费使用它们（通常是以引用该 applet 创建者作为交换）。许多 applet 都可以通过调用 applet 的 HTML 文件所提供的参数进行自定义。例如，图 24.1 包含了调用图 24.2 中 `SiteSelector` applet 的 HTML。

![](img/1df0d1e8ac6007b95647eb8ea38390af_1157_1.png)

## 24.2 操作 URL

HTML 文档包含通过 `param` 标签指定的 8 个参数——这些行必须出现在开始和结束标签之间。applet 可以读取这些值并使用它们进行自定义。任意数量的 `param` 标签都可以出现在开始和结束 applet 标签之间。每个参数都有一个名称和一个值。`getParameter` 方法检索与特定参数关联的值并作为字符串返回。传递给 `getParameter` 的参数是包含元素名称的字符串。在本例中，参数代表用户可以选择的每个站点的标题和位置。该 applet 的参数名为 `title#`，其中 `#` 的值从 0 开始，每个新标题递增 1。每个标题都应该有一个对应的 `location#` 参数，其中 `#` 的值从 0 开始，每个新标题递增 1。

（注：原文后续部分存在大量 OCR 重复文本错误，已根据指令要求进行清理处理。）

## 24.3 在 Web 服务器上读取文件

```java
// 图. 24.3: ReadServerFile.java
// 使用 JEditorPane 显示 Web 服务器上的文件内容。

import java.awt.BorderLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.IOException;
```
