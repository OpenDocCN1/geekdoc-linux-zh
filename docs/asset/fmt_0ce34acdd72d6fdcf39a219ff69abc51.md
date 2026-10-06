
```java
package penguins.access.db;
import java.util.*;

public class Order {
    private Vector orderIDs = new Vector();
    private Hashtable timestamps = new Hashtable();
    private Hashtable productIDs = new Hashtable();

    public Order() {
        super();
    }

    public void add_order(String order_id, String order_timestamp, String product_id) {
        orderIDs.add(order_id);
        timestamps.put(order_id, order_timestamp);
        productIDs.put(order_id, product_id);
    }

    public Enumeration orderIDs() {
        return orderIDs.elements();
    }

    public String productID(String orderID) {
        return (String) productIDs.get(orderID);
    }

    public String timestamp(String orderID) {
        return (String) timestamps.get(orderID);
    }
}
```

## 附录 C 与数据库相关的 Java 代码

本附录提供了 Domino 相关的 Java 代码列表。

### C.1 Java servlet TestDomino

```java
import java.io.*;
import java.util.*;
import javax.servlet.*;
import javax.servlet.http.*;
import lotus.domino.*;

public class TestDomino extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse response) {
        // 实现细节略略
    }
}
```

### C.2 Java servlet VBDList

```java
import java.io.*;
import java.util.*;
import javax.servlet.*;
import javax.servlet.http.*;
import lotus.domino.*;
import java.util.Vector;

public class VBDList extends HttpServlet {
    String viewname = "platform sorted";
    String dbname = "Redbooks";
    String host = "localhost:8000";
    String category = null;
    String tm;
    DateTime dt;

    public void doGet(HttpServletRequest req, HttpServletResponse response) {
        doService(req, response);
    }

    public void doPost(HttpServletRequest req, HttpServletResponse response) {
        doService(req, response);
    }

    public void doService(HttpServletRequest req, HttpServletResponse response) {
        String catcat = null;
        Vector listParam = new Vector();

        /* 获取参数名和值 */
        for (Enumeration e = req.getParameterNames(); e.hasMoreElements(); e++) {
            String param = (String) e.nextElement();
            String paramValue = req.getParameter(param);
            listParam.addElement(paramValue);
        }

        for (int i = 0; i < listParam.size(); i++) {
            catcat = (String) listParam.elementAt(i);
            if (catcat.equals("item1")) {
                catcat = "item1";
            }
            if (catcat.equals("item2")) {
                catcat = "item2";
            }
        }

        ViewEntry entry = view.getFirst();
        int count = 0;
        while (entry != null && count < 10) {
            if (entry.isCategory()) {
                out.println("");
            }
            if (entry.getDocument()) {
                Vector dm = entry.getDocument().getValue("PublishDate");
                if (dm.size() > 0) {
                    dt = (DateTime) dm.elementAt(0);
                    tm = dt.getDateOnly();
                } else {
                    if (tm == null) {
                        out.println("");
                    }
                }
            }
            // ... 逻辑继续
        }
    }
}
```

### C.3 Java servlet VBDServlet

