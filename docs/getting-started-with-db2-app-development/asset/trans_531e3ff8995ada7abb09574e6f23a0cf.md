

## 112 DB2 应用程序开发入门

![](img/5f6ba170efa3a607142589708531bef8_111_0.png)

**图 3.15 – 创建数据 Web 服务**

虽然您已创建了一个 Web 服务，但它目前没有任何方法或操作。要向 Web 服务添加操作，您只需将之前在 Data Studio 中创建的存储过程或 SQL 脚本拖放到该服务中即可。例如，请查看下方的图 3.16。

上图展示了存储过程 `GETALLEMP`，它基于语句 `SELECT * FROM EMPLOYEE.` 返回一个游标。在该过程被部署和测试之后，只需将其拖放到 Web 服务 **MyWebService** 中，即可简单地将其作为该 Web 服务的操作添加进来，如图中高亮所示。对于之前创建的 SQL 脚本，甚至对于已经部署到数据库并从数据源资源管理器视图中找到的存储过程，也可以执行类似的操作。

一旦 Web 服务至少包含一个操作，您可以通过选择该 Web 服务，右键单击它并选择 *Build and Deploy*（构建并部署）来构建和部署它，如下图所示的图 3.17。

![](img/5f6ba170efa3a607142589708531bef8_112_0.png)

**图 3.16 – 拖放以创建数据 Web 服务操作**

## 114 DB2 应用程序开发入门

![](img/5f6ba170efa3a607142589708531bef8_113_0.png)

选择 *Build and Deploy*（构建并部署）后，将显示 *Deploy Web Service*（部署 Web 服务）窗口，如 *图 3.18* 所示。

![](img/5f6ba170efa3a607142589708531bef8_114_0.png)

**图 3.18 – 部署 Web 服务窗口**

在部署 Web 服务窗口的 Web 服务器部分，我们为 *type*（类型）字段选择了 WAS CE 2.1。其他受支持的应用服务器包括 Apache Tomcat 和 WebSphere Application Server (WAS)。由于我们已在与 DB2 数据服务器相同的计算机上安装了 WAS CE，因此我们选择 *Server*（服务器）选项，而不是 *Build deployable files only, do not deploy to a Web server*（仅构建可部署文件，不部署到 Web 服务器）。第二个选项会创建 WAR 文件，您可以稍后将它们传输到您想要部署 Web 服务的应用服务器。在上图 3.20 中，应用服务器已添加到 IBM Data Studio。如果尚未添加，您需要点击 *New*（新建）按钮，并针对大多数面板接受所有默认设置。您需要指定的一件事是 WAS CE 的安装位置。Windows 上的默认安装路径为：

`C:\Program Files\IBM\WebSphere\AppServer\CommunityEdition`

回到 *Deploy Web Service*（部署 Web 服务）窗口，确保勾选 *Launch Web Services Explorer after deployment*（部署后启动 Web 服务资源管理器）复选框。然后点击 *Finish*（完成）。此时，WAS CE 将启动，随后部署数据 Web 服务。这可能需要大约 10 到 20 秒。完成后，Web 服务资源管理器将启动。图 3.19 展示了 Web 服务资源管理器。

![](img/5f6ba170efa3a607142589708531bef8_115_0.png)

**图 3.19 – Web 服务资源管理器**

在上图中，Web 服务资源管理器左侧面板中有一个树状结构，起始于我们可以找到 Web 服务描述语言 (WSDL) 文档的 URL。对于这个特定示例，WSDL 位于：

<http://localhost:8080/MyProject/myWebService/wsdl>

该树状结构还显示了以下项：

- myWebServiceHTTPGET
- myWebServiceHTTPGET
- myWebServiceSOAP

前两项对应于 REST 协议，最后一项对应于 SOAP 协议。在图 3.18 的消息协议部分，我们勾选了 REST 和 SOAP 协议，因此生成了这两种类型的 Web 服务。REST 和 SOAP 是可用于 Web 服务的两种标准，具体使用哪一种由您决定。IBM Data Studio 可以使用其中一种或两种来生成 Web 服务。在图 3.19 中，SOAP 版本下的 GETALLEMOP 方法被高亮显示，当您在右侧面板点击 Go（执行）时，将测试此方法，并在右侧面板底部提供输出，同时以表单形式显示输出。在图 3.19 中，我们实际上是以源代码形式显示输出。

如果您希望从浏览器调用 REST 版本的 GETALLEMOP 方法，请先查看 WSDL 以了解如何调用该方法。如果您向下滚动 WSDL，您将看到如何调用该方法。图 3.20 对此进行了说明。

![](img/5f6ba170efa3a607142589708531bef8_116_0.png)

**图 3.20 – WSDL**

在上图中，我们高亮显示了用于调用 Web 服务的 URL。我们需要在这个 URL 后附加要执行的方法名称。我们示例的完整 URL 如下：

> http://localhost:8080/MyProject/myWebService/rest/myWebService/GETALLEMOP

请注意，方法名称区分大小写。图 3.21 展示了在浏览器中输入上述 URL 后的输出。

![](img/5f6ba170efa3a607142589708531bef8_117_0.png)

