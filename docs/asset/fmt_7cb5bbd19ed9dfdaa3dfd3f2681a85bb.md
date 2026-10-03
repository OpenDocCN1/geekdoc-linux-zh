
SQL 查询返回一组行。这被称为结果集。使用语句的 `executeQuery` 方法，它返回 `ResultSet` 类型。我们可以编写简单的 SQL 查询从 `USERINFO` 表中的所有行：

```java
String sqlType="select * from USERINFO";
ResultSet rs=stmt.executeQuery(sqlType);
```

每个结果集都由其元数据描述。要获取结果的元数据，我们使用结果集的 `getMetaData()` 方法。例如：

```java
ResultSetMetadata rsmd = rs.getMetaData();
```

我们可以通过一些示例代码来更好地说明这一点。对于以下示例代码，我们假设连接已经创建（参见第 84 页的“创建 DB2 连接”）并且有一个输出流 `out`。

- a. 首先，我们创建语句：
  `Statement stmt = con.createStatement();`

- b. 接下来，我们执行一个查询类型的语句，返回类型为 `ResultSet` 的结果：
  ```java
  ResultSet rs = stmt.executeQuery("select * from userinfo");
  ```

- c. 为了打印每个结果集行的第一列，我们有以下代码段：
  ```java
  while (rs.next()) {
    out.print(rs.getString());
  }
  ```

- d. 为了更进阶的操作，我们可以通过获取结果集元数据、确定结果集中列的数，然后使用 `getMethod` 打印每个结果集的所有列：
  ```java
  ResultSetMetaData rsmd = rs.getMetaData();
  int numFields = rsmd.getColumnCount();
  while (rs.next()) {
    for (int currField = 1; currField < numFields; currField++) {
      out.print(rs.getString(currField));
    }
    // 下一行
    out.println();
  }
  ```

### 字段/列从 1 开始

注意，字段/列计数从 1 开始。因此，上述示例代码中的循环从 1 开始循环。

`getString` 方法可以像我们之前的那样使用列号，也可以使用列名，例如：
`rs.getString("first_name")`

你将在随后的示例中看到该方法以两种形式出现。

### 显式关闭 DB2 语句

DB2 语句在到达最后一行结果或 Java 实例终止时会自动关闭。在某些情况下，立即释放语句的数据库和 JDBC 资源是有希望的；`close` 方法提供了这种即时释放：

```java
stmt.close();
```

在位于 `USERSTUF` 数据库的 `USERINFO` 表上执行简单的 DB2 查询语句所需的最小代码见第 87 页的图 67。

