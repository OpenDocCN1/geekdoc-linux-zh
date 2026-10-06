
```html
<!DOCTYPE HTML PUBLIC "//W3C//DTD HTML 3.2 FINAL//">
<HTML>
<HEAD>
<BASE TARGET="_parent">
</HEAD>
<BODY bgcolor="#FFFFFF" LINK="#000080" VLINK="#000000" TEXT="#000000">
<FORM NAME="LAYOUTFORM" METHOD="POST">
<TABLE ORDER=0 CELLPADDING=0 WIDTH=126>
<TR WIDTHIGN=TOP ALIGN-LEFT>
<TD WIDTH=56><IMG SRC="../clearpixel.gif" WIDTH=6 HEIGHT=1 BORDER=0></TD>
</TR>
<TR WIDTHIGN=TOP ALIGN-LEFT>
<TD HEIGHT=17></TD>
</TR>
```

# D.15 Left_registrationpage.html

```html
<TR VALIGN="TOP ALIGN-LEFT>
<TD COLSPAN=2 HEIGHT=9></TD>
</TR>
<TR VALIGN="TOP ALIGN-LEFT>
<TD HEIGHT=17></TD>
<TD>
<20 ALIGNIGN-
<1-11AAARegistrationregistrationregistration.."><">< ID="Picture15"1117"11120 SRC="../Users.gif" BORDER"0"="新用户"a></TD>
</TR>
<TR VALIGN="TOP ALIGN-LEFT>
<TD COLSPAN=2 HEIGHT=9></TD>
</TR>
<TR VALIGN="TOP ALIGN-LEFT>
<TD HEIGHT=17></TD>
<TD WIDTH=120 ALIGN-LEFT><A HREF="../Login/loginpage.jsp"><IMG SRC="../Registered_users.gif" BORDER=0 ALT></TD>
</TR>
<TR VALIGN="TOP ALIGN-LEFT>
<TD COLSPAN=2 HEIGHT=9></TD>
</TR>
<TR VALIGN="TOP ALIGN-LEFT>
<TD HEIGHT=17></TD>
<TD WIDTH=120 ALIGN-LEFT><A HREF="../Home/homepage.jsp"><IMG ID="Picture6" HEIGHT=17 SRC="../home.gif" BORDER=0 ALT="首页"></a></TD>
</TR>
<TR VALIGN="TOP ALIGN-LEFT>
<TD COLSPAN=2 HEIGHT=9></TD>
</TR>
<TR VALIGN="TOP ALIGN-LEFT>
<TD HEIGHT=17></TD>
<TD WIDTH=120 ALIGN-LEFT><A HREF="../Access/servletUseraction=listorders&ListOrdersPage/order.gif" Alt="上一个 /><IMG SRC="../body.gif" Id="Picture30" HEIGHT=17 WIDTH=120 SRC="../orders.gif" /></a></TD>
</TR>
<TR>
</TABLE>
</FORM>
</BODY>
</HTML>
```

```html
<!DOCTYPE HTML PUBLIC "//W3C//DTD HTML 3.2//EN">
<HTML>
<HEAD>
<BASE TARGET="parent" />
</HEAD>
<BODY BACKGROUND="#FFFFFF" LINK="#0000FF" VLINK="#000000">
<form NAME="registration" ACTION="/servlet/Insertinfo" METHOD="POST">
<TABLE ORDER=0 CELLPADDING=0 WIDTH=126>
<TR VALIGN-TOP ALIGN-LEFT>
<TD WIDTH=56 SRC="../clearpixel.gif" HEIGHT=6 BORDER=0></TD>
</TR>
<TR VALIGN-TOP ALIGN-LEFT>
<TD HEIGHT=17></TD>
</TR>
<TD HEIGHT=17></TD>
</TR>
<TR VALIGN-TOP ALIGN-LEFT>
<TD COLSPAN=2 HEIGHT=9/></TD>
```

