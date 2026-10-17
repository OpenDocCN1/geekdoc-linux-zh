
## D.18 Listorder.jsp

```html
<html>
<head>
<% session=request.getSession(true); %>
</head>
<center>
<p><h4 align="center">发生错误</h4></p>
<p><h4 align="center"><%= session.getAttribute("error") %></h4></p>
<p><b>返回</b></p>
<p><a href="../OrderPage/orderpage.html"><img alt="Homepage" src="home.gif" height="17" border="0"></a></p>
</center>
</body>
</html>
```

## D.19 Listorders.jsp

```jsp
<%@ page language="java" import="java.util.*" %>
<html>
<head>
<base target="_parent">
</head>
<body>
<table name="orders" border="1">
<%
Enumeration e = orders;
while (e.hasMoreElements()) {
    String key = (String) e.nextElement();
    out.println("<tr><td>" + key + "</td><td>" + key + "</td><td>" + key + "</td></tr>");
}
%>
</table>
</body>
</html>
```

Linux 托管于 WebSphere、DB2 和 Domino

## D.20 Loginpage.jsp

## D.21 Login.jsp

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 FINAL//EN">
<HTML>
<HEAD>
<%@ page language="java" %>
...
</HEAD>
<BODY>
<CENTER>
<p><h3 align="center">发生错误</h3></p>
<p><h4 align="center"><%= (String) session.getValue("error") %></h4></p>
<p><b>返回</b></p>
<p><a href="../Loginpage.jsp"><img alt="Home" src="../home.gif" height="17" border="0"></a></p>
</CENTER>
</BODY>
</HTML>
```

## D.22 Logout.jsp

## D.23 order.jsp

```html
<html>
<head>
<% session=request.getSession(true); %>
</head>
<body>
<center>
<p><h3 align="center">发生错误</h3></p>
<p><h4 align="center"><%= (String) session.getAttribute("error") %></h4></p>
<p><b>返回</b></p>
<p><a href="../OrderPage/orderpage.html"><img alt="Homepage" src="../home.gif" height="17" width="120" border="0"></a></p>
</center>
</body>
</html>
```

## D.24 Orderpage.html

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 FINAL//EN">
<HTML>
<HEAD>
<FRAMESET ROWS="142,*">
<FRAME NAME="header" SRC="header_default.html" SCROLLING="NO">
<FRAMESET COLS="152,*">
<FRAME NAME="left" SRC="../Orderpage/left.html" SCROLLING="AUTO">
<FRAME NAME="body" SRC="../Orderpage/body.jsp" SCROLLING="AUTO">
</FRAMESET>
</FRAMESET>
</HEAD>
</HTML>
```

## D.25 Success.jsp

```jsp
<%@ page language="java" %>
<HTML>
<HEAD>
<BASE TARGET="parent">
<% HttpSession session = request.getSession(true); %>
</HEAD>
<BODY BGCOLOR="#FFFFFF" LINK="#0000FF" VLINK="#000080" TEXT="#000000" TOPMARGIN="20" MARGINLEFT="2" MARGINHEIGHT="2">
<TABLE BORDER="0" CELLSPACING="0" CELLPADDING="0">
<TR VALIGN="LEFT">
<TD WIDTH="96" HEIGHT="17"><IMG SRC="../clearpixel.gif" WIDTH="96" HEIGHT="1" BORDER="0"></TD>
<TD WIDTH="419" HEIGHT="1"><IMG SRC="../clearpixel.gif" WIDTH="419" HEIGHT="1" BORDER="0"></TD>
</TR>
<TR VALIGN="LEFT">
<TR>
<TD WIDTH="419" HEIGHT="1"><CENTER><FONT SIZE="+2">订单信息</FONT></CENTER></TD>
</TR>
</TABLE>

| 产品编号 | <%= session.getValue("product_id") %> |
| :--- | :--- |
| 客户名称 | <%= session.getValue("last_name") %> |
| 地址 | <%= session.getValue("address") %> |

邮寄详情

200 带有 WebSphere、DB2 和 Domino 的 Linux 托管
```

## D.26 Passwdsuccess.jsp

```jsp
<%@ page language="java" %>
<HTML>
<HEAD>
<% HttpSession session=request.getSession(true); %>
</HEAD>
<BODY>
<CENTER>
<P>
<H3 ALIGN="CENTER">您的密码已成功修改</H3>
</P>
<P>
<H4 ALIGN="CENTER">您的新密码是：
<B ALIGN="CENTER"><%= session.getValue("password") %></B></H4>
</P>
<P>
<CENTER>
<P>
<B>返回</B>
</P>
<P>
<A href="../Page/homepage.jsp"><IMG HEIGHT="120" WIDTH="120" SRC="../home.gif" BORDER="0" ALT="首页"></A>
</P>
</CENTER>
</BODY>
</HTML>
```

## D.27 Passwdfailure.jsp