```xml
<ns1:GETALLMPResponse>
  <rowset>
    <row>
      <EMPNO>00010</EMPNO>
      <FIRSTNAME>CHRISTINE</FIRSTNAME>
      <MIDINT>I</MIDINT>
      <LASTNAME>HAAS</LASTNAME>
      <WORKDEPT>A00</WORKDEPT>
      <PHONE>6-3878</PHONE>
      <HIREDATE>1995-01-01</HIREDATE>
      <JOB>PRE S </JOB>
      <EDLEVEL>16</EDLEVEL>
      <SEX>F</SEX>
      <BIRTHDATE>1963-08-24</BIRTHDATE>
      <SALARY>15750.00</SALARY>
      <BONUS>1000.00</BONUS>
      <COMM>4220.00</COMM>
    </row>
    <row>
      <EMPNO>00020</EMPNO>
      <FIRSTNAME>MICHAEL</FIRSTNAME>
      <MIDINT>L</MIDINT>
      <LASTNAME>THOMPSON</LASTNAME>
      <WORKDEPT>B01</WORKDEPT>
      <PHONE>43476</PHONE>
...
```

**图 3.21 — 从 myWebService 调用 GETALLMP 方法**

如果愿意，您也可以对此 XML 输出应用 XSLT。这可以通过在 Data Studio 中右键单击数据 Web 服务中的方法并选择 *Manage XSLT*（管理 XSLT）来实现，如 *图 3.22* 所示。

![](img/5f6ba170efa3a607142589708531bef8_118_0.png)

**图 3.22 – 对 Web 服务方法的输出应用 XSLT**

在配置 XSL 转换窗口中，点击 *Browse*（浏览）查找之前创建的 XSL 文件。例如，清单 3.14 展示了本示例中使用的 XSL 文件的一部分。

![](img/5f6ba170efa3a607142589708531bef8_119_0.png)

**清单 3.14 - 数据 Web 服务示例中使用的 XSL 文件**

**图 3.23** 展示了如何指定此 XSL 文件。

![](img/5f6ba170efa3a607142589708531bef8_119_1.png)

**图 3.23 – 指定要使用的 XSL 文件**

点击 **Finish**（完成）后，您需要再次构建和部署 Web 服务，然后在浏览器中刷新并使用与 **图 3.21** 中相同的 URL，您将看到如图 **3.24** 所示的输出。

第 3 章 - 存储过程、UDF、触发器和数据 Web 服务

![](img/5f6ba170efa3a607142589708531bef8_120_0.png)

**图 3.24 – 应用 XSLT 调用 GETALLEMP 方法后的输出**

注意：

若要完整演示此数据 Web 服务示例，请观看此视频：
http://www.channeldb2.com/video/video/show?id=807741%3AVideo%3A1482

## 3.8 练习

在本练习中，您将使用 IBM Data Studio 创建一个标量 UDF。这将为您带来更多关于 Data Studio 的使用经验，并提高您对用于用户定义函数的 SQL PL 语言的熟悉程度。

### 步骤

1. 打开 IBM Data Studio（提示：可通过“开始”菜单访问）。
2. 创建一个新的项目，该关联到第 5 章练习中创建的 EXPRESS 数据库，如本章节前面所述。然后向下钻取直到找到 *User-Defined Functions*（用户定义函数）文件夹。
3. 右键单击 *User-Defined Functions*（用户定义函数）文件夹。选择 New -> *User-defined functions*（新建 -> 用户定义函数）。
4. 函数名称使用 *booktitle*，语言选择 *SQL*，这意味着您将创建一个 SQL PL 用户定义函数。
5. 此时，您可以多次点击 *NEXT*（下一步）按钮，接受所有默认值，直到完成 UDF 的创建。或者，现在就点击 *Finish*（完成）按钮。
6. 将显示一个包含一些示例代码的编辑器窗口。删除所有这些代码，并将其替换为以下代码。

```sql
CREATE FUNCTION booktitle(p_bid INTEGER)
RETURNS VARCHAR(300)
--------------------------------------------------------
SQL UDF (Scalar)
--------------------------------------------------------
SPECIFIC booktitle
F1: BEGIN ATOMIC
  DECLARE v_book_title VARCHAR(300);
  DECLARE v_err VARCHAR(70);
  SET v_book_title = (SELECT title FROM books WHERE p_bid = book_id);
  SET v_err = 'Error: The book with ID ' || CHAR(p_bid) || '
              ' was not found.';
  IF v_book_title IS NULL THEN SIGNAL SQLSTATE '80000' SET
    MESSAGE_TEXT=v_err;
  END IF;
  RETURN v_book_title;
END
```

7. 通过右键单击函数名称并选择 *Deploy*（部署），然后从 *Deploy options*（部署选项）面板中选择 *Finish*（完成）来构建函数。
8. 通过右键单击函数名称并选择 *Run*（运行）来运行该函数。
9. 由于该函数接受一个输入参数，将显示一个对话框窗口，要求您填写参数的值。

输入值：80002

结果是什么？

再次尝试，输入值：1002

这次发生了什么？（提示：查看 *SQL Results*（SQL 结果）选项卡）。

10. 完成后，关闭 IBM Data Studio。