```java
import java.servlet.*;
import java.servlet.http.*;
import java.sql.*;

public class DB2Servlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) throws Exception {
        try {
            Class.forName("com.ibm.db2.jdbc.DB2Driver");
            String url = "jdbc:db2:userstuf";
            String uid = "db2inst1";
            String pwd = "imdb2";
            Connection conn = DriverManager.getConnection(url, uid, pwd);
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("select * from userinfo");
            // 在此处对结果集进行操作
            stmt.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

图 67. 从 servlet 访问 DB2 表所需的最小代码

## 3.5.3.3 DB2 servlet AccessUserstuf

AccessUserstuf servlet 负责所有涉及 `USERINFO`、`USERPROFILE`、`USERVER` 和 `ORDERORDERS` 数据库表的操作。因此，它必须执行以下操作：

- 在初始化时（当被 WebSphere 引擎首次加载时），它必须注册 DB2 类库并创建到 `USERSTUF` 数据库的连接。我们已经在第 83 页的 3.5.3，“通过 JDBC 访问 DB2”中讨论过如何实现这些，并在第 87 页的图 67 中提供了示例代码。

- 在调用时，通过 POST 方法，它必须实现所需的操作。我们将在本节进一步讨论这些操作实现。

DB2 servlet 必须处理 POST 方法。它是一个 `HttpServlet`。每个操作都可以成功或失败。对在用户 servlet 中实现的操作进行简要讨论如下：

- login：该操作期望 Request 对象中设置了用户名和密码，并对它们进行验证。

- changepword：该操作要求 Request 对象中设置了用户名和密码。

- register：该操作要求 Request 对象中设置了用户名和密码。

- update：该操作要求 Request 对象中设置了用户名和密码。

- delete：该操作要求 Request 对象中设置了用户名和密码。

- order：该操作要求 Request 对象中设置了用户名和密码。

- listorders：该操作要求 Request 对象中设置了用户名和密码。

### 3.5.3.4 DB2 servlet action-login

当使用以下方式调用 servlet 时，会执行以下任务序列：

1. login 操作期望 Request 对象中设置了用户名和密码，并通过 `getParameter` 方法对它们进行验证。假设变量为 `HttpRequest req`，执行此操作的代码如下：

```java
String username = req.getParameter("username");
String password = req.getParameter("password");
```

出于我们的目的，这段代码经常重用；因此，我们编写了 `getUsername` 和 `getPassword` 私有方法。`getUsername` 方法为：

```java
private String getUsername(HttpRequest req) {
    return req.getParameter("username");
}
```

因此，我们将代码更改为：

```java
String username = getUsername(req);
String password = getPassword(req);
```

#### 方法重载

我们使用了另一种形式的 `getUsername` 方法，例如在 listorder 操作中，它从 `HttpSession` 对象获取值。因此，我们有如下的 `getUsername` 方法：

```java
private String getUsername(HttpSession session) {
    return session.getValue("username");
}
```

我们重载了 `getUsername` 和 `getPassword` 方法。这些方法通过传递的参数类型来区分。

```java
protected boolean passwordsMatch(String username, String password) {
    boolean match=false;
    try {
        String sqlStmt="select password from userverify where username="+username+"";
        Statement stmt=conn.createStatement();
        ResultSet rs=stmt.executeQuery(stmt);
        if (rs.next()) {
            ResultSetMetaData rmd=rs.getMetaData();
            if (rs.getColumnCount()>0) {
                String password=rs.getString(1);
                if (password.equals(password)) match=true; 
            }
        }
    } catch (SQLException e) { e.printStackTrace(); }
    return match;
}
```

图 68. passwordsMatch 方法的 Java 代码

- 26. 如果登录成功，我们必须使用 `putValue` 方法向 Session 对象填充以下信息：

  a. username，password

  这些信息已经存在于 username 和 password 变量中。因此，代码简单如下：

  `session.putValue("username", username);`
  `session.putValue("password", password);`

  b. 用户信息

  用户信息（例如地址或电子邮件）必须从 USERINFO 数据库表中获取。我们对相关信息进行查询，然后遍历要填充到 Session 对象中的 USERINFO 列列表。

  我们定义了一个名为 `infoCols` 的字符串数组，它包含我们打算从 select 语句中获取的值列表，然后将其放入 Session 对象中（实际上是使用此字符串数组作为过滤器）。代码看起来类似于第 92 页的图 69。

```java
private String infoCols[]={"first_name", "last_name", "email_address", "date_joined", "birth_date", "address"};
....
String sqlStmt="select * from userinfo where username="+username+"";
Statement stmt=con.createStatement();
ResultSet rs=stmt.executeQuery(sqlStmt);
if (rs.next()) {
  for (int i=0; i<infoCols.length; i++) {
    String info=infoCols[i];
    session.putValue(info, rs.getString(info));
  }
}
```

在 Session 对象中填充用户信息的 Java 代码

#### 用户配置文件

同样地，我们从 USERPROFILE 表中查询相关的列。如果特定类别（如 as400、entity 等）没有空值，则意味着用户对该类别表示了兴趣，因此我们应该在 Session 对象中设置该值。

我们再次使用一个名为 `profileCols` 的字符串数组作为过滤器。代码类似于图 70。

图 70. 在 Session 对象中填充用户信息的 Java 代码

- 4. 最后，一旦登录成功，并且我们重定向填充了适当信息的 Session 对象，我们就可以将流重定向到服务器上的另一个页面，由 `successpage` 变量指示：
  `res.callPage(successpage, req);`

## 3.5.4 在 Linux 中使用 Java 访问 Domino 数据

Java 程序有多种机制可以访问 Domino 数据、Domino 服务或其他数据库管理系统，例如：

- 通过与 NCSO 或 `notes.jar` 包含的 `lotus.domino` 包提供的 Java Domino 对象。Domino 对象表示并可以用于操作 Domino 数据，例如项目值、组件（如数据库）以及服务（如用户注册函数）。

- 用于调用 C 或 C++ API 函数或程序的 Java Native Interface (JNI)。Lotus C 或 C++ Domino 和 Notes API 可以比 Domino 对象提供的更细粒度的级别上操作 Domino 数据和服务。

- Lotus Script 扩展器 (LSX) 工具包及其 Java 适配器。LSX 工具包允许 LotusScript 开发者在 C++ 中创建自定义对象并在 LotusScript 中调用它们。Java 适配器提供了从 Java 调用这些对象的功能。由于用于创建对象的语言是 C++，因此这些 C++ 程序可以调用 Domino 和 Notes API 或其他 API 来访问数据和服务。

在本版红书中，我们重点关注使用 Domino 对象类来访问 Domino 数据和服务。要需有关有关 Lotus C 和 C++ API 以及 LSX 工具包的完整信息，请访问 Developer Central 网站：http://www.lotus-developer.com。

Domino 对象类架构基于概念性的包含模型，其中容器定义了对象的范围。容器对象始终用于访问它所包含的对象。例如，我们使用 Session 对象来获取 Database 对象，使用 Database 对象创建 Document 对象。

由于一个 Domino 对象可能被其他对象包含，完整的包含关系超出了本红书的范围。然而，一些关键的包含关系如下表所示。

| Session | Database | ACL | ACLEntry |
| --- | --- | --- | --- |
| | | Document | Item |
| | | DocumentCollection | RichTextItem |
| | | Form | |
| | | View | ViewColumn |
| | | Agent | ViewEntry |
| | | | NavigationView |

Domino Java 类在以下包中：

- Domino `notes.jar` 文件包含用于本地 Java 访问的 `lotus.domino` 类。
- Domino `NCSO.jar` 文件包含用于远程 Java 访问的 `lotus.domino` 类。

在后续章节中，我们将解释如何开发 servlet。仅显示代码的重要部分。有关 servlet 的完整列表，请参阅第 159 页的附录 C，“与相关的 Java 代码”。

### 导入包

我们的 servlet 需要以下包：

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import lotus.domino.*;
import java.util.Vector;
```