```java
import java.io.*;
import java.util.*;
import javax.servlet.*;
import javax.servlet.http.*;
import lotus.domino.*;
import java.util.Vector;

public class VBDServlet extends HttpServlet {
    String viewname = "All books";
    String dbname = "Redbooks";
    String host = "localhost:8000";
    String category = null;
    String tm;
    DateTime dt;

    public void doGet(HttpServletRequest req, HttpServletResponse response) {
        doService(req, response);
    }

    public void doPost(HttpServletRequest req, HttpServletResponse response) {
        doService(req, response);
    }

    public void doService(HttpServletRequest req, HttpServletResponse response) {
        int no;
        /* 获取参数名和值 */
        category = req.getParameter("category");
        if (category.equals("All")) {
            viewname = "All books";
        } else {
            viewname = "platform sorted";
        }

        try {
            /* 创建话并打开数据库 */
            Session s = NotesFactory.createSession();
            Database db = s.getDatabase(s.getServerName(), dbname);
            View view = db.getView(viewname);
        } catch (Exception e) {
            e.printStackTrace();
        }

        res.setContentType("text/html");
        ServletOutputStream out = res.getOutputStream();
        out.println("<<html><head><title>Redbooks 访问测试</title></head>");
        out.println("<body>");
        out.println("<blockquote>");
        out.println("<li><font size=1>" + category + "</b></li>");

        if (category == null || category.equals("")) {
            out.println("未分类");
        }
        out.println("</</blockquote>");
        out.println("<table BORDER='3' WIDTH='95%'>");
        out.println("<tr ALIGN='LEFT' ALIGN='CENTER'>");
        out.println("<td ALIGN='LEFT' ALIGN='CENTER' WIDTH='15%'>");
        out.println("<center><b>表单编号</b></center></td>");
        out.println("</center></td>");
        out.println("<<td>");
        out.println(entry.getDocument().getItemValueString("BookTitle"));
        out.println("</td>");
        out.println("<td></center>");
        out.println(tm);
        out.println("</center></td></tr>");
        // ... 表格剩余部分
    }

    public String getServletInfo() {
        return "创建一个显示指定数据库标题的页面";
    }
}
```

```java
String host="btest3:8000";
String query=null;
String tm, dumb;
DateTime dt;
```

```java
public void doGet(HttpServletRequest req, HttpServletResponse res)
throws SQLException, IOException {
    doService(req,res);
}
```

```java
public void doPost(HttpServletRequest req, HttpServletResponse res)
throws SQLException, IOException {
    doService(req,res);
}
```

```java
public void doService(HttpServletRequest req, HttpServletResponse res)
throws SQLException, IOException {

```

```java
int no;
/* 获取参数名和值 */

query = req.getParameter("search");
```

```java
try {

/* 创建话并打开数据库 */
Session s=NotesFactory.createSession(host);
Database db=s.getDatabase(s.getServerName(), dbname);
View view = db.getView(view);

res.setContentType("text/html");
ServletOutputStream out=res.getOutputStream();
out.println("<head><title>Redbooks 查询结果</title></head>");
out.println("<body>");
out.println("</p>");
```

```java
out.println("Parameter = "+query+"</p>");

ViewEntryCollection vec = view.getAllEntries();
vec.FTSearch(query);
ViewEntry entry = vec.getFirstEntry();
if (vec.getCount() != 0) {

out.println("<table BORDER=3 WIDTH=95%");
out.println("<tr ALIGN=LEFT VALIGN=CENTER>");
```

```java
out.println("</body></html>");
}

public String getServletInfo() {
    return "创建一个显示指定数据库客户端标题的页面";
}
```

## C.5 Java servlet

```java
import java.io.*;
//import java.util.*;
import javax.servlet.*;
import javax.servlet.http.*;
import lotus.domino.*;
import java.util.Vector;

public class VDBOpen extends HttpServlet {

    String dbname="RedBooks";
    String host="btest3:8000";
    String tm;
    DateTime dt;

    public void doGet (HttpServletRequest req, HttpServletResponse res)
        throws ServletException, IOException {
        doService(req, res);
    }

    public void doPost (HttpServletRequest req, HttpServletResponse res)
        throws ServletException, IOException {
        doService(req, res);
    }

    public void doService (HttpServletRequest req, HttpServletResponse res)
        throws ServletException, IOException {

        /* 获取参数名和值 */
        String docid=(String)req.getParameter("docid");
        HttpSession sess=req.getSession(true);
        String username = (String)sess.getValue("username");
        try {
```

```java
/* 创建会话并打开数据库 */
Session s=NotesFactory.createSession(host);
Database db=s.getDatabase(s.getServerName(), dbname);
```

```java
out.println("<FONT FACE=\"Arial\">"+doc.getItemValue("BookTitle"));
```

```java
out.println("<TR ALIGN=\"top\"><TD WIDTH=\"100%\">");
```