```html
<TR VALIGN="TOP-ALIGN-LEFT>
<TD HEIGHT="17"><A HREF="../Registrationpage/registration.jsp" target="_blank"><IMG ID="Picture15" HEIGHT="17" WIDTH="120" SRC="../New_users.gif" BORDER=0></a></TD>
</TR>
<TR VALIGN="TOP-ALIGN-LEFT">
<TD COLSPAN="2" HEIGHT="9"></TR>
<TR VALIGN="TOP-ALIGN-LEFT">
<TD HEIGHT="17"></TD>
<TD WIDTH="120" ALIGN="TOP-LEFT"><A HREF="../Login/logging.jsp"><IMG ID="Picture16" HEIGHT="17" WIDTH="120" SRC="../Registered_users.gif" BORDER=0></a></TD>
</TR>
<TR VALIGN="TOP-ALIGN-LEFT">
<TD COLSPAN="2" HEIGHT="9"></TR>
<TR VALIGN="TOP-ALIGN-LEFT">
<TD HEIGHT="17"></TD>
<TD WIDTH="120" ALIGN-LEFT><A HREF="../index.html"><IMG ID="Picture16" HEIGHT="17" WIDTH="120" SRC="../home.gif" BORDER=0></a></TD>
</TR>
<TR VALIGN="TOP-IGN-LEFT">
<TD COLSPAN="2" HEIGHT="9"></TR>
<TR VALIGN="TOP-IGN-LEFT">
<TD HEIGHT="17"></TD>
</TR>
</TABLE>
</FORM>
</BODY>
```

# D.16 Left_registration.jsp

```html
<!DOCTYPE HTML PUBLIC "//W3C//DTD HTML 3.2 FINAL//">
<HTML>
<HEAD>
<BASE TARGET="parent">
</HEAD>
<% HttpSession session=request.getSession(true);%>
<BODY BGCOLOR="#FFFFFF" LINK="#000080" VLINK="#000000">
<FORM NAME="registration" ACTION="/servlet/AccessUserInfo" METHOD="POST">
<TABLE>
<TD WIDTH="56"><IMG SRC="../clearpixel.gif" WIDTH="1" HEIGHT="6" BORDER=0></TD>
</TR>
<TR VALIGN="TOP-ALIGN-LEFT">
<TD HEIGHT="17"></TD>
</TR>
<TR VALIGN="TOP-ALIGN-LEFT">
<TD HEIGHT="17"></TD>
<TR VALIGN="TOP-ALIGN-LEFT">
<TD COLSPAN="2" HEIGHT="9"></TD>
</TR>
<TR VALIGN="TOP-ALIGN-LEFT">
<TD HEIGHT="17"></TD>
```

# D.17 Left_updatepage.html

```html
<TR VALIGN-TOP ALIGN-LEFT>
<TD COLSPAN=2 HEIGHT=9></TD>
</TR>
<TR VALIGN-TOP ALIGN-LEFT>
<TD HEIGHT=17></TD>
<TD WIDTH=120 ALIGN-LEFT VALIGN-TOP><A HREF="/Page/login.html"><IMG ID="Picture" HEIGHT=17 WIDTH=120 SRC="../registered_users.gif" BORDER=0 ALT="已注册"></a></TD>
</TR>
<TR VALIGN-TOP ALIGN-LEFT>
<TD COLSPAN=2 HEIGHT=9></TD>
</TR>
<TR VALIGN-TOP ALIGN-LEFT>
<TD HEIGHT=17></TD>
<TD WIDTH=120 ALIGN-LEFT VALIGN-TOP><A HREF="/OrderPage/orderpage.html"><IMG ID="Picture" HEIGHT=17 WIDTH=120 SRC="../orders.gif" BORDER=0 ALT="上一个"></a></td>
</TR>
</TR>
</TABLE>
</FORM>
</BODY>
</CENTER>
</HEAD>
</HTML>
```

# D.18 Listorderliste.jsp

# D.19 Listorderspage.jsp

```html
<% language="java" %>
<html
<head>
<base target="parent">
</head>
<body>
<bean name="orders" type="penguins.access.DB2.Orders">
</bean>订单列表 <p

<table border=1>
<<tr><th>订单ID=</th><th>时间戳</th><th>产品ID=</th>
</tr>
<%@page import="java.util.*" %>
<% for (Enumeration e=orders.orderIDs(); e.hasMoreElements(); {) {
	String key=(String)e.nextElement();
	out.println("<tr><td>"+key+"<td>"+timestamp(key)+"</td><td>"+orders.productID+"</td></tr>");
	}
%>
</table>
</body>
</html>
```

# D.20 Loginpage.jsp