除了标准的 Java 包和 servlet 包外，`lotus.domino` 是我们需要访问 Domino 数据库的包。我们还使用 `java.util.Vector` 提供动态长度支持。

### 访问 Domino 会话和数据库

Session 是 Domino 包含层次结构的根。我们可以根据访问服务器的方式使用多种方法打开会话。

有两种访问服务器的方法：

- 远程访问：对于要远程访问 Domino 数据库，我们需要在 `NotesFactory.createSession` 方法中使用主机名、用户名和密码。例如，尝试在服务器 host1 上使用用户名 myUser 和密码 myPass 打开 myDB：

```java
Session s = NotesFactory.createSession("host1:8000","myUser","myPass");
Database db = s.get("myDB");
```

记住 HTTP 和 DIOP 服务器必须在运行中。在我们的情况下，我们使用匿名访问 DIOP，因此只需要在 `NotesFactory.createSession` 方法中放入主机名。有关如何设置 DIOP 服务器的更多信息，请参阅第 26 页第 4.2.4.2 节，“Domino 服务器 Java 和 CORBA 要求”。

```java
Database db = s.getDatabase("mydb");
```

### 访问视图

成功打开数据库后，我们可以通过 `getView` 和 `getViews` 访问数据库中的视图和文件夹。通过 `View` 类，我们可以在视图中定位文档并在那里执行操作。

```java
View view = db.getView(viewname);
```

`viewname` 必须包含 Domino 数据库中视图或文件夹的名称。视图或文件夹的名称必须完全指定。

### 使用 ViewNavigator 访问文档
