
```java
46 private Properties books = new Properties();
47 public Options()
48 {
49 初始化要存储在
50 // session bean 中的
51 // 值 Properties 对象。
52 books.setProperty("Java", 
53 books.setProperty("C", 
54 books.setProperty("C++", 
55 books.setProperty("Visual Basic 2005", 
56 books.setProperty("Visual C# 2005"));
57 } // end constructor
58 protected ApplicationBean getApplicationBean()
59 {
60 return (ApplicationBean1) getBean("ApplicationBean");
61 } // end method getApplicationBean
62 protected RequestBean getBean()
63 {
64 return (RequestBean) getBean();
65 } 
```

**图 26.30** | 在 SessionBean 属性中存储语言选择的 page bean。（4 部分中的第 1。）

## 26 Web 应用：第一部分

```java
    protected SessionBean getApplicationBean()
    {
        return (ApplicationBean1) getBean("ApplicationBean");
    } // end method getApplicationBean

    public void init()
    {
        super.init();
        try {
            _init();
        } // end try
        catch (Exception e) {
            log("SessionBean Initialization Failure", e);
            throw e instanceof FacesException ? FacesException(e) :
            new FacesException(e);
        } // end catch
    } // end method init

    public void passivate()
    {
        // 空方法体
    } // end method passivate

    public void activate()
    {
        // 空方法体
    } // end method activate

    public void destroy()
    {
        // 空方法体
    } // end method destroy

    private int numSelections = 0; // 存储唯一选择的数量
    public int getNumSelections()
    {
        return this.numSelections;
    } // end method getNumSelections

    public void setNumSelections(int numSelections)
    {
        this.numSelections = numSelections;
    } // end method setNumSelections

    // 存储已选语言的键值对
    private Properties selectedProperties = new Properties();

    public Properties getSelectedLanguages()
    {
        return this.selectedLanguages;
    } // end method getSelectedLanguages

    public void setSelectedLanguages(Properties selectedLanguages)
    {
        this.selectedLanguages = selectedLanguages;
    } // end method setSelectedLanguages
} // end class SessionBean
```

**图 26.29** | 用于存储语言选择的 SessionBean。（3 部分中的第 3。）

## 26.7 会话跟踪 1293

### 软件工程观察 26.2

使用 SessionBean 属性（而不是 cookie）的用处是，它们可以将任何类型的对象（而不只是字符串）作为属性值存储。这让您在维护客户端状态信息时具有更大的灵活性。

## 根据会话值显示推荐

如示例所示，此应用程序提供了一个指向 Recommendations.jsp（图 26.31）的链接，该页面根据用户的语言选择显示书籍推荐列表。它与示例中的 recommendation.jsp（图 26.23）完全相同。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- 图 26.31: Recommendations.jsp -->
<!-- 该 JSP 文件根据存储在 session 作用范围内的语言
<!-- 选择来显示书籍推荐。 -->
<jsp:root0="1" xmlns:f="http://java.sun.com/jsp/core"
xmlns:j="http://java.sun.com/jsp/html" xmlns:ui="http://www.sun.com/web/ui">
<jsp:directive content="text/html; charset=UTF-8"
encoding="UTF-8"/>
<f:view>
<ui:page binding="#{Recommendations.page}" id="page">
<ui:html binding="#{Recommendations.html}" id="html">
<ui:head binding="#{Recommendations.head}" id="head">
<ui:link binding="#{Recommendations.link}" id="link"
url="/resources/stylesheets.css" />
</ui:head>
<ui:body binding="#{Recommendations.body}" id="body"
style="-ave-layout: grid">
<ui:form binding="#{Recommendations.form}" id="form">
<ui:label binding="#{Recommendations.languageLabel}" 
for="ListBoxBox" id="languageLabel" style="-
font-size:20px; font-weight:bold; left:24px; top:24px; position:absolute; text=""/>
<ui:listbox binding="#{Recommendations.bookListBox}" id="nListBoxItem" items="#{Recommendations.
bookslistDefaultOptions.options}" rows="0"
style="left:24px; top:72px; position: absolute;
width:360px"/>
<ui:hyperlink action="case1binding" id="optionsLink"
style="left:24px; top:192px; position: absolute"
value="Click here to choose another language."/>
</ui:form>
</ui:body>
</ui:html>
</ui:page>
</f:view>
</jsp:root0>
```

**图 26.31** 根据存储在 session 作用范围内的语言选择显示书籍推荐的 JSP 文件。（2 部分中的第 1 部分）

![](img/1df0d1e8ac6007b95647eb8ea38390af_1338_0.png)

## 1294 第26 章 Web ：第一部分

![](img/1df0d1e8ac6007b95647eb8ea38390af_1339_0.png)