```jsp
<HTML>
<HEAD>
<% HttpSession session=request.getSession(true); %>
</HEAD>
<BODY>
<CENTER>
<P>
<H3 ALIGN="CENTER">发生了错误</H3>
</P>
<P>
<H4 ALIGN="CENTER"><%= (String) session.getValue("error") %>
<B><% session.removeValue("error"); %></B>
</H4>
</P>
<P>
<B>返回</B>
</P>
<P>
<A href="../Page/homepage.jsp"><IMG HEIGHT="120" WIDTH="120" SRC="../home.gif" BORDER="0" ALT="首页"></A>
</P>
</CENTER>
</BODY>
</HTML>
```

## D.28 Registerfailure.jsp

```jsp
<HTML>
<HEAD>
<% HttpSession session=request.getSession(true); %>
</HEAD>
<CENTER>
<P>
<H3 ALIGN="CENTER">发生了错误</H3>
</P>
<H4 ALIGN="CENTER"><%= (String) session.getValue("error") %>
<% session.removeValue("error"); %>
</H4>
<P>
<B>返回</B>
</P>
<P>
<A href="../RegistrationPage/registrationpage.jsp"><IMG HEIGHT="17" WIDTH="120" SRC="../home.gif" BORDER="0" ALT="首页"></A>
</P>
</CENTER>
</BODY>
</HTML>
```

## D.29 Registersuccess.jsp

```jsp
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 FINAL//EN">
<HTML>
<HEAD>
<BASE TARGET="_parent">
</HEAD>
<% HttpSession session=request.getSession(true); %>
<BODY BGCOLOR="#FFFFFF" LINK="#000000" VLINK="#000000" TOPMARGIN="22" LEFTMARGIN="2">
<TABLE BORDER="0" CELLSPACING="0" CELLPADDING="3">
<TR>
<TD WIDTH="60" HEIGHT="30"><IMG SRC="./clearpixel.gif" WIDTH="60" HEIGHT="1" BORDER="0"></TD>
<TD WIDTH="273"><IMG SRC="./clearpixel.gif" WIDTH="273" HEIGHT="1" BORDER="0"></TD>
</TR>
<TR>
<TD VALIGN="TOP">
<TD WIDTH="273"><P ALIGN="CENTER"><B><FONT SIZE="+1">用户资料 : <%= session.getValue("username") %></FONT></B></P></TD>
</TR>
</TABLE>
<TABLE BORDER="0" CELLSPACING="0" CELLPADDING="0">
<TR>
<TD VALIGN="TOP">
<TD WIDTH="40" HEIGHT="62"><IMG SRC="./clearpixel.gif" WIDTH="40" HEIGHT="1" BORDER="0"></TD>
</TR>
<TR>
<TD VALIGN="TOP">
<TD WIDTH="459">
<TABLE ID="Table5" BORDER="1" CELLSPACING="3" CELLPADDING="1" WIDTH="459">
<TR>
<TD WIDTH="199"><P>
<TABLE WIDTH="96" BORDER="0" CELLSPACING="0" CELLPADDING="2" ALIGN="LEFT">
<TR>
<TD><P>名</TD>
</TR>
<TD WIDTH="241"><P><%= session.getValue("first_name") %></TD>
</TR>
</TABLE>
<TD WIDTH="199" BORDER="0" CELLSPACING="0" CELLPADDING="0" ALIGN="LEFT">
<TD><P>姓</TD>
</TR>
<TD WIDTH="241"><P><%= session.getValue("last_name") %></TD>
</TR>
</TABLE>
<TD WIDTH="199" BORDER="0" CELLSPACING="0" CELLPADDING="0" ALIGN="LEFT">
<TD><P>电子邮箱</TD>
</TR>
<TD WIDTH="241"><P><%= session.getValue("email_address") %></TD>
</TR>
</TABLE>
<TD WIDTH="199" BORDER="0" CELLSPACING="0" CELLPADDING="0" ALIGN="LEFT">
<TD><P>详细地址</TD>
</TR>
<TD WIDTH="241"><P><TEXTAREA NAME="address" ROWS="5" COLS="30"><%= session.getValue("address") %></TEXTAREA></P>
</TR>
</TABLE>
<TD WIDTH="199" BORDER="0" CELLSPACING="0" CELLPADDING="0" ALIGN="LEFT">
<TD><P>出生日期</TD>
</TR>
<TD WIDTH="241"><P><%= session.getValue("birth_date") %></TD>
</TR>
</TABLE>
<TABLE BORDER="0" CELLSPACING="0" CELLPADDING="0" WIDTH="460">
<TR>
<TD WIDTH="241"><IMG SRC="../clearpixel.gif" WIDTH="241" HEIGHT="1" BORDER="0"></TD>
</TR>
<TR>
<TD WIDTH="219"><P>在下表中，您选择了以下感兴趣的平台：</P>
</TR>
</TABLE>
<TABLE WIDTH="55">
<TR>
<TD>
<TD>
<TD>
<TD>
<TD>
<TABLE BORDER="2" CELLSPACING="1" WIDTH="70">
<TR>
<TD WIDTH="73"><% if (session.getValue("as400") == null) { %>selected<% } else { %>not selected<% } %></TD>
<TD WIDTH="600"><% if (session.getValue("rs600") == null) { %>selected<% } else { %>not selected<% } %></TD>
</TR>
</TABLE>
```

## D.33 Updates_success.jsp
