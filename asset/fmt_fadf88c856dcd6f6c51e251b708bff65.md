
## 附录 B. 连接到 DB2 的 Java 代码

```sql
sqlSnt = sqlSnt + " 'y'";
else
sqlSnt = sqlSnt + " null";

sqlSnt = sqlSnt + "where username=' + username + "'";
stmt = conn.createStatement(sqlSnt);
rs = stmt.executeUpdate(sqlSnt);
stmt.close();
if (rs != 1)
    raiseError("USERPROFILMENT: result !==1 from " + sqlSnt);

failurepage, req, res);

    // 设置浏览器 cookie;
for (int i = 0; i < infoCols.length; i++) {
    if (req.getParameter(infoCols(i)) != null) {
        session.putValue(infoCols(i), req.getParameter(infoCols(i)));
    }
}

    // 用户个人资料的 cookies
for (int i = 0; i < profileCols.length; i++) {
    if (req.getParameter(profileCols(i)) != null) {
        session.putValue(profileCols(i));
    }
}
req.getParameter(profileCols(i))
else // 未定义兴趣类别
    res.removeValue(profileCols(i));
}

res.callPage(success, req);
else
    raiseError("the following error(s) have been detected. Please correct
and and try again." + toString(error), failurepage, req, res);
else
    uidPwError(username, password, failurepage, req, res);
else
    raiseError("ACTIONERROR: Please report the following: <p> ACTION \* " + action +
"* not defined in URI " + req.getRequestURI() + " *", failurepage, req, res);
    res.callPage(failurepage, req);
catch (SQLException e) {
    e.printStackTrace();
    session.putValue("SQLERROR " + e.getMessage());
    res.callPage(failurepage, req);
}

private String getPassword(HttpServletRequest req) {
    return req.getParameter("password");
}

private String getPassword(HttpSession session) {
    return (String) session.getValue("password");
}

private String getUsername(HttpServletRequest req) {
    return req.getParameter("username");
}

private String getUsername(HttpSession session) {
    return (String) session.getValue("username");
}

protected void initDB() {
try {
    String url = "jdbc:db2:userutf";
    String uid = "db2inst";
```

## 附录 B. 与 DB2 155相关的 Java 代码

```
String pwd = "lmbnd2";
con = DriverManager.getConnection(url, uid, pwd);
catch (SQLException e) {
    e.printStackTrace();
}

protected boolean passwordMatch(String username, String password) {
    boolean match = false;
    try {
        String sqlStmt = "select password from userverify where username='" + 
            username + "' + ";
        Statement stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery(sqlStmt);
        if (rs.next()) {
            ResultSetMetaData md = rs.getMetaData();
            if (md.getColumnCount() > 0) {
                // 实现任何用于检查的密码算法
                String hash = rs.getString(1);
                if (password.equals(hash)) {
                    match = true;
                }
            }
        }
    } catch (SQLException e) {
        e.printStackTrace();
    }
    return match;
}

protected void handleError(String errorText, String errorPage, HttpServletRequest req) {
    try {
        HttpSession session = req.getSession(true);
        session.setAttribute("error", errorText);
        session.callPage(errorPage, req);
    } catch (Exception e) {
        e.printStackTrace();
    }
}

private String toString(Hashtable elements) {
    Enumeration he = elements.keys();
    String errorText = "";
    String fieldName = "";
    while (he.hasMoreElements()) {
        fieldName = (String) he.nextElement();
        errorText += fieldName + " = " + elements.get(fieldName) + " *";
    }
    return errorText;
}

private void useError(String username, String password, String redirectedPage, HttpServletRequest req) {
    HttpSession session = req.getSession();
    raise("username = " + username + " * with password = " + password + " * \* invalid");
    req.sendRedirect(redirectedPage, req, res);
}

private void useError(String username, String redirectedPage, HttpServletRequest req) {
    raise("username = " + username + " \* does not exist", redirectedPage, req, res);
}

protected boolean usernameExists(String username) {
    boolean exists = false;
    try {
        if (username == null) {
```

