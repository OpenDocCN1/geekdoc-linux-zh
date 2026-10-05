# 130 • CHAPTER 8

```
<@ page import="java.sql.*" %>
<%@ page import="java.math.*" %>

<%! Connection con = null; %>

<%! public Connection getConnection() {
    if (con != null) {
        return con;
    }
    try {
        Class.forName("com.ibm.as400.access.AS400JDBCDriver");
    } catch (ClassNotFoundException e) {
        System.out.println("JDBCBasics driver load error: "+e);
        return null;
    }
    try {
        con = DriverManager.getConnection(
            "jdbc:as400://207.212.90.55",
            "denoncourt","jiujitsu");
    } catch (SQLException e) {
        System.out.println("JDBCBasics SQL Connection error: "+ e);
        return null;
    }
    return con;
} %>

<html><body>
<%
    con = getConnection();
    Statement stmt = con.createStatement();
    ResultSet rs = stmt.executeQuery(
        "SELECT CUSUM, LSTNAM, INIT, STREET, " + 
        "CITY, STATE, ZIPCOD, CDLTMT, " + 
        "CHCGOD, BALDUE, CDTOUE " + 
        "FROM WIQS.CUSTUM");
    while (rs.next()) {
        String cusnum = =
        rs.getString(1);
        String cusnam = =
        rs.getString("LSTNAM");
        BigDecimal baldeue = =
        rs.getBigDecimal(10, 2);
        
        <%= cusnum % &nbsp; << cusnam % &nbsp; << baldeue % <br>
    }
} catch (SQLException e) {
    SQL error: &nbsp; << e %
} %>
</body></html>
```

Figure 8.3: JDBC can be accessed in JSPs.

It might be tempting to use JSP rather than servlet for development because the compile process is automated. However, production Web applications work better when complex code is kept in Java servlets and JavaServer Pages are used for the presentation layer.