```html
<!DOCTYPE HTML PUBLIC "//W3C//DTD HTML 3.2 FINAL//">
<HTML>
<HEAD>
<BASE TARGET="_parent">
</HEAD>
<%@ HttpSession session=request.getSession(true);%>
<BODY BGCOLOR="#FFFFFF" LINK="#000080" VLINK="#000000">
<FORM NAME="login" ACTION="/servlet/AccessUserInfo" METHOD="POST">
<INPUT TYPE="HIDDEN" NAME="action" VALUE="login">

<CENTER>
<P>
<H3 ALIGN="CENTER">发生了错误</summary>
</P>
<P>
<H4 ALIGN="CENTER">%= (String)session.getValue("error")%>
<% session.removeValue("error") %>
</P>
<P>返回/ B</P>
<A href="/LoginPage/login.jsp"><img HEIGHT="17" WIDTH="120" SRC="../home.gif" BORDER=0 ALT="首页" /></a>
</CENTER>
</BODY>
</HTML>
```

# D.21 Loginpage.jsp

```html
<!DOCTYPE HTML PUBLIC "//W3C//DTD HTML 3.2 FINAL//EN">
<%@ LANGUAGE="Java" %>
<HTML>
<HEAD>
<BASE TARGET="_parent">
</HEAD>
<FRAMSET>
<BODY>
<FRAME NAME="header" SRC="/header_defaultmasterborder.html" SCROLLING="AUTO MARGINWIDTH="2" MARGINHEIGHT="1" BORDER=5 NORESIZE>
<FRAMSET>
<FRAME NAME="left" SRC="/LoginPage/left_loginpage.jsp" SCROLLING="AUTO MARGINWIDTH="2" MARGINHEIGHT="1" BORDER=5 NORESIZE>
<FRAME NAME="body" SRC="../LoginPage/body_loginpage.jsp" SCROLLING="AUTO MARGINWIDTH=2 />
</FRAMSET>
</FRAMSET>
</BODY>
</HTML>
```

## D.22 Logout.jsp

```html
注意：图片提供的代码包含一些伪迹/拼写错误，但这反映了可见的文本。
```

## D.23 orderfile.jsp

```html
<HTML>
<HEAD>
<% HttpSession session=request.getSession(true); %>
</HEAD>
<BODY>
<CENTER>
<P>
<H3 ALIGN=CENTER>发生了一个错误</H3>
</P>
<P>
<H4 ALIGN=CENTER><%= (String)session.getValue("error") %>
</P>
</CENTER></HTML>
```

```jsp
<% session.removeValue("error") %>
<P>
<B>返回</B>
<P>
<A href="../Orderpage/orderpage.html"><IMG HEIGHT=17 WIDTH=120 SRC="../home.gif" BORDER=0 ALT="首页"></a>
<P>
<CENTER>
<BODY>
<html
```

## D.24 Orderpage.html

```html
<!DOCTYPE HTML "-//W3C//DTD HTML 3.2 FINAL//">
<HTML>
<HEAD>
<FRAMESET ROWS="142,*">
<FRAME NAME="header" SRC="header_defaultmasterborder.html" SCROLLING=TO MARGIN=1 MARGINHEIGHT=5 NORESIZE>
<FRAMESET COLS="152,*">
<FRAME NAME="left" SRC="../Orderpage/left_order.html" SCROLLING=AUTO MARGIN=1 BORDER=1>
<FRAME NAME="body" SRC="../Orderpage/body_order.jsp" SCROLLING=AUTO MARGIN=2 MARGINHEIGHT=2>
</FRAMESET>
</FRAMESET>
</HEAD>
```

## D.25 Success.jsp

```html
<% language="java" %>
<HTML>
<HEAD>
<TITLE TARGET="parent">
<% HttpSession session=request.getSession(true); %>
</HEAD>
<BODY BGCOLOR="#FFFFFF" LINK="#0000FF" VLINK="#800080" TEXT="#000000" TOP=2 MARGINHEIGHT=2>
<TABLE ALIGN="LEFT" CELLPADDING="0">
<TR>
<TD WIDTH=96 HEIGHT=17><IMG SRC="../clearpixel.gif" WIDTH=96 HEIGHT=1 BORDER=0></TD>
<TD WIDTH=419><IMG SRC="../clearpixel.gif" WIDTH=419 HEIGHT=1 BORDER=0></TD>
</TR>
<TR>
<TD VALIGN="TOP" ALIGN="LEFT"><n<TD WIDTH=419><CENTER><FONT SIZE="*2">订单信息</B></FONT></CENTER></B></TD>
</TR>
<TABLE BORDER="0" CELLPADDING="0">
<TR>
<TD WIDTH=56 HEIGHT=33><IMG SRC="../clearpixel.gif" WIDTH=56 HEIGHT=1 BORDER=0></TD>
</TR>
</TABLE>
<TD WIDTH="457.
```