return false;

/*

注意此处我们从 userinfo 而不是 userverify 获取用户名

如果用户名之前被删除过，

由于 userinfo 中仍然存在，因此可以避免在 userinfo 中产生重复

*/

String sqlStmt = "select * from userinfo where username=' + username +

PreparedStatement stmt = conn.prepareStatement(sqlStmt);

ResultSet rs = stmt.executeQuery(sqlStmt);

if (rs.next()) {

    ResultSetMetaData md = rs.getMetaData();

    if (md.getColumnCount() > 0) {

        // 实现任何用于检查的密码算法

        String hash = rs.getString(1);

        if (password.equals(hash)) {

            exists = true;

        }

    }

}

} catch (SQLException e) {

    e.printStackTrace();

}

return exists;

protected boolean validateData(HttpServletRequest req) {

    Hashtable errors = new Hashtable();

    try {

        for (int i = 0; i < infoCols.length; i++) {

            if (req.getParameter(infoCols(i)) != null) {

                session.putValue(infoCols(i), req.getParameter(infoCols(i)));

            }

        }

        // 用户个人资料的 cookies

        for (int i = 0; i < profileCols.length; i++) {

            if (req.getParameter(profileCols(i)) != null) {

                session.putValue(profileCols(i));

            }

        }

        req.getParameter(profileCols(i))

        else // 未定义兴趣类别

            res.removeValue(profileCols(i));

    }

}

res.callPage(success, req);

else

    raiseError("the following error(s) have been detected. Please correct

and and try again." + toString(error), failurepage, req, res);

else

    uidPwError(username, password, failurepage, req, res);

else

    raiseError("ACTIONERROR: Please report the following: <p> ACTION \* " + action +

"* not defined in URI " + req.getRequestURI() + " *", failurepage, req, res);

    res.callPage(failurepage, req);

catch (SQLException e) {

    e.printStackTrace();

    session.putValue("SQLERROR " + e.getMessage());

    res.callPage(failurepage, req);

}

private String getPassword(HttpServletRequest req) {

    return req.getParameter("password");

}

private String getPassword(HttpSession session) {

    return (String) session.getValue("password");

}

private String getUsername(HttpServletRequest req) {

    return req.getParameter("username");

}

private String getUsername(HttpSession session) {

    return (String) session.getValue("username");

}

protected void initDB() {

try {

    String url = "jdbc:db2:userutf";

    String uid = "db2inst";

```

## 附录 C. 与 Domino 相关的 Java 代码

此附录提供了 Domino 相关的代码列表。

### C.1 Java servlet TestDomino

（代码部分略，保持原样）

### C.2 Java servlet VBDList10

```java
import java.*;
import java.util.*;
import javax.servlet.*;
import javax.servlet.http.*;
import lotus.domino.*;
import java.util.Vector;

public class VBDList10 extends HttpServlet {

    String viewname = "platform sorted";
    String dname = "RedBooks";
    String host = "bdtest3:8000";
    String category = null;
    String tm, dumb;
    DateTime dt;

    public void doGet(HttpServletRequest req, HttpServletResponse res)
            throws ServletException, IOException {
        doService(req, res);
    }

    public void doPost(HttpServletRequest req, HttpServletResponse res)
            throws ServletException, IOException {
        doService(req, res);
    }

    public void doService(HttpServletRequest req, HttpServletResponse res)
            throws ServletException, IOException {
        String catcat = null;
        int no;
        Vector listParam = new Vector();

        /* 获取参数名和值 */
        for (Enumeration e = req.getParameterNames(); e.hasMoreElements(); ) {
            String param = (String) e.nextElement();
            String paramValue = (String) req.getParameter(param);
            listParam.addElement(paramValue);
        }

        for (int i = 0; i < listParam.size(); i++) {
            catcat = (String) listParam.elementAt(i);
            if (catcat.equals("item1")) category = "AS/400";
        }
    }
}
```
